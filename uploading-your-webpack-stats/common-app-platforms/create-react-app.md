---
description: >-
  Create React App is a powerful, opinionated tool for bootstrapping a modern
  React web application.
---

# Create React App

## For CircleCI or GitHub Actions Users

If you're using CircleCI or GitHub Actions, the packaged stat reporter for these integrations automatically handles the process of uploading the build stats of your Create React App application.

{% page-ref page="../circleci-orb.md" %}

{% page-ref page="../github-actions.md" %}

## Not using CircleCI or GitHub Actions?

{% hint style="danger" %}
This documentation works **only for projects using Create React App 2.x**

Unfortunately they have removed the `--stats` flag in 3.x
{% endhint %}

While the [Create React App](https://facebook.github.io/create-react-app/) project maintains great usability by hiding much of the ceremony of webpack behind it's own set of scripts, without ejecting you would otherwise not be able to use our service to track your bundle sizes.

To allow you to maintain your usage of the CRA scripts, we have provided a CLI tool along side our plugin that allows you to upload your stats to us as long as you have a static json stats file available.

You will still need to install our plugin in your project

```text
npm install @packtracker/webpack-plugin
```

The provided command, `packtracker-upload`, will upload your stats to our service from a static json file. Luckily, Create React App exposes this json via the `--stats` flag.

The only caveat to using the command \(instead of the plugin\) is that you **must** use environment variables to configure your stat reporting \(most importantly `PT_PROJECT_TOKEN`\).

{% hint style="info" %}
See [our plugin documentation](https://github.com/packtracker/webpack-plugin#options) for a full list of configuration options available via environment variable.
{% endhint %}

### Get your project token

After [creating your organization and project on packtracker.io](https://docs.packtracker.io/creating-your-first-project), grab your project token and assign it to `PT_PROJECT_TOKEN` as an environment variable.

```text
export PT_PROJECT_TOKEN=your-project-token-here
```

### **Creating the npm script to report your stats**

Now that your environment has your environment variable available.  In your `package.json` you can add a npm script like the following

```text
{
  "scripts": {
    "packtracker": "react-scripts build --stats && packtracker-upload --stats=build/bundle-stats.json"
  }
}
```

Then running `npm run packtracker` should upload your stats to our service

Once you've tested that you are all set up, be sure to set this script to run in your CI environment or on deployment of your application so we can track each and every commit.





