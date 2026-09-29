# Connection examples

Drop-in config for the clients people actually use. The server is hosted, so
every one of these is just a URL — there is no command to run and no key to set.

| File | Where it goes |
|---|---|
| `claude-desktop.json` | merge into `claude_desktop_config.json` |
| `cursor.json` | `.cursor/mcp.json` in your project, or the global one |

Claude Code needs no file:

    claude mcp add --transport http talval https://talval.com/mcp

For the paid endpoint use `https://talval.com/mcp/pro`, which asks for OAuth the
first time a tool is called.
