# cursorrules

A collection of cursor rules I bring in to many projects

## Quick start

### Add to your shell profile

Add this function to your `~/.zprofile`, `~/.profile`, or `~/.zshrc`:

```bash
function install-cursor-rules() {
  # Create .cursor/rules directory if it doesn't exist
  mkdir -p .cursor/rules

  # Download the repository as a zip file
  # Create a temporary directory
  TEMP_DIR=$(mktemp -d)
  curl -L https://github.com/jhgaylor/cursorrules/archive/main.zip -o $TEMP_DIR/cursorrules.zip

  # Extract the zip file
  unzip -q $TEMP_DIR/cursorrules.zip -d $TEMP_DIR

  # Copy the rules to the current project
  cp $TEMP_DIR/cursorrules-main/rules/* .cursor/rules/

  # Clean up
  rm -rf $TEMP_DIR

  echo "Cursor rules installed successfully to .cursor/rules/"
}
```

After adding the function, remember to reload your profile:
```bash
# For ~/.zprofile or ~/.profile
source ~/.zprofile  # or source ~/.profile

# For ~/.zshrc
source ~/.zshrc
```

### Install rules in your project

Navigate to the root of your project directory and run:

```bash
install-cursor-rules
```

This will install the cursor rules into your current project directory. After running the command, you'll have the rules in `./.cursor/rules`

## Usage

To use these cursor rules in your project:

### Option 1: Clone the Repository

Clone this repository and copy the rules to your project:

```bash
# Navigate to your project directory
cd path/to/your/project

# Create .cursor/rules directory if it doesn't exist
mkdir -p .cursor/rules

# Clone the repository (can be anywhere temporary)
git clone https://github.com/jhgaylor/cursorrules.git cursorrules-temp

# Copy the rules to your project
cp cursorrules-temp/rules/* .cursor/rules/

# Clean up
rm -rf cursorrules-temp
```

### Option 2: Direct Download of Rules

If you just want to download the rules directly:

```bash
# Navigate to your project directory
cd path/to/your/project

# Create .cursor/rules directory if it doesn't exist
mkdir -p .cursor/rules

# Download each rule file
curl -o .cursor/rules/mcp.mdc https://raw.githubusercontent.com/jhgaylor/cursorrules/main/rules/mcp.mdc
curl -o .cursor/rules/typescript-mcp.mdc https://raw.githubusercontent.com/jhgaylor/cursorrules/main/rules/typescript-mcp.mdc
```

### Option 3: Add as a Git Submodule

Add this repository as a Git submodule and create a symbolic link to the rules:

```bash
# Navigate to your project directory
cd path/to/your/project

# Create .cursor directory if it doesn't exist
mkdir -p .cursor/rules

# Add as a submodule (in a subdirectory)
git submodule add https://github.com/jhgaylor/cursorrules.git .cursor/cursorrules

# Create symbolic links to the rules
ln -s ../.cursor/cursorrules/rules/* .cursor/rules/

# Initialize and update the submodule
git submodule update --init
```

After setup, Cursor will automatically load the rules when you open your project.
