---
path: "/docs/cli-command-reference/installing-cli-tool"
title: "Installing the Galasa CLI"
---

This section provides details about prerequisite software requirements and information about how to download and install the Galasa command line interface tool (Galasa CLI) on your local machine. 

## Prerequisites

| Software |  Description  |
| :---- | :-------- | 
| Java JDK  | Required. Galasa tests and Managers are written in Java - you need to install a Java version 11 JDK or later to use it. _Note:_ We do not currently support Java 17 or later. |
| Maven or Gradle  | You must install either Maven or Gradle in order to build Galasa projects. Galasa projects are hierarchical file structures that provide the ability to store and run Galasa tests. All Galasa versions are compatible with Gradle releases 6.8.x and later. |
| 3270 emulator | Optional. Although you do not need a 3270 emulator to run a Galasa test (even if it tests a 3270 application) you can use one to explore Galasa Simbank, a simulated version of an application that helps you get acquainted with Galasa before connecting to a real mainframe to run your own tests. There are many such emulators available but IBM's Personal Communications (PCOMM) is frequently used, as is IBM's Host on Demand software, which includes support for Windows, Linux and MacOS.| 


## Downloading the Galasa CLI

To install Galasa for using in the command-line you first need to download the binary file for the Galasa CLI from the Galasa cli respository in GitHub. 

The following versions of the Galasa CLI are available to download for different operating systems and machine architectures:

| Operating system  |  Download  |
| :---- | :-------- | 
| MacOSX  | galasactl-darwin-x86_64 |
| MacOSX  | galasactl-darwin-arm64 |
| Linux 64-bit x86 | galasactl-linux-x86_64 | 
| Linux arm64 | galasactl-linux-arm64 | 
| zLinux  | galasactl-linux-s390x | 
| Windows | galasactl-windows-x86_64.exe | 


## Installing the Galasa CLI

Complete the following steps to install Galasa for using the command line:

On Mac or Unix:

1. Find out the architecture of your machine by typing the command `uname -m` into your terminal.
2. Download the appropriate binary of the Galasa CLI for your machine architecture from the [Galasa cli repository](https://github.com/galasa-dev/cli/releases) in GitHub and re-name it to `galasactl`.
3. Add Galasa CLI to your PATH to enable you to run CLI commands from anywhere on your file system without having to specify the absolute path. To set the path permanently, you need add the Galasa CLI path to your shell's initialization file. For example, if you downloaded the galasactl executable to a folder called `~/tools` in your home directory, you need to add `~/tools` to the list of directories that your shell searches through when you enter a command. You can do this by adding the line ```export PATH=$PATH:$HOME/tools``` to your shell’s initialization file (for example `~/.bashrc` or `~/.zshrc`). 
4. Set execute permission on the binary by running the `chmod +x galasactl` command in the directory containing `galasactl`.
5. If you are using a Mac, you can set permission to open the Galasa CLI tool by running the `spctl --add galasactl` command in the directory containing `galasactl`. You are prompted by a security panel asking you to log in to show that you are issuing the command.

You can now run the Galasa CLI too from any directory in your file system without having to specify the absolute path.


On Windows (Powershell)

1. Download the binary and re-name it to `galasactl`.
2. Add `galasactl` to your PATH to enable the tool to be called from the command line without having to specify the path to the directory in which it is stored. For example, save the galasactl executable to a folder called `~/tools` in your `C:` directory and run the `setx PATH "C:\tools;%PATH%"` command to add it to your PATH.
3. Open `cmd.exe` and type `start galasactl.exe` in the directory containing `galasactl`.

You can now run the Galasa CLI too from any directory in your file system without having to specify the absolute path.


## Next steps

Read the [Initialising your local environment](/docs/initialising-home-folder) documentation to help you to set up some basic file structures and files in your home folder so that you can start using Galasa.






