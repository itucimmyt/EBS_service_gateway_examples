# EBS_service_gateway_examples
simple use of basic components

# What's inside

## example project (Enterprise Service Bus project)

### examplePxS
A simple proxy service which routes incoming HTTP requests for batch processing, returning an HTTP Status Code 202: Accepted.

  - Log at the beginning shows context of the request as well as the body
  - The router expects URLs to have a query parameter 'name' which depending on its value route messages to different sequences
  
### switchPxS
A proxy service which uses switch mediator to route messages and return the response of the specific endpoint back to the client

 - Log shows the 'To' property, that is, the recipient of a message. For HTTP requests that means the URI of the request
 - /field-expt path will call a dummy Endpoint which returns a field API example 
 - /jsonb path will call an Endpoint which returns some data stored as jsonb column as String.
 - Switch defaults to a specific Sequence if nomatch is found
 
### transformPxS
A proxy service which invokes a data service and transforms the response before sending it to the client

 - Makes use o a Defined Endpoint (which can be reused across all the project)
 - Uses a Script mediator to transform the result with a JS function

### Sequences
Reusable series of mediators which perform more complex and/or specific tasks. 

### TaskExample
Timed action which emits a mesage to examplePxS proxy every 5 seconds up to five times. Tasks also support cron format for scheduling tasks.
WARNING: we are investigating how to unregister a task

## data services project

### nestingDS
Example of a dataservice with two datasources, one B4R and one Sample Manager database.

 - /req and /req2 are examples of nested queries from Sample Manager DB
 - /configs reads 5 records from B4R platform.config

Although there are not examples (yet), a data service can nest queries from all of their registered databases in one single query and expose it as one REST call.

