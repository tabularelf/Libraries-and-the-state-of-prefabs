This repository aims to be a set of instructions for developers or users, who are interested in testing various of libraries from the GameMaker Kitchen registry.

## For everyone

Please ensure that you are on at minimal LTS 2026.1.X (aka betas or newer) (` IDE v2026.100.0.1139 Beta Runtime v2026.100.0.1090`). You can see this by looking at the top right.

No other version will be supported.

## Known issues

- CE2/CE1/LSP/Feather do not highlight or recognise any functions/macros/enums.

## For users

If you find any specific bugs involving the prefab system or the package manager, please file a bug report via Help -> Report a GameMaker Bug.

If there's a specific bug with the way the prefab has been setup, please instead make an issue in this repository here.

Please follow the guide [here](/adding-gmk-registry.md) in order to test & use the GM Kitchen prefabs.

## For developers who want to add a prefab to the registry

Firstly, please ensure that your library is on 2024.14.4 or higher. I am not supporting any libraries that are older than 2024.14.4 (with exceptions).

Secondly, follow this guide [here](/exporting-your-functions-macros-enums.md). And finally, please ensure that you have some kind of documentation included in your project. (A note asset that links to your documents will suffice.)

As of the latest 2026.100.0 betas, the prefab builder is now available to utilize. So you may build & submit your prefabs directly to the GM Kitchen registry.

For actually submitting packages, currently the gmpm interface does not support creating a user account. So you will need to instead use npm version 11. GameMaker does include node.js v24.14.1 and npm v11.11.0 by default, which on Windows it's under `%appdata%\GameMakerStudio2-LTS2026\USERNAME\node\node\npm.cmd`. 
Though I would personally recommend just installing node.js v24.20.0.

> Only npm v11.X is needed for creating a user account. npm v12.X and above has `adduser` removed.

Note: If you don't want to specify `--registry` every time, you may set the configured registry away from `https://registry.npmjs.org/` by using `npm config set registry https://gmpm.gamemakerkitchen.com/`. Or under specific scopes `npm config set @scope:registry https://gmpm.gamemakerkitchen.com/`.

For making a new account:
`npm adduser --registry https://gmpm.gamemakerkitchen.com/`

For verifying current account:
`npm whoami --registry https://gmpm.gamemakerkitchen.com/`

For logging in, if not logged in:
`npm login --registry https://gmpm.gamemakerkitchen.com/`

For submitting (Need to be in the same folder as where your prefab is exported):
`npm publish --registry https://gmpm.gamemakerkitchen.com/`
