---
api_metadata:
  apiVersion: "flowcontrol.apiserver.k8s.io/v1beta3"
  import: "k8s.io/api/flowcontrol/v1beta3"
  kind: "FlowSchema"
content_type: "api_reference"
description: "FlowSchema defines the schema of a group of flows."
title: "FlowSchema v1beta3"
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

`apiVersion: flowcontrol.apiserver.k8s.io/v1beta3`

`import "k8s.io/api/flowcontrol/v1beta3"`

## FlowSchema {#FlowSchema}

FlowSchema defines the schema of a group of flows. Note that a flow is made up of a set of inbound API requests with similar attributes and is identified by a pair of strings: the name of the FlowSchema and a "flow distinguisher".

<hr>

- **apiVersion**: flowcontrol.apiserver.k8s.io/v1beta3

- **kind**: FlowSchema

- **metadata** (<a href="{{< ref "../common-definitions/object-meta#ObjectMeta" >}}">ObjectMeta</a>)

  `metadata` is the standard object's metadata. More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

- **spec** (<a href="{{< ref "../cluster-resources/flow-schema-v1beta3#FlowSchemaSpec" >}}">FlowSchemaSpec</a>)

  `spec` is the specification of the desired behavior of a FlowSchema. More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#spec-and-status

- **status** (<a href="{{< ref "../cluster-resources/flow-schema-v1beta3#FlowSchemaStatus" >}}">FlowSchemaStatus</a>)

  `status` is the current status of a FlowSchema. More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#spec-and-status

## FlowSchemaSpec {#FlowSchemaSpec}

FlowSchemaSpec describes how the FlowSchema's specification looks like.

<hr>

- **priorityLevelConfiguration** (PriorityLevelConfigurationReference), required

  `priorityLevelConfiguration` should reference a PriorityLevelConfiguration in the cluster. If the reference cannot be resolved, the FlowSchema will be ignored and marked as invalid in its status. Required.

  <a name="PriorityLevelConfigurationReference"></a>
  _PriorityLevelConfigurationReference contains information that points to the "request-priority" being used._

  - **priorityLevelConfiguration.name** (string), required

    `name` is the name of the priority level configuration being referenced Required.

- **distinguisherMethod** (FlowDistinguisherMethod)

  `distinguisherMethod` defines how to compute the flow distinguisher for requests that match this schema. `nil` specifies that the distinguisher is disabled and thus will always be the empty string.

  <a name="FlowDistinguisherMethod"></a>
  _FlowDistinguisherMethod specifies the method of a flow distinguisher._

  - **distinguisherMethod.type** (string), required

    `type` is the type of flow distinguisher method The supported types are "ByUser" and "ByNamespace". Required.

- **matchingPrecedence** (int32)

  `matchingPrecedence` is used to choose among the FlowSchemas that match a given request. The chosen FlowSchema is among those with the numerically lowest (which we take to be logically highest) MatchingPrecedence. Each MatchingPrecedence value must be ranged in [1,10000]. Note that if the precedence is not specified, it will be set to 1000 as default.

- **rules** ([]PolicyRulesWithSubjects)

  _Atomic: will be replaced during a merge_

  `rules` describes which requests will match this flow schema. This FlowSchema matches a request if and only if at least one member of rules matches the request. if it is an empty slice, there will be no requests matching the FlowSchema.

  <a name="PolicyRulesWithSubjects"></a>
  _PolicyRulesWithSubjects prescribes a test that applies to a request to an apiserver. The test considers the subject making the request, the verb being requested, and the resource to be acted upon. This PolicyRulesWithSubjects matches a request if and only if both (a) at least one member of subjects matches the request and (b) at least one member of resourceRules or nonResourceRules matches the request._

  - **rules.subjects** ([]Subject), required

    _Atomic: will be replaced during a merge_

    subjects is the list of normal user, serviceaccount, or group that this rule cares about. There must be at least one member in this slice. A slice that includes both the system:authenticated and system:unauthenticated user groups matches every request. Required.

    <a name="Subject"></a>
    _Subject matches the originator of a request, as identified by the request authentication system. There are three ways of matching an originator; by user, group, or service account._

    - **rules.subjects.kind** (string), required

      `kind` indicates which one of the other fields is non-empty. Required

    - **rules.subjects.group** (GroupSubject)

      `group` matches based on user group name.

      <a name="GroupSubject"></a>
      _GroupSubject holds detailed information for group-kind subject._

      - **rules.subjects.group.name** (string), required

        name is the user group that matches, or "\*" to match all user groups. See https://github.com/kubernetes/apiserver/blob/master/pkg/authentication/user/user.go for some well-known group names. Required.

    - **rules.subjects.serviceAccount** (ServiceAccountSubject)

      `serviceAccount` matches ServiceAccounts.

      <a name="ServiceAccountSubject"></a>
      _ServiceAccountSubject holds detailed information for service-account-kind subject._

      - **rules.subjects.serviceAccount.name** (string), required

        `name` is the name of matching ServiceAccount objects, or "\*" to match regardless of name. Required.

      - **rules.subjects.serviceAccount.namespace** (string), required

        `namespace` is the namespace of matching ServiceAccount objects. Required.

    - **rules.subjects.user** (UserSubject)

      `user` matches based on username.

      <a name="UserSubject"></a>
      _UserSubject holds detailed information for user-kind subject._

      - **rules.subjects.user.name** (string), required

        `name` is the username that matches, or "\*" to match all usernames. Required.

  - **rules.nonResourceRules** ([]NonResourcePolicyRule)

    _Atomic: will be replaced during a merge_

    `nonResourceRules` is a list of NonResourcePolicyRules that identify matching requests according to their verb and the target non-resource URL.

    <a name="NonResourcePolicyRule"></a>
    _NonResourcePolicyRule is a predicate that matches non-resource requests according to their verb and the target non-resource URL. A NonResourcePolicyRule matches a request if and only if both (a) at least one member of verbs matches the request and (b) at least one member of nonResourceURLs matches the request._

    - **rules.nonResourceRules.nonResourceURLs** ([]string), required

      _Set: unique values will be kept during a merge_

      `nonResourceURLs` is a set of url prefixes that a user should have access to and may not be empty. For example:

      - "/healthz" is legal
      - "/hea\*" is illegal
      - "/hea" is legal but matches nothing
      - "/hea/\*" also matches nothing
      - "/healthz/_" matches all per-component health checks.
        "_" matches all non-resource urls. if it is present, it must be the only entry. Required.

    - **rules.nonResourceRules.verbs** ([]string), required

      _Set: unique values will be kept during a merge_

      `verbs` is a list of matching verbs and may not be empty. "\*" matches all verbs. If it is present, it must be the only entry. Required.

  - **rules.resourceRules** ([]ResourcePolicyRule)

    _Atomic: will be replaced during a merge_

    `resourceRules` is a slice of ResourcePolicyRules that identify matching requests according to their verb and the target resource. At least one of `resourceRules` and `nonResourceRules` has to be non-empty.

    <a name="ResourcePolicyRule"></a>
    _ResourcePolicyRule is a predicate that matches some resource requests, testing the request's verb and the target resource. A ResourcePolicyRule matches a resource request if and only if: (a) at least one member of verbs matches the request, (b) at least one member of apiGroups matches the request, (c) at least one member of resources matches the request, and (d) either (d1) the request does not specify a namespace (i.e., `Namespace==""`) and clusterScope is true or (d2) the request specifies a namespace and least one member of namespaces matches the request's namespace._

    - **rules.resourceRules.apiGroups** ([]string), required

      _Set: unique values will be kept during a merge_

      `apiGroups` is a list of matching API groups and may not be empty. "\*" matches all API groups and, if present, must be the only entry. Required.

    - **rules.resourceRules.resources** ([]string), required

      _Set: unique values will be kept during a merge_

      `resources` is a list of matching resources (i.e., lowercase and plural) with, if desired, subresource. For example, [ "services", "nodes/status" ]. This list may not be empty. "\*" matches all resources and, if present, must be the only entry. Required.

    - **rules.resourceRules.verbs** ([]string), required

      _Set: unique values will be kept during a merge_

      `verbs` is a list of matching verbs and may not be empty. "\*" matches all verbs and, if present, must be the only entry. Required.

    - **rules.resourceRules.clusterScope** (boolean)

      `clusterScope` indicates whether to match requests that do not specify a namespace (which happens either because the resource is not namespaced or the request targets all namespaces). If this field is omitted or false then the `namespaces` field must contain a non-empty list.

    - **rules.resourceRules.namespaces** ([]string)

      _Set: unique values will be kept during a merge_

      `namespaces` is a list of target namespaces that restricts matches. A request that specifies a target namespace matches only if either (a) this list contains that target namespace or (b) this list contains "_". Note that "_" matches any specified namespace but does not match a request that _does not specify_ a namespace (see the `clusterScope` field for that). This list may be empty, but only if `clusterScope` is true.

## FlowSchemaStatus {#FlowSchemaStatus}

FlowSchemaStatus represents the current state of a FlowSchema.

<hr>

- **conditions** ([]FlowSchemaCondition)

  _Patch strategy: merge on key `type`_

  _Map: unique values on key type will be kept during a merge_

  `conditions` is a list of the current states of FlowSchema.

  <a name="FlowSchemaCondition"></a>
  _FlowSchemaCondition describes conditions for a FlowSchema._

  - **conditions.lastTransitionTime** (Time)

    `lastTransitionTime` is the last time the condition transitioned from one status to another.

    <a name="Time"></a>
    _Time is a wrapper around time.Time which supports correct marshaling to YAML and JSON. Wrappers are provided for many of the factory methods that the time package offers._

  - **conditions.message** (string)

    `message` is a human-readable message indicating details about last transition.

  - **conditions.reason** (string)

    `reason` is a unique, one-word, CamelCase reason for the condition's last transition.

  - **conditions.status** (string)

    `status` is the status of the condition. Can be True, False, Unknown. Required.

  - **conditions.type** (string)

    `type` is the type of the condition. Required.

## FlowSchemaList {#FlowSchemaList}

FlowSchemaList is a list of FlowSchema objects.

<hr>

- **apiVersion**: flowcontrol.apiserver.k8s.io/v1beta3

- **kind**: FlowSchemaList

- **metadata** (<a href="{{< ref "../common-definitions/list-meta#ListMeta" >}}">ListMeta</a>)

  `metadata` is the standard list metadata. More info: https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

- **items** ([]<a href="{{< ref "../cluster-resources/flow-schema-v1beta3#FlowSchema" >}}">FlowSchema</a>), required

  `items` is a list of FlowSchemas.

## Operations {#Operations}

<hr>

### `get` read the specified FlowSchema

#### HTTP Request

GET /apis/flowcontrol.apiserver.k8s.io/v1beta3/flowschemas/{name}

#### Parameters

- **name** (_in path_): string, required

  name of the FlowSchema

- **pretty** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#pretty" >}}">pretty</a>

#### Response

200 (<a href="{{< ref "../cluster-resources/flow-schema-v1beta3#FlowSchema" >}}">FlowSchema</a>): OK

401: Unauthorized

### `get` read status of the specified FlowSchema

#### HTTP Request

GET /apis/flowcontrol.apiserver.k8s.io/v1beta3/flowschemas/{name}/status

#### Parameters

- **name** (_in path_): string, required

  name of the FlowSchema

- **pretty** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#pretty" >}}">pretty</a>

#### Response

200 (<a href="{{< ref "../cluster-resources/flow-schema-v1beta3#FlowSchema" >}}">FlowSchema</a>): OK

401: Unauthorized

### `list` list or watch objects of kind FlowSchema

#### HTTP Request

GET /apis/flowcontrol.apiserver.k8s.io/v1beta3/flowschemas

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

200 (<a href="{{< ref "../cluster-resources/flow-schema-v1beta3#FlowSchemaList" >}}">FlowSchemaList</a>): OK

401: Unauthorized

### `create` create a FlowSchema

#### HTTP Request

POST /apis/flowcontrol.apiserver.k8s.io/v1beta3/flowschemas

#### Parameters

- **body**: <a href="{{< ref "../cluster-resources/flow-schema-v1beta3#FlowSchema" >}}">FlowSchema</a>, required

- **dryRun** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#dryRun" >}}">dryRun</a>

- **fieldManager** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#fieldManager" >}}">fieldManager</a>

- **fieldValidation** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#fieldValidation" >}}">fieldValidation</a>

- **pretty** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#pretty" >}}">pretty</a>

#### Response

200 (<a href="{{< ref "../cluster-resources/flow-schema-v1beta3#FlowSchema" >}}">FlowSchema</a>): OK

201 (<a href="{{< ref "../cluster-resources/flow-schema-v1beta3#FlowSchema" >}}">FlowSchema</a>): Created

202 (<a href="{{< ref "../cluster-resources/flow-schema-v1beta3#FlowSchema" >}}">FlowSchema</a>): Accepted

401: Unauthorized

### `update` replace the specified FlowSchema

#### HTTP Request

PUT /apis/flowcontrol.apiserver.k8s.io/v1beta3/flowschemas/{name}

#### Parameters

- **name** (_in path_): string, required

  name of the FlowSchema

- **body**: <a href="{{< ref "../cluster-resources/flow-schema-v1beta3#FlowSchema" >}}">FlowSchema</a>, required

- **dryRun** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#dryRun" >}}">dryRun</a>

- **fieldManager** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#fieldManager" >}}">fieldManager</a>

- **fieldValidation** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#fieldValidation" >}}">fieldValidation</a>

- **pretty** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#pretty" >}}">pretty</a>

#### Response

200 (<a href="{{< ref "../cluster-resources/flow-schema-v1beta3#FlowSchema" >}}">FlowSchema</a>): OK

201 (<a href="{{< ref "../cluster-resources/flow-schema-v1beta3#FlowSchema" >}}">FlowSchema</a>): Created

401: Unauthorized

### `update` replace status of the specified FlowSchema

#### HTTP Request

PUT /apis/flowcontrol.apiserver.k8s.io/v1beta3/flowschemas/{name}/status

#### Parameters

- **name** (_in path_): string, required

  name of the FlowSchema

- **body**: <a href="{{< ref "../cluster-resources/flow-schema-v1beta3#FlowSchema" >}}">FlowSchema</a>, required

- **dryRun** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#dryRun" >}}">dryRun</a>

- **fieldManager** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#fieldManager" >}}">fieldManager</a>

- **fieldValidation** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#fieldValidation" >}}">fieldValidation</a>

- **pretty** (_in query_): string

  <a href="{{< ref "../common-parameters/common-parameters#pretty" >}}">pretty</a>

#### Response

200 (<a href="{{< ref "../cluster-resources/flow-schema-v1beta3#FlowSchema" >}}">FlowSchema</a>): OK

201 (<a href="{{< ref "../cluster-resources/flow-schema-v1beta3#FlowSchema" >}}">FlowSchema</a>): Created

401: Unauthorized

### `patch` partially update the specified FlowSchema

#### HTTP Request

PATCH /apis/flowcontrol.apiserver.k8s.io/v1beta3/flowschemas/{name}

#### Parameters

- **name** (_in path_): string, required

  name of the FlowSchema

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

200 (<a href="{{< ref "../cluster-resources/flow-schema-v1beta3#FlowSchema" >}}">FlowSchema</a>): OK

201 (<a href="{{< ref "../cluster-resources/flow-schema-v1beta3#FlowSchema" >}}">FlowSchema</a>): Created

401: Unauthorized

### `patch` partially update status of the specified FlowSchema

#### HTTP Request

PATCH /apis/flowcontrol.apiserver.k8s.io/v1beta3/flowschemas/{name}/status

#### Parameters

- **name** (_in path_): string, required

  name of the FlowSchema

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

200 (<a href="{{< ref "../cluster-resources/flow-schema-v1beta3#FlowSchema" >}}">FlowSchema</a>): OK

201 (<a href="{{< ref "../cluster-resources/flow-schema-v1beta3#FlowSchema" >}}">FlowSchema</a>): Created

401: Unauthorized

### `delete` delete a FlowSchema

#### HTTP Request

DELETE /apis/flowcontrol.apiserver.k8s.io/v1beta3/flowschemas/{name}

#### Parameters

- **name** (_in path_): string, required

  name of the FlowSchema

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

### `deletecollection` delete collection of FlowSchema

#### HTTP Request

DELETE /apis/flowcontrol.apiserver.k8s.io/v1beta3/flowschemas

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
