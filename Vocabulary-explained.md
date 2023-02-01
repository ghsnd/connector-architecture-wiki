The connector architecture exists of multiple components. On this page, all elements have a definition and little examples.

## Processor

A processor is a step inside a pipeline, often a data transformation. It can literally be anything, but in the connector architecture, a processor is usually a stream processor, transforming incoming data.
A processor is programming language independent and runtime independent, as long as a matching runner exists. 

Configuration is required per processor at two levels. On the highest level, a processor should be defined as an instance of the processor linked to the specific runner. This also makes it required to define the required fields (runner specific). A processor can also define required fields for the lower level of configuration, the actual instantiation.
_In short_: the high level is the processor declaration and the lower level is the instantiation in the pipeline.

### Example

```turtle
@prefix js: <https://w3id.org/conn/js#> .
@prefix fno: <https://w3id.org/function/ontology#> .
@prefix fnom: <https://w3id.org/function/vocabulary/mapping#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
@prefix : <https://w3id.org/conn#> .
@prefix sh: <http://www.w3.org/ns/shacl#> .

js:Print a js:JsProcess;
  js:file "./example.js";
  js:function "print";
  js:location <./>;
  js:mapping [
    a fno:Mapping;
    fno:parameterMapping [
      a fnom:PositionParameterMapping ;
      fnom:functionParameter js:message ;
      fnom:implementationParameterPosition "0"^^xsd:int
    ]
  ].
```

Here a javascript processor is defined with is an instance of `js:JsProcess`. `js:JsProcess` requires four fields: the file location, the function name, the root location, and a mapping object that defines the required parameters.


## Channel

Processors in the connector architecture are usually stream processors. The stream they consume or generate is technology independent. A channel is an instance of a stream between two processors, a transportation method of some kind. The easiest examples are websocket streams or kafka streams.

A channel consists of a `reader` and a `writer` part and can be linked in a channel.

Each channel has it's own configuration (separate for readers and writers) that defines the required fields. So here the configuration is also in two layers, the highest level says a channel type is created and defines the required fields. The lower level is an actual instantiation of these channels.

### Example

```turtle

```


## Connector

A connector is a piece of code that communicates with a channel for a specific runner.


## Pipeline

A pipeline is the total picture, the total data transformation happening. It can consist of multiple steps that link together. It does not have to be an easy left-to-right flow. Cycles and aggregations and everything in between are also supported.

The pipeline is configured in linked data and is constrained by all definitions of the used runners, processors, and channels.


## Runner
