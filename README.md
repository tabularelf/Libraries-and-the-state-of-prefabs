# Libraries and the state of prefabs

This document lists out the current state of the prefab system, and what difficulty curve for each and every library if it were to be ported over. As well as guiding others who may wish to eventually port over their libraries over to prefabs, and looking out for any very specific caveats. 

Not every asset type has been tested by me, but for the sole purpose of this document, this is mainly applying to scripts, functions, macros and enums.

__Note__: This is purely my own thoughts, and has no direct opinion on prefabs as a whole. As of writing, the system is still unfinished, and therefore subject to change. 

## How exporting works
When it comes to prefabs, a prefab is essentially a fancier yymps, with a yymanifest .xml and a prefab.json file. These are important as they describe what the prefab has, and more importantly with prefab.json, what assets are public and what the dependencies are (assets, functions, datafiles).

However, when it comes to functions, macros and enums, exposure is handled differently. Instead, they are handled via the keyword `#export`, and are only exposed when prefabs are included as a collection reference. And may be structured like so.

```gml
#export ENABLE_FEATURE, Type, do_thing

#macro ENABLE_FEATURE true

enum Type {
	A,
	B,
	C
}

function do_thing(_a, _b) {
	return _a + do_other_thing(_b, A_NUM);
}

// This is private, not known by the main project
#macro A_NUM 2

function do_other_thing(_a, _b) {
	return _a * _b;
}
```

Each exported function, macro or enum becomes a global keyword, and therefore works about as expected as if you were to put them in your own project standalone, with one caveat. Modifying a macro from a prefab requires using the namespace scope `#macro ::prefab_name::MACRO_NAME <<statement>>`

```gml
#macro ::MyPrefab::ENABLE_FEATURE false
```

A version may be specified optionally, but just the name itself is sufficient enough. Additionally, `#export` does not need to be per script. You can have a single script that contains all of your exports, as it's specifically targeting global keywords. And as an additional note to assets, the above namespace scope reference can be used for public assets too, if there's two assets with the same name, one in the prefab, one in the project. 

As one final additional note, anything exported *can* be overriden safely by the project, without affecting the prefab. This means it is possible to declare your own functions, macros or enums with the same name, that do something different in your project, while the prefabs exported functions, macros or enums continues to work as expected.

__Note__: It is currently not possible to namespace scope reference a prefab exposed function, macro or enum, if they were overriden. 

__Additional note__: Enums exposed will include all of its children names. Like in the example above, `Type.A` through `Type.C` will be included.

__Pending__: It is unknown if two prefabs with the same exported names will cause a conflict of some kind. 
## How difficulty would it be to convert existing libraries?
Outside of having to specify `#export` for anything you wish to be public, and using the namespace feature to modify a macro, there is in fact very few number of libraries that will have trouble being ported over. And in fact, most libraries will have the least friction. There are of course a few caveats.

### Known libraries that will have to be reworked
- [Input (offalynne, Jujuadams, friends)](https://codeberg.org/offalynne/Input) - The [current verb config](https://codeberg.org/offalynne/Input/src/branch/main/scripts/__InputConfigVerbs/__InputConfigVerbs.gml) is not going to be modifiable by the end user, therefore the mechanic itself requires a change in how verbs are declared by the library itself. All of the existing macro configs are however __safe__.
  
  Suggestion: Add a macro config that points to an end user function, or add in a verb declare start/end helper.

## What about functions or macros that reference an asset from within the prefab?
Provided that the library in question actually uses them as a hard reference in code (not `"obj_xy"`) or has an asset tag and `gml_pragma("MarkTagAsUsed", "<<tag name>>");` is supplied, they will be included with the project.

## What about functions that rely on an existing datafile?
There is actually an existing mechanism for datafiles to be included as dependencies, though it is not fully stable. This is still being worked on as per conversing with YYG, and ultimately will likely be fully fleshed out by the time the user prefab builder is available for everyone. 

## Do scripts in prefabs run all of their code at runtime, even if not directly referenced but added as a collection reference?
Yes.

## My prefab references another prefab that is from another registry, is this okay?
While this is mainly about scripts, macros and functions, it is important to know that a prefab will only soft reference another prefab that is included as a collection reference or included as a customizable item. This means that for your prefab to utilise the other prefab, the other prefab must be downloaded and installed. If the registry itself is setup for it, it is possible to upstream any unknown prefab requests to other registries. For example, the GameMaker Kitchen registry (WIP) is capable of pulling any prefabs from the GameMaker prefabs registry. Making it very plausible to include certain sounds or graphics provided for free by YoYoGames as library examples, without having to outsource third party assets.