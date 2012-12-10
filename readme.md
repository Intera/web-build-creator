# Create a deployment ready custom build of a HTML\CSS\Javascript project.

- Javascript, CSS and HTML compression
- File and directory tree synchronisation with renaming
- File merging
- Gzip compression
- Inheritable configuration

# Dependencies
- nodejs

all other dependencies are included.

# Usage
* Create a Javascript file
* Load the wbc module
* Define a config object
* Call wbc.create_build(config)

## Caveats
If you compress HTML, you must use semicolons for inline Javascript, and you can use Javascript line-comments only for the last lines in a ``<script>`` tag.

## Configuration
See example-build-config.js

The configuration object is a javascript object

``{}``

and can have the following keys

- css_base_path
- debug
- html
- html_base_path
- javascript_base_path
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
		sources: sources,
		gzip: boolean
	},
  ...
]
```

- Sources can be a single path or an array of paths, and paths are relative to the css_base_path, with or without filename suffixes. Example: "test" stands for "js/test.js"
- Target is one path, relative to the target_dir
- Gzip, if true, creates a gzip compressed copy of the file with the same name and a .gz suffix. Can also be omitted or false

### style
```javascript
style: [
	{
    target: target,
		sources: sources,
		gzip: boolean
	},
  ...
]
```

- Sources can be a single path or an array of paths, and paths are relative to the css_base_path, with or without filename suffixes. example: "test" stands for "css/test.css".
- Target is one path, relative to the target_dir
- Gzip, if true, creates a gzip compressed copy of the file with the same name and a .gz suffix. Can also be omitted or false

### html
```javascript
html: [
	{
    target: target,
		sources: sources,
		gzip: boolean
	},
  ...
]
```

- Sources can be a single path or an array of paths, and paths are relative to the html_base_path, with or without filename suffixes. Example: "test" stands for "html/test.html".
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
|css_base_path||"css/"|
|debug|if debug is true the js/html/css files are not compressed|false|
|javascript_base_path||"js/"|
|html_base_path||"html/"|
|source_dir||""|
|target_dir||"../distrib/"|

## Full example
```javascript
var wbc = require("web-build-creator")

var websiteBuild = {
	target_dir: "../website",
	//if debug is true the js/html/css files are not compressed
	debug: false,
	script: [
		{
			target: "js/my-target-file",
			sources: ["file-1", "file-2", "file-3"]
			gzip: true
		},
		{
			target: "js/my-target-file",
			sources: "file-4"
		}
	],
	style: [
		{
			target: "css/file-5",
			sources: [
				"../lib/css/file-6",
				"file-7"
			]
		}
	],
	html: [
		{
			target: "index",
			sources: "index-website"
		}
	],
	sync: [
		"img",
		["content-source.html", "test/html/content.html"]
	]
}

wbc.create_build(websiteBuild)
```

# Developer infos
The included dependencies as node modules are:

- clean-css
- coffee-script
- html-minifier
- ncp
- uglifyjs
- underscore

It is written in coffee-script for the most part.
