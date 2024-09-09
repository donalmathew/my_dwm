### Part 2: Resizing Windows in `dwm`

`dwm` uses tiling by default, but it also allows window resizing in both tiling and floating modes.

#### Resize Windows in Tiling Mode

By default, in tiling mode, resizing affects the size of the master window and the stack windows.

- **Increase the size of the master window**:
  Press `Mod + L` (default).

- **Decrease the size of the master window**:
  Press `Mod + H` (default).

#### Resize Floating Windows in `dwm`

In floating mode, you can freely resize windows using the mouse or keyboard shortcuts.

1. **Enable Floating Mode**:
   Press `Mod + Shift + Space` to toggle a window into floating mode.

2. **Resize Floating Windows with the Mouse**:
   - **Alt + Right-click and drag** on the window border to resize it.

3. **Resize Floating Windows with Keyboard Shortcuts**:
   To resize floating windows using the keyboard, add these keybindings in `config.h`:

   ```c
   { MODKEY, XK_Up,      resize,    {.v = (int[]){0, -10}} }, // Shrink vertically
   { MODKEY, XK_Down,    resize,    {.v = (int[]){0, 10}} },  // Grow vertically
   { MODKEY, XK_Left,    resize,    {.v = (int[]){-10, 0}} }, // Shrink horizontally
   { MODKEY, XK_Right,   resize,    {.v = (int[]){10, 0}} },  // Grow horizontally
   ```

4. **Rebuild and Restart `dwm`**:
   After adding the new keybindings, recompile `dwm`:

   ```bash
   sudo make clean install
   ```

Now, you should be able to resize windows using both the mouse and keyboard in floating mode.

---

### Summary:

1. **Brightness Control**: Use `brightnessctl` to bind brightness control keys in `dwm`.
2. **Window Resizing**:
   - Use `Mod + H`/`Mod + L` to resize master/stack windows in tiling mode.
   - Toggle floating mode with `Mod + Shift + Space` and resize with the mouse or use custom keybindings for keyboard resizing.

Let me know if you need further assistance!