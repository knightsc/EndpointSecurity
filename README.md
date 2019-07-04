# EndpointSecurity

This module allows you to import the C based Endpoint Security framework into your Swift code. You will also need to link against libEndpointSecurity.dylib. If you want to read more about exposing C headers to Swift you can see the Clang documentation [here](https://clang.llvm.org/docs/Modules.html#module-maps).

## Usage

```swift
import EndpointSecurity

var client: OpaquePointer?

let res = es_new_client(&client) { (client, message) in
    // Do something with events
}

guard res == ES_NEW_CLIENT_RESULT_SUCCESS else {
    fatalError("Could not connect to endpoint security subsystem.")
}
```

# Building

```shell
swiftc -I ./EndpointSecurity test.swift -lEndpointSecurity
```
