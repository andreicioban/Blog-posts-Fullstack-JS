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
      "buildJs": "browserify yourapp/scripts/app.js > dist/app.js",
      "buildCss": "stylus public/styles/app.styl > dist/app.css",
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

  NPM is a complex tool that can save you a lot of time, we started with npm because all the tools we will explore next are managed using npm.
