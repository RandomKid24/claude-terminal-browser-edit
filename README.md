# claude-terminal-browser-edit

Claude opens a real browser inside your terminal and shows you what it is doing.

Great for web apps (ERP, dashboards, anything with a UI): Claude starts your project, opens it next to the chat, and you watch the UI change as it edits.

Fork of [zenbu-labs/terminal-browser](https://github.com/zenbu-labs/terminal-browser). The only change: Claude's browser tool is on by default.

## Setup (one prompt)

1. Install the browser:
   ```bash
   curl -fsSL https://terminal-browser.sh/install | bash
   ```
2. Open **Ghostty** or **kitty** (Apple Terminal does not work), start Claude Code, and paste this:

   ```
   Set up terminal-browser for me:
   1. Run: claude plugin marketplace add RandomKid24/claude-terminal-browser-edit
   2. Run: claude plugin install terminal-browser@terminal-browser
   3. In ~/.claude/settings.json, add "CLAUDE_CODE_ENABLE_FUNCTION_HOOKS": "1" under "env" (keep everything else).
   4. Append this to ~/.claude/CLAUDE.md (keep existing content):
      # web project preview
      - In web projects, start the dev server in the background if it is not running, then call the `open` tool with its local url so the user can watch in the browser pane.
      - After UI edits, check the pane with the `terminal-browser action` CLI and reload if there is no hot reload.
      - Reuse a running dev server instead of starting another.
   5. Tell me to restart Claude Code.
   ```

3. Restart Claude Code. Done.

From now on, in any web project Claude opens the browser by itself.

## Try it

Ask Claude: `open example.com and tell me the heading`

## Turn it off

In `~/.claude/settings.json`:

```json
{ "pluginConfigs": { "terminal-browser@terminal-browser": { "options": { "agentTool": false } } } }
```

## Good to know

- Only web pages open in the browser. Editing a file does not open anything.
- Works in terminals that support the kitty graphics protocol: Ghostty, kitty, cmux, supacode.
- Claude decides when to open it. If it forgets, say "show it in the browser".

## More

Browser commands, shortcuts, SSH, terminal API, telemetry: [upstream docs](https://github.com/zenbu-labs/terminal-browser#readme)

Plugin details: [claude-code-plugin/README.md](claude-code-plugin/README.md)
