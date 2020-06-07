---
title: Running Existing Tasks
difficulty: Intermediate
time: Approximately 10 minutes
---

In this exercise you will explore existing tasks, including several tasks that take advantage of Puppet under-the-hood.

- [Install Puppet Using Bolt](#use-the-puppet_agent-module-to-install-puppet-agent)

## Prerequisites
Complete the following before you start this lesson:

- [Installing Bolt](../01-installing-bolt)
- [Setting Up Test Targets](../02-acquiring-targets)
- [Running Commands](../03-running-commands)
- [Running Scripts](../04-running-scripts)

## Inspect Installed Tasks （インストール済みTaskの検査）

>> Bolt is packaged with useful modules and task content.

Boltには便利なmoduleとTaskがパッケージされています。

>> Run the `bolt task show` command to view a list of the tasks installed in the project directory.

`bolt task show`コマンドをを実行するとプロジェクトディレクトリにインストールされたタスクのリストを表示します。

```shell
bolt task show
```

The result:

```plain
facts                              Gather system facts
facts::bash                        Gather system facts using bash
facts::powershell                  Gather system facts using powershell
facts::ruby                        Gather system facts using ruby and facter
package                            Manage and inspect the state of packages
puppet_agent::install              Install the Puppet agent package
puppet_agent::install_powershell
puppet_agent::install_shell
puppet_agent::version              Get the version of the Puppet agent package installed. Returns nothing if none present.
puppet_agent::version_powershell
puppet_agent::version_shell
puppet_conf                        Inspect puppet agent configuration settings
service                            Manage and inspect the state of services
service::linux                     Manage the state of services (without a puppet agent)
service::windows                   Manage the state of Windows services (without a puppet agent)

MODULEPATH:
/project/Boltdir/modules:/project/Boltdir/site-modules:/project/Boltdir/site

Use bolt task show <task-name> to view details and parameters for a specific task.
```

## Use the puppet_agent Module to Install Puppet Agent. 

Install puppet agent with the `puppet_agent::install` task.

``` shell
bolt task run puppet_agent::install --targets linux --run-as root
```

The result:

```
Installed:
puppet-agent.x86_64 0:6.0.1-1.el7                                             
 
Complete!
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirror.tocici.com
 * extras: mirror.tocici.com
 * updates: ftp.osuosl.org
No packages marked for update
{
}
Successful on 3 targets: target1,target2,target3
Ran on 3 targets in 68.71 seconds
```

## View and Use Parameters For a Specific Task

Run `bolt task show package` to view the parameters that the package task uses. 

```shell
bolt task show package
```

The result:

```plain
package - Manage and inspect the state of packages

USAGE:
bolt task run --targets <target-name> package action=<value> name=<value> version=<value> provider=<value>

PARAMETERS:
- action: Enum[install, status, uninstall, upgrade]
    The operation (install, status, uninstall and upgrade) to perform on the package
- name: String[1]
    The name of the package to be manipulated
- version: Optional[String[1]]
    Version numbers must match the full version to install, including release if the provider uses a release moniker. Ranges or semver patterns are not accepted except for the gem package provider. For example, to install the bash package from the rpm bash-4.1.2-29.el6.x86_64.rpm, use the string '4.1.2-29.el6'.
- provider: Optional[String[1]]
    The provider to use to manage or inspect the package, defaults to the system package manager

MODULE:
built-in module
```

Using parameters for the package task, check on the status of the bash package:

```shell
bolt task run package action=status name=bash --targets target1
```

The result:

```    
Started on target1...
Finished on target1:
  {
    "status": "up to date",
    "version": "4.2.46-30.el7"
  }
Successful on 1 target: target1
Ran on 1 target in 3.84 seconds
```

Using parameters for the package task, install the vim package across all your targets:

```shell
bolt task run package action=install name=vim --targets linux --run-as root
```

The result:

```
Started on target1...
Started on target3...
Started on target2...
Finished on target1:
  {
    "status": "present",
    "version": "2:7.4.160-4.el7"
  }
Finished on target3:
  {
    "status": "installed",
    "version": "2:7.4.160-4.el7"
  }
Finished on target2:
  {
    "status": "installed",
    "version": "2:7.4.160-4.el7"
  }
Successful on 3 targets: target1,target2,target3
Ran on 3 targets in 10.03 seconds
```

# More Tips, Tricks and Ideas

See the [installing modules](https://puppet.com/docs/bolt/latest/bolt_installing_modules.html) documentation to learn how to install external modules. 
These exercises introduce you to Bolt tasks.

# Next Steps

Now that you know how to run existing tasks with Bolt you can move on to:

[Writing Plans](../07-writing-plans)
