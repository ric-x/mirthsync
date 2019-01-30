# Mirthsync

Mirthsync is a command line tool for synchronizing Mirth Connect code between servers by allowing you to push or pull channels, code templates, configuration map and global scripts using version control tools like Git or SVN. The only requirements are having credentials for the server that is being synced and the server also needs to support and allow access to Mirth Connect's REST API.

Mirthsync is ideal for implementing code across environments such as Production, Test and Development. Environment specific variables such as data sources can be stored in the configuration map allowing the rest of the Mirth Connect code to be environment agnostic.

## Status
The v0.1.0 tag and release is stable. 

Recently, preliminary support was added for groups on the master branch. There is no release or tag for this yet. If you would like to use a version that supports groups you'll need to build from the master branch source. The current groups code will only pull groups - not push. Code for pushing groups will be coming soon.

## Installation 

`$ git clone https://github.com/SagaHealthcareIT/mirthsync.git`


## Prerequisites 

Requires Java JRE or JDK version 8 (versions 9 and above are not currently supported)


## Help

How to generate help dialogue:

`$ java -jar mirthsync.jar -h`

### Help Dialogue:

Usage: mirthsync [options] action

Options:

  -s, --server SERVER_URL  https://localhost:8443/api  Full HTTP(s) url of the Mirth Connect server  
  -u, --username USERNAME  admin                       Username used for authentication  
  -p, --password PASSWORD                              Password used for authentication  
  -f, --force                                          Overwrite any conflicting files in the target directory  
  -t, --target TARGET_DIR  .                           Base directory used for pushing or pulling files  
  -v                                                   Verbosity level; may be specified multiple times to increase value  
  -h, --help
  

Actions:
  
  push     Push local code to remote  
  pull     Pull remote code to local
 


## Examples

How to pull Mirth Connect code from a remote repository:

`$ java -jar mirthsync.jar  -s https://localhost:8443/api -u admin -p admin pull -t /home/user/`

Pull/Push from a REPL using mostly CLI defaults. The following pulls
code to a directory called 'tmp' (relative to the execution
environment), overwriting existing files ("-f"), and then pushes back
to the local server from the same directory.

```clojure
(do (mirthsync.core/run (mirthsync.cli/config ["pull" "-t" "tmp" "-p" "admin" "-f"]))
    (mirthsync.core/run (mirthsync.cli/config ["push" "-t" "tmp" "-p" "admin"])))
```

## Build from Source

Requires [Leiningen](https://leiningen.org/)

`$ lein uberjar`

## Todo

- strip or encode filenames created from server data
- look into bulk group download

## License

Copyright © 2017 Saga IT LLC

Distributed under the Eclipse Public License either version 1.0 or any later version.

## Disclaimer

This tool is still under development. Use at your own discretion. 
