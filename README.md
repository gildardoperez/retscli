# retscli

[![Gem Version](https://badge.fury.io/rb/retscli.svg)](https://badge.fury.io/rb/retscli)
[![Build Status](https://travis-ci.org/summera/retscli.svg?branch=master)](https://travis-ci.org/summera/retscli)

CLI for querying RETS servers and searching metadata.

This gem is built on top of the [rets](http://github.com/estately/rets) gem, which handles the actual querying and parsing of the RETS server requests. Big thanks to the [Estately](http://www.estately.com) team for their work!

![retscli gif](https://github.com/summera/gifs/blob/master/retscli/search_metadata_cropped.gif?raw=true)
![retscli png](https://github.com/summera/gifs/blob/master/retscli/search.png?raw=true)

## RVM Version
    $ rvm use ruby-2.1.5

## Installation
    $ gem install retscli

## Features
- Search metadata for keywords. Results are highlighted for readability.
- Search resources. Results are displayed in a nicely formatted ascii table.
- Open command results in your editor of choice.
- Debug RETS requests and queries in debug mode.
- Command results are paged using less by default.

## Usage

#### CLI Commands
```bash
$ retscli help
Commands:
  retscli capabilities [LOGIN URL]  # Display capabilities for rets server
  retscli console [LOGIN URL]       # Start rets console
  retscli help [COMMAND]            # Describe available commands or one specific command
  retscli validate [LOGIN URL]      # Validate rets credentials
```

To see the available flags/options, run help on the command

```bash
$ retscli help console
Usage:
  retscli console [LOGIN URL]

Options:
  -u, [--username=USERNAME]        # Username
  -p, [--password=PASSWORD]        # Password
  -v, [--version=VERSION]          # Rets version
                                   # Default: RETS/1.7.2
  -a, [--agent=AGENT]              # User agent
  -t, [--ua-password=UA_PASSWORD]  # User agent password
  -d, [--debug], [--no-debug]      # Debug mode

Start rets console
```

#### Debug Mode
To view requests being made to the RETS server, enable debug mode with the `-d` flag. Once enabled, helpful info will be logged to `$stdout`. This is helpful to debug errors thrown by the RETS server and to adjust queries.

#### Rets Console Commands
After dropping into the RETS console, you get a bunch of useful commands for searching and exploring the RETS server

```bash
$ retscli console http://rets.server.com -u summera -p password

summera@rets.server.com > help
Commands:
  capabilities                       # Display capabilities for rets server
  classes [RESOURCE]                 # List available classes for resource
  help [COMMAND]                     # Describe available commands or one specific command
  login                              # Re-Login to RETS server. Use if session is no longer valid
  metadata                           # View metadata
  objects [RESOURCE]                 # List available objects for resource
  resources                          # List available resources
  search [RESOURCE] [CLASS] [QUERY]  # Search resources, e.g. properties, open houses, etc.
  search-metadata                    # Search metadata tables
  tables [RESOURCE] [CLASS]          # List available tables for class of resource
  timezone-offset                    # System timezone offset
```

Again, to see available flags/options, run help on the command. Many of the commands have an `editor` option if you feel the need to get down and dirty in your editor of choice.


```bash
summera@rets.server.com > help search-metadata
Usage:
  search-metadata

Options:
  -r, [--resources=one two three]  # Filter metadata by resources
  -c, [--classes=one two three]    # Filter metadata by classes
  -e, [--editor=EDITOR]            # Open search results in editor

Search metadata tables
```

## Notes
- When opening output in your editor, retscli will check the `$EDITOR` environment variable. If this is not set, it falls back to nano.
- Much of the output is piped through `less` by default to allow for easy paging. If you'd like to change this, set your preferred pager in the `$PAGER` environment variable.
- Retscli uses the ruby readline module for the rets console.
- If any arguments and/or options have spaces in them, you will need to wrap them in quotes so that retscli does not split on the spaces.

## Contributing

1. Fork it ( https://github.com/summera/retscli/fork )
1. Create your feature branch (`git checkout -b my-new-feature`)
1. Commit your changes (`git commit -am 'Add some feature'`)
1. Run the test suite (`bundle exec rake`)
1. Push to the branch (`git push origin my-new-feature`)
1. Create a new Pull Request


## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

