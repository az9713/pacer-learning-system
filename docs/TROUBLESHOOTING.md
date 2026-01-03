# PACER Learning System - Troubleshooting Guide

## Table of Contents

1. [Quick Fixes](#quick-fixes)
2. [Installation Issues](#installation-issues)
3. [Command Issues](#command-issues)
4. [Skill Issues](#skill-issues)
5. [Agent Issues](#agent-issues)
6. [Hook Issues](#hook-issues)
7. [Learning System Issues](#learning-system-issues)
8. [Error Messages](#error-messages)
9. [Platform-Specific Issues](#platform-specific-issues)
10. [Getting More Help](#getting-more-help)

---

## Quick Fixes

### Try These First

Before diving into specific issues, try these quick fixes:

#### 1. Restart Claude Code

```bash
# Exit Claude (type 'exit' or press Ctrl+C)
exit

# Start again
claude
```

#### 2. Verify You're in the Right Directory

```bash
# Check current directory
pwd

# Should show: /path/to/pacer_bestpartnerstv
```

#### 3. Check File Permissions

**Windows**:
```powershell
# Right-click folder → Properties → Security
# Ensure you have Read & Write access
```

**Mac/Linux**:
```bash
ls -la .claude/
# Should show read/write permissions (rw-)
```

#### 4. Verify Claude Code Version

```bash
claude --version
# Should show current version
```

---

## Installation Issues

### Problem: "claude: command not found"

**Cause**: Claude Code isn't installed or not in your PATH.

**Solution**:

**Step 1**: Check if Claude Code is installed
```bash
which claude   # Mac/Linux
where claude   # Windows
```

**Step 2**: If not found, install Claude Code:
1. Visit https://claude.ai/code
2. Follow installation instructions for your OS
3. Restart your terminal

**Step 3**: Add to PATH if installed but not found:

**Windows**:
1. Find where Claude is installed (usually `%APPDATA%\Claude\`)
2. Add to PATH:
   - Press Win + X → System → Advanced system settings
   - Environment Variables → Path → Edit → New
   - Add the Claude installation directory

**Mac/Linux**:
```bash
# Add to ~/.bashrc or ~/.zshrc
export PATH="$PATH:/path/to/claude"
source ~/.bashrc
```

---

### Problem: ".claude folder not recognized"

**Cause**: Claude Code not started from the project directory.

**Solution**:

**Step 1**: Navigate to the project folder first
```bash
cd /path/to/pacer_bestpartnerstv
```

**Step 2**: Then start Claude
```bash
claude
```

**Step 3**: Verify the folder exists
```bash
ls -la .claude/   # Mac/Linux
dir .claude       # Windows
```

---

### Problem: "Permission denied" errors

**Cause**: Insufficient file permissions.

**Solution**:

**Mac/Linux**:
```bash
# Fix permissions
chmod -R 755 .claude/
chmod 644 .claude/**/*.md
chmod 644 .claude/**/*.json
```

**Windows**:
1. Right-click the `.claude` folder
2. Properties → Security → Edit
3. Ensure your user has Full Control

---

## Command Issues

### Problem: "Unknown slash command: pacer"

**Cause**: Project-level commands don't register as built-in slash commands.

**This is expected behavior.** Project-level commands work differently.

**Solution - Method 1**: Ask Claude to follow the command

Instead of:
```
/pacer [content]
```

Type:
```
Please classify this content using the PACER system:

[your content here]
```

**Solution - Method 2**: Reference the command file

```
Follow the instructions in .claude/commands/pacer.md to classify:

[your content here]
```

**Solution - Method 3**: Trigger via skill

The `pacer-classifier` skill auto-triggers when you discuss learning content:
```
I'm trying to learn this material. What type of content is it?

[your content here]
```

---

### Problem: Command produces unexpected output

**Cause**: Claude may interpret instructions differently.

**Solution**:

**Step 1**: Be more explicit about the format
```
Use the PACER classification system. Output should include:
- A table with P/A/C/E/R categories
- Count of each type
- Recommendations for each type
```

**Step 2**: Reference the example output
```
Classify using PACER. Format like the examples in
.claude/commands/pacer.md
```

---

### Problem: Command seems to be ignored

**Cause**: Claude may not recognize the request as related to the command.

**Solution**:

Be explicit about which command you want:
```
I want to use the /grinde command to create a mind map for:
[topic]
```

Or reference the skill:
```
Using the grinde-mapper skill, create a mind map for:
[topic]
```

---

## Skill Issues

### Problem: Skill doesn't auto-trigger

**Cause**: The conversation context doesn't match the skill's description.

**Solution**:

**Step 1**: Check the skill description
```bash
# Read the skill file
cat .claude/skills/pacer-classifier/SKILL.md
```

Look at the `description` field - it tells Claude when to activate.

**Step 2**: Use trigger phrases from the description

For `pacer-classifier`:
> "Use when learning new material, studying, reading educational content..."

So say:
```
I'm studying this material and want to learn it effectively:
[content]
```

**Step 3**: Explicitly invoke the skill
```
Using the pacer-classifier skill, analyze this:
[content]
```

---

### Problem: Skill produces wrong output format

**Cause**: Claude may not follow the exact format specified.

**Solution**:

**Step 1**: Ask for the specific format
```
Use PACER classification. Follow the exact output format from
the skill file, including the table with categories.
```

**Step 2**: Provide an example of desired output
```
Classify this. Output should look like:

| Category | Count | Items |
|----------|-------|-------|
| P | X | [items] |
...
```

---

### Problem: Multiple skills conflict

**Cause**: Several skills might apply to the same request.

**Solution**:

Be specific about which skill you want:
```
Using ONLY the layer-learning skill (not pacer-classifier),
check my understanding of:
[topic]
```

---

## Agent Issues

### Problem: Agent not spawning

**Cause**: The request doesn't match the agent's description.

**Solution**:

**Step 1**: Explicitly request the agent
```
Spawn the learning-analyzer agent to analyze this content:
[content]
```

Or:
```
Use the learning-analyzer subagent for this task:
[task]
```

**Step 2**: Check agent file exists
```bash
ls .claude/agents/
# Should list: learning-analyzer.md, digestion-coach.md, learner-diagnostic.md
```

---

### Problem: Agent uses wrong tools

**Cause**: Tools not specified correctly in agent file.

**Solution**:

**Step 1**: Check the agent's tools
```bash
head -10 .claude/agents/learning-analyzer.md
# Look for the 'tools:' line
```

**Step 2**: Edit if needed
```yaml
tools: Read, Write, Edit, Grep, Glob, WebFetch
```

Valid tools: `Read`, `Write`, `Edit`, `Bash`, `Grep`, `Glob`, `WebFetch`, `WebSearch`, `Task`, `TodoWrite`

---

### Problem: Agent doesn't inherit skills

**Cause**: Skills not listed in agent's frontmatter.

**Solution**:

**Step 1**: Check the agent file
```yaml
---
name: learning-analyzer
skills: pacer-classifier, layer-learning  # Must list skills here
---
```

**Step 2**: Edit to add skills
The `skills:` field should list skill names (not paths).

---

## Hook Issues

### Problem: Hook doesn't fire

**Cause**: Usually a configuration issue.

**Solution**:

**Step 1**: Validate JSON syntax
```bash
# Use a JSON validator or:
cat .claude/settings.json | python -m json.tool
```

Common JSON errors:
- Missing commas between items
- Trailing commas (not allowed in JSON)
- Unquoted strings

**Step 2**: Check event name spelling
Valid events: `PreToolUse`, `PostToolUse`, `Notification`, `Stop`

**Step 3**: Check matcher pattern
```json
"matcher": "Read|WebFetch"   # Correct: pipe for OR
"matcher": "Read, WebFetch"  # Wrong: comma doesn't work
```

---

### Problem: Hook command fails

**Cause**: Shell command has errors or wrong paths.

**Solution**:

**Step 1**: Test the command manually
```bash
echo test >> /path/to/log.txt
# See if it works
```

**Step 2**: Check environment variables
```json
"command": "echo $TOOL_NAME >> \"$CLAUDE_PROJECT_DIR/.claude/test.log\""
```

Variables available:
- `$TOOL_NAME` - Name of tool used
- `$CLAUDE_PROJECT_DIR` - Project directory

**Step 3**: Check path format for your OS

**Windows**:
```json
"command": "echo %TOOL_NAME% >> \"%CLAUDE_PROJECT_DIR%\\.claude\\test.log\""
```

**Mac/Linux**:
```json
"command": "echo $TOOL_NAME >> \"$CLAUDE_PROJECT_DIR/.claude/test.log\""
```

---

### Problem: Hook runs but log file not created

**Cause**: Path issues or permissions.

**Solution**:

**Step 1**: Check the path exists
```bash
ls .claude/
# The directory should exist
```

**Step 2**: Check write permissions
```bash
touch .claude/test.txt
# Should work without error
```

**Step 3**: Use absolute paths
```json
"command": "echo test >> /full/path/to/project/.claude/log.txt"
```

---

## Learning System Issues

### Problem: Everything classified as R-type

**Cause**: Misunderstanding of PACER classification.

**Solution**:

This is a classification error, not a technical issue. Challenge each R classification:

```
I classified this as Reference, but I'm not sure.
Can this be understood instead of memorized?

[content]
```

Remember: **Most content is NOT R-type!**
- If it explains WHY → Conceptual
- If it's steps to follow → Procedural
- If it's a comparison → Analogous
- If it supports another idea → Evidence
- Only truly arbitrary facts → Reference

---

### Problem: Mind maps too simple or too complex

**Cause**: Input too brief or too detailed.

**Solution**:

**For too simple**: Provide more context
```
Create a detailed GRINDE map for [topic].
Include at least 4 major chunks with relationships.
```

**For too complex**: Request simplification
```
Create a high-level GRINDE map for [topic].
Focus on the 3-4 most important concepts only.
```

---

### Problem: Balance check always shows imbalance

**Cause**: Either hooks aren't logging, or you're genuinely imbalanced.

**Solution**:

**Step 1**: Check if logging works
```bash
cat .claude/learning-balance.log
# Should show timestamps of Read/WebFetch usage
```

**Step 2**: If no log, check hook configuration

**Step 3**: If logging works, you might actually have a balance problem!
Follow the recommendations to create maps and practice.

---

## Error Messages

### "Cannot read file" / "File not found"

**Cause**: Wrong path or file doesn't exist.

**Solution**:
```bash
# List all skill files
ls -la .claude/skills/*/

# List all command files
ls -la .claude/commands/

# Verify specific file
cat .claude/skills/pacer-classifier/SKILL.md
```

---

### "Invalid JSON"

**Cause**: Syntax error in settings.json.

**Solution**:

**Step 1**: Find the error
```bash
python -m json.tool .claude/settings.json
# Will show error location
```

**Step 2**: Common fixes:
```json
// Wrong: trailing comma
{"key": "value",}

// Correct: no trailing comma
{"key": "value"}

// Wrong: single quotes
{'key': 'value'}

// Correct: double quotes
{"key": "value"}
```

---

### "Tool not available"

**Cause**: Agent requesting unavailable tool.

**Solution**:

Check the tool name is spelled correctly in agent file:
```yaml
tools: Read, Write, Edit  # Not: read, WRITE, edit
```

Valid tool names (case-sensitive):
- `Read`, `Write`, `Edit`
- `Bash`, `Grep`, `Glob`
- `WebFetch`, `WebSearch`
- `Task`, `TodoWrite`

---

## Platform-Specific Issues

### Windows

#### Problem: Paths with backslashes fail

**Solution**: Use forward slashes or escape backslashes
```json
// Both work on Windows:
"path/to/file"
"path\\to\\file"
```

#### Problem: Commands don't run in hooks

**Solution**: Use Windows-compatible commands
```json
// Linux/Mac command:
"command": "echo test >> log.txt"

// Windows equivalent:
"command": "cmd /c echo test >> log.txt"
```

---

### Mac

#### Problem: Permission denied for .claude folder

**Solution**:
```bash
chmod -R 755 .claude/
```

#### Problem: Claude not in PATH after install

**Solution**:
```bash
# Add to ~/.zshrc (or ~/.bash_profile)
export PATH="$PATH:/Applications/Claude.app/Contents/MacOS"
source ~/.zshrc
```

---

### Linux

#### Problem: Claude command not found after install

**Solution**:
```bash
# Check installation location
which claude || find /usr -name "claude" 2>/dev/null

# Add to PATH in ~/.bashrc
export PATH="$PATH:/path/to/claude"
source ~/.bashrc
```

---

## Getting More Help

### Step 1: Gather Information

Before seeking help, collect:

1. **Your OS and version**
   ```bash
   uname -a        # Mac/Linux
   ver             # Windows
   ```

2. **Claude Code version**
   ```bash
   claude --version
   ```

3. **The exact error message** (copy-paste, don't paraphrase)

4. **What you were trying to do** (step by step)

5. **What you expected vs what happened**

### Step 2: Check Existing Resources

1. **This troubleshooting guide** (you're here!)
2. **User Guide**: `docs/USER_GUIDE.md`
3. **Developer Guide**: `docs/DEVELOPER_GUIDE.md`
4. **Claude Code documentation**: https://docs.anthropic.com/claude-code

### Step 3: Ask Claude

Claude can often help troubleshoot:
```
I'm getting this error when trying to [action]:
[error message]

I expected [expected behavior].
How can I fix this?
```

### Step 4: Check File Contents

Verify your files match expected format:
```bash
# Check skill format
head -20 .claude/skills/pacer-classifier/SKILL.md

# Check settings syntax
cat .claude/settings.json
```

### Step 5: Start Fresh

If all else fails, you can regenerate the PACER files:
```
Please regenerate the PACER Learning System files in .claude/
```

---

## Preventive Measures

### Avoid Common Problems

1. **Always start Claude from the project directory**
   ```bash
   cd /path/to/pacer_bestpartnerstv
   claude
   ```

2. **Keep JSON valid**
   - Use a JSON validator before saving settings.json
   - No trailing commas
   - Double quotes only

3. **Use relative paths when possible**
   - They're more portable across systems

4. **Test changes incrementally**
   - Change one thing at a time
   - Test after each change

5. **Back up working configurations**
   ```bash
   cp .claude/settings.json .claude/settings.json.backup
   ```

---

## Quick Reference: Common Commands

```bash
# Start Claude in project
cd /path/to/pacer_bestpartnerstv && claude

# Check file exists
ls .claude/skills/pacer-classifier/SKILL.md

# Validate JSON
python -m json.tool .claude/settings.json

# Check permissions (Mac/Linux)
ls -la .claude/

# View log file
cat .claude/learning-balance.log

# Fix permissions (Mac/Linux)
chmod -R 755 .claude/
```

---

If you're still stuck after trying these solutions, the issue may be specific to your environment. Provide all the information from "Getting More Help" when asking for assistance.
