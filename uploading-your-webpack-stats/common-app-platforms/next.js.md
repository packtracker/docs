# Next.js

Similar to other platforms that allow for webpack plugin use, you can use [our webpack plugin](../webpack-plugin.md) along side the [configuration strategy provided by Next.js](https://nextjs.org/docs/api-reference/next.config.js/custom-webpack-config).

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

Then, anytime you run `yarn build` and `isCI` is true, it will attempt to report your stats to our service. You will likely want to run this reporting **only in your CI** on every push, so make sure you put safeguards to ensure this.  Additionally, do not forget to provide your project token, as stated [in the plugin documentation](../webpack-plugin.md).

For more information about all the configuration options and concerns in using the webpack plugin, see our documentation.

{% page-ref page="../webpack-plugin.md" %}



