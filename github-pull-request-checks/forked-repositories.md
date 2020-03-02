# Forked Repositories

### My checks are stuck "in progress"!

Many CI providers \(like TravisCI\) run pull request build jobs on the merged result of the base and head commit.  This is **great** because you get to test the _result_ of the pull request, not only it's current state.

The problem this creates for us, is that because we try \(by default\) to glean the head commit SHA by running something like `git rev-parse --short HEAD`, we end up getting the merge commit SHA instead of most recent commit SHA of the pull request.

In order to report your data to the SHA we expect, most CI providers have environment variables that provide the data we need.  We can adjust our configuration to look to those variables for the data we want.

For example, TravisCI provides not only `TRAVIS_BRANCH` but also `TRAVIS_PULL_REQUEST_BRANCH`

The difference is subtle, but important \(from the TravisCI documentation\)

> `TRAVIS_BRANCH`:
>
> * for push builds, or **builds not triggered by a pull request**, this is the name of the branch.
> * **for builds triggered by a pull request** this is the name of the branch targeted by the pull request.

> `TRAVIS_PULL_REQUEST_BRANCH`:
>
> * **if the current job is a pull request**, the name of the branch from which the PR originated.
> * if the current job is a push build, this variable is empty \(`""`\).

This distinction also extends to the way Travis exposes their commit SHA, so to correctly report your packtracker information to your forked pull requests, configure your plugin similarly as follows

```javascript
new PacktrackerPlugin({
  branch: process.env.TRAVIS_PULL_REQUEST_BRANCH || process.env.TRAVIS_BRANCH,
  commit: process.env.TRAVIS_PULL_REQUEST_SHA || process.env.TRAVIS_COMMIT,
}),

```

And in this way, we can apply your build stats against the head commit of your pull request resulting in the correct reporting for forked pull requests.

