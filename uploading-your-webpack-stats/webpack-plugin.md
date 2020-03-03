---
description: >-
  Use our open source webpack plugin to report your webpack build information to
  our service.
---

# Webpack Plugin

The way we gather stats from your webpack builds is via [our open source plugin](https://github.com/packtracker/webpack-plugin).  This plugin simply gathers some metadata about the build from source control, extracts the webpack stats object, and uploads the payload to our service for processing.

We **always filter out your source from the stats object**, and **do not have access to your source code**.

### Install the webpack plugin

Once you have a project created, and a `project_token` in hand you can get your data flowing by installing and configuring our [webpack plugin](https://github.com/packtracker/webpack-plugin).

```bash
npm install --save @packtracker/webpack-plugin
```

### Configure and push your first commit

Include the plugin in your configuration along with your project token.

```javascript
const PacktrackerPlugin = require('@packtracker/webpack-plugin')

module.exports = {
  plugins: [
    new PacktrackerPlugin({
      project_token: '<your packtracker project token>',
      upload: true,
      fail_build: true
    })
  ]
}
```

{% hint style="warning" %}
If the plugin fails to upload your stats, by default it **will not error out your build** but it will **log output signaling the failure**.  You can force it to fail your build by passing the `fail_build` configuration option or by setting the `PT_FAIL_BUILD` environment variable.
{% endhint %}

If your are using Webpacker for Ruby on Rails, Laravel Mix, or Next.js you can reference the following documentation for a more relevant configuration example.

{% page-ref page="common-app-platforms/webpacker-with-rails.md" %}

{% page-ref page="common-app-platforms/laravel-mix.md" %}

{% page-ref page="common-app-platforms/next.js.md" %}



Once your configuration is in place, run your webpack build and we'll take care of the rest.

### Uploading in CI

The `upload`option above tells the plugin whether or not to upload your build stats when running webpack. By default, this option is set to `false` to prevent accidental uploading from your local machine. If the upload option is left `false`, the plugin will do nothing.

Once you see your stats are uploading, it is common to only upload when building your assets in a CI environment or during deployment. You can also omit this option, and set the `PT_UPLOAD` environment variable on a per environment basis or check your CI provider's environment variables to control the upload of your stats.

For example...

```javascript
const PacktrackerPlugin = require('@packtracker/webpack-plugin')

module.exports = {
  plugins: [
    new PacktrackerPlugin({
      project_token: '<your packtracker project token>',
      upload: process.env.CI === 'true'
    })
  ]
}
```

You could can also set any packtracker configuration option \(including the `project_token` !\) from an environment variable.  In this case, if your environment has the `PT_UPLOAD` environment variable set to `"true"` the plugin will upload.  [See our complete list of options and environment variables](https://github.com/packtracker/webpack-plugin/tree/master#options).

### Using automation for continuous feedback 

While not a **requirement**, packtracker is most useful in the presence of build automation, whether that be a simple deployment script, a platform as a service, or a CI/CD service that runs with every commit. When automation is in place to handle uploading your statistics you gain a much more reliable mechanism for uploading and reporting.  This also helps you take advantage of our GitHub Pull Request Checks.

