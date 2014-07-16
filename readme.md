# HTML/CSS/Javascript compression/merge and filesystem structure sync/creation. automatic coffeescript support

- Javascript, CSS and HTML compression
- File and directory tree synchronisation with renaming
- File merging
- Gzip compression
- Coffeescript\Coffeekup support
- Inheritable configuration

# Dependencies
- nodejs

all other dependencies are included.

# Usage
* Create a Javascript configuration file
* Load the wbc module
* Define a config object
* Call wbc.create_build(config)

## Configuration
[Example](https://raw.githubusercontent.com/Intera/web-build-creator/master/example-build-config.js)

The configuration object is a javascript object

``{}``

and can have the following keys

- debug
- html
- script
- source_dir
- style
- sync
- target_dir

Following are descriptions for the key associations.

### script
```javascript
script: [
	{
    target: target,
    path_prefix: string,
		sources: sources,
		gzip: boolean
	},
  ...
]
```

- Sources can be a single path or an array of paths, with or without filename suffixes. Example: "js/test" stands for "js/test.js"
- The value of path_prefix is prepended to all source paths
- Target is one path, relative to the target_dir
- Gzip, if true, creates a gzip compressed copy of the file with the same name and a .gz suffix. Can also be omitted or false

### style
```javascript
style: [
	{
    target: target,
    path_prefix: string,
		sources: sources,
		gzip: boolean
	},
  ...
]
```

- Sources can be a single path or an array of paths, with or without filename suffixes. example: "css/test" stands for "css/test.css".
- The value of path_prefix is prepended to all source paths
- Target is one path, relative to the target_dir
- Gzip, if true, creates a gzip compressed copy of the file with the same name and a .gz suffix. Can also be omitted or false

### html
```javascript
html: [
	{
    target: target,
    path_prefix: string,
		sources: sources,
		gzip: boolean
	},
  ...
]
```

- Sources can be a single path or an array of paths, with or without filename suffixes. Example: "html/test" stands for "html/test.html".
- The value of path_prefix is prepended to all source paths
- Target is one path, relative to the target_dir
- Gzip, if true, creates a gzip compressed copy of the file with the same name and a .gz suffix. Can also be omitted or false

### sync
```javascript
sync: [
  path,
	[source-path, target-path],
	...
]
```

path can be a single path relative to source_dir, or a two element array with paths where the first path is the source path and the second is the target path.
Directory structures are created automatically. Existing files are overwritten and never deleted.

### other keys
|key|description|default value|
----|----|----
|debug|if debug is true the js/html/css files are not compressed|false|
|source_dir|path prefix for source files|""|
|target_dir|path prefix for compiled target files|"../compiled/"|

## Caveats
If you compress HTML, you must use semicolons for inline Javascript, and line-comments can only be used for the last line of a ``<script>`` tag.

# Developer infos
The included dependencies as node modules are:

- clean-css
- coffee-script
- html-minifier
- ncp
- uglifyjs
- underscore

It is written in coffee-script for the most part.

# Possible enhancements
- lesscss support
- set working directory per task
