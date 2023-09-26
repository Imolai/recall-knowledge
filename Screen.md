# Screen summary

The `screen` is a terminal multiplexer that allows you to create multiple virtual terminals within a single physical terminal. Here are some basic usage modes:

1. **Starting a new screen session:**
   ```sh
   screen
   ```
   or you can name the session:
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

3. **Attaching to an existing session:**
   ```sh
   screen -r session_name
   ```

4. **Detaching from a session:**
   To detach from the current session, use the `Ctrl-a d` keyboard shortcut.

5. **Closing a screen session:**
   After detaching from a session, you can close the session with the following command:
   ```sh
   screen -X -S [session_id] quit
   ```

6. **Managing Virtual Windows:**
   - Create a new window: `Ctrl-a c`
   - Switch between windows: `Ctrl-a n` for the next window, and `Ctrl-a p` for the previous window
   - Switch by window number: `Ctrl-a [number]`
   - Naming a window: `Ctrl-a A`

7. **Scroll mode / Scrolling:**
   Activate scroll mode with `Ctrl-a [` and use the arrow keys to scroll. To exit scroll mode, press `Enter` or `Esc`.

8. **Displaying help:**
   If you need more commands, press `Ctrl-a ?` to access the help.

9. **Exiting a screen session:**
   To exit and close the session, type `exit` in the prompt.

10. **Configuration file:**
    The configuration file for `screen` is `~/.screenrc`. Here, you can customize the settings for `screen`.

These are the most important commands and functions to use `screen` effectively.
