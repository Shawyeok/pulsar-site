---
id: admin-api-permissions
title: Managing permissions
sidebar_label: "Permissions"
description: Learn how to manage permissions using Pulsar CLI and admin APIs.
---

````mdx-code-block
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';
````


:::tip

 This page only shows **some frequently used operations**.

 - For the latest and complete information about `Pulsar admin`, including commands, flags, descriptions, and more, see [Pulsar admin docs](pathname:///reference/#/@pulsar:version_reference@/pulsar-admin/).

 - For the latest and complete information about `REST API`, including parameters, responses, samples, and more, see {@inject: rest:REST:/} API doc.

 - For the latest and complete information about `Java admin API`, including classes, methods, descriptions, and more, see [Java admin API doc](/api/admin/).

:::

Pulsar allows you to grant namespace-level or topic-level permission to users.

- If you grant namespace-level permission to a user, then the user can access all the topics under the namespace.

- If you grant topic-level permission to a user, then the user can access only the topic.

The chapters below demonstrate how to grant namespace-level permissions to users. For how to grant topic-level permissions to users, see [manage topics](admin-api-topics.md#grant-permission).

## Grant permissions

You can grant permissions to specific roles for lists of operations such as `produce` and `consume`.

````mdx-code-block
<Tabs groupId="api-choice"
  defaultValue="pulsar-admin"
  values={[{"label":"pulsar-admin","value":"pulsar-admin"},{"label":"REST API","value":"REST API"},{"label":"Java","value":"Java"}]}>
<TabItem value="pulsar-admin">

Use the [`grant-permission`](pathname:///reference/#/@pulsar:version_reference@/pulsar-admin/namespaces?id=grant-permission) subcommand and specify a namespace, actions using the `--actions` flag, and a role using the `--role` flag:

```shell
pulsar-admin namespaces grant-permission test-tenant/namespace1 \
    --actions produce,consume \
    --role admin10
```

Wildcard authorization can be performed when `authorizationAllowWildcardsMatching` is set to `true` in `broker.conf`.

**Example**

```shell
pulsar-admin namespaces grant-permission test-tenant/namespace1 \
      --actions produce,consume \
      --role 'my.role.*'
```

Then, roles `my.role.1`, `my.role.2`, `my.role.foo`, `my.role.bar`, etc. can produce and consume.

```shell
pulsar-admin namespaces grant-permission test-tenant/namespace1 \
      --actions produce,consume \
      --role '*.role.my'
```

Then, roles `1.role.my`, `2.role.my`, `foo.role.my`, `bar.role.my`, etc. can produce and consume.

:::note

A wildcard matching works at **the beginning or end of the role name only**.

:::

**Example**

```shell
pulsar-admin namespaces grant-permission test-tenant/namespace1 \
      --actions produce,consume \
      --role 'my.*.role'
```

In this case, only the role `my.*.role` has permissions.
Roles `my.1.role`, `my.2.role`, `my.foo.role`, `my.bar.role`, etc. **cannot** produce and consume.

</TabItem>
<TabItem value="REST API">

[](swagger:/admin/v2/Namespaces_grantPermissionOnNamespace)

</TabItem>
<TabItem value="Java">

```java
admin.namespaces().grantPermissionOnNamespace(namespace, role, getAuthActions(actions));
```

</TabItem>

</Tabs>
````

## Get permissions

You can see which permissions have been granted to which roles in a namespace.

````mdx-code-block
<Tabs groupId="api-choice"
  defaultValue="pulsar-admin"
  values={[{"label":"pulsar-admin","value":"pulsar-admin"},{"label":"REST API","value":"REST API"},{"label":"Java","value":"Java"}]}>
<TabItem value="pulsar-admin">

Use the [`permissions`](pathname:///reference/#/@pulsar:version_reference@/pulsar-admin/namespaces?id=grant-permission) subcommand and specify a namespace:

```shell
pulsar-admin namespaces permissions test-tenant/namespace1
```

Example output:

```
my.role.*    [produce, consume]
```

</TabItem>
<TabItem value="REST API">

[](swagger:/admin/v2/Namespaces_getPermissions)

</TabItem>
<TabItem value="Java">

```java
admin.namespaces().getPermissions(namespace);
```

</TabItem>

</Tabs>
````

## Revoke permissions

You can revoke permissions from specific roles, which means that those roles will no longer have access to the specified namespace.

````mdx-code-block
<Tabs groupId="api-choice"
  defaultValue="pulsar-admin"
  values={[{"label":"pulsar-admin","value":"pulsar-admin"},{"label":"REST API","value":"REST API"},{"label":"Java","value":"Java"}]}>
<TabItem value="pulsar-admin">

Use the [`revoke-permission`](pathname:///reference/#/@pulsar:version_reference@/pulsar-admin/namespaces?id=revoke-permission) subcommand and specify a namespace and a role using the `--role` flag:

```shell
pulsar-admin namespaces revoke-permission test-tenant/namespace1 \
      --role admin10
```

</TabItem>
<TabItem value="REST API">

[](swagger:/admin/v2/Namespaces_revokePermissionsOnNamespace)

</TabItem>
<TabItem value="Java">

```java
admin.namespaces().revokePermissionsOnNamespace(namespace, role);
```

</TabItem>

</Tabs>
````
