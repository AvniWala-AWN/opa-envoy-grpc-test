# opa-envoy-grpc-test


## Installation

Add following line to your /etc/hosts: <br>

```
      127.0.0.1 httpbin
```

$ cd ``directory-where-docker-compose-is``<br>
$ docker-compose up -d <br>

<br>

<b>For seeing allow operation decision logs:</b>

$ curl -X GET -v http://httpbin:18080

You should see a decision log like so in OPA:

```
opa_1            | {"bundles":{"nginx":{}},"decision_id":"80e24e8a-3c1b-4c3b-8bc1-a65c744c287c","input":{"attributes":{"destination":{"address":{"Address":{"SocketAddress":{"PortSpecifier":{"PortValue":80},"address":"192.168.144.4"}}}},"metadata_context":{},"request":{"http":{"headers":{":authority":"httpbin:18080",":method":"GET",":path":"/","accept":"*/*","user-agent":"curl/7.72.0","x-forwarded-proto":"http","x-request-id":"a2094131-0aa2-45be-bfe7-3b9037fab8ab"},"host":"httpbin:18080","id":"15668612591623305780","method":"GET","path":"/","protocol":"HTTP/1.1"},"time":{"nanos":993019000,"seconds":1624539171}},"source":{"address":{"Address":{"SocketAddress":{"PortSpecifier":{"PortValue":54934},"address":"192.168.144.1"}}}}},"parsed_body":null,"parsed_path":[""],"parsed_query":{},"truncated_body":false,"version":{"encoding":"encoding/json","ext_authz":"v2"}},"labels":{"id":"3089b485-79bf-4686-96fc-f55511c2be05","version":"0.28.0-envoy"},"level":"info","metrics":{"timer_rego_query_compile_ns":150700,"timer_rego_query_eval_ns":113100,"timer_server_handler_ns":801000},"msg":"Decision Log","query":"data.envoy.authz.allow","requested_by":"","result":{"allowed":true,"headers":{"x-ext-auth-deny-reason":"-"}},"time":"2021-06-24T12:52:52Z","timestamp":"2021-06-24T12:52:51.9997918Z","type":"openpolicyagent.org/decision_logs"}
```

<b>For seeing deny operation decision logs:</b>

$ curl -X PUT -v http://httpbin:18080

You should see a decision log like so in OPA:

```
opa_1            | {"bundles":{"nginx":{}},"decision_id":"d0cfa22f-4979-417e-9a75-5f9f0e7927c1","input":{"attributes":{"destination":{"address":{"Address":{"SocketAddress":{"PortSpecifier":{"PortValue":80},"address":"192.168.144.4"}}}},"metadata_context":{},"request":{"http":{"headers":{":authority":"httpbin:18080",":method":"PUT",":path":"/","accept":"*/*","user-agent":"curl/7.72.0","x-forwarded-proto":"http","x-request-id":"72313fdb-e662-4612-95ca-9d154beff5af"},"host":"httpbin:18080","id":"18165380986405074551","method":"PUT","path":"/","protocol":"HTTP/1.1"},"time":{"nanos":483860000,"seconds":1624539267}},"source":{"address":{"Address":{"SocketAddress":{"PortSpecifier":{"PortValue":54962},"address":"192.168.144.1"}}}}},"parsed_body":null,"parsed_path":[""],"parsed_query":{},"truncated_body":false,"version":{"encoding":"encoding/json","ext_authz":"v2"}},"labels":{"id":"3089b485-79bf-4686-96fc-f55511c2be05","version":"0.28.0-envoy"},"level":"info","metrics":{"timer_rego_query_eval_ns":316800,"timer_server_handler_ns":554800},"msg":"Decision Log","query":"data.envoy.authz.allow","requested_by":"","result":{"allowed":false,"headers":{"x-ext-auth-deny-reason":"PUT_NOT_ALLOWED"}},"time":"2021-06-24T12:54:27Z","timestamp":"2021-06-24T12:54:27.4882917Z","type":"openpolicyagent.org/decision_logs"}
```
