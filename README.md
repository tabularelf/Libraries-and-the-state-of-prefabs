This repository aims to be a set of instructions for developers or users, who are interested in testing various of libraries from the GameMaker Kitchen registry.

## For users

I want to first stress that this is a **TEST** and not something officially stable as of yet. I would advice not relying on these prefabs in production builds, until I say it's safe.

If you find any specific bugs involving the prefab system or the package manager, please file a bug report via Help -> Report a GameMaker Bug.

If there's a specific bug with the way the prefab has been setup, please instead make an issue in this repository here.

Please follow the guide [here](/adding-gmk-registry.md) in order to test & use the GM Kitchen prefabs.

## For developers who want to add a prefab to the registry

Firstly, follow this guide [here](/exporting-your-functions-macros-enums.md). Secondly, please ensure that you have some kind of documentation included in your project. (A note asset that links to your documents will suffice.)

Make an issue in the repository with the following format:

```
Name: name_of_library

Logo: logo_if_available

Instructions on making a prefab:
```

If you have any specific instructions for your libraries that you want me to be aware of, please note them down. Otherwise I wll make an assumption based on your library.

The default assumption would be anything that looks like it is apart of the public folder, will just be included.