---
description: Configure Aidbox using environment variables and Zen
---

# Zen Configuration

{% hint style="warning" %}
This feature is in alpha. It may change in backward-incompatible way in the future.
{% endhint %}

## Find configuration options

`aidbox/config` schema lists available Zen configuration options with descriptions

Open _Profiles_ in Aidbox UI. Navigate to `aidbox/config` schema.&#x20;

![](<../.gitbook/assets/image (96).png>)

## Set configuration option

To set a configuration option set a corresponding environment variable prefixed with `box_`. Path elements are separated with underscore (`_`), dashes (`-`) are replaced with double underscore (`__`)

### Example

To set the `rest-search` value of the `features.graphql.access-control` option use the `box_features_graphql_access__control` environment variable:

```
box_features_graphql_access__control=rest-search
```