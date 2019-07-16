#Grunt Setup
##Step 1 : Install Node.js
Install Node.js and then you can use the Node.js package manager npm to install and manage Grunt and Grunt plugins.

##Step 2: Install grunt-cli
Grunt's command line interface (CLI) is installed one time for the entire system. You may need to use sudo (for OSX, *nix, BSD etc) or run your command shell as Administrator (for Windows) to do this
```
npm install -g grunt-cli
```

##Step 3: Create package.json file
package.json describes your project: name, git repository, but most importantly your npm dependencies. You need to create package.json in your project directory
```
cd ~/your_project_directory
npm init
```
package.json example:
```
{
    "name": "Grunt",
    "version": "0.0.1",
    "description": "grunt demo",
    "main": "index.html",
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
    },
    "author": "me",
    "license": "ISC"
}
```

##Step 4: Install Grunt
Grunt is installed for each project in the project directory
```
npm install grunt --save-dev
```
Check it in package.json:
```
{
    "name": "Grunt",
    "version": "0.0.1",
    "description": "grunt demo",
    "main": "index.html",
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
    },
    "author": "me",
    "license": "ISC",
    "devDependencies": {
        "grunt": "^0.4.5"
    }
}
```

##Step 5: Install plugins
Search for grunt plugins and install it in the project directory
```
npm install <plugin-name> --save-dev
```

##Step 6: Create gruntfile.js file
gruntfile.js is the file that loads plugins, configures those plugins and define tasks. Create the gruntfile.js in the top of your project directory.

gruntfile.js example:
```
module.exports = function(grunt) {
    // Configure tasks
    grunt.initConfig({
        pkg: grunt.file.readJSON('package.json'),
        uglify: {
            build: {
                src: 'src/js/*js',
                dest: 'js/script.min.js'
            }
        }
    });

    // Load the plugins
    grunt.loadNpmTasks('grunt-contrib-uglify');

    // Register tasks
    grunt.registerTask('default', ['uglify:build']);
};
```

