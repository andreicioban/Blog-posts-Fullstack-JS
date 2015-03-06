# Modern developer toolbelt

  In today's web development ecosystem where a lot of programing and scripting languages rise from the necessity to simplify, extend or augment the consecrated languages. Where every day you can find a new framework. Where day by day the standards are adapted to fulfill the modern web applications needs. How do you stay up to date? How do you stay productive? 
  
  The tools made by developers for developers come in handy and take off your tasks and make your developer life easier. From automating tasks, enforcing coding style, managing dependencies to building, deploying and continuous integration we will explore a list of essential tools for a modern developer. If you want to use your time efficiently bare with me. 
  
## The command line

  Everithing begins with the command line. Learn to use it efficiently and you'll have all the power at the tips of your fingers.
  
#### Shortcuts

   `Ctrl+R` Search your command history for something specific.
   
   `Tab` Auto complete.
   
   `Ctrl+Left / Ctrl+Right` Jumps a whole word in your command.
   
   `Ctrl+Shift+Left / Ctrl+Shift+Right` Selects a whole word in your command.
   
   `Shift+Home / Shift+End` Selects from the cursor to start or end of the command.
   
   `Ctrl+U` Deletes the command from start to the curssor position.
   
   `Ctrl+K` Deletes from the cursor to the end of the line.
   
   `Ctrl+W` Deletes from the cursor to the start of the world.
   
   `Ctrl+A or Home` Jumps to the start of the line.
   
   `Ctrl+E or End` Jumps to the end of the line.
  
### [cmder](http://bliker.github.io/cmder/) for Windows

  - replace your boring windows cmd.

### [iTerm2](http://iterm2.com/) for Mac

 - autocomplete, paste history, replay command history, Moseless copy.

### [Guake](http://guake.org/) for Linux

### [Prezto](https://github.com/sorin-ionescu/prezto) — Instantly Awesome Zsh

 - the configuration framework for Zsh. Themes, autocomplete, aliases. 
 
## Chrome developer tools
![Chrome dev tools](https://drive.google.com/file/d/0B0ro1Nj6IFdVbDg2S25YRFBqY1k/view?usp=sharing)

  Master this tool and you will save a lot of time:
  - debugging
  - testing
  - emulating devices and networks
  - Remote Debugging with Screencast
 
## Automation and buid tools

  If you are not using automation tools you are working too hard.
  
#### LiveReload 

  - is a tool that monitors changes in the file system and refreshes the page in the browser as soon as you save a file.
  - it can help save you F5 key, and a lot of time ofcourse.
 
#### NPM
  Npm comes bundled with nodeJS and at the origins is a packet manager for JavaScript, but it can be used as `task runner` or `build tool`. The feature that allows us to use `npm` in multiple ways is `npm run script`.
  
  To initiate a `npm` configuration file we can use the `npm init` command, which will create for us the package.json file. 

Let's see an example of `npm` scripts that will help us automate some of the front end processes:

    "scripts": {
      "buildJs": "browserify yourapp/scripts/*.js > dist/app.js",
      "buildCss": "stylus public/styles/*.styl > dist/app.css",
      "buildHtml": "jade public/html/index.jade > dist/index.html",
      "build": "npm run buildJs && npm run buildCss && npm run buildHtml",
      "watch": "watch 'npm run build' ."
    }

Ofcourse in order for scripts to work we would need the following dependencies:

    "devDependencies": {
      "browserify": "latest",
      "stylus": "latest",
      "jade": "latest",
      "watch": "latest"
    }
  
To install dependencies we use `npm install` command. After installing dependencies just run the `npm run-script watch`, and start developing your app, npm will take care of building everithing for you. You can even extend npm scripts to also run the tests, checking code style and alot of other tasks that we will explore further.

  NPM is a complex tool that can save you a lot of time, we started with npm because all the tools we will explore next are managed using npm, or lets call them `npm helpers`.

Lets explore some helpfull `npm` packages:

#### [jshint](https://www.npmjs.com/package/jshint)

  `jshint` is a tool that detects errors and potential problems in JavaScript code. To use it you have to install the package: `npm installl -save-dev jshint` - the `-save-dev` flag is telling `npm` to add this package to `devDependecies` object in `package.json`.
  
  After installing just add the next script to `npm` scripts:
  
      "jshint": "jshint yourapp/**/*.js test/**/*.js"

  Now run the script using `npm run-script jshint` command and start fixing your JS errors.
  
#### [eslint](https://www.npmjs.com/package/eslint)

  `eslint` is a similar tool to `jshint`, the difference is that in case of `eslint` you can define your own rules, this making the tool more flexible. Ofcourse it comes with lots of predefined rules which you can configure to fulfill your needs.
  
  Install the package just like `jshint` and add the following script to `npm`:
  
      "eslint": "./node_modules/.bin/eslint *.js yourapp/**/*.js test/**/*.js"

  Both code checking tools are useful and can be configured using dot files, here's an axample on how to you can configure `eslint`.
  
  Create a file named `.eslintrc` in the root of your app, this file will look something like this:
  
    {
      "ecmaFeatures": {
          "generators": true
      },
      "env": {
          "browser": false,
          "node": true
      },
      "globals": {
          "config": true
      },
      "rules": {
          "no-trailing-spaces": 0,
          "no-mixed-spaces-and-tabs": 2,
          "quotes": [1, "single"],
          "eqeqeq": 2
    }

  Let's explain the configuration file. The `ecmaFeatures` reffer to `ES6` features, if you write plain javascript(`ES5`) then you can ignore this option. The `env` option define in which environments your app will run, this helps the plugin to detect specific global variable like `window` for browser or `require` for node. In addition to environment globals you can inform the plugin of your own global variables using `global` option. The most important option is `rules` here you can configure the default or your own rules, there are 3 levels of configuration:
    0 - rule is disabled
    1 - rule is treated as warning
    2 - rule is treated as error
  
  Ofcourse the rules can have complex objects as configuration, take for example `quotes` , the config object is passed to your confiuration rule and helps you to fine tune the rule.
  
  In most cases you will need to ignore some files that are still `work in progress` or for other reasons. Create a new file called `.eslintignore`, this file will tel the plugin which files to ignore and works similar to `gitignore`.
  
      lint/**/*.js // your custom eslint rules reside here
      Gruntfile.js
      out/**/*js

  Similar to `eslint` , `jshint` can be configured using `.jshintrc` and `.jshintignore` files. And here comes the best part once configured you can integrate them with your editor (`SublimeText` and `Webstorm` tested) and check your code for mistakes in real time.
  
#### [precomit](https://www.npmjs.com/package/pre-commit)

  Another usefull `npm` package is `pre-commit`. This tool is attaching a pre-commit hook to git and lets you run `npm scripts` whenever you make a git commit, the good part is that the commit will fail if the scripts you are runinning are failing fit error code 1. 
  
  Imagine you can run code checking scripts before each commit and enforce a valid coding style. In most cases you will also want to run the test at this point and fail the commit if there are tests that are not passed. You're writing test for your code aren't you? 
  
  Lets see an example. Install the plugin: `npm install pre-commit`.
  
  Is **very importan** to install this plugin after the `git` repo is initialised since it will need a git repo to hook the pre-commit.
  
  Now add the following object to `package.json`:
  
      "pre-commit": [
        "eslint",
        "test"
      ]

  This will tell the plugin which scripts to run before each `commit`, in our case we will check our code style and run the tests. If you try to make a `commit` at this point and one of the scripts will exit with `code 1`, which will hapen if the code style checker will report errors or if the test will fail. The `commit` will be aborted in this case, and you will need to fix the errors before commiting.
  
  Some times you will need to commit *bad code* anyway, worry not, you can force a commit with `-no-verify` or `-n` flag.
  
  Since we mentioned `testing` we will also mention some helpfull tools in this area.
  
#### [mocha](https://www.npmjs.com/package/mocha) - a simple test framework
  
- `npm install mocha` , we will not get into details here since is a complex topic.

#### [istanbul](https://www.npmjs.com/package/istanbul) -  a JS code coverage tool.

- `npm install istanbul` , generates realy nice reports regarding the code coverage.

![istanbul report](https://drive.google.com/file/d/0B0ro1Nj6IFdVa1NoUWNvSlpxbGc/view?usp=sharing) 

  We will use both tools in one script since both are related to teststing:

      "test": "node_modules/istanbul/lib/cli.js cover node_modules/.bin/_mocha test/**/*.js"
  
#### [Grunt](https://www.npmjs.com/package/grunt) - a javascript task runner

  - `npm install -g grunt grunt-cli` - you have to install globally grunt and grunt-cli which will add to your system path the grunt command.
   
  Grunt works using plugins so before configuring it lets install some plugins:

  - `npm install grunt-contrib-watch grunt-contrib-jshint` - will install two simple plugins that will accomplish the same job as the `npm` plugins used by now.
   
  Configuration files again. Create a file named `Gruntfile.js` in your project root. This file will look like this:

      module.exports = function(grunt) {
      
        grunt.initConfig({
          jshint: {
            files: ['Gruntfile.js', 'yourapp/scripts/*.js', 'test/**/*.js'],
            options: {
              globals: {
                config: true
              }
            }
          },
          watch: {
            files: ['<%= jshint.files %>'],
            tasks: ['jshint']
          }
        });
      
        grunt.loadNpmTasks('grunt-contrib-jshint');
        grunt.loadNpmTasks('grunt-contrib-watch');
      };

  Now running the command `grunt watch` grunt will watch over our app files and wil run `jshint` task whenever we save a file. 
  
  #### [Gulp](https://www.npmjs.com/package/gulp) - a streaming build system
  
    - `npm install -g gulp` install gulp globaly.
    - `npm install gulp-jshint` - just like grunt gulp is using plugins to accomplish different tasks.
  
  Create the configuration file named `gulpfile.js`. The file will look like this:
  
      var gulp = require("gulp");
      var jshint = require("gulp-jshint");
      
      gulp.task("jshint", function() {
       gulp.src("yourapp/scripts/*.js")
       .pipe(jshint())
       .pipe(jshint.reporter('default'));
      });
  
  
  
  Now running `gulp jshint` will produce the same efect as expected from previous experince with `npm` and `grunt`.
  
  The `grunt` and `gulp` tools are quite complex too and can accomplish a lage variety of tasks using plugins. Even the tools, from a developer perspective, are doing the same job they are quite diferen at the bottom. 
  
  Grunt is based on files with *configuration over code* paradigm at origins. 
  
  Gulp is based on streams with *code over configuration* paradigm at origins, which make it gulp a little faster that grunt at building tasks since it doesn't need to write temporary files to disk.  
  
  
