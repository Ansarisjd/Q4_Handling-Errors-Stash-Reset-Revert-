# Handling Errors (Stash, Reset, Revert)

## Objective
Learn how to manage mistakes, unfinished work, and safely undo changes using Git commands like stash, reset, and revert.

---

# Step 1: Make Changes to `app.py` but DO NOT Commit

Open `app.py` and add some temporary code.

Example:

```python
print("Work in progress feature")
```

Check file status:

```bash
git status
```

Expected output:

```bash
modified: app.py
```

---

# Step 2: Stash the Changes (Including Untracked Files)

If you also created new files, stash everything using:

```bash
git stash -u
```

## Explanation

- `-u` = include untracked files

Example output:

```bash
Saved working directory and index state WIP on master
```

---

# Step 3: Check the Stash List

```bash
git stash list
```

Example output:

```bash
stash@{0}: WIP on master
```

---

# Step 4: Apply the Stashed Changes Back

```bash
git stash apply
```

Now verify restored changes:

```bash
git status
```

You should see modified files restored.

---

# Step 5: Commit the Changes

Stage files:

```bash
git add .
```

Commit the changes:

```bash
git commit -m "Added temporary feature changes"
```

---

# Step 6: Make Another Commit with Incorrect Code

Modify `app.py`.

Example incorrect code:

```python
print("Incorrect buggy code")
```

Stage and commit:

```bash
git add .
git commit -m "Added incorrect code"
```

---

# Step 7: Undo the Last Commit Using Reset

## Option 1 → Keep File Changes Staged

```bash
git reset --soft HEAD~1
```

### What it does:
- Removes the last commit
- Keeps changes staged

---

## Option 2 → Remove Commit and Unstage Changes

```bash
git reset --mixed HEAD~1
```

---

## Option 3 → Completely Remove Commit and Changes

⚠ Dangerous command:

```bash
git reset --hard HEAD~1
```

For practice, use:

```bash
git reset --soft HEAD~1
```

Verify history:

```bash
git log --oneline
```

---

# Step 8: Make Another Commit

Fix the code properly in `app.py`.

Example:

```python
print("Corrected feature implementation")
```

Stage and commit:

```bash
git add .
git commit -m "Added corrected implementation"
```

---

# Step 9: Undo a Commit Using Revert

Create a reversing commit:

```bash
git revert HEAD
```

Git opens an editor for the commit message.

Save and close the editor.

## What `git revert` does:
- Creates a NEW commit
- Safely reverses previous commit changes
- Keeps history intact

---

# Step 10: Verify Commit History

```bash
git log --oneline
```

Example output:

```bash
a1b2c3d Revert "Added corrected implementation"
x7y8z9 Added corrected implementation
p4q5r6 Added temporary feature changes
```

---

# Important Difference: Reset vs Revert

| Command | What It Does | Safe for Shared Repository? |
|----------|--------------|-----------------------------|
| `git reset` | Removes commits/history | ❌ No |
| `git revert` | Creates reversing commit | ✅ Yes |

---

# Full Command Flow

```bash
# Modify file only

git status

git stash -u

git stash list

git stash apply

git add .
git commit -m "Added temporary feature changes"

# Add incorrect code

git add .
git commit -m "Added incorrect code"

git reset --soft HEAD~1

# Fix code

git add .
git commit -m "Added corrected implementation"

git revert HEAD

git log --oneline
```

---

# Result

Successfully practiced:
- Stashing unfinished work
- Restoring stashed changes
- Undoing commits using reset
- Safely reversing commits using revert
- Managing Git commit history
