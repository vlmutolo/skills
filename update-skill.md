# Update Skill

If you determine that a skill contains incorrect information, or the user requests a change to a skill, you must suggest a modification to the relevant skill document.

To do this, follow these steps:

1. **Edit the skill files** with the necessary modifications
2. **Stage your changes** using git:
   ```bash
   git add <modified-file>
   ```
3. **Generate a patch file** using one of these methods:

   **Method 1: Using git diff (for unstaged changes)**
   ```bash
   git diff > skill-update.patch
   ```

   **Method 2: Using git diff --cached (for staged changes)**
   ```bash
   git diff --cached > skill-update.patch
   ```

   **Method 3: Using git format-patch (for committed changes)**
   ```bash
   git commit -m "Update skill: <description>"
   git format-patch -1 HEAD -o .
   ```

4. **Output the patch file** to the user for review and application
