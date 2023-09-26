# Screen summary

The `screen` is a terminal multiplexer that allows you to create multiple virtual terminals within a single physical terminal.
`screen` is a very useful tool for managing long-running processes and tasks in an SSH session, especially when there's a risk of the session being terminated by network issues, server policies, or other disruptions.
When you start a `screen` session, the processes running within that session are not tied to the SSH session.
If an SSH session is terminated for any reason, any `screen` sessions running within that SSH session will automatically detach. The processes running inside the `screen` session will continue to run in the background.
You can later reattach to the `screen` session and resume your work where you left off.

After reconnecting via SSH, you can reattach to the detached `screen` session using:

```sh
screen -r [session_id_or_name]
```

## Table of contents

<!-- TOC start (generated with https://github.com/derlin/bitdowntoc) -->

* [Start a Screen Session](#start-a-screen-session)
* [Run Your Long-Running Process](#run-your-long-running-process)
* [Detach from Screen](#detach-from-screen)
* [Reattach to Screen](#reattach-to-screen)
* [Starting a new screen session](#starting-a-new-screen-session)
* [Listing sessions](#listing-sessions)
* [Attaching (*R*esume) to an existing session](#attaching-resume-to-an-existing-session)
* [Detaching from a session](#detaching-from-a-session)
* [Closing a screen session](#closing-a-screen-session)
* [Managing Virtual Windows](#managing-virtual-windows)
* [Scroll mode / Scrolling](#scroll-mode--scrolling)
* [Displaying help](#displaying-help)
* [Exiting a screen session](#exiting-a-screen-session)
* [Killing all windows and terminating screen](#killing-all-windows-and-terminating-screen)
* [Configuration file](#configuration-file)
* [Troubleshooting](#troubleshooting)
  + [Attach to not detached session](#attach-to-not-detached-session)
  + [Screen session is garbled or disturbed](#screen-session-is-garbled-or-disturbed)

<!-- TOC end -->

Here’s a brief example of how you might use `screen` in this scenario:

## Start a Screen Session<a name="start-a-screen-session"></a>

```sh
screen -S mysession
```

## Run Your Long-Running Process<a name="run-your-long-running-process"></a>

Start your task or process within the `screen` session.

## Detach from Screen<a name="detach-from-screen"></a>

If you need to, you can detach from the `screen` session by pressing `Ctrl-a d`. The processes running within the `screen` session will continue even if you are detached.

## Reattach to Screen<a name="reattach-to-screen"></a>

If your SSH session is terminated, you can SSH back into the server and reattach to the `screen` session with:

```sh
screen -r mysession
```

This way, `screen` can indeed help prevent data loss due to terminated SSH sessions by allowing processes to run uninterrupted and preserving your command-line environment between connections.

Here are some basic usage modes:

## Starting a new screen session<a name="starting-a-new-screen-session"></a>

```sh
screen
```

or you can name (***S**ubstitue*) the session (it has already a name `[pid.tty.host]`):

```sh
screen -S session_name
```

## Listing sessions<a name="listing-sessions"></a>

```sh
screen -ls
```

or

```sh
screen -list
```

## Attaching (*R*esume) to an existing session<a name="attaching-resume-to-an-existing-session"></a>

```sh
screen -r [pid.tty.host]/[session_name]
```

or simply (if there is only one)

```sh
screen -r
```

## Detaching from a session<a name="detaching-from-a-session"></a>

To detach from the current session, use the **`Ctrl-a d`** keyboard shortcut.

## Closing a screen session<a name="closing-a-screen-session"></a>

After detaching from a session, you can close the session with the following command (*e**X**ecute*):

```sh
screen -X -S [session_id] quit
```

## Managing Virtual Windows<a name="managing-virtual-windows"></a>

* Create a new window: **`Ctrl-a c`**
* Switch between windows: **`Ctrl-a n`** for the *N*ext window, and **`Ctrl-a p`** for the *P*revious window
* Switch by window number: **`Ctrl-a [number]`**
* Naming a window: `Ctrl-a A`

## Scroll mode / Scrolling<a name="scroll-mode--scrolling"></a>

Activate scroll mode with **`Ctrl-a [`** and use the arrow keys to scroll. To exit scroll mode, press `Enter` or `Esc`.

## Displaying help<a name="displaying-help"></a>

If you need more commands, press **`Ctrl-a ?`** to access the help.

## Exiting a screen session<a name="exiting-a-screen-session"></a>

To exit and close the session, type `exit` in the prompt.

## Killing all windows and terminating screen<a name="killing-all-windows-and-terminating-screen"></a>

To kill all windows and terminate screen, press **`Ctrl-a \`**.

Or

1. Press **`Ctrl-a`** to enter command mode.
2. Then type **`:quit`** and press `Enter`.

This will quit the `screen` session by closing all windows at once. Please note that this will immediately terminate all processes running in each window, so make sure to save any unsaved work before using this command.

## Configuration file<a name="configuration-file"></a>

The configuration file for `screen` is **`~/.screenrc`**. Here, you can customize the settings for `screen`.

Example:

```text
startup_message off
defscrollback 100000
shell -${SHELL}
#https://lizdenys.com/journal/articles/understanding-gnu-screens-captions.html
#https://www.gnu.org/software/screen/manual/html_node/String-Escapes.html
caption always '%{= kw}[ %{y}%H%{-} ][ %= %-Lw%{+b M}%n%f* %t%{-}%+LW %= ][ %{r}%l%{-} ][ %{c}%c%{-} ]'
screen -t "bash" 0 bash
screen -t "man" 1 bash
screen -t "nvim" 2 nvim
screen -t "mc" 3 mc
select 0
```

These are the most important commands and functions to use `screen` effectively.

## Troubleshooting<a name="troubleshooting"></a>

### Attach to not detached session<a name="attach-to-not-detached-session"></a>

SSH session terminated by server remotely. When you log on again, you get this:

```text
$ screen -ls
There is a screen on:
        40383.pts-36.host001      (Attached)
1 Socket in /tmp/uscreens/S-noname.
```

Given that the screen session is still marked as "Attached", you won’t be able to directly reattach to it. However, you can forcefully reattach the session using the following command:

```sh
$ screen -d -r 40383.pts-36.host001
```

In this command:

* The `-d` option tells `screen` to detach the session if it is still attached.
* The `-r` option is used to reattach to a session. You will need to specify the session identifier after `-r`, which in this case is `40383.pts-36.host001`.

After running this command, you should be reconnected to your screen session, and any processes or tasks that were running in it will continue to do so.

### Screen session is garbled or disturbed<a name="screen-session-is-garbled-or-disturbed"></a>

If the display of your `screen` session is garbled or disturbed, you can try a couple of things to redraw or refresh the interface:

1. **Redraw Window:**
   Press `Ctrl-a` followed by `Ctrl-l`. This command sends a redraw signal to the terminal, and it should clean up the display.

2. **Redraw Using Reset:**
   Type the `reset` command in the terminal and press `Enter`. This command will reset and reinitialize the terminal, which can often clear up display issues.

3. **Resize Window:**
   Sometimes resizing the terminal window can force it to redraw and correct any display issues.

Remember that if you are using any text-based applications with a user interface (like text editors), they may have their own redraw or refresh commands. For instance, in `vim`, you can press `Ctrl-l` to redraw the interface.
