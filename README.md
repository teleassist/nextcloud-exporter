# nextcloud-exporter

A [prometheus](https://prometheus.io) exporter for getting some metrics of a nextcloud server instance.

## Installation

If you have a working Go installation, getting the binary should be as simple as

```bash
go get github.com/kylegrantlucas/nextcloud-exporter
```

## Client credentials

To access the serverinfo API you will need the credentials of an admin user. It is recommended to create a separate user for that purpose.

## Usage

```
$ nextcloud-exporter --help
Usage of nextcloud-exporter:
  -a, --addr string        Address to listen on for connections. (default ":9205")
  -p, --password string    Password for connecting to nextcloud.
  -t, --timeout duration   Timeout for getting server info document. (default 5s)
  -l, --url string         URL to nextcloud serverinfo page.
  -u, --username string    Username for connecting to nextcloud.
```

After starting the server will offer the metrics on the `/metrics` endpoint, which can be used as a target for prometheus.

The exporter will query the nextcloud server every time it is scraped by prometheus. If you want to reduce load on the nextcloud server you need to change the scrape interval accordingly:

```yml
scrape_configs:
  - job_name: 'nextcloud'
    scrape_interval: 90s
    static_configs:
      - targets: ['localhost:9205']
```
