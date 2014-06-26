Heroku Buildpack for Synth
============================

This is the [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for [Synth](http://www.synthjs.com) web apps.


How it Works
------------

Here's an overview of what this buildpack does:

- Detects if your app is a Synth app by looking to see if you have a `synth.json` file in the root of your project.
- Does all the stuff that the [Official Heroku Node.js Buildpack](https://github.com/heroku/heroku-buildpack-nodejs) does plus the following.
- Reads `package.json` from the `back/` directory.
- Installs `node_modules` in `back/`.
- Reads `bower.json` in `front/`.
- Installs `bower_components` in `front/`.
- Caches the `bower_components` directory across builds for fast deploys (just like it does for `node_modules`).
- Doesn't use either cache if `node_modules` or `bower_components` are checked into version control.
- Auto-generates a Procfile in the root of your app if you don't have one. Has one line: `web: synth prod`
- 
For more technical details, see the [heavily-commented compile script](https://github.com/JonAbrams/heroku-buildpack-synth/blob/master/bin/compile).

Usage
-------

```
# Create a new Heroku app that uses this buildpack
heroku create --buildpack https://github.com/JonAbrams/heroku-buildpack-synth -a <your_apps_name>

# Configure an existing Heroku app to use this buildpack
heroku config:set BUILDPACK_URL=https://github.com/JonAbrams/heroku-buildpack-synth
```
