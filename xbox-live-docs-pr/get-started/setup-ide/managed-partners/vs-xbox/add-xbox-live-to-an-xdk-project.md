---
title: Add Xbox Live to an XDK project
description: Adding Xbox Live to a new or existing Xbox Developer Kit (XDK) project.
ms.assetid: fc6f987c-1a87-4ff5-b063-891591aa6653
ms.date: 04/04/2017
ms.topic: article
keywords: xbox live, xbox, games, uwp, windows 10, xbox one, xdk
ms.localizationpriority: medium
---

# Add Xbox Live to an XDK project

You can add Xbox Live to a new or existing XDK project.

The process is:

- Set up Up Your Xbox One Development Environment.
- Get your IDs.
- Configure your development console.
- Add the TitleID and SCID to your binary.

These steps are detailed below.


## Set up Up Your Xbox One Development Environment

First, set up the console by following "Setting Up Your Xbox One Development Environment" section in the XDK documentation.


## Get your IDs

To enable Xbox Live services, you will need to obtain several IDs to configure your development kit and your title.
See the section "Get your IDs" in [Xbox Live service configuration](../../../../xbox-live-service-configuration.md#get_ids).


## Configure your development console

Once you have your IDs, set up your development console; see [Configuring an Xbox development console](configure-your-development-console.md).


## Add the TitleID and SCID to your binary

Although the Sandbox is configured on a platform level for each Development Kit, the TitleID and SCID are bound to a specific binary.

To add a TitleID and SCID to your binary, modify the `Package.appxmanifest` for that binary by adding a new node in the <Extensions> node as follows:

```xml
<Applications>
    ...
    <Application ...>
      ...
      <Extensions>
        <mx:Extension Category="xbox.live">
           <mx:XboxLive TitleId="<your titleID>" PrimaryServiceConfigId="<your SCID>" RequireXboxLive="<boolean indicating Live requirement>" />
        </mx:Extension>
      </Extensions>
   </Application>
</Applications>
```

For more information about the `AppxManifest.xml` file, refer to Project Templates in Visual Studio for Xbox One Development.

For a description of the application manifest schema, see Application Manifest Schema.


**The RequireXboxLive Flag:**
If the `RequireXboxLive` flag is set to true, the title will not launch unless the `Windows.Networking.Connectivity` Connection Level returns as XboxLiveAccess and the title clears authentication with Xbox Live.
This ensures that the title has taken the latest content updates.
If connectivity is lost while the title is running, the title is suspended.

Only "Internet Required" titles should mark `RequireXboxLive` as true.
Marking your title in this way does not guarantee the required services for the title are up and running.
