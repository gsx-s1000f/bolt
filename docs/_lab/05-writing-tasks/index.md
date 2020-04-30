---
title: Writing Tasks
difficulty: Basic
time: Approximately 15 minutes
---

>> In this exercise you will write your first Bolt Tasks for use with Bolt. 

この演習では、最初のBoldタスクを書いてみましょう。

- [How Do Tasks Work?](#how-do-tasks-work)
- [Write Your First Task in Bash](#write-your-first-task-in-bash)
- [Write Your First Task in PowerShell](#write-your-first-task-in-powershell)
- [Write Your First Task in Python](#write-your-first-task-in-python)

## Prerequisites （前提条件）
>> Complete the following before you start this lesson:

このレッスンを開始する前に、以下を完了させておいてください。

- [Installing Bolt](../01-installing-bolt)
- [Setting Up Test Targets](../02-acquiring-targets)
- [Running Commands](../03-running-commands)
- [Running Scripts](../04-running-scripts)


## How Do Tasks Work?

>> Tasks are scripts with optional metadata, and can be implemented in any language that runs on your targets. Tasks are stored and shared in Puppet modules. By giving your script metadata and including it in a Puppet module, tasks make scripts easy to reuse and share. You can upload and download tasks in modules from the [Puppet Forge](https://forge.puppet.com/), run them from GitHub, or use them locally to organize your regularly used commands.

Taskは任意の属性（メタデータ）を含むスクリプトで、ターゲット上で実行するあらゆる言語を実装できます。TaskはPuppetモジュールで保存し、共有されます。スクリプトの属性（メタデータ）を付与することで、Puppetモジュールに取り込み、再利用し共有することを容易にします。Taskは[Puppet Forge](https://forge.puppet.com/)にアップロードしたりダウンロードすることができ、Githubから起動したり、日常的に使うコマンドを整理しローカルで使う事ができます。

>> Tasks are stored in the `tasks` directory of a module, a module being a directory with a unique name. You can have several tasks per module, but the `init` task is special and runs by default if you do not specify a task name.

Taskは、モジュールの`tasks`ディレクトリにユニークな名称で保存する。モジュールごとに複数のTaskを保存できますが、`init`は特殊で、名前を指定しないとデフォルトで実行されます。

>> By default tasks take arguments as environment variables prefixed with `PT`. 

デフォルトでは、Taskは `PT` というプレフィクスを持った環境変数として受け取ります。

## Write Your First Task in Bash

>> This exercise uses `sh`, but you can use Perl, Python, Lua, or JavaScript or any language that can read environment variables or take content on stdin.

この演習では`sh`を使用しますが、Perl、Python、Lua、Javascript、環境変数や標準入力を読み込める数多の言語を使用することができます。

>> Save the following to `Boltdir/site-modules/exercise5/tasks/init.sh`:

`Boltdir/site-modules/exercise5/tasks/init.sh`に次のシェルを保存して下さい。

```shell
{% include lesson1-10/Boltdir/site-modules/exercise5/tasks/init.sh -%}
```

>> By default, Bolt will search both the `modules` and `site-modules` directories in a Bolt project directory for a matching task name. Typically, any project-specific tasks will be saved to the `site-modules` directory.

デフォルトでは、Boltはプロジェクトディレクトリ内の `modules` と `site-modules` の両方を検索し、Task名に一致するものを探します。

>> Run the exercise5 task. Note the `message` argument. This will be expanded to the `PT_message` environment variable expected by our task. By naming parameters explicitly it's easier for others to use your tasks.

exercise5 Taskを実行します。引数 `message` に注目して下さい。これはTaskによって想定される環境変数を `PT_message` に展開します。パラメータを明示的にいていすることで、他の人がTaskを使うことを容易にします。

```shell
bolt task run exercise5 message=hello --targets target1
```

The result:

```
Started on target1...
Finished on target1:
  localhost.localdomain received the message: hello
  {
  }
Successful on 1 target: target1
Ran on 1 target in 0.99 seconds
```

>> Run the Bolt command with a different value for `message` and see how the output changes.

`message`に異なる値を設定してBoltコマンドを実行し、出力がどの様にかわるか確認します。

## Write Your First Task in PowerShell

>> If you're targeting Windows targets then you might prefer to implement the task in PowerShell. 

もしWindowsをターゲットにするなら、TaskはPowerShellで実装するのがいいかもしれません。

>> Save the following as `Boltdir/site-modules/exercise5/tasks/print.ps1`:

`Boltdir/site-modules/exercise5/tasks/print.ps1`に次のスクリプトを保存して下さい。

```powershell
{% include lesson1-10/Boltdir/site-modules/exercise5/tasks/print.ps1 -%}
```

>> Run the exercise5 task. Note that since the task is not named `init`, you must prepend the name of the task with the name of its module like so `module::task`.

exercise5 Taskを実行して下さい。Task の名前が `init` でないことに注目して下さい。Task名にmodule名を繋げて`module::task` の様にしなければなりません。

```shell
bolt task run exercise5::print message="hello powershell" --targets windows
```

The result:

```
Started on localhost...
Finished on localhost:
  Nano received the message: hello powershell
  {
  }
Successful on 1 target: winrm://localhost:55985
Ran on 1 target in 3.87 seconds
```

**Note:**

>> * The name of the file on disk (minus any file extension) translates to the name of the task when run via Bolt, in this case `print`.
>> * The name of the module (directory) is also used to find the relevant task, in this case `exercise5`.
>> * As with the Bash example above, name parameters so that they're more easily understood by users of the task.
>> * By default tasks with a `.ps1` extension executed over WinRM use PowerShell standard agrument handling rather than being supplied as prefixed environment variables or via `stdin`. 

* ディスク上の（拡張子を除いた）ファイル名は、Bolt経由で実行された時に変換されます。この場合は `print` です。
* モジュール（ディレクトリ）の名前は、関連Taskを見つける為にも使用されます。この場合は`exercise5`です。
* 上のBashの例の様に、タスクの使用者が理解しやすい様に名前をつけなければなりません。
* 拡張子が`.ps1`ののデフォルトTaskは、プレフィクスのついた環境変数や標準入力ではなく、WinRM上で使用されるPowerShellの引数として扱います。


## Write Your First Task in Python

When running a task, Bolt assumes that the required runtime is already available on the targets. For the following examples to work, Python 2 or 3 must be installed on the targets. This task will also work on Windows system with Python 2 or 3 installed.

Save the following as `Boltdir/site-modules/exercise5/tasks/gethost.py`:

```python
{% include lesson1-10/Boltdir/site-modules/exercise5/tasks/gethost.py -%}
```

Run the task using the command `bolt task run <task-name>`.

```shell
bolt task run exercise5::gethost host=google.com --targets linux
```

The result:

```
Started on target1...
Finished on target1:
  google.com is available at 172.217.3.206 on localhost.localdomain
  {
    "host": "google.com",
    "hostname": "localhost.localdomain",
    "ipaddr": "172.217.3.206"
  }
Successful on 1 target: target1
Ran on 1 target in 0.97 seconds
```

## Next Steps

Now that you know how to write tasks you can move on to:

[Downloading and Running Existing Tasks](../06-downloading-and-running-existing-tasks)
