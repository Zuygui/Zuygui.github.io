+++
title = "Introducing FlowUpdater JSON Creator"
description = "FlowUpdater JSON Creator is a tool to create JSON files compatibles with FlowUpdater."
date = "2024-01-29T20:09:05+01:00"
github_link = "https://github.com/Zuygui/flowupdater-json-creator"
draft = false
author = "Zuygui"
tags = ["rust", "minecraft", "json"]
image = "/images/fujc.jpg"
toc = true
mathjax = true

+++

FlowUpdater JSON Creator is a tool to create JSON files compatibles with FlowUpdater.

## Introduction

While discussing and assisting people on the [Support Launcher](https://discord.gg/zJkc7nZHRk) Discord server, a discord server for helping people to make customs Minecraft launchers, I realized that creating JSON files compatible with [Flow Updater](https://github.com/FlowArg/FlowUpdater) was time-consuming and tedious. This led me to the idea of developing a command-line tool to replace [the existing desktop application](https://github.com/FlowArg/FlowUpdaterJsonCreator).

## What is Flow Updater ?

Flow updater is a Java library to install, update and launch Minecraft (retrieved from officials servers) and mods loaded through Forge or any other mods loader. To load the mod list and other configurations, it is possible to host a JSON file and pass it into the library, ... So a JSON compatible with FlowUpdater looks like :

_Note:_ JSON (JavaScript Object Notation) is a data file format easy to read and write for humans and machines.

```json
{
  "curseFiles": [
    {
      "projectID": 123456, // random curseforge project id
      "fileID": 123456 // random curseforge file id
    }
  ]
}
```

Writing this JSON is very tedious and time-consuming because you have to find the project id and the file id for each mod. So I decided to write a CLI tool to make this task easier.

## Tech Stack

To build this software, I had to utilize several tools, including:

- [Rust](https://rust-lang.com), a compiled functional programming language developed by Mozilla (the company behind Firefox).
- [Request TTY](https://github.com/Lutetium-Vanadium/requestty/), a Rust crate that facilitates the creation of command-line forms.
- [Eternal API](https://docs.curseforge.com/), the new Curseforge API, which allows me to retrieve the necessary information from mods for JSON generation.
- [Serde JSON](https://github.com/serde-rs/json), an extension of the `serde` crate that enables the serialization and deserialization of Rust structs.

I've only mentioned the most significant elements present in the [source code](https://github.com/zuygui/flowupdater-json-creator).

## Initial goal

I wanna replace the Java application (GUI) by a CLI application in Rust. I also wanna make the application more fast and accessible. Finally, I wanna add new features to the application like locals mods support and archives exports.

## The refactoring

With [Bricklou](https://github.com/bricklou), we have decided to refactor all the code of the app for a better readability and a better maintainability. The first version of code are always available at the [`old`](https://github.com/zuygui/flowupdater/tree/old) branch. The new version of the code is available at the [`master`](https://github.com/zuygui/flowupdater) branch. I've migrated all the backend code to the backend in a rust crate called [`fujc_api`](https://crates.io/crates/fujc_api) for a better integration to the (future) GUI app and CLI. Why have two backend when we can have one ?
For install the crate, you can use the following command :

```sh
cargo add fujc_api
```

or add the following line to your `Cargo.toml` file :

```toml
fujc_api = "0.1.0"
```

## The GUI

Bricklou suggested to implement a GUI app for a better accessibility. It's not already implemented but we are working on. We think to use [Qt](https://www.qt.io/) for the GUI app. We are working on the GUI app in the [`gui`](https://github.com/zuygui/flowupdater-json-creator/tree/gui) branch.

## Credits

I wanna thank [Bricklou](https://github.com/bricklou) for maintening the project with me. I also wanna thank [FlowArg](https://github.com/FlowArg) for creating the original project. Finally, I wanna thank [Asthowen](https://github.com/Asthowen) for helping me with Github CI.

## Conclusion

Thank you for reading this article on my blog. I hope you enjoyed it. Please feel free to leave a comment and give the GitHub repository of this blog a star ⭐
