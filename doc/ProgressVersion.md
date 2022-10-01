## Description

Stores the Progress version in properties.

## XML namespace

`<pct:progress_version />`

## Parameters

| **Attribute**| **Description**| **Default value**|
|:-------------|:---------------|:--------:|
|dlcHome ‡     |Progress installation directory|None|
|majorVersion  |Major version (extracts "12" from 12.2.4)| |
|minorVersion  |Minor version (extracts "2" from 12.2.4)| |
|patchLevel    |Patch level (extracts "4" from 12.2.4)| |
|fullVersion   |Extracts the full string from $DLC/version| |
|shortVersion  |Extracts only the version from $DLC/version| |
|rcodeVersion  |R-Code version  | |

† Only one of those attributes is mandatory
‡ Mandatory attribute

## Parameters as nested elements
None

## Examples
```xml
<ProgressVersion dlcHome="/path/to/dlc" majorVersion="major" minorVersion="minor" fullVersion="full" />
<echo message="${major}.${minor}" />
```
could display the following string :
```
[echo] 12.2
```

