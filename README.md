# Prometheus

## Description
A server for monitoring events and services.

## Requirement
For Prometheus to monitor your services, they must be generating metrics that it can read, and must be exposing those metrics to it.

How each programming language sets this up is out of the scope of this README.

## Running the server
Just run the **docker-compose.yml** file

## Usage
Visit **localhost:9090** and query for the following metrics:
- For the GRPC server:
    * `grpc_server_started_total`: Total number of RPCs started on the server.
    * `grpc_server_handled_total`: Total number of RPCs completed on the server, regardless of success or failure.
    * `grpc_server_handled_latency_seconds`: (Optional) Histogram of response latency of rpcs handled by the server, in seconds.
    * `grpc_server_msg_received_total`: Total number of stream messages received from the client.
    * `grpc_server_msg_sent_total`: Total number of stream messages sent by the server.
- (any other metrics are to be added later)

## Modifying the configuration file
For Prometheus to find your services, you must add them to the **prometheus.yml** file.
1. Navigate to the end of the file
2. Find the **scrape_configs** section
3. Add a job using the following structure:
```yml
  - job_name: ${service_name}
    static_configs:
      - targets: [ ${address:port at which your metrics are exposed} ]
```