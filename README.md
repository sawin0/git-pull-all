## 🚀 Git Sync All Projects Script

This Bash script loops through all subdirectories in a given folder (e.g., `~/projects`) and performs a `git pull` on the **currently checked-out branch** for each Git project.

It ensures all your projects are updated with the latest changes from their remote repositories.

---

## 🧰 Features

- Automatically detects Git repositories.
- Fetches all remote updates with `git fetch --all`.
- Pulls the latest changes into the current branch (`git pull origin <current-branch>`).
- Skips non-Git folders.

---

## 📝 Script

```bash
#!/bin/bash

# Set the base directory where your Git projects are
BASE_DIR="$HOME/projects"  # Change this path as needed

# Go to base directory
cd "$BASE_DIR" || exit

# Loop through each subdirectory
for dir in */; do
    echo "========================================"
    echo "Checking project: $dir"
    cd "$BASE_DIR/$dir" || continue

    if [ -d ".git" ]; then
        # Get current branch name
        current_branch=$(git symbolic-ref --short HEAD 2>/dev/null)

        echo "-> On branch: $current_branch"
        echo "-> Fetching..."
        git fetch --all

        echo "-> Pulling latest changes..."
        git pull origin "$current_branch"
    else
        echo "⚠️  Skipping '$dir' — not a git repo."
    fi

    echo "========================================"
    echo
done
```

---

## 🧪 How to Use

1. **Save the script** as `git-pull-all.sh`.
2. **Make it executable**:
   ```bash
   chmod +x git-pull-all.sh
   ```
3. **Run it**:
   ```bash
   ./git-pull-all.sh
   ```

---

## 🧠 How It Works – Line-by-Line

| Line | What It Does |
|------|--------------|
| `BASE_DIR=...` | Sets the directory where all your Git repos live. Change this as needed. |
| `cd "$BASE_DIR"` | Navigates to the base directory. |
| `for dir in */;` | Loops over each subdirectory (assumed to be a Git repo). |
| `cd "$BASE_DIR/$dir"` | Moves into each project folder. |
| `if [ -d ".git" ]; then` | Checks if it's actually a Git repo. |
| `git symbolic-ref --short HEAD` | Gets the name of the current branch (e.g., `main`, `develop`). |
| `git fetch --all` | Updates the repo with the latest info from the remote. |
| `git pull origin "$current_branch"` | Pulls the latest commits into the current branch. |
| `else ...` | Skips non-Git folders. |

---

## 💡 Tip

If you want to update **all branches** instead of just the current one, let me know — I can help expand the script to handle that too.
