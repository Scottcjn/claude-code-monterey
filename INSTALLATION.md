# Detailed Installation Guide

## Prerequisites Check

Before installing Claude Code, verify your system:

```bash
# Check macOS version
sw_vers

# Expected output for Monterey:
# ProductName:    macOS
# ProductVersion: 12.x.x
# BuildVersion:   21Hxxxx
```

## Step-by-Step Installation

### Step 1: Install nvm

```bash
# Download and install nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

# Close and reopen your terminal, or run:
source ~/.zshrc  # for zsh (default on macOS)
# OR
source ~/.bash_profile  # for bash

# Verify nvm installation
nvm --version
```

### Step 2: Install Node.js

```bash
# Install Node.js 22.21.0
nvm install 22.21.0

# Use this version
nvm use 22.21.0

# Set as default
nvm alias default 22.21.0

# Verify installation
node --version  # Should show v22.21.0
npm --version   # Should show npm version
```

### Step 3: Install Claude Code

```bash
# Install globally via npm
npm install -g @anthropic-ai/claude-code

# Verify installation
claude --version
```

### Step 4: First Run

```bash
# Test Claude Code
claude --help

# Run a simple test
claude -p "What is 2+2?"
```

## Configuration

Claude Code will create configuration files on first run:
- `~/.claude.json` - Main configuration
- `~/.claude/` - Application data directory

## Shell Integration

### For zsh (default on macOS):

Edit `~/.zshrc`:

```bash
# Load nvm automatically
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"
```

### For bash:

Edit `~/.bash_profile`:

```bash
# Load nvm automatically
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"
```

## Verification

Run this command to verify everything is working:

```bash
# Check all components
echo "Node: $(node --version)"
echo "npm: $(npm --version)"
echo "Claude Code: $(claude --version)"
```

Expected output:
```
Node: v22.21.0
npm: 10.x.x
Claude Code: 2.0.76 (Claude Code)
```

## Common Issues

### Issue: command not found: nvm

**Solution**: Source nvm in your current shell:
```bash
source ~/.nvm/nvm.sh
```

### Issue: command not found: claude

**Solution**: Make sure Node.js is active and npm global bin is in PATH:
```bash
source ~/.nvm/nvm.sh
nvm use 22.21.0
```

### Issue: Permission denied when installing

**Solution**: Don't use sudo with nvm. Reinstall Node.js via nvm:
```bash
nvm deactivate
nvm uninstall 22.21.0
nvm install 22.21.0
```

## Updating

### Update Claude Code

```bash
npm update -g @anthropic-ai/claude-code
```

### Update Node.js

```bash
nvm install 22.21.0  # or latest LTS
nvm use 22.21.0
npm install -g @anthropic-ai/claude-code
```

## Uninstallation

### Remove Claude Code

```bash
npm uninstall -g @anthropic-ai/claude-code
rm -rf ~/.claude ~/.claude.json
```

### Remove Node.js and nvm

```bash
nvm deactivate
nvm uninstall 22.21.0
rm -rf ~/.nvm
# Remove nvm lines from ~/.zshrc or ~/.bash_profile
```
