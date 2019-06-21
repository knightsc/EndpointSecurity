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

# Usefulness?

Unfortunately this isn't actually that useful. Swift [can't call variadic C](https://developer.apple.com/documentation/swift/imported_c_and_objective-c_apis/using_imported_c_functions_in_swift) functions unless they use the `va_list` arguement type. Unfortunately the `es_subscribe` function simply uses the `...` notation. So while you can import this module and create a new client you can't actually subscribe to any events. For now at least the best way to use the Endpoint Security framework in Swift code is to create an Objective-C class and a bridging header.
