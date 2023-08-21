# ViteJS bug reproduction repository

File structure generated from `yarn create vite` with the Typescript and React preset.

TSConfig and Yarn config are from my project's repo

## What should happen

The console log in [App.tsx](./src/App.tsx) should be of a function

## What actually happens

The console log in [App.tsx](./src/App.tsx) is `undefined`

## Bug hack reproduction

To generate a patch to replicate the confirmation that the `browser` field is being resolved, simply do the following:

1. Run the following

```sh
yarn patch bwip-js
```

2. The above command should contain a line like this

```
You can now edit the following folder: /tmp/xfs-0ab1e518/user
```

3. Run the following, replacing `<<patchDir>>` with the temp dir from the above logged line (i.e. `/tmp/xfs-0ab1e518/user`)

```sh
sed -i 's/  "browser": ".\/dist\/bwip-js.js",/  "browser": ".\/dist\/bwip-js.mjs",/g' "<<patchDir>>/package.json"

# Generates a patch and sets the resolution map entry for bwip-js to the patch
yarn patch-apply -s "<<patchDir>>"

# Install the newly resolved patch
yarn
```
