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
If you compress HTML, you must use semicolons for inline Javascript, and you can create Javascript comments only on the last line in a ``<script>`` tag.

## Configuration
See example-build-config.js

The configuration object is a javascript object

``{}``

and can contain the following keys

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

Following are descriptions of the key associations.

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

- sources can be a single path or an array of paths, and paths are relative to the css_base_path, without filename suffixes. eample "css/test.css" -> "test"
- target is one path, relative to the target_dir
- gzip is true or false or omitted, and leads to a gzip compressed copy of the target file

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

- sources can be a single path or an array of paths, and paths are relative to the css_base_path, without filename suffixes. eample "css/test.css" -> "test"
- target is one path, relative to the target_dir
- gzip is true or false or omitted, and leads to a gzip compressed copy of the target file

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

- sources can be a single path or an array of paths, and paths are relative to the html_base_path, without filename suffixes. eample "html/test.html" -> "test"
- target is one path, relative to the target_dir
- gzip is true or false or omitted, and leads to a gzip compressed copy of the target file

### sync
```javascript
sync: [
  path,
	[source-path, target-path],
	...
]
```

path can be a single path relative to source_dir, or a two element array with paths where the first path is the source path and the second is the target path.
directory structures are created automatically. existing files are overwritten and never deleted.

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