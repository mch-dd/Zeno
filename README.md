# Zeno Web Crawler

Zeno is a state-of-the-art web crawler designed for both wide crawls and single-page archiving. Its key concepts are portability, performance, and simplicity, with a strong emphasis on performance.

## Table of Contents

1. [Installation](#installation)
2. [Usage](#usage)
3. [Commands](#commands)
   - [get](#get)
   - [get url](#get-url)
   - [get list](#get-list)
   - [get hq](#get-hq)
4. [Configuration](#configuration)
5. [Authors](#authors)

## Installation

(Include installation instructions here)

## Usage

To use Zeno, run the following command:

```
Zeno [command] [flags]
```

If no command is provided, Zeno will display the help information.

## Commands

### get

The `get` command is used to archive web content. It has three subcommands: `url`, `list`, and `hq`.

#### get url

Archive specific URLs.

```
Zeno get url [URL...] [flags]
```

This command takes one or more URLs as arguments and archives them.

#### get list

Start crawling with a seed list.

```
Zeno get list [FILE] [flags]
```

This command takes a file containing a list of URLs as input and starts crawling from those seed URLs.

#### get hq

Start crawling with the crawl HQ connector.

```
Zeno get hq [flags]
```

This command uses the Crawl HQ system to manage the crawl.

## Configuration

Zeno supports multiple configuration methods with the following precedence (highest to lowest):

1. Command-line flags
2. Environment variables
3. Configuration file
4. Consul configuration

### Configuration File

By default, Zeno looks for a configuration file named `zeno-config.yaml` in the user's home directory. You can specify a different configuration file using the `--config-file` flag.

### Environment Variables

Zeno uses environment variables prefixed with `ZENO_`. Hyphens in flag names are replaced with underscores. For example, `--log-level` becomes `ZENO_LOG_LEVEL`.

### Consul Configuration

To use Consul for configuration, set the `--consul-config` flag to true and provide the `--consul-address` flag with the Consul server address.

### Configuration Options

Here are some of the key configuration options available:

- `log-level`: Set the stdout log level (debug, info, warn, error)
- `user-agent`: Set the User-Agent string for requests
- `job`: Job name to use for persistent queue, seencheck database, and WARC files
- `workers`: Number of concurrent workers to run
- `max-hops`: Maximum number of hops to execute
- `headless`: Use headless browsers instead of standard GET requests
- `warc-prefix`: Prefix for WARC files
- `proxy`: Proxy to use for requests
- `hq-address`: Crawl HQ address
- `hq-key`: Crawl HQ key
- `hq-secret`: Crawl HQ secret
- `hq-project`: Crawl HQ project

For a complete list of configuration options, refer to the `Config` struct in the `config.go` file or run `Zeno get --help`.

### Special Behaviors

- If `live-stats` is enabled, stdout logging is automatically disabled.
- If `prometheus` is enabled, the API is automatically enabled.

### Aliases

Some flags have aliases for backward compatibility:

- `hops` is an alias for `max-hops`
- `ca` is an alias for `max-concurrent-assets`
- `msr` is an alias for `min-space-required`

These aliases are deprecated and should be avoided in new configurations.

## Authors

- Corentin Barreau <corentin@archive.org>
- Jake LaFountain <jakelf@archive.org>
- Thomas Foubert <thomas@archive.org>

---

This updated documentation incorporates the configuration details from the `config.go` file, providing a more comprehensive overview of Zeno's configuration system and options. Users can refer to this documentation to understand how to configure Zeno for their specific needs.
