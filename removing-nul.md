# 🗑️ The Mysterious NUL File Problem

> AI tools sometimes create `nul` files that you can't delete normally. Here's how to fix it!

---

## ❌ The Problem

Some AI tools (like Cursor, Copilot, etc.) accidentally create files named **`nul`**, which is a [reserved name in Windows](https://learn.microsoft.com/en-us/windows/win32/fileio/naming-a-file#naming-conventions). This makes them impossible to delete using normal methods like File Explorer or the standard `del` command.

You'll see error messages, but the file just won't budge!

## 🔀 Git Won't Push It

The good news? Git recognizes that `nul` is a reserved name and will **automatically ignore it**. Your repository is safe!

However, having it sit in your working directory is annoying and can clutter your `git status`.

## ✅ The Solution

Use **PowerShell running as Administrator** with this special command that uses the Windows UNC path syntax:

```powershell
cmd /c del /f /q "\\?\C:\YOUR-FOLDER\nul"
```

### Step by Step

1. Open **PowerShell as Administrator**
   *(right-click Start → Windows PowerShell (Admin))*
2. Replace `YOUR-FOLDER` with the actual path to your folder
3. Run the command and watch that stubborn file disappear! 🎉

### Example

```powershell
# If your project is in C:\Users\you\projects\my-app
cmd /c del /f /q "\\?\C:\Users\you\projects\my-app\nul"
```

## 🤔 Why This Works

The `\\?\` prefix tells Windows to **bypass normal path parsing** and access the file directly. This lets you target reserved names that would normally be blocked.

It's a special Windows feature designed for exactly these edge cases. Pretty neat!

### Other Reserved Names in Windows

For reference, these are all reserved names that can cause the same issue:

`CON` · `PRN` · `AUX` · `NUL` · `COM0–COM9` · `LPT0–LPT9`

---

## 📚 Further Reading

- [Microsoft Docs — Naming Files, Paths, and Namespaces](https://learn.microsoft.com/en-us/windows/win32/fileio/naming-a-file)

---

<p align="center">Created with ♥ by <a href="https://github.com/apsolut/">AP</a></p>