---
title: Running Scripts
difficulty: Basic
time: Approximately 5 minutes
---

>> In this exercise you will run existing scripts against remote targets using Bolt.

この演習では、Bolt を使用してリモートターゲットに対して既存のスクリプトを実行します。

- [Test Linux Targets for ShellShock](#test-linux-targets-for-shellshock)
- [Test Windows External Connectivity](#test-windows-external-connectivity)

## Prerequisites（前提条件）
>> Complete the following before you start this lesson:

このレッスンを始める前に、以下の内容をコンプリートさせてください。:

- [Installing Bolt](../01-installing-bolt)
- [Setting up test targets](../02-acquiring-targets)
- [Running Commands](../03-running-commands)

## Test Linux Targets for ShellShock
Run the [bashcheck](https://github.com/hannob/bashcheck) script to check on ShellShock and related vulnerabilities.

>> **Tip:** You likely already have a set of scripts that you run to accomplish common systems administration tasks. Bolt makes it easy to reuse your scripts without modification and to run them quickly across a large number of targets. Feel free to replace the bashcheck script in this exercise with one of your own. Just set the shebang line correctly and you can run scripts in Python, Ruby, Perl or another scripting language.

**ヒント:** あなたは既に一般的なシステム管理タスクを適える為に実行するスクリプトセットを持っているかと思います。Boltは、スクリプトを修正なしに再利用でき、多くのターゲットに素早く実行することができます。この演習で使用するbashcheck.shを自由に自身のものに置き換えてください。shebang行を正しく修正すれば、Python、Ruby、Perl、その他のスクリプト言語を実行することができます。

>> Download the `bashcheck.sh` script using `curl`, `wget`,  or similar:

`curl`、`wget`、あるいは似た様なのもので、`bashcheck.sh`をダウンロードして下さい。:

```shell
curl -O https://raw.githubusercontent.com/puppetlabs/bolt/master/docs/_includes/lesson1-10/src/bashcheck.sh
```

>> Run the script using the command `bolt script run <script-name>`. This uploads the script to the targets you have specified, ensures it's executable, runs it, and returns output to the console.

`bolt script run <script-name>`コマンドでスクリプトを実行します。この指定したターゲットにアップロードしたスクリプトは、実行可能であることを確認し、実行し、コンソールに出力します。

```shell
bolt script run bashcheck.sh --targets target1
```

The result:

```
Started on target1...
Finished on target1:
  STDOUT:
    Testing /usr/bin/bash ...
    Bash version 4.2.46(2)-release

    Variable function parser pre/suffixed [(), redhat], bugs not exploitable
    Not vulnerable to CVE-2014-6271 (original shellshock)
    Not vulnerable to CVE-2014-7169 (taviso bug)
    Not vulnerable to CVE-2014-7186 (redir_stack bug)
    Test for CVE-2014-7187 not reliable without address sanitizer
    Not vulnerable to CVE-2014-6277 (lcamtuf bug #1)
    Not vulnerable to CVE-2014-6278 (lcamtuf bug #2)
Successful on 1 target: target1
Ran on 1 target in 0.89 seconds
```

## Test Windows External Connectivity（Windows外部接続テスト）

>> Create a simple PowerShell script to test connectivity to a known website.

簡単なPowerShellで、既知のウェブサイトへの接続テストを行うスクリプトを作成します。

>>**Tip:** You likely already have a set of scripts that you run to accomplish common systems administration tasks. Bolt makes it easy to reuse your scripts without modification and to run them quickly across a large number of targets. Feel free to replace the script in this exercise with one of your own.

**ヒント:** あなたは既にシステム管理タスク上のよくあるタスクを解決するスクリプトを持っている可能性が高いです。Boltは簡単に改修なしで採用することができ、多数のターゲットに対し迅速に実行することができます。この演習で使用するスクリプトをあなた自身の者に置き換えてみてください。

>> Save the following as `testconnection.ps1`:

以下を`testconnection.ps1`という名前で保存してください。

```powershell
{% include lesson1-10/src/testconnection.ps1 -%}
```

>> Run the script using the command `bolt script run <script-name>`. This uploads the script to the targets you have specified, ensures it's executable, runs it, and returns output to the console.

`bolt script run <script-name>`コマンドでスクリプトを実行します。この指定したターゲットにアップロードしたスクリプトは、実行可能であることを確認し、実行し、コンソールに出力します。

```shell
bolt script run src/testconnection.ps1 --targets windows
```

>>The result:

結果:

```
Started on localhost...
Finished on localhost:
  STDOUT:

    Source        Destination     IPV4Address      IPV6Address                              Bytes    Time(ms)
    ------        -----------     -----------      -----------                              -----    --------
    Nano          example.com                                                               256      4
    Nano          example.com                                                               256      4
    Nano          example.com                                                               256      5


Successful on 1 target: winrm://localhost:55985
Ran on 1 target in 8.55 seconds
```

## Next steps

Now that you know how to use Bolt to run existing scripts you can move on to:

[Writing Tasks](../05-writing-tasks)
