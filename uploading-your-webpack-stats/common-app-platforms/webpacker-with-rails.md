---
description: >-
  Webpacker makes it easy to use the JavaScript pre-processor and bundler
  webpack to manage application-like JavaScript in Rails.  The default
  JavaScript build tool in Rails 6.
---

# Webpacker \(with Rails\)

In addition to supporting a standard webpack configuration, we also are compatible with the [Ruby on Rails webpacker gem](https://github.com/rails/webpacker).

You can add the plugin configuration in `config/webpack/environment.js` 

```javascript
const { environment } = require('@rails/webpacker')
const PacktrackerPlugin = require('@packtracker/webpack-plugin')

environment.plugins.append(
  'PacktrackerPlugin',
  new PacktrackerPlugin({
    project_token: '<your packtracker project token>',
    upload: true
  })
)

module.exports = environment
```

This is the only specific difference in setting up a project with us using the webpacker gem with Rails, please see the rest of our  documentation below for more detail.

{% page-ref page="../webpack-plugin.md" %}



