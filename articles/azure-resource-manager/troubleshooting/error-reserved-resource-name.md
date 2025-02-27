---
title: Reserved resource name errors
description: Describes how to resolve errors when providing a resource name that includes a reserved word.
ms.topic: troubleshooting
ms.date: 11/02/2021
---
# Resolve reserved resource name errors

This article describes the error you get when deploying a resource that includes a reserved word in its name.

## Symptom

When deploying a resource that is available through a public endpoint, you may receive the following error:

```
Code=ReservedResourceName;
Message=The resource name <resource-name> or a part of the name is a trademarked or reserved word.
```

## Cause

Resources that have a public endpoint can't use reserved words or trademarks in the name.

The following words are reserved:

* ACCESS
* APP_CODE
* APP_THEMES
* APP_DATA
* APP_GLOBALRESOURCES
* APP_LOCALRESOURCES
* APP_WEBREFERENCES
* APP_BROWSERS
* AZURE
* BING
* BIZSPARK
* BIZTALK
* CORTANA
* DIRECTX
* DOTNET
* DYNAMICS
* EXCEL
* EXCHANGE
* FOREFRONT
* GROOVE
* HOLOLENS
* HYPERV
* KINECT
* LYNC
* MSDN
* O365
* OFFICE
* OFFICE365
* ONEDRIVE
* ONENOTE
* OUTLOOK
* POWERPOINT
* SHAREPOINT
* SKYPE
* VISIO
* VISUALSTUDIO

The following words can't be used as either a whole word or a substring in the name:

* MICROSOFT
* WINDOWS

## Solution

Provide a name that doesn't use one of the reserved words.
