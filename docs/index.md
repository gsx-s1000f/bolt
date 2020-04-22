---
title: Bolt Hands-on Lab（に、変な和訳をつける）
---

**＜訳注＞
自分で動かしていてよくわからないところに、超意訳で訳をつけていきます。忙しかったり飽きたりしたら止まります。
訳が間違っていることにより何らかの問題が発生しても、当方は一切責任を負いかねますので、よしなにお願いします。**


## Introduction

Bolt is an open source orchestration tool that automates the manual work it takes to maintain your infrastructure. Use Bolt to automate tasks that you perform on an as-needed basis or as part of a greater orchestration workflow. For example, you can use Bolt to patch and update systems, troubleshoot servers, deploy applications, or stop and restart services. Bolt can be installed on your local workstation and connects directly to remote nodes with SSH or WinRM, so you are not required to install any agent software.

## About This Lab

This repository contains a step-by-step introduction to [Bolt](https://github.com/puppetlabs/bolt) and to the Bolt Tasks ecosystem. It's designed to be followed in order, with each exercise introducing the basic concepts. If you complete all of the exercises you should be well on your way to understanding how you can use Bolt and Bolt Tasks to help manage your infrastructure.

[Watch Intro Video](https://www.youtube.com/watch?v=9Z7nYlspUJw){: .btn}

## Prerequisites

These exercises will help you get Bolt installed and make sure you have a few targets to target with tasks and commands. 

- [Installing Bolt](lab/01-installing-bolt)
- [Acquiring Targets](lab/02-acquiring-targets)

## Exercises

These step through the basic functionality of Bolt Tasks and focus on simple commands you can copy and paste.

1. [Running Commands](lab/03-running-commands)
1. [Running Scripts](lab/04-running-scripts)
1. [Writing Tasks](lab/05-writing-tasks)
1. [Downloading and running existing Tasks](lab/06-downloading-and-running-existing-tasks)
1. [Writing Plans](lab/07-writing-plans)
1. [Writing advanced Tasks](lab/08-writing-advanced-tasks)
1. [Writing advanced Plans](lab/09-writing-advanced-plans)
1. [Deploying an Application](lab/10-deploying-an-application)
1. [Applying manifest code](lab/11-apply-manifest-code)

## Self-Paced Training

Learn to run tasks everywhere you need them, when you need them. Our [free, online self-paced training](https://learn.puppet.com/course/puppet-orchestration-bolt-and-tasks) gets you up and running with the open-source task runner Bolt and Bolt Tasks for Puppet Enterprise.
