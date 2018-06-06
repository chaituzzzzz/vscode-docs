---
Order: 9
Area: editor
TOCTitle: Integrated Terminal
ContentId: 7B4DC928-2414-4FC7-9C76-E4A13D6675FE
PageTitle: Integrated Terminal in Visual Studio Code
DateApproved: 5/3/2018
MetaDescription: VisuaStudio Code has an integrated terminal so you can work in the shell of your choice without leaving the editor.
---
# Integrated Terminal

In Visual Studio Code, you can open an integrated terminal, initially starting at the root of your workspace. This can be very convenient as you don't have to switch windows or alter the state of an existing terminal to perform a quick command line task.

To open the terminal:

* Use the `kb(workbench.action.terminal.toggleTerminal)` keyboard shortcut with the backtick character.
* Use the **View** | **Integrated Terminal** menu command.
* From the **Command Palette** (`kb(workbench.action.showCommands)`), use the **View:Toggle Integrated Terminal** command.

![Terminal](images/integrated-terminal/integrated-terminal.png)

> **Note:** You can still open an external shell with the `kb(workbench.action.terminal.openNativeConsole)` keyboard shortcut if you prefer to work outside VS Code.

## Managing Multiple Terminals

You can create multiple terminals open to different locations and easily navigate between them. Terminal instances can be added by hitting the plus icon on the top-right of the **TERMINAL** panel or by triggering the `kb(workbench.action.terminal.new)` command. This creates another entry in the dropdown list that can be used to switch between them.

![Multiple Terminals](images/integrated-terminal/terminal-multiple-instances.png)

Remove terminal instances by pressing the trash can button.

>**Tip:** If you use multiple terminals extensively, you can add key bindings for the `focusNext`, `focusPrevious` and `kill` commands outlined in the [Key Bindings section](/docs/editor/integrated-terminal.md#terminal-key-bindings) to allow navigation between them using only the keyboard.

### Terminal Splitting

You can also split the terminal by triggering the `kb(workbench.action.terminal.split)` command or via the right click context menu.

![Split terminals](images/integrated-terminal/terminal-split-pane.png)

When focusing a split terminal pane, you can move focus and resize using one of the following commands:

Key|Command
---|---
`kb(workbench.action.terminal.focusPreviousPane)` | Focus Previous Pane
`kb(workbench.action.terminal.focusNextPane)` | Focus Next Pane
`kb(workbench.action.terminal.resizePaneLeft)` | Resize Pane Left
`kb(workbench.action.terminal.resizePaneRight)` | Resize Pane Right
`kb(workbench.action.terminal.resizePaneUp)` | Resize Pane Up
`kb(workbench.action.terminal.resizePaneDown)` | Resize Pane Down

## Configuration

The shell used defaults to `$SHELL` on Linux and macOS, PowerShell on Windows 10 and cmd.exe on earlier versions of Windows. These can be overridden manually by setting `terminal.integrated.shell.*` in [settings](/docs/getstarted/settings.md). Arguments can be passed to the terminal shell using the `terminal.integrated.shellArgs.*` settings.

### Windows

Correctly configuring your shell on Windows is a matter of locating the right executable and updating the setting. Below are a list of common shell executables and their default locations:

```json
// Command Prompt
"terminal.integrated.shell.windows": "C:\\Windows\\System32\\cmd.exe"
// PowerShell
"terminal.integrated.shell.windows": "C:\\Windows\\System32\\WindowsPowerShell\\v1.0\\powershell.exe"
// Git Bash
"terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe"
// Bash on Ubuntu (on Windows)
"terminal.integrated.shell.windows": "C:\\Windows\\System32\\bash.exe"
```

There is also the convenience command `Select Default Shell` that can be accessed through the command palette which can detect and set this for you.

>**Note:** To be used as an integrated terminal, the shell executable must be a console application so that `stdin/stdout/stderr` can be redirected.

>**Tip:** The integrated terminal shell is running with the permissions of VS Code. If you need to run a shell command with elevated (administrator) or different permissions, you can use platform utilities such as `runas.exe` within a terminal.

### Shell arguments

You can pass arguments to the shell when it is launched.

For example, to enable running bash as a login shell (which runs `.bash_profile`), pass in the `-l` argument (with double quotes):

```json
// Linux
"terminal.integrated.shellArgs.linux": ["-l"]
```

## Terminal Display Settings

You can customize the integrated terminal font and line height with the following settings:

* `terminal.integrated.fontFamily`
* `terminal.integrated.fontSize`
* `terminal.integrated.fontWeight`
* `terminal.integrated.fontWeightBold`
* `terminal.integrated.lineHeight`

## Terminal Key Bindings

The **View: Toggle Integrated Terminal** command is bound to `kb(workbench.action.terminal.toggleTerminal)` to quickly toggle the integrated terminal panel in and out of view.

Below are the keyboard shortcuts to quickly navigate within the integrated terminal:

Key|Command
---|---
`kb(workbench.action.terminal.toggleTerminal)`|Show integrated terminal
`kb(workbench.action.terminal.new)`|Create new terminal
`kb(workbench.action.terminal.scrollUp)`|Scroll up
`kb(workbench.action.terminal.scrollDown)`|Scroll down
`kb(workbench.action.terminal.scrollUpPage)`|Scroll page up
`kb(workbench.action.terminal.scrollDownPage)`|Scroll page down
`kb(workbench.action.terminal.scrollToTop)`|Scroll to top
`kb(workbench.action.terminal.scrollToBottom)`|Scroll to bottom
`kb(workbench.action.terminal.clear)`|Clear the terminal

Other terminal commands are available and can be bound to your preferred keyboard shortcuts.

They are:

* `workbench.action.terminal.focus`: Focus the terminal. This is like toggle but focuses the terminal instead of hiding it, if it is visible.
* `workbench.action.terminal.focusNext`: Focuses the next terminal instance.
* `workbench.action.terminal.focusPrevious`: Focuses the previous terminal instance.
* `workbench.action.terminal.focusAtIndexN`: Focuses the terminal at index N (N=1-9)
* `workbench.action.terminal.kill`: Remove the current terminal instance.
* `workbench.action.terminal.runSelectedText`: Run the selected text in the terminal instance.
* `workbench.action.terminal.runActiveFile`: Run the active file in the terminal instance.

### Run Selected Text

To use the `runSelectedText` command, select text in an editor and run the command **Terminal: Run Selected Text in Active Terminal** via the **Command Palette** (`kb(workbench.action.showCommands)`):

![Run selected text](images/integrated-terminal/terminal_run_selected.png)

The terminal will attempt to run the selected text.

![Run selected text result](images/integrated-terminal/terminal_run_selected_result.png)

If no text is selected in the active editor, the line that the cursor is on is run in the terminal.

### Copy & Paste

The keybindings for copy and paste follow platform standards:

* Linux: `kbstyle(Ctrl+Shift+C)` and `kbstyle(Ctrl+Shift+V)`
* macOS: `kbstyle(Cmd+C)` and `kbstyle(Cmd+V)`
* Windows: `kbstyle(Ctrl+C)` and `kbstyle(Ctrl+V)`

### Right click behavior

The right click behavior differs based on the platform:

* Linux: Show the context menu.
* macOS: Select the word under the cursor and show the context menu.
* Windows: Copy and drop selection if there is a selection, otherwise paste.

This can be configured using the `terminal.integrated.rightClickBehavior` setting.

### Find

The Integrated Terminal has basic find functionality which can be triggered with `kb(workbench.action.terminal.focusFindWidget)`.

If you want `kbstyle(Ctrl+F)` to go to the shell instead of launching the Find widget on Linux and Windows, you will need to remove the keybinding like so:

```js
// Windows/Linux
{ "key": "ctrl+f", "command": "-workbench.action.terminal.focusFindWidget",
                      "when": "terminalFocus" },
// macOS
{ "key": "cmd+f",  "command": "-workbench.action.terminal.focusFindWidget",
                      "when": "terminalFocus" },
```

### Rename terminal sessions

Integrated Terminal sessions can now be renamed using the **Terminal: Rename** (`workbench.action.terminal.rename`) command. The new name will be displayed in the terminal selection drop-down.

### Forcing key bindings to pass through the terminal

While focus is in the integrated terminal, many key bindings will not work as the keystrokes are passed to and consumed by the terminal itself. The `terminal.integrated.commandsToSkipShell` setting can be used to get around this. It contains an array of command names whose key bindings will skip processing by the shell and instead be processed by the VS Code key binding system. By default, this includes all terminal key bindings in addition to a select few commonly used key bindings.

## Next Steps

The basics of the terminal have been covered in this document, read on to find out more about:

* [Tasks](/docs/editor/tasks.md) - Tasks let you integrate with external tools and leverage the terminal heavily.
* [Mastering VS Code's Terminal](https://www.growingwiththeweb.com/2017/03/mastering-vscodes-terminal.html) - An external blog with plenty of power user tips for the terminal.
* Explore the rest of the terminal commands by browsing your keybindings.json file within VS Code.

## Common Questions

**Q. Why is VS Code shortcut X not working when the terminal has focus?**

**A:** Currently the terminal consumes many key bindings, preventing Visual Studio Code from reacting to them. Some examples are `kbstyle(F1)` to open the **Command Palette** and `kbstyle(Ctrl+P)` for **Quick Open** on Linux and Windows. This is necessary as various terminal programs and/or shells may respond to these key bindings themselves. There are plans to explore a blacklist that would prevent certain key bindings from being handled by the terminal (see [#7269](https://github.com/Microsoft/vscode/issues/7269)).

**Q: Integrated terminal exited with code 1 on Windows 10.**

**A:** This can happen if you run VS Code in compatibility mode which may be turned on automatically if you have upgraded Windows. You can change this by right-clicking the executable and selecting properties, then uncheck "Run this program in compatibility mode" in the compatibility tab.

**Q: Can I use Cmder's shell with the terminal on Windows?**

**A:** Yes, to use the [Cmder](http://cmder.net/) shell in VS Code, you need to create a `vscode.bat` file in your cmder path with the following contents:

```bat
@echo off
SET CurrentWorkingDirectory=%CD%
SET CMDER_ROOT=C:\cmder (your path to cmder)
CALL "%CMDER_ROOT%\vendor\init.bat"
CD /D %CurrentWorkingDirectory%
```

then in your VS Code user settings, add the following to your `settings.json` file:

```json
"terminal.integrated.shell.windows": "C:\\WINDOWS\\System32\\cmd.exe",
"terminal.integrated.shellArgs.windows": ["/K", "C:\\cmder\\vscode.bat"]
```

**Q: Powershell on macOS is complaining about a "-l" argument, how do I fix it?**

**A:** When configuring the integrated terminal to use Powershell on macOS you may hit [this error](https://github.com/Microsoft/vscode/issues/33022) complaining about a `"-l"` argument. To fix this you will need to override the shell args setting as it defaults to `["-l"]` to run login shells by default (for bash/zsh/etc.).

```js
"terminal.integrated.shellArgs.osx": []
```

**Q: How can I change my default Windows terminal back to PowerShell?**

**A:** If you want to put the default Integrated Terminal shell back to the default (PowerShell on Windows), you can remove the shell override from your User [Settings](/docs/getstarted/settings.md) (`kb(workbench.action.openSettings)`).

For example, if you have set your default terminal to bash, you will find `terminal.integrated.shell.windows` in your `settings.json` pointing to your bash location.

```json
"terminal.integrated.shell.windows": "C:\\WINDOWS\\System32\\bash.exe",
```

Remove the entry to use the built-in VS Code default or set it to another shell executable path.

**Q: Why is the terminal not working when running the 32-bit Windows client on 64-bit Windows?**

The easy fix for this is to use the 64-bit version. If you must use the 32-bit version you need to use the `sysnative` path when configuring your paths instead of `System32`:

```json
"terminal.integrated.shell.windows": "C:\\WINDOWS\\sysnative\\cmd.exe",
```

**Q: Why is Cmd+k/Ctrl+k not clearing the terminal?**

**A:** Normally `kbstyle(Cmd+k)`/`kbstyle(Ctrl+k)` clears the terminal on macOS/Windows, but this can stop working when chord keybindings are added either by the user or extensions. The `kbstyle(Cmd+k)`/`kbstyle(Ctrl+k)` keybindings rely on the VS Code keybinding priority system which defines which keybinding is active at any given time (user > extension > default). In order to fix this, you need to redefine your user keybinding which will have priority, preferably at the bottom of your user `keybindings.json` file:

macOS:

```json
{ "key": "cmd+k",                 "command": "workbench.action.terminal.clear",
                                     "when": "terminalFocus" },
```

Windows:

```json
{ "key": "ctrl+k",                "command": "workbench.action.terminal.clear",
                                     "when": "terminalFocus" },
```

### Why is nvm complaining about a prefix option when the Integrated Terminal is launched

nvm (Node Version Manager) users often see this error for the first time inside VS Code's Integrated Terminal:

```bash
nvm is not compatible with the npm config "prefix" option: currently set to "/usr/local"
Run `npm config delete prefix` or `nvm use --delete-prefix v8.9.1 --silent` to unset it
```

This is mostly a macOS problem and does not happen in external terminals. The typical reasons for this are the following:

* `npm` was globally installed using another instance of `node` which is somewhere in your path (such as `/usr/local/bin/npm`).
* In order to get the development tools on the `$PATH`, VS Code will launch a bash login shell on start up. This means that your `~/.bash_profile` has already run and when an Integrated Terminal launches, it will run **another** login shell, reordering the `$PATH` potentially in unexpected ways.

To resolve this issue, you need to track down where the old `npm` is installed and remove both it and its out of date node_modules. You can do this by finding the `nvm` initialization script and running `which npm` before it runs, which should print the path when you launch a new terminal.

Once you have the path to npm, you can find the old node_modules by resolving the symlink by running a command something like this:

```bash
ls -la /usr/local/bin | grep npm
```

This will give you the resolved path at the end:

```bash
... npm -> ../lib/node_modules/npm/bin/npm-cli.js
```

From there, removing the files and relaunching VS Code should fix the issue:

```bash
rm -R /usr/local/bin/npm /usr/local/lib/node_modules/npm/bin/npm-cli.js
```
