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

This feature makes `screen` especially useful for long-running tasks or processes, as it allows them to continue running even if the SSH connection is lost, and you can reattach to the session later to check the progress or results.

Here’s a brief example of how you might use `screen` in this scenario:

1. **Start a Screen Session:**
   ```sh
   screen -S mysession
   ```

2. **Run Your Long-Running Process:**
   Start your task or process within the `screen` session.

3. **Detach from Screen:**
   If you need to, you can detach from the `screen` session by pressing `Ctrl-a d`. The processes running within the `screen` session will continue even if you are detached.

4. **Reattach to Screen:**
   If your SSH session is terminated, you can SSH back into the server and reattach to the `screen` session with:
   ```sh
   screen -r mysession
   ```

This way, `screen` can indeed help prevent data loss due to terminated SSH sessions by allowing processes to run uninterrupted and preserving your command-line environment between connections.

Here are some basic usage modes:

1. **Starting a new screen session:**
   ```sh
   screen
   ```
   or you can name (***S**ubstitue*) the session (it has already a name `[pid.tty.host]`):
   ```sh
   screen -S session_name
   ```

2. **Listing sessions:**
   ```sh
   screen -ls
   ```
   or
   ```sh
   screen -list
   ```

3. **Attaching (*R*esume) to an existing session:**
   ```sh
   screen -r [pid.tty.host]/[session_name]
   ```
   or simply (if there is only one)
   ```sh
   screen -r
   ```

5. **Detaching from a session:**
   To detach from the current session, use the **`Ctrl-a d`** keyboard shortcut.

6. **Closing a screen session:**
   After detaching from a session, you can close the session with the following command (*e**X**ecute*):
   ```sh
   screen -X -S [session_id] quit
   ```

7. **Managing Virtual Windows:**
   - Create a new window: **`Ctrl-a c`**
   - Switch between windows: **`Ctrl-a n`** for the *N*ext window, and **`Ctrl-a p`** for the *P*revious window
   - Switch by window number: **`Ctrl-a [number]`**
   - Naming a window: `Ctrl-a A`

8. **Scroll mode / Scrolling:**
   Activate scroll mode with **`Ctrl-a [`** and use the arrow keys to scroll. To exit scroll mode, press `Enter` or `Esc`.

9. **Displaying help:**
   If you need more commands, press **`Ctrl-a ?`** to access the help.

10. **Exiting a screen session:**
   To exit and close the session, type `exit` in the prompt.

11. **Killing all windows and terminating screen:**
   To kill all windows and terminate screen, press **`Ctrl-a \`**.
   Or
      1. Press **`Ctrl-a`** to enter command mode.
      2. Then type **`:quit`** and press `Enter`.
   This will quit the `screen` session by closing all windows at once. Please note that this will immediately terminate all processes running in each window, so make sure to save any unsaved work before using this command.

13. **Configuration file:**
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
