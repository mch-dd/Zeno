# Zeno: State-of-the-Art Web Crawler 🔱

Zeno is a cutting-edge web crawler designed for both wide-scale crawls and single-page archiving. Named after Zenodotus, the first librarian of the ancient Library of Alexandria, Zeno embodies the spirit of knowledge preservation in the digital age.

## Introduction

Originally developed by Corentin Barreau at the Internet Archive, Zeno stands on three pillars:

1. Portability
2. Performance
3. Simplicity

With a strong emphasis on performance, Zeno leverages the powerful `warc` module for efficient traffic recording into WARC files, ensuring high-fidelity web archiving.

## Features

- Extract URLs from WARC files
- Fetch web pages with configurable concurrency
- Process and analyze web archive data
- Highly configurable with multiple configuration methods
- Headless browsing capability for JavaScript-rendered content
- Intelligent concurrency control
- Time-limited crawls
- CDX deduplication
- Prometheus integration for metrics
- API access for crawl control

## Getting Started

### Prerequisites

- Go 1.18+ installed on your machine
- Access to web pages or WARC files for processing

### Installation

1. Clone the repository:
    ```bash
    git clone https://github.com/internetarchive/Zeno.git
    cd Zeno
    ```

2. Build the project:
    ```bash
    go build -o zeno
    ```

## Usage

Zeno's powerful features are accessible through an intuitive command-line interface. To get started, simply run:

```bash
./zeno [command] [flags]
```

For a comprehensive list of commands and options, use:

```bash
./zeno -h
```

### Commands

Zeno offers several commands to cater to different archiving needs:

#### get

The `get` command is the heart of Zeno, used for archiving web content. It offers three specialized subcommands:

##### get url

Archive specific URLs:

```bash
./zeno get url [URL...] [flags]
```

##### get list

Start crawling with a seed list:

```bash
./zeno get list [FILE] [flags]
```

##### get hq

Leverage the power of Crawl HQ for managed crawls:

```bash
./zeno get hq [flags]
```

#### version

Display the current version of Zeno:

```bash
./zeno version
```

#### help

Access help information for any command:

```bash
./zeno help [command]
```

### Configuration

Zeno offers unparalleled flexibility in configuration, supporting multiple methods with a clear precedence:

1. Command-line flags
2. Environment variables
3. Configuration file
4. Consul configuration

#### Configuration File

By default, Zeno looks for a `zeno-config.yaml` file in the user's home directory. Customize the config file location with the `--config-file` flag.

#### Environment Variables

Easily integrate Zeno into your workflow using environment variables prefixed with `ZENO_`. For example, set the log level with `ZENO_LOG_LEVEL`.

#### Key Configuration Options

- `--user-agent`: Customize the User-Agent string (default: "Zeno")
- `--workers, -w`: Set the number of concurrent workers (default: 1)
- `--max-hops`: Limit the crawl depth (default: 0, unlimited)
- `--headless`: Use headless browsers for JavaScript-heavy sites
- `--warc-prefix`: Customize WARC file naming (default: "ZENO")
- `--proxy`: Specify a proxy for network requests
- `--hq-address`: Connect to a Crawl HQ instance for advanced crawl management

For a full list of options, refer to the output of `./zeno -h` or check the `Config` struct in `config.go`.

### Example

Here is an example of how to run Zeno to crawl a list of URLs:

```bash
./zeno get list seed_urls.txt --workers 10 --max-hops 3 --warc-prefix "MY_CRAWL"
```

## Files in the Repository

- `cmd/`: Contains command-related files (`cmd.go`, `get.go`, `get_hq.go`, `get_list.go`, `get_url.go`)
- `config/`: Configuration-related files (`config.go`)
- `internal/pkg/`: Core functionality packages
- `main.go`: Main entry point for Zeno
- `main_test.go`: Tests for the main functionality
- `README.md`: This file
- `LICENSE`: License information

## Contributing

Contributions are welcome! Please fork the repository and submit a pull request for any enhancements or bug fixes.

## Authors and Contributors

Zeno is the result of collaborative effort from talented developers:

- Corentin Barreau ([@CorentinB](https://github.com/CorentinB)) - Original creator
- Jake LaFountain ([@NGTmeaty](https://github.com/NGTmeaty))
- Thomas Foubert ([@equals215](https://github.com/equals215))

## License

This project is licensed under the AGPL-3.0 License - see the [LICENSE](LICENSE) file for details.

---

Join the Zeno community! Star the [GitHub repository](https://github.com/internetarchive/Zeno), watch for updates, or contribute to its development. Whether you're preserving a single page or embarking on a web-wide crawl, Zeno provides the power, flexibility, and efficiency you need. Start exploring the web's past and present with Zeno today!
```

This README.md now combines the detailed information about Zeno with the structure of a typical GitHub project README, making it both informative and easy to navigate for potential users and contributors.
