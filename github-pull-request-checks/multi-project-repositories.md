---
description: >-
  Commonly referred to "Monorepos", these are the steps you need to take to set
  up multiple webpack projects in a single GitHub repository.
---

# Multi-project repositories

{% hint style="warning" %}
First and foremost, you should begin by [setting up a single project.](../uploading-your-webpack-stats/)
{% endhint %}

This will give you the experience and understanding of how to report your webpack build stats to us.  The rest of this documentation will assume you have done this, and will outline the additional steps needed to set you the other projects you have in your repository.

### One packtracker.io project for every webpack project

The first step in this process will be to create a project on packtracker.io for every webpack project you wish to track.  For example, **if you have 3 different projects** in your repository, **you need to have 3 separate projects** on packtracker.io.

### Reporting

You then will take the project tokens provided by each project to configure reporting for each webpack build.  If you are using our GitHub Action, you will need to create a job for each webpack build, [setting the appropriate project token and project root](https://github.com/packtracker/monorepo-test/blob/master/.github/workflows/push.yml#L11-L12).

### GitHub Checks

Finally, if you have done everything correctly, you should see multiple projects report their GitHub Checks successfully

![](../.gitbook/assets/image.png)

### Example Repository

You can see an example configuration and pull request here:

[https://github.com/packtracker/monorepo-test](https://github.com/packtracker/monorepo-test)

