---
api_metadata:
  apiVersion: "rbac.authorization.k8s.io/v1"
  import: "k8s.io/api/rbac/v1"
  kind: "ClusterRoleBinding"
content_type: "api_reference"
description: "ClusterRoleBinding references a ClusterRole, but not contain it."
title: "ClusterRoleBinding"
weight: 7
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

`apiVersion: rbac.authorization.k8s.io/v1`

`import "k8s.io/api/rbac/v1"`

## ClusterRoleBinding {#ClusterRoleBinding}

ClusterRoleBinding references a ClusterRole, but not contain it. It can reference a ClusterRole in the global namespace, and adds who information via Subject.

<hr>

- **apiVersion**: rbac.authorization.k8s.io/v1

- **kind**: ClusterRoleBinding

- **metadata** (<a href="{{< ref "../common-definitions/object-meta#ObjectMeta" >}}">ObjectMeta</a>)

  Standard object's metadata.

- **roleRef** (RoleRef), required

  RoleRef can only reference a ClusterRole in the global namespace. If the RoleRef cannot be resolved, the Authorizer must return an error.

  <a name="RoleRef"></a>
  _RoleRef contains information that points to the role being used_

  - **roleRef.apiGroup** (string), required

    APIGroup is the group for the resource being referenced

  - **roleRef.kind** (string), required

    Kind is the type of resource being referenced

  - **roleRef.name** (string), required

    Name is the name of resource being referenced

- **subjects** ([]Subject)

  Subjects holds references to the objects the role applies to.

  <a name="Subject"></a>
  _Subject contains a reference to the object or user identities a role binding applies to. This can either hold a direct API object reference, or a value for non-objects such as user and group names._

  - **subjects.kind** (string), required

    Kind of object being referenced. Values defined by this API group are "User", "Group", and "ServiceAccount". If the Authorizer does not recognized the kind value, the Authorizer should report an error.

  - **subjects.name** (string), required

    Name of the object being referenced.

  - **subjects.apiGroup** (string)

    APIGroup holds the API group of the referenced subject. Defaults to "" for ServiceAccount subjects. Defaults to "rbac.authorization.k8s.io" for User and Group subjects.

  - **subjects.namespace** (string)

    Namespace of the referenced object. If the object kind is non-namespace, such as "User" or "Group", and this value is not empty the Authorizer should report an error.

## ClusterRoleBindingList {#ClusterRoleBindingList}

ClusterRoleBindingList is a collection of ClusterRoleBindings

<hr>

- **apiVersion**: rbac.authorization.k8s.io/v1

- **kind**: ClusterRoleBindingList

- **metadata** (<a href="{{< ref "../common-definitions/list-meta#ListMeta" >}}">ListMeta</a>)

  Standard object's metadata.

- **items** ([]<a href="{{< ref "../authorization-resources/cluster-role-binding-v1#ClusterRoleBinding" >}}">ClusterRoleBinding</a>), required

  Items is a list of ClusterRoleBindings

## Operations {#Operations}

<hr>

### `get` read the specified ClusterRoleBinding

#### HTTP Request

GET /apis/rbac.authorization.k8s.io/v1/clusterrolebindings/{name}

#### Parameters

- **name** (_in path_): string, required

  name of the ClusterRoleBinding

- **pretty** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#pretty" >}}">pretty</a>

#### Response

200 (<a href="{{< ref "../authorization-resources/cluster-role-binding-v1#ClusterRoleBinding" >}}">ClusterRoleBinding</a>): OK

401: Unauthorized

### `list` list or watch objects of kind ClusterRoleBinding

#### HTTP Request

GET /apis/rbac.authorization.k8s.io/v1/clusterrolebindings

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

200 (<a href="{{< ref "../authorization-resources/cluster-role-binding-v1#ClusterRoleBindingList" >}}">ClusterRoleBindingList</a>): OK

401: Unauthorized

### `create` create a ClusterRoleBinding

#### HTTP Request

POST /apis/rbac.authorization.k8s.io/v1/clusterrolebindings

#### Parameters

- **body**: <a href="{{< ref "../authorization-resources/cluster-role-binding-v1#ClusterRoleBinding" >}}">ClusterRoleBinding</a>, required

- **dryRun** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#dryRun" >}}">dryRun</a>

- **fieldManager** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#fieldManager" >}}">fieldManager</a>

- **fieldValidation** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#fieldValidation" >}}">fieldValidation</a>

- **pretty** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#pretty" >}}">pretty</a>

#### Response

200 (<a href="{{< ref "../authorization-resources/cluster-role-binding-v1#ClusterRoleBinding" >}}">ClusterRoleBinding</a>): OK

201 (<a href="{{< ref "../authorization-resources/cluster-role-binding-v1#ClusterRoleBinding" >}}">ClusterRoleBinding</a>): Created

202 (<a href="{{< ref "../authorization-resources/cluster-role-binding-v1#ClusterRoleBinding" >}}">ClusterRoleBinding</a>): Accepted

401: Unauthorized

### `update` replace the specified ClusterRoleBinding

#### HTTP Request

PUT /apis/rbac.authorization.k8s.io/v1/clusterrolebindings/{name}

#### Parameters

- **name** (_in path_): string, required

  name of the ClusterRoleBinding

- **body**: <a href="{{< ref "../authorization-resources/cluster-role-binding-v1#ClusterRoleBinding" >}}">ClusterRoleBinding</a>, required

- **dryRun** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#dryRun" >}}">dryRun</a>

- **fieldManager** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#fieldManager" >}}">fieldManager</a>

- **fieldValidation** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#fieldValidation" >}}">fieldValidation</a>

- **pretty** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#pretty" >}}">pretty</a>

#### Response

200 (<a href="{{< ref "../authorization-resources/cluster-role-binding-v1#ClusterRoleBinding" >}}">ClusterRoleBinding</a>): OK

201 (<a href="{{< ref "../authorization-resources/cluster-role-binding-v1#ClusterRoleBinding" >}}">ClusterRoleBinding</a>): Created

401: Unauthorized

### `patch` partially update the specified ClusterRoleBinding

#### HTTP Request

PATCH /apis/rbac.authorization.k8s.io/v1/clusterrolebindings/{name}

#### Parameters

- **name** (_in path_): string, required

  name of the ClusterRoleBinding

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

200 (<a href="{{< ref "../authorization-resources/cluster-role-binding-v1#ClusterRoleBinding" >}}">ClusterRoleBinding</a>): OK

201 (<a href="{{< ref "../authorization-resources/cluster-role-binding-v1#ClusterRoleBinding" >}}">ClusterRoleBinding</a>): Created

401: Unauthorized

### `delete` delete a ClusterRoleBinding

#### HTTP Request

DELETE /apis/rbac.authorization.k8s.io/v1/clusterrolebindings/{name}

#### Parameters

- **name** (_in path_): string, required

  name of the ClusterRoleBinding

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

### `deletecollection` delete collection of ClusterRoleBinding

#### HTTP Request

DELETE /apis/rbac.authorization.k8s.io/v1/clusterrolebindings

#### Parameters

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
