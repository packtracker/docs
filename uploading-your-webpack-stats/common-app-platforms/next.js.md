# Next.js

Similar to other platforms that allow for webpack plugin use, you can use our webpack plugin along side the configuration strategy provided by Next.js.

For example, adding the plugin to your configuration

```javascript
const PacktrackerPlugin = require('@packtracker/webpack-plugin')

module.exports = {
  webpack: (config, { buildId, dev, isServer, defaultLoaders, webpack }) => {
    if (!isServer && isCI) {
      config.plugins.push(
        new PacktrackerPlugin({ upload: true })
      )
    }
    return config
  }
}
```

You will likely want to run this reporting **only in your CI** on every push, so make sure you put safeguards to ensure this.

For more information about all the configuration options and concerns in using the webpack plugin, see our documentation.

{% page-ref page="../webpack-plugin.md" %}



