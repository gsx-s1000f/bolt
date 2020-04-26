---
title: Installing Bolt and Creating a Project
difficulty: Basic
time: Approximately 10 minutes
---

In this exercise you will install Bolt and create a Bolt project directory so you can get started with Bolt.

## Installing Bolt

```
Bolt is packaged for the major operating systems. Please refer to the [installation documentation](https://puppet.com/docs/bolt/latest/bolt_installing.html) to install Bolt for the OS you are using. 
```

Boltには、メジャーどころのOS向けのパッケージがあります。お使いのOSにインストールするには、[installation documentation](https://puppet.com/docs/bolt/latest/bolt_installing.html) を参考にしてください。

**Note** 
```
For this lab and for most use cases it is recommended that bolt is NOT installed as a Ruby Gem. This is because optional (but highly useful) supporting modules are only included in packages and must be installed manually when using the Gem.
```

このLabやよくあるユースケースでは、Ruby Gem形式ではインストール**しない**ことをおすすめします。なぜならオプション（しかしとても有用な）サポートモジュールはパッケージにのみ含まれており、Gemを使用した場合はマニュアルインストールしなければならないからです。

## Creating a Bolt Project Directory

```
By default `$HOME/.puppetlabs/bolt/` is the base directory for user-supplied data such as the configuration and inventory files. It is effectively the default Bolt project directory. 
You may find it useful to maintain a project specific Bolt project directory. When you commit a Bolt project directory to a project you can share Bolt configuration and code between users.
```

デフォルトでは、'$HOME/.puppetlabs/bolt'が、ユーザー提供データやイベントリファイルを格納するベースディレクトリとなります。事実上、デフォルトのBolt project ディレクトリです。
プロジェクト固有のBolt project directoryを定義するのが有用なこともあるかもしれません。しかしBolt project directoryに格納していれば、Boltの設定やコードをシェアすることができます。

```
Bolt treats a directory containing a subdirectory called `Boltdir` as a project directory, and will traverse parents of the current directory until it finds a directory containing a `Boltdir`. You can read the official documentation to learn more about additional [types of project directories](https://puppet.com/docs/bolt/latest/bolt_project_directories.html#project-directory-types).
```

Boltは`Boltdir`というサブディレクトリを持つディレクトリをプロジェクトディレクトリとして扱います。そして、`Boltdir` を含むディレクトリが見つかるまでカレントディレクトリの親ディレクトリをたどっていきます。追加の公式ドキュメントで更に学ぶことができます。 [types of project directories](https://puppet.com/docs/bolt/latest/bolt_project_directories.html#project-directory-types)

```
To get started, create a directory called `Boltdir` within your project directory. Within the `Boltdir` you should also create a `modules/` subdirectory, which holds modules from the Puppet Forge and code repositories, and a `site-modules/` subdirectory, which holds project-specific modules. These two subdirectories are where Bolt will look for tasks, plans, and manifests.
```
はじめるにあたって、プロジェクトディレクトリの中に`Boltdir`というディレクトリを作ってください。`Boltdir`の中には、Puppet Forgeやコードリポジトリから取得したモジュールを格納する`modules/`と、プロジェクト固有のモジュールを格納する`site-modules/`を作成してください。これら二つのサブディレクトリは、Boltがタスク、プラン、マニフェストを探しに行くサブディレクトリです。

```
If you are using the [files included with this lab](https://github.com/puppetlabs/bolt/tree/master/docs/_includes) your project directory will end up looking like:
```

もし、[files included with this lab](https://github.com/puppetlabs/bolt/tree/master/docs/_includes)を使用するのであれば、プロジェクトディレクトリは以下の様になります。：

```
lesson1-10/
├── Boltdir
│   ├── inventory.yaml
│   ├── modules
│   │   └── ...
│   └── site-modules
│       └── ...
├── docker-compose.yml
├── Dockerfile
├── src/
└── Vagrantfile
```

## Next Steps

```
Now that you have Bolt installed and have created a Bolt project directory you can move on to:
```

今、あなたはBoltをインストールし、プロジェクトディレクトリも作成しました。次へ進みましょう。（※超意訳）

[Setting Up Test Targets](../02-acquiring-targets)
