# Galateia Bluetooth JSON-RPC API Specification

[//]: # (TODO: view the spec link)

The Galateia JSON-RPC API Specification is a collection of methods that the 
pump implements and clients, i.e. Apps, can use to control the pump. 
This interface allows for log inspection (metrics) as well as downstream tooling 
(firmware upgrades) and provides the infrastructure to treat different Apps 
as modules that can be swapped at will.

## Building

The specification is split into multiple files to improve readability. It
can be compiled into a single document as follows:

```console
$ npm install
$ npm run build
Build successful.
```

This will output the file `openrpc.json` in the root of the project. This file
will have all schema `#ref`s resolved.

[//]: # (TODO: ## Testing)
