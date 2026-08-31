This repository aims to be a set of instructions for developers or users, who are interested in testing various of libraries from the GameMaker Kitchen registry.

## For everyone

Please ensure that you are on at minimal 2026.1.X (aka betas or newer) (` IDE v2026.100.0.1139 Beta Runtime v2026.100.0.1090`). You can see this by looking at the top right.

No other version will be supported.

## Known issues

- CE2/CE1/LSP/Feather do not highlight or recognise any functions/macros/enums.

## For users

If you find any specific bugs involving the prefab system or the package manager, please file a bug report via Help -> Report a GameMaker Bug.

If there's a specific bug with the way the prefab has been setup, please instead make an issue in this repository here.

Please follow the guide [here](/adding-gmk-registry.md) in order to test & use the GM Kitchen prefabs.

## For developers who want to add a prefab to the registry

Firstly, please ensure that your library is on 2024.14.4 or higher. I am not supporting any libraries that are older than 2024.14.4 (with exceptions).

Secondly, follow this guide [here](/exporting-your-functions-macros-enums.md) for exposing functions/macros/enums that you want to be **PUBLIC**. And finally, please ensure that you have some kind of documentation included in your project. (A note asset that links to your documents will suffice.) Reason for documentation is to allow an end user to quickly glance through what's available. 

As of the latest 2026.100.0 betas, the prefab builder is now available to utilize. So you may build & submit your prefabs directly to the GM Kitchen registry.

For actually submitting packages, currently the gmpm interface does not support creating a user account. So you will need to instead use npm version 11. GameMaker does include node.js v24.14.1 and npm v11.11.0 by default, which on Windows it's under `%appdata%\GameMakerStudio2-LTS2026\USERNAME\node\node\` under `npm.cmd`. You may open a CMD window in that folder path and run `npm.cmd` in place of `npm`. I am uncertain about other operating systems, but I will update these when I have a moment.

Though I would personally recommend just installing node.js v24.20.0 if you are able to. You can find the downloads for Node.js here. https://nodejs.org/en/download

> Only npm v11.X is needed for creating a user account. npm v12.X and above has `adduser` removed. But other commands work fine.

For prefab setup: 
Please ensure that you fill both package name fields (the scope field **is** required), the publisher name, collection name & package id. See from the example below.<br>
<img width="630" height="776" alt="image" src="https://github.com/user-attachments/assets/be867f84-2e36-48a4-b7e7-9e8eee85e3c2" />


Please ensure that it is exported to a directory on its own, and open a terminal window from there.

> GM own prefabs are supported as well. You may use sdf filters, layer effects, other gm prefab assets, etc. The GM Kitchen registry will search for any included GM stock prefab if needed so.

If you don't want to specify `--registry` every time, you may set the configured registry away from `https://registry.npmjs.org/` by using `npm config set registry https://gmpm.gamemakerkitchen.com/`. Or under specific scopes `npm config set @scope:registry https://gmpm.gamemakerkitchen.com/`. (This may change when this FR is fulfilled. https://github.com/YoYoGames/GameMaker-Bugs/issues/15183)

For making a new account:
`npm adduser --registry https://gmpm.gamemakerkitchen.com/`

For verifying current account:
`npm whoami --registry https://gmpm.gamemakerkitchen.com/`

For logging in, if not logged in:
`npm login --registry https://gmpm.gamemakerkitchen.com/`

For submitting (Need to be in the same folder as where your prefab is exported):
`npm publish --registry https://gmpm.gamemakerkitchen.com/`

# FAQ

Q: Will there be a nicer account creation/login workflow down the line?<br>
A: Eventually, yes. When I have time to poke around and get that all going. Ideally I'd like to mainly transition towards an OpenID implementation.

Q: If I have issues with the package manager/prefab builder, where do I report?<br>
A: https://github.com/YoYoGames/GameMaker-Bugs/issues
