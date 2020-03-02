---
description: >-
  In addition to our webpack plugin, we also offer a command line tool to upload
  your stats.
---

# Command Line Interface

If you prefer it, we also offer a command line tool to upload your stats.  This is especially useful with frameworks like Create React App that don't expose webpack configuration directly, but are happy to provide a stats file.

The tool is fairly simple and accepts 2 command line arguments

1. `--stats=path/to/stats.json` - The path to your stats json file
2. `--output-path=path/to/your/build` - The path to your build output directory

All other configuration can be accomplished using the [environment variables documented for our webpack plugin](https://github.com/packtracker/webpack-plugin#options).

To tool itself is distributed alongside the webpack plugin as a bin script.

```text
npm install @packtracker/webpack-plugin --save
```

Then you can access the bin script from within your run scripts within package.json as `packtracker-upload` .

```javascript
  ...
  "scripts": {
    ...
    "packtracker": "packtracker-upload --stats=build/bundle-stats.json"
  },
  ...
```

Then running `npm run packtracker` will upload your stats to our service.

