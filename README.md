# Admin Crawler

## Features

- Concurrent crawling with configurable number of workers
- Customizable user agent
- Cookie handling and global cookie jar support
- Headless browser support
- Local seen-check to avoid re-crawling
- JSON logging
- Live statistics
- API support with Prometheus metrics export
- Configurable redirect and retry limits
- Domain-specific crawling
- HTML tag filtering
- Proxy support with bypass options
- WARC file generation with customizable settings
- CDX deduplication
- ElasticSearch integration for crawl logs
- Crawl HQ integration for URL management
- Configurable crawl time limits
- Disk space management

## Installation

[Provide installation instructions here]

## Usage

Zeno provides several subcommands for different crawling scenarios:

### Basic Usage

To see all available commands and options:

```
./Zeno -h
```

### Crawling Specific URLs

To crawl specific URLs:

```
./Zeno get url [URL...]
```

### Crawling from a Seed List

To crawl using a seed list:

```
./Zeno get list [FILE]
```

### Crawling with Crawl HQ

To start crawling with the Crawl HQ connector:

```
./Zeno get hq [options]
```

## Configuration

Zeno supports a flexible configuration system with the following priority order:

1. Command-line flags
2. Environment variables (prefixed with `ZENO_`)
3. Configuration file (`zeno-config.yaml` in the user's home directory by default)
4. Consul configuration (if enabled)

### Key Configuration Options

- `--log-level`: Set the logging level (default: "info")
- `--user-agent`: Custom user agent (default: "Zeno")
- `--job`: Job name for persistent queue, seencheck database, and WARC files
- `--workers, -w`: Number of concurrent workers (default: 1)
- `--max-concurrent-assets`: Max concurrent assets per worker (default: 8)
- `--max-hops`: Maximum number of hops to execute (default: 0)
- `--headless`: Use headless browsers instead of standard GET requests
- `--local-seencheck`: Enable local seen-check to avoid re-crawling
- `--json`: Output logs in JSON format
- `--debug`: Enable debug logging
- `--live-stats`: Enable live statistics (disables standard logging)
- `--api`: Enable API for monitoring
- `--prometheus`: Export metrics in Prometheus format
- `--domains-crawl`: Treat seeds as domains to crawl
- `--proxy`: Specify a proxy for requests
- `--bypass-proxy`: Domains that should not be proxied
- `--crawl-time-limit`: Set a time limit for the crawl in seconds
- `--min-space-required`: Minimum space required in GB to continue the crawl (default: 20)
- `--http-timeout`: Number of seconds to wait before timing out a request (default: 30)
- `--max-concurrent-per-domain`: Maximum number of concurrent requests per domain (default: 16)
- `--concurrent-sleep-length`: Milliseconds to sleep when max concurrency per domain is reached (default: 500)

### WARC Configuration

- `--warc-prefix`: Set the prefix for WARC filenames (default: "ZENO")
- `--warc-operator`: Specify contact information for the crawl operator
- `--warc-cdx-dedupe-server`: Enable CDX deduplication and specify the server
- `--warc-on-disk`: Store WARC data on disk instead of RAM
- `--warc-pool-size`: Set the number of concurrent WARC files to write (default: 1)
- `--warc-temp-dir`: Specify a custom directory for WARC temporary files
- `--warc-dedupe-size`: Set the minimum size for WARC record deduplication (default: 1024 bytes)
- `--disable-local-dedupe`: Disable local URL agnostic deduplication
- `--cert-validation`: Enables certificate validation on HTTPS requests

### Crawl HQ Configuration

- `--hq-address`: Crawl HQ address
- `--hq-key`: Crawl HQ key
- `--hq-secret`: Crawl HQ secret
- `--hq-project`: Crawl HQ project
- `--hq-batch-size`: Crawl HQ feeding batch size
- `--hq-continuous-pull`: Enable continuous URL pulling from Crawl HQ
- `--hq-strategy`: Crawl HQ feeding strategy (default: "lifo")
- `--hq-rate-limiting-send-back`: Send back rate-limited URLs to Crawl HQ

### ElasticSearch Configuration

- `--es-url`: Comma-separated ElasticSearch URLs for log indexing
- `--es-user`: ElasticSearch username
- `--es-password`: ElasticSearch password
- `--es-index-prefix`: ElasticSearch index prefix (default: "zeno")

## WARC Processing

Zeno generates WARC (Web ARChive) files during crawling. The WARC writer is initialized at the start of the crawl process. Key features include:

- Configurable WARC file naming with customizable prefix
- GZIP compression
- CDX deduplication support
- Local deduplication option
- On-disk or in-memory processing
- Concurrent WARC file writing

## Crawl Process

1. The crawl starts by initializing the frontier, which manages the URLs to be crawled.
2. WARC writer is initialized with the specified settings.
3. HTTP client is set up for making requests and recording them in WARC format.
4. If specified, a proxy HTTP client is also initialized.
5. Workers are started to process URLs from the frontier.
6. If Crawl HQ is used, background processes for pulling and pushing seeds are started.
7. The crawl continues until it reaches the time limit or there are no more URLs to process.

## API and Monitoring

When enabled, Zeno provides an API for monitoring the crawl progress. Prometheus metrics can be exported for more detailed monitoring and alerting.

## Contributing

[Provide information on how to contribute to the project]

## License

[Specify the license information]

## Authors

- Corentin Barreau
- Jake LaFountain
- Thomas Foubert

## Acknowledgments

Zeno relies heavily on the warc module for traffic recording into WARC files.
