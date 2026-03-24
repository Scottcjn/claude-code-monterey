# Contributing to claude-code-monterey

Thank you for your interest in contributing to claude-code-monterey! This project documents running Claude Code 2.0.76 on macOS Monterey 12.7.6 (2013 Mac Pro and compatible systems).

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [How Can I Contribute?](#how-can-i-contribute)
- [Development Setup](#development-setup)
- [Style Guidelines](#style-guidelines)
- [Submitting Changes](#submitting-changes)
- [Testing Requirements](#testing-requirements)
- [Community](#community)

## Code of Conduct

This project expects all participants to:
- Be respectful and welcoming to newcomers
- Provide constructive feedback
- Focus on helping users run Claude Code on older macOS versions
- Respect differing technical expertise levels

## Getting Started

### Prerequisites

To contribute to this project, you'll need:

- **Hardware**: 2013 Mac Pro (Trashcan) or compatible Mac
- **OS**: macOS Monterey 12.7.6 (primary target)
- **Node.js**: v22.21.0 (via nvm recommended)
- **Architecture**: Intel x86_64
- **Claude Code**: v2.0.76 or later

### Supported Systems

| Device | Year | CPU | macOS | Status |
|--------|------|-----|-------|--------|
| Mac Pro (Trashcan) | 2013 | Intel Xeon | Monterey 12.7.6 | ✅ Primary target |
| MacBook Pro 15" | 2013-2015 | Intel Core i7 | Monterey 12.7.6 | ✅ Supported |
| iMac 27" | 2013-2015 | Intel Core i5/i7 | Monterey 12.7.6 | ✅ Supported |
| Mac mini | 2014 | Intel Core i5 | Monterey 12.7.6 | ✅ Supported |

### Repository Structure

```
claude-code-monterey/
├── README.md           # Main documentation
├── install.sh          # Automated installation script
├── configs/            # Configuration examples
│   ├── .zshrc.example
│   ├── .bash_profile.example
│   └── .claude.json.example
├── troubleshooting/    # Common issues and solutions
├── scripts/            # Helper scripts
└── tests/              # Verification tests
```

## How Can I Contribute?

### Reporting Issues

Before creating an issue:

1. **Check existing issues** to avoid duplicates
2. **Verify your setup** matches documented requirements
3. **Gather system information**:
   ```bash
   # System information
   sw_vers
   uname -m
   
   # Node.js version
   node --version
   
   # Claude Code version
   claude --version
   
   # nvm status
   nvm list
   ```

**Issue report template:**
```markdown
**System**: 2013 Mac Pro / MacBook Pro 2015 / etc.
**macOS Version**: 12.7.6 (Build 21H1320)
**Node.js Version**: v22.21.0
**Claude Code Version**: 2.0.76
**Installation Method**: Manual / install.sh script

**Description**:
Clear description of the issue

**Steps to Reproduce**:
1. Step one
2. Step two
3. Step three

**Expected Behavior**:
What you expected to happen

**Actual Behavior**:
What actually happened

**Error Messages**:
```
Paste any error messages here
```

**Additional Context**:
Any other relevant information
```

### Adding New Hardware Compatibility

When documenting Claude Code on new hardware:

1. **Test all functionality**:
   - Interactive mode (`claude`)
   - Print mode (`claude -p "test"`)
   - Auto-updates
   - Configuration persistence

2. **Document specifications**:
   - Exact model identifier
   - CPU details
   - RAM amount
   - macOS build number

3. **Note any special considerations**:
   - Additional setup steps
   - Known limitations
   - Performance characteristics

### Improving Installation Scripts

When modifying `install.sh` or related scripts:

- Test on fresh macOS installations
- Handle edge cases (missing nvm, wrong Node version)
- Provide clear error messages
- Support both interactive and non-interactive modes

### Documentation Improvements

Documentation contributions are highly valued:
- README clarifications
- Troubleshooting guides
- Performance optimization tips
- Alternative installation methods

## Development Setup

### Setting Up Development Environment

1. **Install Homebrew** (if not already installed):
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. **Install nvm**:
   ```bash
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
   ```

3. **Configure shell** (add to `~/.zshrc` or `~/.bash_profile`):
   ```bash
   export NVM_DIR="$HOME/.nvm"
   [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
   ```

4. **Install Node.js**:
   ```bash
   nvm install 22.21.0
   nvm use 22.21.0
   nvm alias default 22.21.0
   ```

5. **Install Claude Code**:
   ```bash
   npm install -g @anthropic-ai/claude-code
   ```

### Testing Installation Scripts

When modifying installation scripts:

```bash
# Test on clean environment (VM recommended)
./install.sh

# Verify installation
claude --version

# Test interactive mode
claude

# Test print mode
claude -p "Hello from Monterey"
```

### Using Virtual Machines for Testing

For testing without physical hardware:

```bash
# Using VMware Fusion or Parallels
# Create Monterey VM with 4GB+ RAM

# Test installation process
./install.sh

# Verify all functionality
./tests/verify-installation.sh
```

## Style Guidelines

### Shell Script Style

Scripts should follow these conventions:

```bash
#!/bin/bash
set -euo pipefail

# Colors for output
readonly RED='\033[0;31m'
readonly GREEN='\033[0;32m'
readonly NC='\033[0m' # No Color

# Functions: lowercase with underscores
log_info() {
    echo -e "${GREEN}[INFO]${NC} $*"
}

log_error() {
    echo -e "${RED}[ERROR]${NC} $*" >&2
}

# Error handling
die() {
    log_error "$*"
    exit 1
}

# Check prerequisites
check_prerequisites() {
    command -v curl >/dev/null 2>&1 || die "curl is required"
    # ...
}

# Main installation
install_claude_code() {
    log_info "Installing Claude Code..."
    # ...
}

# Main execution
main() {
    check_prerequisites
    install_claude_code
    log_info "Installation complete!"
}

main "$@"
```

### Documentation Style

- Use clear, step-by-step instructions
- Include command examples
- Specify which macOS version for each instruction
- Use formatting for readability:
  - `code` for commands and filenames
  - **Bold** for important notes
  - > Blockquotes for warnings or tips

### Configuration Examples

When providing configuration examples:

```bash
# ~/.zshrc - Claude Code Monterey Setup

# Load nvm
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"

# Claude Code auto-update check
export CLAUDE_CODE_AUTO_UPDATE=true

# Optional: Set default editor
export EDITOR=vim
```

## Submitting Changes

### Pull Request Process

1. **Fork the repository** on GitHub
2. **Clone your fork**:
   ```bash
   git clone https://github.com/YOUR_USERNAME/claude-code-monterey.git
   cd claude-code-monterey
   ```
3. **Create a branch**:
   ```bash
   git checkout -b feature/your-feature-name
   # or
   git checkout -b fix/issue-description
   # or
   git checkout -b docs/improvement-description
   ```
4. **Make your changes** following style guidelines
5. **Test your changes** on Monterey 12.7.6
6. **Commit with clear messages**:
   ```bash
   git commit -m "docs: add MacBook Pro 2015 compatibility

   - Tested on MacBook Pro 15" Mid 2015
   - Intel Core i7, 16GB RAM
   - All Claude Code features working"
   ```
7. **Push to your fork**:
   ```bash
   git push origin feature/your-feature-name
   ```
8. **Open a Pull Request** on GitHub

### Commit Message Format

Follow conventional commits:

- `feat:` - New feature or hardware support
- `fix:` - Bug fix in scripts or documentation
- `docs:` - Documentation changes
- `test:` - Test additions or improvements
- `chore:` - Build process or script changes

**Examples**:
```
feat: add iMac 2014 compatibility documentation
fix: resolve nvm detection in install.sh
docs: update troubleshooting for permission errors
test: add installation verification script
```

### PR Checklist

Before submitting:

- [ ] Changes tested on macOS Monterey 12.7.6
- [ ] Documentation updated if needed
- [ ] Scripts follow style guidelines
- [ ] Commit messages are clear and descriptive
- [ ] No breaking changes without justification
- [ ] Error handling included in scripts
- [ ] Tested on target hardware (or VM)

## Testing Requirements

### Minimum Testing Checklist

All changes must pass:

```bash
# 1. Installation test
./install.sh

# 2. Version check
claude --version
# Expected: 2.0.76 (or later)

# 3. Interactive mode test
claude
# Should start interactive session

# 4. Print mode test
claude -p "What is 2+2?"
# Should return answer

# 5. Configuration persistence test
# Restart terminal, verify claude still works

# 6. Auto-update check (if applicable)
# Check ~/.claude.json for update settings
```

### Hardware-Specific Testing

When adding hardware compatibility:

```bash
# Document system info
system_profiler SPHardwareDataType
sw_vers
node --version
claude --version

# Test all Claude Code features
claude -p "Write a hello world in Python"
claude -p "Explain recursion"
claude -p "Debug this code: ..."
```

### Script Testing

For installation script changes:

```bash
# Test on fresh macOS VM
# 1. Clean install Monterey 12.7.6
# 2. Run install.sh
# 3. Verify all steps complete
# 4. Test Claude Code functionality
# 5. Document any issues
```

## Community

### Getting Help

- **GitHub Issues**: For bugs and feature requests
- **Discussions**: For questions about setup and usage
- **Wiki**: For additional tips and tricks

### Related Projects

- [Official Claude Code](https://github.com/anthropics/claude-code) - Upstream project
- [claude-code-ppc](https://github.com/Scottcjn/claude-code-ppc) - Claude Code for PowerPC Macs
- [nvm](https://github.com/nvm-sh/nvm) - Node Version Manager

### Sharing Your Setup

We welcome reports of successful installations on:
- Different Mac models
- Different macOS versions (within Monterey 12.x)
- Different configurations

Share your setup in Discussions with:
- Hardware specifications
- Installation method used
- Any modifications made
- Performance notes

### Recognition

Contributors will be recognized in:
- README.md contributors section
- Release notes for significant contributions
- Project documentation

---

Thank you for helping expand Claude Code compatibility! Your contributions help users get modern AI tooling on older but capable hardware.
