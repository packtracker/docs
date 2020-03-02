---
description: >-
  Laravel Mix provides a fluent API for defining Webpack build steps for your
  Laravel application using several common CSS and JavaScript pre-processors.
---

# Laravel Mix

If you are using Laravel Mix for your Webpack configuration management, you should be able to customize your Webpack config and add our plugin [via the `webpackConfig` method](https://laravel.com/docs/5.6/mix#custom-webpack-configuration).

```javascript
const PacktrackerPlugin = require('@packtracker/webpack-plugin')

mix.webpackConfig({
  plugins: [
    new PacktrackerPlugin({
      project_token: '<your packtracker project token>',
      upload: true
    })
  ]
})
```

This is the only specific difference in setting up a project with us using Laravel Mix, please see the rest of our documentation below for more detail.

{% page-ref page="../webpack-plugin.md" %}

