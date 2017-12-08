# Optimizely X Command Line Interface

Optimizely-X-CLI (`optxcli`) is a command line tool that lets developers build Optimizely X experiments 
faster by using the sofware tools you already love, and publish to Optimizely X when ready. With this tool
you can use your own source code editors (like Vim or Notepad++) and Git to develop Optimizely experiments 
and variations locally. This had a *significant* positive impact on the test velocity.

Optimizely-X-CLI includes a command line executable that also integrates with either the 
[Tampermonkey](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo?hl=en) (Google Chrome) 
or [Greasemonkey](https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/) (Firefox) browser extensions 
for local development / preview and the Optimizely REST API for publishing tests.

Optimizely-X-CLI was proudly developed by Optimizely Solutions Partner, [Web Marketing ROI](https://webmarketingroi.com.au). 
This tool is orignally based on the [optimizely-cli](https://github.com/FunnelEnvy/optimizely-cli) project by FunnelEnvy.

## Installation

```
npm install -g optimizely-x-cli
```

This will install the `optxcli` executable on your system.

### Dependencies

You'll need to have [Node.js](http://nodejs.org/) installed locally to run `optxcli` and either the 
Tampermonkey or Greasemonkey browser extensions to view variations locally.

## Commands

### View available commands

```
optxcli
```

### Initialize a new Optimizely X project in current directory

Before you create an experiment or variation you’ll want to initialize a project. 
If have an existing project and have been issued an API key you can use the remote 
(-r) option, and if not just create it locally. You’ll need to specify the project 
id (required):

```
optxcli init [options] <project_id>
```

Argument:

 - `project_id` - the Optimizely X project ID. Required.

Options:

 - `-r --remote` - pull the remote project with `project_id`
 - `-j --jquery` - include jQuery
 
### Create a local experiment

Create a local experiment under a project with the command: 

```
optxcli experiment <folder> <description> <url>
```

Arguments:

 - `<folder>` – The folder (directory) for the new experiment. Required.
 - `<description>` – The experiment description that will show up in Optimizely. Required
 - `<edit_url>` – The default editor url for the experiment. Required.

### Create a local variation

Create a local variation and scaffold the source files

```
optxcli variation <experiment> <folder> <description> <traffic_allocation>
```

Arguments:

 - `<experiment>` – The directory or id of the experiment. Required.
 - `<folder>` – The new folder (directory) that will be created for the variation. Required.
 - `<description>` – The variation description that will show up in Optimizely. Required.
 - `<traffic_allocation>` - The percentage of traffic allocation. Required.

### Host a variation locally

Compiles the experiment and variation CSS / JS, creates a user script for injection and 
starts a local web server to host the files. Pointing your browser to the root URL 
(default http://localhost:8080) will show a page with installation steps and variation URLs.

```
optxcli host [options] <path> [port] [host]
```

Arguments:

 - `<path>` – Path to the variation directory. Required.
 - `[port]` – Port to host the server. Default to 8080.
 - `[host]` - Hostname. Default to localhost.
 
Options:

 - `-s` - use the self-signed SSL certificate (if you use HTTPS)
 
### Push a local experiment to Optimizely.

Push (create or update) an experiment to Optimizely X through the REST API. This will 
create a new experiment remotely if it hasn’t been pushed before, or update the existing Optimizely experiment 
and its variations if it has.
 
```
optxcli push-experiment <path>
```

Arguments:

 - `<path>` – The path to the experiment directory. Required.

## Copyright and license

Code copyright 2017 Web Marketing ROI. Released under the [Apache 2.0 License](http://www.apache.org/licenses/LICENSE-2.0).
