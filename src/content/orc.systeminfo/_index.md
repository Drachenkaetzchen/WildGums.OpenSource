+++
title = "Orc.SystemInfo" 
description = ""
+++

Name|Badge
---|---
Chat|[![Join the chat at https://gitter.im/WildGums/Orc.SystemInfo](https://badges.gitter.im/Join%20Chat.svg?classes=inline)](https://gitter.im/WildGums/Orc.SystemInfo?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
Downloads|![NuGet downloads](https://img.shields.io/nuget/dt/orc.systeminfo.svg?classes=inline)
Stable version|![Version](https://img.shields.io/nuget/v/orc.systeminfo.svg?classes=inline)
Unstable version|![Pre-release version](https://img.shields.io/nuget/vpre/orc.systeminfo.svg?classes=inline)

Find the source at [https://github.com/WildGums/Orc.SystemInfo](https://github.com/WildGums/Orc.SystemInfo)

This library is used to retrieve the system information details from a computer.

Use the `GetSystemInfo()` method or the `ISystemInfoService` to get the system information details.

`GetSystemInfo()` returns an `IEnumerable<SystemInfoElement>`

```
[Serializable]
public class SystemInfoElement
{
    ...
    public string Name { get; set; }
    public string Value { get; set; }
    ...
}
```

The following information will be retreived:

- User name
- User domain
- Machine name
- OS version
- OS name Microsoft
- MaxProcessRAM
- Architecture
- ProcessorId 
- Build 
- CPU name 
- Description
- Address width 
- Data width 
- SpeedMHz
- BusSpeedMHz
- Number of cores
- Number of logical processors
- System up time
- Application up time
- Total memory
- Available memory
- Current culture
- .Net Framework versions  

A kind of code example with TextBox txtBxAboutSystem displaying info collected
```
txtBxAboutSystem.Text += "--- System Info ---" + Environment.NewLine;
var sis = ServiceLocator.Default.GetServiceLocator().ResolveType<ISystemInfoService>();
if (sis != null)
{
    var systemInfo = await TaskHelper.Run(() => sis.GetSystemInfo(), true);
    txtBxAboutSystem.Text += string.Join(Environment.NewLine, systemInfo.Select(x => string.Format("{0} {1}", x.Name, x.Value)));
}
```
