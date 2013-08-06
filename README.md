# karma-handlebars-preprocessor

> Preprocessor to compile Handlebars on the fly.

Forked from [hanachin's code](https://github.com/hanachin/karma-handlebars-preprocessor) (kudos!)

Only works with **Karma 0.9 or later** which enables custom plugins.

For more information on Karma see the [homepage].


## Installation

1. Install Karma and karma-osx-reporter plugin. The plugin requires Karma 0.9+, but Karma's stable version is now 0.10 so it's pretty easy.

  a. Globally. System-wide with `karma` available on command line.

    ```
    npm install -g karma
    npm install -g karma-handlebars-preprocessor
    ```

  b. Locally. If you want to install Karma to your project instead, add the dependencies to `package.json` and run `npm install`:

    ```js
    "devDependencies": {
      "karma": ">=0.9",
      "karma-handlebars-preprocessor": "*"
    }
    ```

    If you install locally, you'll need to run Karma using `node_modules/.bin/karma`.

  In any case, the plugin needs to be installed as a peer dependency to Karma (i.e. in the sibling folder). This just means you cannot use global Karma with local plugins or vice-versa.


4. Define it as a reporter in the config file

  ```js
    preprocessors: {
      '**/*.hbs': 'handlebars'
    }
  ```

  or pass through the command line

  ```sh
    $ karma start --preprocessors handlebars karma.conf.js
  ```


## Configuration

You can configure default behaviour in the `handlebarsPreprocessor` section of the config file. The following shows the default implementation:

```js
// karma.conf.js
module.exports = function(config) {
  config.set({
    preprocessors: {
      '**/*.hbs': ['handlebars']
    },

    handlebarsPreprocessor: {

      // name of the variable to store the templates hash
      templates: "Handlebars.templates",

      // translates original file path to template name
      templateName: function(filepath) {
        return filepath.replace(/^.*\/([^\/]+)\.hbs$/, '$1');
      },

      // transforms original file path to path of the processed file
      transformPath: function(path) {
        return path.replace(/\.hbs$/, '.js');
      }
      
    }
  });
};
```

## Note on version

This plugin precompiles templates using handlebars.js version `1.0.0`. You'll need to provide handlebars.runtime.js of the same version in your page.


## License

MIT License


[homepage]: http://karma-runner.github.io

