Heroku Buildpack for Synth
============================

This is the [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for [Synth](http://www.synthjs.com) web apps.


How it Works
------------

Here's an overview of what this buildpack does:

- Uses the [semver.io](https://semver.io) webservice to find the latest version of node that satisfies the [engines.node semver range](https://npmjs.org/doc/json.html#engines) in your package.json.
- Allows any recent version of node to be used, including [pre-release versions](https://semver.io/node.json).
- Uses an [S3 caching proxy](https://github.com/heroku/s3pository#readme) of nodejs.org for faster downloads of the node binary.
- Discourages use of dangerous semver ranges like `*` and `>0.10`.
- Uses the version of `npm` that comes bundled with `node`.
- Puts `node` and `npm` on the `PATH` so they can be executed with [heroku run](https://devcenter.heroku.com/articles/one-off-dynos#an-example-one-off-dyno).
- Caches the `node_modules` directory across builds for fast deploys.
- Caches the `bower_components` directory across builds for fast deploys.
- Doesn't use the cache if `node_modules` is checked into version control.
- Runs `npm rebuild` if `node_modules` is checked into version control.
- Always runs `npm install` to ensure [npm script hooks](https://npmjs.org/doc/misc/npm-scripts.html) are executed.
- Always runs `npm prune` after restoring cached modules to ensure cleanup of unused dependencies.

For more technical details, see the [heavily-commented compile script](https://github.com/heroku/heroku-buildpack-nodejs/blob/master/bin/compile).

Hacking
-------

To make changes to this buildpack, fork it on Github. Push up changes to your fork, then create a new Heroku app to test it, or configure an existing app to use your buildpack:

```
# Create a new Heroku app that uses your buildpack
heroku create --buildpack <your-github-url>

# Configure an existing Heroku app to use your buildpack
heroku config:set BUILDPACK_URL=<your-github-url>

# You can also use a git branch!
heroku config:set BUILDPACK_URL=<your-github-url>#your-branch
```
