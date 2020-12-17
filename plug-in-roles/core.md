---
description: The SkydelCoreInterface role gives access to basic integration with Skydel.
---

# Core

## SkydelCoreInterface

### setLogPath

Skydel calls `setLogPath` during the simulation initialization state. `path` contains an absolute path pointing to a runtime temporary directory unique for every plug-in instance. S_kydel Data Folder / Output / A / B_, where _A_ is the Skydel configuration name and _B_ the plug-in instance name. 

{% hint style="info" %}
The content of the Skydel Output folder is accessible at the end of the simulation, but starting a new simulation will wipe it's content.
{% endhint %}



  


```text
setNotifier
```

