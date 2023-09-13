# Dst-admin 1.5.0  remote command execution

## 目录

-   [Vulnerability Title:](#Vulnerability-Title)
-   [Affected version:](#Affected-version)
-   [Discovery time:](#Discovery-time)
-   [Discovered by:](#Discovered-by)
-   [分析报告: ](#分析报告-)
    -   [The GitHub repository](#The-GitHub-repository)
    -   [Vulnerability exploitation](#Vulnerability-exploitation)
-   [Repair plan](#Repair-plan)

# Vulnerability Title:

Dst-admin 1.5.0  remote command execution

# Affected version:

Dst-admin 1.5.0 &#x20;

# Discovery time:

2023-04-26

# Discovered by:

libestor

# Analysis report:&#x20;

## The GitHub repository

[GitHub - qinming99/dst-admin: Steam平台的Don't Starve Together 饥荒联机版管理后台](https://github.com/qinming99/dst-admin "GitHub - qinming99/dst-admin: Steam平台的Don't Starve Together 饥荒联机版管理后台")

Dst-admin is a *Dont Starve Together* server background management program, and has over 300 stars on github. It is regarded by many servers as the best tool for *Dont Starve Together* back-office management. But the background command execution route is not filtered using blacklist, resulting in arbitrary command execution.

## Vulnerability exploitation

Arbitrary code execution can be performed through the `/home/playerOperate` interface using the parameter `userId`.It is possible to initiate the attack remotely.

&#x20;the POC like:

```bash
/home/playerOperate?type=0&userId=')" || echo "this is test">/tmp/test.txt #
```

![](https://picture.libestor.top//src/DstAdminRce/image_025lKGGN1b.png)

After that, the 'test.txt' file is found in the '/tmp' path and data is successfully written, indicating that the command is executed successfully.

![](https://picture.libestor.top//src/DstAdminRce/image_DPG8Wnv-gD.png)

And we also found traces of command execution in the logs:

![](https://picture.libestor.top//src/DstAdminRce/image_HXoS_rUHHZ.png)

# Repair plan

Change strong passwords or use other products
