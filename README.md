# train-nvim
An interactive Neovim plugin to help you learn and practice Neovim motions and custom keymaps through guided exercises and real-time feedback.

## Prerequisites 

### macOS Setup

1. **Install LuaJIT**:
   ```bash
   brew install luajit
   ```

2. **Install Lua 5.1**:
   ```bash
   curl -LO http://www.lua.org/ftp/lua-5.1.5.tar.gz
   tar xvzf lua-5.1.5.tar.gz
   cd lua-5.1.5/src
   make macosx
   sudo cp lua /usr/local/bin/lua
   ```

3. **Install Luarocks** (for Lua package management):
   ```bash
   brew install luarocks
   ```

4. **Install SQLite3** (required for database functionality):
   ```bash
   brew install sqlite3
   ```

5. **Set LuaRocks Path**:  
   Ensure your shell recognizes LuaRocks paths:
   ```bash
   eval `luarocks path`
   ```
   > _Tip_: To make this permanent, add the above `eval` command to your shell profile (`.bashrc`, `.zshrc`, etc.).

6. **Install `lsqlite3` for Lua 5.1**:
   ```bash
   luarocks install lsqlite3 SQLITE_LIBDIR=/usr/local/opt/sqlite/lib SQLITE_INCDIR=/usr/local/opt/sqlite/include
   ```

7. **Verify Installation**:
   Open Neovim and run:
   ```vim
   :lua require('lsqlite3')
   ```
   If no errors occur, the setup is complete.


## Plugin Installation

Install the plugin using your preferred plugin manager. For example, if you're using `lazy.nvim`:

```lua
-- train-nvim plug-in
return {
  {
    'stefanobianchimazzone/train-nvim.lua',
    config = function()
      require('train-nvim').setup({
        -- Configuration options
        allow_freeride = true,
        collect_data = true,
        data_collection_consent = true,
        log_level = 'info', 
      })
    end,
    dependencies = {
      'kkharji/sqlite.lua',
    },
  },
}
```

Ensure all dependencies, like `lsqlite3`, are installed and configured properly.

## Format

The CI uses `stylua` to format the code; customize the formatting by editing `.stylua.toml`.

## Test

Uses [busted](https://lunarmodules.github.io/busted/) for testing. Installs by using `luarocks --lua-version=5.1 install vusted` then runs `vusted ./test`
for your test cases. `vusted` is a wrapper of Busted especially for testing Neovim plugins.

Create test cases in the `test` folder. Busted expects files in this directory to be named `foo_spec.lua`, with `_spec` as a suffix before the `.lua` file extension. For more usage details please check
[busted usage](https://lunarmodules.github.io/busted/)

## CI

- Auto generates doc from README.
- Runs the Busted/vusted integration tests
- Lints with `stylua`.

