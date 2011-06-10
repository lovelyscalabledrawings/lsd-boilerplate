# LSD Boilerplate

Dive in the world of Lovely Scalable Drawings! 

Clone this project and use it a base for your javascript application.
To get started as quick as possible, update submodules to get all dependencies:

`git submodule update --init`.


## Structure

   /my_project              # This folder
      package.yml           # Package manifest
      README.md             # This readme
     /Source                # Code goes in Source folder
       Application.js       # A file with code that requires some dependencies
     /Dependencies          # Dependencies are here as submodules
       /mootools             
       /lsd                 # LSD framework
       ...
       
     /Compiled              # This directory only appears after compilation 
       /my_project.js       # A compiled all-in-one javascript file
       /includes.js         # A file that includes all other files at their places (-g)
       /tree.json           # Optional introspective information about package dependencies
       /scripts.json        # Optional legacy mootools package listing
       
       
       
## Compiling the code

You will need jsus here. Navigate to this directory and execute this:

    jsus . Compiled -d Dependencies -g -b -v
         ^  ^          ^            ^  ^  ^
         |  |          |- packages  |  |  |- Be verbose about problems with sources
         |  |- output directory     |  |- Measure compilation time
         |- this directory          |- Generate includes.js for development
    

It will take all javascript files in this package, and their dependencies and make
them includable right away. It may look like this:

### Development environment 

`<script src="javascript/my_project/Compiled/includes.js"></script>`

Files are loaded one by one, which is slow, but it browser shows correct 
stack traces in right files. `includes.js` only contains list of files to require.
you can define custom `window.loader` function in javascript to redefine
the loader. `window.prefix` string sets the prefix for every of the files.

-g option can be also set as --generate-includes=path, where path is a relative path
that should be used as a base for all includes.

You can also add --watch parameter for jsus to enable "watch" mode that recompiles 
the package whenever the code is changed.


### Production environment
`<script src="javascripts/my_project/Compiled/my_project.js"></script>` for production

All files are packed in one.  

You can also add --compress parameter for jsus that enables yui-compressor, 
strips comments and compresses javascript (up to 50%).

It is strongly advised to serve javascript with a fast web server (like nginx)
that can compress files even more with gzip (and probably cache it) for optimal 
performance. 

Jsus may also be used as a ruby rack middleware to serve files dynamically. 
You can find examples of the setups at http://github.com/jsus

## Dependencies

* LSD libraries:
  * **lsd** it's what we're after. LSD framework itself.
  * **lsd-mobile** mobile widgets
  * **lsd-native** native form fields
  * **lsd-widget** various custom widgets
* Official mootools libraries
  * **mootools-core** v1.3
  * **mootools-more** v1.3 (used for dates and sortables)
  * **mootools-color** mootools color module
* Unofficial mootools extensions
  * **mootools-ext** extra mootools events, properties and features
  * **mootools-string-inflections** a module for railsesque string pluralization 
  * **mootools-custom-event** a library for pseudo events
  * **mootools-mobile** (fork) mootools tweaks for mobile devices
* Extras
  * **mootools-resource** a lightweight javascript REST ORM
  * **mootools-uploader** multiple file uploader 
  * **qfocuser** a library for native focus
  * **slick** (fork) a crossbrowser selector engine
  * **Sheet.js** (fork) stylesheet parser library
* Just in case
  * **art** SVG/VML drawing tool for vector graphics
  * **lsd-specs** spec suite for LSD for maintenance
  * **lsd.wiki**, documentation