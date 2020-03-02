# FAQ

## Do you have access to my source code?

No, [the way we gather your webpack stats is entirely open source and open for inspection](https://github.com/packtracker/webpack-plugin).  We filter out your source code specifically.

We also do not request source code access through our GitHub App integration.

## Can I upload my stats from my local development environment?

Yes, **this is possible** though we don't recommend it.

Any run of your webpack build process in which our plugin has `upload` set to  `true` will send your stats to our service.

We recommend setting your process up to upload your stats in an automated way when you push your code.  Generally this is done either:

* In a CI environment
* In your deployment process

This ensures that your not creating a lot of noise in your asset metrics, and allows everyone on your team to take advantage of the tool without additional training and manual intervention.

## Why can't the plugin determine my branch name?

Our webpack plugin uses the local git checkout to query against to determine the branch name.  Commonly in CI environments this query comes back as `HEAD` which doesn't quite give us the information we want.

When this is the case the plugin will thrown an error informing you of this **\(as of version `1.2.0`\)**. In this case you need to provide the branch name as either [a plugin configuration or environment variable](https://github.com/packtracker/webpack-plugin#options).  In most CI environments there is an environment variable available to you to pass along to the plugin.  For example, in CodeShip this environment variable is called `CI_BRANCH`, and you would pass it along to us like so:

```javascript
const PacktrackerPlugin = require('@packtracker/webpack-plugin')
​
module.exports = {
  plugins: [
    new PacktrackerPlugin({
      project_token: '<your packtracker project token>',
      branch: process.env.CI_BRANCH,
    })
  ]
}
```

