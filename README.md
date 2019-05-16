This project was forked from https://github.com/ozra/mmap-io to provide Electron prebuilds.

## Prebuilding
New prebuilds will have to be built when the Electron ABI changes, probably for each major release.

For more information about prebuild, visit https://github.com/prebuild/prebuild

In short, the process is:
##### 1. Install prebuild globally
`yarn global add prebuild`

##### 2. Run prebuild
This must be done on both Mac and Windows

`prebuild -t <ELECTRON_VERSION> -r electron`

##### 3. Publish a new version
`yarn publish`

##### 4. Attach the prebuilt files to the release
`prebuild --upload-all <YOUR_GITHUB_TOKEN>`

Alternatively, [create a release on GitHub and attach the files manually](https://help.github.com/articles/creating-releases/)

## Common Problems

### Electron Version Errors
You may see errors like this:

> Error: Could not detect abi for version 4.0.1 and runtime electron.  Updating "node-abi" might help solve this issue if it is a new release of electron

If that's the case, delete any node-abi entries in `yarn.lock` (or just delete `yarn.lock`), then re-run `yarn install` to ensure all packages pull the latest version of it.

### Windows

They may need to be run from an administrative powershell or command prompt.

```
yarn global remove prebuild
yarn cache clean
yarn global upgrade-interactive
yarn global add prebuild
prebuild -t <ELECTRON_VERSION> -r electron
```