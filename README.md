# Observability Stack

`docker compose` to spin up a Observability Stack
with `Grafana`, `Prometheus`, `Loki` and `OTEL Collector`.

## Usage

Run the stack

```bash
docker compose up -d
```

Stop the stack

```bash
# use -v if you want to force the volume to be deleted
docker compose down
```

## Services and ports

|                                         | Service | Port           | Container                    | Description |
| --------------------------------------- | ------- | -------------- | ---------------------------- | ----------- |
| [Grafana](http://localhost:3000)        | 3000    | grafana        | Grafana for visualization    |
| [Prometheus](http://localhost:9090)     | 9090    | prometheus     | Prometheus for metrics       |
| [Loki](http://localhost:3100)           | 3100    | loki           | Loki for logs                |
| [Otel Collector](http://localhost:4317) | 4317    | otel-collector | OpenTelemetry Collector GRPC |
| [Otel Collector](http://localhost:4318) | 4318    | otel-collector | OpenTelemetry Collector HTTP |

## Testing the observability stack

[test-obs-stack.http](../Infrastructure/open-telemetry/grafana-local/test-obs-stack.http) contains some requests that can be used to test the observability stack.
The file can be used with the [REST Client extension](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) in VS Code.
The most important requests are the ones that send data to the Otel Collector.
You can see the result in Grafana, Prometheus, and Loki.

## Retention policy

The retention policy for the logs in Loki is set to 15 days.
This means that logs older than 15 days will be automatically deleted.
The retention policy for the metrics in Prometheus is set to 15 days as well
with the addition that if the data is bigger than 5GB, the oldest data will be deleted first.
