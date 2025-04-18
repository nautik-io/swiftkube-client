# Changelog

## 0.23.0

- Update to Kubernetes model v1.32.2
- Add client support for proxy URLs (#43 by @ewilken)
- Add client support for gzipped server responses (#43 by @ewilken)
- Add an optional `tailLines` parameter to the log request to be able to limit the number of lines requested from the server (#43 by @ewilken)
- Fix a bug on `RequestBuilder` where a path was overwritten where it should have been appended (#43 by @ewilken)
  - This became apparent with users using Rancher, where the base path already had a `/` in it
- Add a `doesNotExist` variant to `LabelSelectorRequirement`, akin to the upstream "DoesNotExist" variant on selectors (#43 by @ewilken)
- Add the upstream `installHint`, `provideClusterInfo` and `interactiveMode` fields to ExecConfig (#43 by @ewilken)
- Make `ExecCredential` public too able to base custom exec implementations on top of it (#43 by @ewilken)
- Add public initializers to `Cluster` and `AuthInfo` (#43 by @ewilken)
- Make `Cluster`, `AuthInfo`, `AuthProviderConfig`, `ExecConfig` and `ExecEnvVar` conform to Hashable and Equatable (#43 by @ewilken)

## 0.22.0

- Make immutable and non-mutating client properties nonisolated
 
## 0.21.0

- Make client implementations actors
- Mark synchronous shutdown methods as nonisolated
- Make API-Groups protocols and implementations as Sendable

## 0.20.0

- Mark configuration structs as Sendable
- Mark `NamespaceSelector`, `LabelSelectorRequirement`, `FieldSelectorRequirement` as Sendable
- Mark `ListOption` and `ReadOptions` as Sendable
- Make client's `watch` and `follow` functions asynchronous

## 0.19.0

### New

- Update to Kubernetes model v1.32.0
- Update dependencies:
  - Async HTTP Client 1.24.2
  - Kubernetes 1.32.0
  - SwiftkubeModel 0.16.0
  - SwiftNIO 2.80.0
  - SwiftLog 1.6.2
  - SwiftMetrics 2.5.1
  - Yams 5.1.3
- Add function to create `KubernetesClientConfig` from string  #41
- Add support for Swift 6 and strict concurrency

### Breaking Change

- Raise minimum Swift version to 5.9
- Raise minimum supported macOS platform version to 12
- `KubernetesResources` is `Sendable` now
  - Any CRDs conforming to `KubernetesResources` must be `Sendable`
- `SwiftkubeClientTask` is an actor now and all its public methods are async
  - Previous calls to `task.start()` must be changed to `await task.start()`


## 0.18.0

### New

- Update to Kubernetes model v1.29.6
- Update dependencies:
  - Async HTTP Client 1.21.2
  - Kubernetes 1.29.6
  - SwiftkubeModel 0.14.0
  - SwiftNIO 2.67.0
  - SwiftLog 1.6.1
  - SwiftMetrics 2.5.0
  - Yams 5.1.2

### Fixes

- Set hard limit for maximum amount of bytes to collect in RequestHandler #40

### Breaking Change

- Raise minimum Swift version to 5.8
  - This aligns supported Swift versions with rest of the ecosystem


## 0.17.0

### New

- Update dependencies:
  - Async HTTP Client 1.19.0
  - Kubernetes 1.28.3
  - SwiftkubeModel 0.13.0
  - SwiftNIO 2.61.0

## 0.16.0

### New

- Update to Kubernetes model v1.28.0
- Add support for exec kube config #29 by @portellaa

### Fixes

- Use DeleteOptions on delete resource #34 by @tallnato

## 0.15.0

### New

- Update to Kubernetes model v1.26.4
- Add support for `resourceVersion` in streaming task

### Fixes

- Set the default response body buffer size for requests returning String to 10MB #30 by @ewilken 
- Fix streaming issues when watching resources with small payloads #31 

### Breaking Changes

- Drop support for Swift 5.5

## 0.14.0

### New

- Update to Kubernetes model v1.24.10

### Fixes

- Fix decoding error when deleting a service #27

### Breaking Changes

- `SwiftkubeModel 0.8.0` makes all `KubernetesResources` Hashable #28 

## 0.13.0

### New

- Use structured concurrency instead of EventLoops for watching resources #25

### Fixes

- Fix client crash in `GenericKubernetesClient.prepareDecoder` due to decoder instance being shared #24
 
### Breaking Changes

- Drop AnyKubernetesAPIResource in favour of UnstructuredResource
- The generic client for a given `GroupVersionResource` uses `UnstructuredResource` for unknown types:
  - `KubernetesClient/``for``(gvr:) -> GenericKubernetesClient<AnyKubernetesAPIResource>` is replaced with:
  - `KubernetesClient/``for``(gvr:) -> GenericKubernetesClient<UnstructuredResource>`
- The `SwiftkubeClientTask` returned by the `watch` and `follow` API must be started explicitly
- The `SwiftkubeClientTask` returns an `AsyncThrowingStream` instead of using a callback delegate 

## 0.12.0

### New

- Update to Kubernetes model v1.24.8
- Update dependencies
  - Async HTTP Client 1.13.1
  - SwiftkubeModel 0.6.0
  - SwiftLog 1.4.4
  - SwiftMetrics 2.3.3
  - SwiftNIO 2.46.0
  - Yams 5.0.1
- Update k3s docker image to k3s:v1.24.8-k3s1
- Add configurable timeout and redirect config for the underlying HTTPClient by @octo47
- Update documentation comments

### Breaking Changes

- Raise minimum supported Swift version to 5.5
- Replace `EventLoops` with `async/await` style API

## 0.11.0

### New

- Update to Kubernetes model v1.22.7
- Add option to retrieve logs once without watching / streaming (#14) by @thomashorrobin
- Add discovery API to load server resources
- Use SwiftkubeModel v0.5.0
- Refactor client to use `GroupVersionResource` instead of `GroupVersionKind` for resource type resolution
- Support creating a parametrised generic client given a `GroupVersionResource`
- Make `GenericKubernetesClient` extensions public
- Update k3s docker image to k3s:v1.22.7-k3s1

### Fixes

- Typo in property name for storage.v1 API Group (#11) by @portellaa
- Add explicit dependency on NIO (#12) by @t089 

## 0.10.0

### New

- Update to Kubernetes model v1.20.9
- Add `LocalFileConfigLoader` for loading KubeConfigs from a local file given a URL #8 by @thomashorrobin
- Add support for `scale` and `status` API
- Setup CI with live K3d cluster and add several tests against it

### Bug Fixes

- Add missing support for `continue` token in  `ListOption` for retrieving subsequent list results #9
- Track dependency on SwiftkubeModel up-to-next minor instead of major #10 

## 0.9.0

- Add supported platforms for Swift package
- Add CI for iOS build

## 0.8.0

### New

- DSL for all API Groups/Versions

## 0.7.0

### New

- Update to Kubernetes model v1.19.8
- Discovery for server API groups and versions 

## 0.6.1

### Bug Fixes

- Fix SwiftkubeClientTask cancelling
 
## 0.6.0

### New

- Implement asynchronous shutdown
- Implement reconnect handling for `watch` and `follow` API requests
- Introduce `ResourceWatcherDelegate` and `LogWatcherDelegate` protocols

### API Changes

- Changed signature of `watch` and `follow` APIs.
- Replace `ResourceWatch` and `LogWatch` with new protocols 
- The `follow` and `watch` functions return a cancellable `SwiftkubeClientTask` instance insteaf of `HTTPClient.Task<Void>`.


## 0.5.0

### New

- Add metrics support for gathering request latencies and counts
- Support `ListOptions` in watch call
- Add `watch` and `follow` API that accept a `RecourceWatch` or `LogWatch` instance
- Add an `errorHandler` closure to `ResourceWatch` and `LogWatch`
- Make Selectors (`NamespaceSelector`, `LabelSelector` etc.) Hashable

### API Changes

- Replace implicit client shutdown on deinit with explicit `syncShutdow`
- Expose `ResourceWatch` and `LogWatch` classes for extension

## 0.4.0

### New

- Add SwiftFormat config and format code base accordingly
- Add support for `ReadOptions`

### Bug Fixes

- Fix massive memory leak by breaking retain cycle between the `JSONDecoder` and `DateFormatters` #4 by @t089

## 0.3.2

- Change personal copyright to Swiftkube Project
- Make `KubernetesClientConfig` initializer public #3

## 0.3.1

- Update to Kubernetes model v1.18.13
  - No model changes between 1.18.9 and 1.18.13. This release is to track the update explicitly via a version bump.

## 0.3.0

### New

- Add support for `DeleteOptions`

### Bug Fixes

- Can not create resources because of "Resource `metadata.name` must be set" error #2 

## 0.2.0

### New

- Add support for `ListOptions`
- Add `core.v1.Pod` status read and update API

### Bug Fixes

- KubernetesClient can't create x509 authentication from local kubeconfig's certificate data and key #1

### API Changes

- Initializers of `GenericKubernetesClients` are no longer public
- Function signature change:
  - from `watch(in:watch:) throws -> EventLoopFuture<Void>`
  - to `watch(in:using:) throws -> HTTPClient.Task<Void>`
- Function signature change:
  -  from`follow(in:name:container:watch:) throws -> HTTPClient.Task<Void>`
  -  to `follow(in:name:container:using:) throws -> HTTPClient.Task<Void>`

## 0.1.0

Initial release
