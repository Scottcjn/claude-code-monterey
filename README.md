# Claude Code for macOS Monterey (12.x)

Successfully running Claude Code 2.0.76 on macOS Monterey 12.7.6 (2013 Mac Pro)

## System Requirements

- **macOS**: Monterey 12.7.6 (tested)
- **Node.js**: v22.21.0 (via nvm)
- **Architecture**: Intel x86_64

## Installation Steps

### 1. Install nvm (Node Version Manager)

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
```

### 2. Install Node.js 22.21.0

```bash
source ~/.nvm/nvm.sh
nvm install 22.21.0
nvm use 22.21.0
nvm alias default 22.21.0
```

### 3. Install Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

### 4. Verify Installation

```bash
claude --version
# Should output: 2.0.76 (Claude Code)
```

## Configuration

Claude Code stores its configuration in:
- `~/.claude.json` - Main configuration
- `~/.claude/` - Debug and stats data

## Usage

```bash
# Start interactive session
claude

# Print mode (non-interactive)
claude -p "your prompt here"

# Get help
claude --help
```

## Compatibility Notes

### What Works
- Full Claude Code functionality
- All command-line options
- Interactive and print modes
- Auto-updates enabled

### Node.js Version Requirement
Claude Code requires Node.js >= 18.0.0. We use v22.21.0 for optimal compatibility with Monterey.

### Shell Integration
Add to your `~/.zshrc` or `~/.bash_profile`:

```bash
# Load nvm
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
```

## Updating Claude Code

```bash
source ~/.nvm/nvm.sh
npm update -g @anthropic-ai/claude-code
```

## System Information

Tested on:
- **Device**: 2013 Mac Pro (Mac Trashcan)
- **Hostname**: Sophias-Mac-Trashcan.local
- **OS**: macOS Monterey 12.7.6 (Build 21H1320)
- **Architecture**: x86_64 (Intel Xeon)
- **Node**: v22.21.0
- **npm**: Included with Node.js
- **Claude Code**: 2.0.76

## Troubleshooting

### npm command not found
Make sure nvm is loaded in your shell:
```bash
source ~/.nvm/nvm.sh
```

### Permission errors
Use nvm instead of system Node.js to avoid permission issues with global packages.

### Auto-updates
Claude Code has auto-updates enabled by default. Check `~/.claude.json` to verify.

## License

Claude Code is provided by Anthropic. See the [official repository](https://github.com/anthropics/claude-code) for license information.

## Links

- [Official Claude Code GitHub](https://github.com/anthropics/claude-code)
- [Anthropic Documentation](https://docs.anthropic.com/)
- [Claude Code NPM Package](https://www.npmjs.com/package/@anthropic-ai/claude-code)

---

**Last Updated**: December 24, 2025
**Claude Code Version**: 2.0.76
**macOS Version**: Monterey 12.7.6

## Multi-Platform Support

This repository documents Claude Code compatibility across various platforms:

### Confirmed Working Platforms

- **macOS Monterey 12.7.6** (Intel x86_64) - Documented here
- **IBM POWER8** (Ubuntu) - See related repositories

### Architecture Support

Claude Code official builds support:
- x86_64 (Intel/AMD)
- ARM64 (Apple Silicon, ARM servers)

For other architectures (like POWER8), custom builds or compatibility layers may be required.

---

**Multi-platform testing and documentation by the community**
