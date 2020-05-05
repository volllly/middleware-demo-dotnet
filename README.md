# fiskaltrust.Middleware demo
Demo applications that demonstrate how to call the fiskaltrust.Middleware from .NET/C#. This repository contains examples for **GRPC**, **WCF** and **REST** based communication, using both JSON and XML.

## Getting Started

### Prerequisites
In order to use this demo application, the following prerequisites are required:
- *The demo application*: Either clone and run locally, or download the latest binaries from [Releases](https://github.com/fiskaltrust/middleware-de-demo-dotnet/releases)
- *The fiskaltrust.Middleware* running on your machine, which can be configured and downloaded via the fiskaltrust.Portal ([AT](https://portal.fiskaltrust.at), [DE](https://portal.fiskaltrust.de), [FR](https://portal.fiskaltrust.fr)). Start it up and let it run in the background to handle your requests.
- *Your Cashbox Id* is visible in the portal. It is also displayed in the startup console log of the Middleware. 

This example used the fiskaltrust.interface and the fiskaltrust.Middleware communication helper packages, which provide a convenient way to implement the middleware interface from .NET. These packages can be downloaded directly from [NuGet](https://www.nuget.org/profiles/fiskaltrust).

### Running the Demo
The Demo app needs three startup parameters: `cashbox-id`, `url` and `market`. The Middleware logs out all available endpoints (i.e. the URLs) as configured in the portal on startup. 

For the HTTP example, further parameters can optionally be provided (the communication type and the access token, with the latter only being required when connecting to SignaturCloud).

Minimal startup example:  

```powershell
fiskaltrust.Middleware.Demo.Grpc.exe --cashbox-id "54c6b434-cd27-442e-b39f-0960c4ad1bda" --url "grpc://localhost:13151"
```

If a parameter is not passed, the user will be prompted at startup.

1. The demo will show up a list of available demo receipts. Before execute any receipt, make sure that the SCU is initialized, by calling the *initial-operation-receipt*/the *start receipt*. 
2. To execute a receipt against the middleware, select it by its leading number and press Enter.
3. This will print the example and call it on the middleware with your defined endpoint. After the middleware processed the receipt, it will return the result back to the demo app, which prints it to the console. 
4. To go back to the list of receipts press a random key.

## Documentation
The full documentation for the interface can be found on https://docs.fiskaltrust.cloud. It is activeliy maintained and developed in our [interface-doc repository](https://github.com/fiskaltrust/interface-doc). 

More information is also available after logging into the portal with a user that has the _PosCreator_ role assigned.

### Communication
The fiskaltrust.Middleware supports different communication protocols, effectively giving our customers the possibility to use it on all platforms. Hence, different protocols are recommended for different platforms.

#### gRPC
gRPC is a cross-platform communication protocol and therefore widely supported by operating systems and programming frameworks. For using it with .NET, we provide a "code-first" client on NuGet. 

The .proto files (i.e. the interface description) can be used to generate clients for all supported programming languages and downloaded [here](https://github.com/fiskaltrust/interface-doc/tree/master/dist/protos).

*gRPC is not supported for Middleware versions < 1.3.*

#### WCF/SOAP
Our WCF implementation supports multiple communication technologies: 
- http
- https
- net.pipe
- net.tcp

Both the middleware and demo automatically detect the communication type for WCF from the given URL. **This option is only available when running on Windows**.

The WSDL file can be downloaded [here](https://github.com/fiskaltrust/interface-doc/tree/master/dist/WSDL).

#### HTTP/REST
HTTP/REST communication is available via JSON and XML, and probably the easiest approach for multi-platform communication. In Middleware versions < 1.3, the _REST helper_ is required - higher versions automatically support this protocol without any helpers.

#### User specific protocols
With the helper topology, it is possible to solve every scenario. Please contact our support if you required assistance for a special case scenario.

## Contributions
We welcome all kinds of contributions and feedback, e.g. via Issues or Pull Requests. 