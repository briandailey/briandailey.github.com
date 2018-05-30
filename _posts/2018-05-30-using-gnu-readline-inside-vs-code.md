---
layout: post
title: "Using GNU Readline (Bash Shortcuts) in VS Code Terminal"
description: ""
category: windows
tags: [windows, vscode, gnureadline]
---
If you use VS Code and a Linux (bash/zsh/what-have-you) terminal, you may have noticed that some keyboard shortcuts (e.g., ctrl+p to cycle previous commands) are intercepted by VS Code. As a fairly [proficient user of shell keyboard shortcuts](http://dailytechnology.net/talk-cli-intro/#/), I found this to be pretty obnoxious. Here's how you can fix it.

First, open your preferences file (hit ctrl+shift+p and type "User Settings". You want to copy the default values for `terminal.integrated.commandsToSkipShell` and remove the following values:

```
    "workbench.action.quickOpen",
    "workbench.action.quickOpenPreviousEditor",
    "workbench.action.quickOpenView",
```

Once removed, you'll find that ctrl+p should now properly rotate through your command-line history. Other shortcuts, like ctrl+k and ctrl+e should also work correctly (as they previously opened the workspace quick-open dialog).

There may be other commands that skip the shell, too. You can remove them from `terminal.integrated.commandsToSkipShell` as necessary.

Happy coding!

_Was this tip useful? Leave a comment and let me know!_
