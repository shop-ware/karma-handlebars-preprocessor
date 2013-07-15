# karma-handlebars-preprocessor

> Preprocessor to compile Handlebars on the fly.

Forked from [hanachin's code](https://github.com/hanachin/karma-handlebars-preprocessor) (kudos!)

Only works with **Karma 0.9 or later** which enables custom plugins.

For more information on Karma see the [homepage].


## Installation

1. Make sure you're using Karma 0.9+ `karma --version`. You may install the latest version using `npm install -g karma@canary`.

2. Install the plugin `npm install -g karma-handlebars-preprocessor`.

3. Add dependency to the plugin section in Karma config file (Karma 0.9.0 - 0.9.2):

  ```js
    plugins = [
      'karma-handlebars-preprocessor'
    ];

  ```

  or, if you're using the new module-based config file format (Karma 0.9.3+):

  ```js
    module.exports = function(karma) {
      karma.configure({
        ...
        plugins: [
          'karma-handlebars-preprocessor'
        ],
        ...
      })
    }
  ```

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

