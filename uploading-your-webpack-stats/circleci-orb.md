---
description: >-
  CircleCI Orbs are reusable bits of configuration, we've combined this with a
  standard Docker image to provide a turn key solution for CircleCI users.  No
  need to modify your project at all.
---

# CircleCI Orb

{% hint style="warning" %}
In order to use the CircleCI Orb, you must first opt-in your organization to allow third party orbs within your Organization Security settings.  
  
You can do this by going to **Settings** &gt; **Organization** &gt; **Security**
{% endhint %}

Next, you will add our orb to your configuration by declaring it in your CircleCI configuration.

```yaml
version: 2.1

orbs:
  packtracker: packtracker/report@2.3.0
```

{% hint style="info" %}
 If you started using CircleCI prior to 2.1, you must enable pipelines within your project configuration to be able to use the `orbs` configuration.
{% endhint %}

### Authentication

In order for us to know what project you are reporting stats for, you must send along your packtracker project token.  To do this with the CircleCI Orb, you must create a new project environment variable in your CircleCI settings called `PT_PROJECT_TOKEN`.  You can find your packtracker project token in your project's settings.

### Configuration

{% hint style="info" %}
If you are not yet using [CircleCI Workflows](https://circleci.com/docs/2.0/workflows/), you will need to do so.  If this is the case, you likely have a single `build` job in your CircleCI configuration.  In order to add the packtracker `job` to your CI run, you will need to set up a [multi-job workflow as seen in this example configuration](https://circleci.com/docs/2.0/workflows/#workflows-configuration-examples).
{% endhint %}

Now that you've declared our orb for use and added your project token, you have access to our `report` **job**.  You can put this job anywhere inside your existing CircleCI workflows.

```yaml
workflows:
  version: 2
  your_existing_workflow:
    jobs:
      - build
      - packtracker/report
```

Or, create a new workflow to run packtracker reporting.

```yaml
workflows:
  version: 2
  your_existing_workflow:
    jobs:
      - build
  packtracker:
    jobs:
      - packtracker/report
```

By default, this base configuration should _just work_ most of the time.  If you have a non-standard setup, you can tweak the job with the following 2 optional parameters.

| Parameter | Description |
| :--- | :--- |
| `project_root`  | The relative path to the directory containing the `package.json` of your project.  By default, this is the root of your repository.  This can be especially useful for projects that do not live at the root of the repository, like lerna mono-repositories for example. |
| `webpack_config` | The relative path to your webpack configuration.  By default, it looks in the root directory for `webpack.config.js`. |
| `selected_resource_class` | Sometimes your Orb might not have enough resources to complete your webpack build, and you might need to specify a higher resource class. |
| `exclude_assets` | There may be assets you wish to exclude from tracking. This options allows you to pass a [regular expression string](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions). When this regular expression matches the name of any asset you are producing, it will exclude it from reporting. This simply gets passed along to the [webpack stats configuration](https://webpack.js.org/configuration/stats/#statsexcludeassets). |

For example, a Ruby on Rails project might look something like this.

```yaml
workflows:
  packtracker:
    jobs:
      - packtracker/report:
          webpack_config: "./config/webpack/production.js"

```



