# Universal Services

DID Methods and Trusted Registries are mostly implemented on ledgers, to achieve
a high level of trust and transparency. In most cases, registries expose REST
API for obtaining information, whereas Create/Update/Delete (CUD) operations are
tightly related to the implementation/underlying technology.

The Universal Services architecture aims to abstract away the underlying
technology and enables to interact with a wide range of registries in a
universal/generic way.

## A high-level overview

Alice wants to interact with a Trusted Registry, e.g., a DID Registry. 
When Alice wants to read from the registry, she calls the REST APIs, e.g. 
`GET https://trusted.registry/v1/indentifiers`
[diagram goes here]
that returns a paginated list of all registered identifiers.

When Alice wants to write to the registry, she needs to call two APIs:
* insert/update/delete helper methods that construct an Operation Signing
  Request (OSR)
* signedOperations that processes the signed OSRs

1. Alice authenticates to the registry (optional for some registries)
2. Alice calls an inser/update/delete helper method with the required input
   arguments
3. The API checks the input method, validates the input arguments and creates an
   Operation Signing Request (OSR)
4. Alice receives the OSR and signs it
5. Alice sends the signed OSR to the Trusted Registry API
6. The API validates and performs the operation

The only technology dependency that remains is the required/supported signature
type.




## Universal APIs

The registry needs to support two sets of APIs:
* REST APIs
* JSON-RPC APIs

REST APIs enable to read from the registry, whereas JSON-RPC APIs help to
construct Operation Signing Requests (OSR) and validate and process the signed
OSRs.

Universal APIs or uAPIs are a collection of REST and JSON-RPC APIs that allow to
perform CRUD operations on registries, in a universal and
implementation-independent way.

Public (or restricted) registry resources SHOULD be available via REST APIs.
Read operations are generic and GET methods don't require any additional
content/payload/...

On the other hand, the Create/Update/Delete (CUD) operations on the registries
depend on the underlying implementation, especially if registries are
implmeneted on or supplemented with a ledger/DLT.

To increase interoperability, ..., registries SHOULD provide helper APIs for the
CUD operations.

As an example, let's consider a registry with a single collection:
/ssi-services/{ssi-service-name}

GET /v1/trusted-ssi-services returns a paginated list of ssi-service names
GET /v1/trusted-ssi-services/{name} returns information about the given SSI service

If registry is implemented on a ledger or the entries/changes must be signed,
the registry SHOULD provide an additional endpoint
- /v1/jsonrpc endpoint supporting methods:
    - insertSSIService
    - updateSSIService
    - deleteSSIService
    - signedOperations

The methods: 
    - insertSSIService
    - updateSSIService
    - deleteSSIService
return a operation signing request (OSR):
{
  "":
  "":
  "":
}

## Immutable APIs
