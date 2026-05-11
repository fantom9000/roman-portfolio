# Claude Code Figma Setup

Claude Code will not automatically see Figma just because this repository contains Figma links. It needs Figma MCP/design tools connected in that Claude Code environment, or Roman must provide screenshots/exported assets.

## Goal

Claude Code should be able to:

- Inspect the Figma file or exact node/frame when needed.
- Compare Figma against the current implemented site.
- Understand that approved site deviations must not be silently reverted.

## Figma Links

- Main page: `https://www.figma.com/design/SKQ1C6VplMtF9IJjDELfSr/Портфолио?node-id=351-26568`
- UI kit: `https://www.figma.com/design/SKQ1C6VplMtF9IJjDELfSr/Портфолио?node-id=365-26027`
- File key: `SKQ1C6VplMtF9IJjDELfSr`

## Setup Checklist

1. Open Claude Code in this project.
2. Check available tools with `/mcp` and available project skills with `/skills`.
3. Confirm whether Figma MCP/design tools are connected.
4. If Figma tools are not connected, connect the official or trusted Figma MCP integration in Claude Code, then restart or refresh the Claude Code session if required.
5. After setup, ask Claude to inspect one small Figma node and report the node name, not to edit code yet.

## Required Agent Behavior

If Figma tools are connected:

- Use the exact node/frame link when possible.
- Fetch only the needed node/frame.
- Compare Figma to the implemented site and the approved deviations in `AGENTS.md`.
- Ask Roman before changing anything that conflicts with an approved deviation.

If Figma tools are not connected:

- Say that Figma is not available in the current Claude Code session.
- Ask Roman for the exact screenshot, node link, or exported asset.
- Do not claim to have inspected Figma.

