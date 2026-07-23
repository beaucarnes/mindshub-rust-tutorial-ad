# rust-systems-tracker

A lightweight systems diagnostics tool written in Rust. Tracks process metrics, disk I/O, CPU usage, and service health across multiple hosts — designed to run as a background daemon and expose data via a simple HTTP interface.

## Features

- Poll and aggregate system metrics at configurable intervals
- Track per-process CPU and memory over time
- Export metrics in Prometheus-compatible format via `/metrics`
- Configurable via `tracker.toml` — reload on `SIGHUP` without restart
- Cross-platform target: Linux primary, Windows in progress

## Getting Started

```bash
cargo build --release
cp tracker.toml.example tracker.toml
./target/release/rust-systems-tracker
```

Requires Rust 1.76+.

## Configuration

See `tracker.toml.example` for all available options. Key fields:

| Field | Default | Description |
|---|---|---|
| `polling_interval` | `5s` | How often to collect metrics |
| `max_processes` | `64` | Max tracked processes |
| `http_port` | `9090` | Port for the metrics endpoint |

## Project Structure

```
src/
  main.rs           # Entry point, signal handling
  collector.rs      # Metric collection loop
  http.rs           # Prometheus HTTP endpoint
data/
  issues.json       # Exported open issues (for tooling / dashboards)
```

## Open Issues

See the [Issues tab](../../issues) for current bugs and planned features.
Common themes right now: memory management, async I/O improvements, and cross-platform compatibility.

## License

MIT
