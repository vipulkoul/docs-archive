# Puppet orchestrator API: inventory endpoint

Use the `/inventory` endpoint to discover which nodes can be reached by the orchestrator.

## GET /inventory

List all nodes that are connected to the PCP broker.

### Response format

The response is a JSON object containing a list of records for connected nodes, using these keys:

|Key|Definition|
|---|----------|
|`name`|The name of the connected node.|
|`connected`|The connection status is either `true` or `false`.|
|`broker`|The PCP broker the node is connected to.|
|`timestamp`|The time when the connection was made.|

For example:

```json
{
  "items" : [
    {
      "name" : "foo.example.com",
      "connected" : true,
      "broker" : "pcp://broker1.example.com/server",
      "timestamp": "2016-010-22T13:36:41.449Z"
    },
    {
      "name" : "bar.example.com",
      "connected" : true,
      "broker" : "pcp://broker2.example.com/server",
      "timestamp" : "2016-010-22T13:39:16.377Z"
    }
  ]
}
```

### Error responses

For this endpoint, the `kind` key of the error displays the conflict.

The server returns a 500 response if the PCP broker can't be reached.

**Related information**  


[Puppet orchestrator API: error responses](orchestrator_api_error_responses.md)

## GET /inventory/:node

Return information about whether the requested node is connected to the PCP broker.

### Response format

The response is a JSON object indicating whether the queried node is connected, using these keys:

|Key|Definition|
|---|----------|
|`name`|The name of the connected node.|
|`connected`|The connection status is either `true` or `false`.|
|`broker`|The PCP broker the node is connected to.|
|`timestamp`|The time when the connection was made.|

For example:

```json
{
  "name" : "foo.example.com",
  "connected" : true,
  "broker" : "pcp://broker.example.com/server",
  "timestamp" : "2017-03-29T21:48:09.633Z"
}
```

### Error responses

For this endpoint, the `kind` key of the error displays the conflict.

The server returns a 500 response if the PCP broker can't be reached.

**Related information**  


[Puppet orchestrator API: error responses](orchestrator_api_error_responses.md)

## POST /inventory

Check if the given list of nodes is connected to the PCP broker.

### Request format

The request body is a JSON object specifying a list of nodes to check. For example:

```json
{
  "nodes" : [
    "foo.example.com",
    "bar.example.com",
    "baz.example.com"
  ]
}
```

### Response format

The response is a JSON object with a record for each node in the request, using these keys:

|Key|Definition|
|---|----------|
|`name`|The name of the connected node.|
|`connected`|The connection status is either `true` or `false`.|
|`broker`|The PCP broker the node is connected to.|
|`timestamp`|The time when the connection was made.|

For example:

```json
{
  "items" : [
    {
      "name" : "foo.example.com",
      "connected" : true,
      "broker" : "pcp://broker.example.com/server",
      "timestamp" : "2017-07-14T15:57:33.640Z"
    },
    {
      "name" : "bar.example.com",
      "connected" : false
    },
    {
      "name" : "baz.example.com",
      "connected" : true,
      "broker" : "pcp://broker.example.com/server",
      "timestamp" : "2017-07-14T15:41:19.242Z"
    }
  ]
}
```

### Error responses

For this endpoint, the `kind` key of the error displays the conflict.

The server returns a 500 response if the PCP broker can't be reached.

**Related information**  


[Puppet orchestrator API: error responses](orchestrator_api_error_responses.md)

