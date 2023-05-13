---
api_metadata:
  apiVersion: "coordination.k8s.io/v1"
  import: "k8s.io/api/coordination/v1"
  kind: "Lease"
content_type: "api_reference"
description: "Lease defines a lease concept."
title: "Lease"
weight: 5
auto_generated: true
---

<!--
The file is auto-generated from the Go source code of the component using a generic
[generator](https://github.com/kubernetes-sigs/reference-docs/). To learn how
to generate the reference documentation, please read
[Contributing to the reference documentation](/docs/contribute/generate-ref-docs/).
To update the reference content, please follow the
[Contributing upstream](/docs/contribute/generate-ref-docs/contribute-upstream/)
guide. You can file document formatting bugs against the
[reference-docs](https://github.com/kubernetes-sigs/reference-docs/) project.
-->

`apiVersion: coordination.k8s.io/v1`

`import "k8s.io/api/coordination/v1"`

## Lease {#Lease}

Lease defines a lease concept.

<hr>

- **apiVersion**: coordination.k8s.io/v1

- **kind**: Lease

- **metadata** (<a href="{{< ref "../common-definitions/object-meta#ObjectMeta" >}}">ObjectMeta</a>)

  More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

- **spec** (<a href="{{< ref "../cluster-resources/lease-v1#LeaseSpec" >}}">LeaseSpec</a>)

  spec contains the specification of the Lease. More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#spec-and-status

## LeaseSpec {#LeaseSpec}

LeaseSpec is a specification of a Lease.

<hr>

- **acquireTime** (MicroTime)

  acquireTime is a time when the current lease was acquired.

  <a name="MicroTime"></a>
  _MicroTime is version of Time with microsecond level precision._

- **holderIdentity** (string)

  holderIdentity contains the identity of the holder of a current lease.

- **leaseDurationSeconds** (int32)

  leaseDurationSeconds is a duration that candidates for a lease need to wait to force acquire it. This is measure against time of last observed renewTime.

- **leaseTransitions** (int32)

  leaseTransitions is the number of transitions of a lease between holders.

- **renewTime** (MicroTime)

  renewTime is a time when the current holder of a lease has last updated the lease.

  <a name="MicroTime"></a>
  _MicroTime is version of Time with microsecond level precision._

## LeaseList {#LeaseList}

LeaseList is a list of Lease objects.

<hr>

- **apiVersion**: coordination.k8s.io/v1

- **kind**: LeaseList

- **metadata** (<a href="{{< ref "../common-definitions/list-meta#ListMeta" >}}">ListMeta</a>)

  Standard list metadata. More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

- **items** ([]<a href="{{< ref "../cluster-resources/lease-v1#Lease" >}}">Lease</a>), required

  items is a list of schema objects.

## Operations {#Operations}

<hr>

### `get` read the specified Lease

#### HTTP Request

GET /apis/coordination.k8s.io/v1/namespaces/{namespace}/leases/{name}

#### Parameters

- **name** (_in path_): string, required

  name of the Lease

- **namespace** (_in path_): string, required

  <a href="{{< ref "../common-parameters/common-parameters#namespace" >}}">namespace</a>

- **pretty** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#pretty" >}}">pretty</a>

#### Response

200 (<a href="{{< ref "../cluster-resources/lease-v1#Lease" >}}">Lease</a>): OK

401: Unauthorized

### `list` list or watch objects of kind Lease

#### HTTP Request

GET /apis/coordination.k8s.io/v1/namespaces/{namespace}/leases

#### Parameters

- **namespace** (_in path_): string, required

  <a href="{{< ref "../common-parameters/common-parameters#namespace" >}}">namespace</a>

- **allowWatchBookmarks** (_in query_): boolean

  <a href="{{< ref "../common-parameters/common-parameters#allowWatchBookmarks" >}}">allowWatchBookmarks</a>

- **continue** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#continue" >}}">continue</a>

- **fieldSelector** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#fieldSelector" >}}">fieldSelector</a>

- **labelSelector** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#labelSelector" >}}">labelSelector</a>

- **limit** (_in query_): integer

  <a href="{{< ref "../common-parameters/common-parameters#limit" >}}">limit</a>

- **pretty** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#pretty" >}}">pretty</a>

- **resourceVersion** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#resourceVersion" >}}">resourceVersion</a>

- **resourceVersionMatch** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#resourceVersionMatch" >}}">resourceVersionMatch</a>

- **sendInitialEvents** (_in query_): boolean

  <a href="{{< ref "../common-parameters/common-parameters#sendInitialEvents" >}}">sendInitialEvents</a>

- **timeoutSeconds** (_in query_): integer

  <a href="{{< ref "../common-parameters/common-parameters#timeoutSeconds" >}}">timeoutSeconds</a>

- **watch** (_in query_): boolean

  <a href="{{< ref "../common-parameters/common-parameters#watch" >}}">watch</a>

#### Response

200 (<a href="{{< ref "../cluster-resources/lease-v1#LeaseList" >}}">LeaseList</a>): OK

401: Unauthorized

### `list` list or watch objects of kind Lease

#### HTTP Request

GET /apis/coordination.k8s.io/v1/leases

#### Parameters

- **allowWatchBookmarks** (_in query_): boolean

  <a href="{{< ref "../common-parameters/common-parameters#allowWatchBookmarks" >}}">allowWatchBookmarks</a>

- **continue** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#continue" >}}">continue</a>

- **fieldSelector** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#fieldSelector" >}}">fieldSelector</a>

- **labelSelector** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#labelSelector" >}}">labelSelector</a>

- **limit** (_in query_): integer

  <a href="{{< ref "../common-parameters/common-parameters#limit" >}}">limit</a>

- **pretty** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#pretty" >}}">pretty</a>

- **resourceVersion** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#resourceVersion" >}}">resourceVersion</a>

- **resourceVersionMatch** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#resourceVersionMatch" >}}">resourceVersionMatch</a>

- **sendInitialEvents** (_in query_): boolean

  <a href="{{< ref "../common-parameters/common-parameters#sendInitialEvents" >}}">sendInitialEvents</a>

- **timeoutSeconds** (_in query_): integer

  <a href="{{< ref "../common-parameters/common-parameters#timeoutSeconds" >}}">timeoutSeconds</a>

- **watch** (_in query_): boolean

  <a href="{{< ref "../common-parameters/common-parameters#watch" >}}">watch</a>

#### Response

200 (<a href="{{< ref "../cluster-resources/lease-v1#LeaseList" >}}">LeaseList</a>): OK

401: Unauthorized

### `create` create a Lease

#### HTTP Request

POST /apis/coordination.k8s.io/v1/namespaces/{namespace}/leases

#### Parameters

- **namespace** (_in path_): string, required

  <a href="{{< ref "../common-parameters/common-parameters#namespace" >}}">namespace</a>

- **body**: <a href="{{< ref "../cluster-resources/lease-v1#Lease" >}}">Lease</a>, required

- **dryRun** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#dryRun" >}}">dryRun</a>

- **fieldManager** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#fieldManager" >}}">fieldManager</a>

- **fieldValidation** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#fieldValidation" >}}">fieldValidation</a>

- **pretty** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#pretty" >}}">pretty</a>

#### Response

200 (<a href="{{< ref "../cluster-resources/lease-v1#Lease" >}}">Lease</a>): OK

201 (<a href="{{< ref "../cluster-resources/lease-v1#Lease" >}}">Lease</a>): Created

202 (<a href="{{< ref "../cluster-resources/lease-v1#Lease" >}}">Lease</a>): Accepted

401: Unauthorized

### `update` replace the specified Lease

#### HTTP Request

PUT /apis/coordination.k8s.io/v1/namespaces/{namespace}/leases/{name}

#### Parameters

- **name** (_in path_): string, required

  name of the Lease

- **namespace** (_in path_): string, required

  <a href="{{< ref "../common-parameters/common-parameters#namespace" >}}">namespace</a>

- **body**: <a href="{{< ref "../cluster-resources/lease-v1#Lease" >}}">Lease</a>, required

- **dryRun** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#dryRun" >}}">dryRun</a>

- **fieldManager** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#fieldManager" >}}">fieldManager</a>

- **fieldValidation** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#fieldValidation" >}}">fieldValidation</a>

- **pretty** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#pretty" >}}">pretty</a>

#### Response

200 (<a href="{{< ref "../cluster-resources/lease-v1#Lease" >}}">Lease</a>): OK

201 (<a href="{{< ref "../cluster-resources/lease-v1#Lease" >}}">Lease</a>): Created

401: Unauthorized

### `patch` partially update the specified Lease

#### HTTP Request

PATCH /apis/coordination.k8s.io/v1/namespaces/{namespace}/leases/{name}

#### Parameters

- **name** (_in path_): string, required

  name of the Lease

- **namespace** (_in path_): string, required

  <a href="{{< ref "../common-parameters/common-parameters#namespace" >}}">namespace</a>

- **body**: <a href="{{< ref "../common-definitions/patch#Patch" >}}">Patch</a>, required

- **dryRun** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#dryRun" >}}">dryRun</a>

- **fieldManager** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#fieldManager" >}}">fieldManager</a>

- **fieldValidation** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#fieldValidation" >}}">fieldValidation</a>

- **force** (_in query_): boolean

  <a href="{{< ref "../common-parameters/common-parameters#force" >}}">force</a>

- **pretty** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#pretty" >}}">pretty</a>

#### Response

200 (<a href="{{< ref "../cluster-resources/lease-v1#Lease" >}}">Lease</a>): OK

201 (<a href="{{< ref "../cluster-resources/lease-v1#Lease" >}}">Lease</a>): Created

401: Unauthorized

### `delete` delete a Lease

#### HTTP Request

DELETE /apis/coordination.k8s.io/v1/namespaces/{namespace}/leases/{name}

#### Parameters

- **name** (_in path_): string, required

  name of the Lease

- **namespace** (_in path_): string, required

  <a href="{{< ref "../common-parameters/common-parameters#namespace" >}}">namespace</a>

- **body**: <a href="{{< ref "../common-definitions/delete-options#DeleteOptions" >}}">DeleteOptions</a>

- **dryRun** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#dryRun" >}}">dryRun</a>

- **gracePeriodSeconds** (_in query_): integer

  <a href="{{< ref "../common-parameters/common-parameters#gracePeriodSeconds" >}}">gracePeriodSeconds</a>

- **pretty** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#pretty" >}}">pretty</a>

- **propagationPolicy** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#propagationPolicy" >}}">propagationPolicy</a>

#### Response

200 (<a href="{{< ref "../common-definitions/status#Status" >}}">Status</a>): OK

202 (<a href="{{< ref "../common-definitions/status#Status" >}}">Status</a>): Accepted

401: Unauthorized

### `deletecollection` delete collection of Lease

#### HTTP Request

DELETE /apis/coordination.k8s.io/v1/namespaces/{namespace}/leases

#### Parameters

- **namespace** (_in path_): string, required

  <a href="{{< ref "../common-parameters/common-parameters#namespace" >}}">namespace</a>

- **body**: <a href="{{< ref "../common-definitions/delete-options#DeleteOptions" >}}">DeleteOptions</a>

- **continue** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#continue" >}}">continue</a>

- **dryRun** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#dryRun" >}}">dryRun</a>

- **fieldSelector** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#fieldSelector" >}}">fieldSelector</a>

- **gracePeriodSeconds** (_in query_): integer

  <a href="{{< ref "../common-parameters/common-parameters#gracePeriodSeconds" >}}">gracePeriodSeconds</a>

- **labelSelector** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#labelSelector" >}}">labelSelector</a>

- **limit** (_in query_): integer

  <a href="{{< ref "../common-parameters/common-parameters#limit" >}}">limit</a>

- **pretty** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#pretty" >}}">pretty</a>

- **propagationPolicy** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#propagationPolicy" >}}">propagationPolicy</a>

- **resourceVersion** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#resourceVersion" >}}">resourceVersion</a>

- **resourceVersionMatch** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#resourceVersionMatch" >}}">resourceVersionMatch</a>

- **sendInitialEvents** (_in query_): boolean

  <a href="{{< ref "../common-parameters/common-parameters#sendInitialEvents" >}}">sendInitialEvents</a>

- **timeoutSeconds** (_in query_): integer

  <a href="{{< ref "../common-parameters/common-parameters#timeoutSeconds" >}}">timeoutSeconds</a>

#### Response

200 (<a href="{{< ref "../common-definitions/status#Status" >}}">Status</a>): OK

401: Unauthorized
