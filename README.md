# SPACEMACS Windows(11) tutorial
This is a SPACEMACS Windows(11) Installation tutorial.

## Introduction
I want to point out that Windows (especially 11) isn't really well optimised for something like Spacemacs,
so problems and errors will likely occur, some of which I'll cover in this tutorial.
I already had Spacemacs on my Linux laptop for a bit, so I decided to try to install it on Windows 11 but didn't find any tutorials.
That's why I'm creating this repo.
Feel free to point out my mistakes.

## Installation
Spacemacs is an addition for Emacs, so you will have to install it first.

**Go to this link:**
[https://ftp.fau.de/gnu/emacs/windows/](https://ftp.fau.de/gnu/emacs/windows/)

Open an `emacs-30/` folder and install Emacs via `.exe` or `.zip`.

**After you successfully installed Emacs, it's time to install SPACEMACS.**

via cmd:
```cmd
git clone https://github.com/syl20bnr/spacemacs %APPDATA%\.emacs.d
```

via powershell:
```powershell
git clone https://github.com/syl20bnr/spacemacs $env:APPDATA\.emacs.d
```

After installing Spacemacs, reopen Emacs and wait until Spacemacs downloads all packages...

**If everything went smooth (which is unlikely), you can skip to the next part of this tutorial.**

Now, the most important part:

**If you get error messages like this:**
```
An error occurred while installing helm-swoop 
(error: (error Failed to checkout 'helm-swoop': 'Creating pipe: Too many open files'))
```

  **1. Edit your .spacemacs config file:**

  Open the `.spacemacs` file with any text editor (I will use notepad)

  via cmd:
```cmd
  notepad %APPDATA%\.spacemacs
```
  via powershell:
```powershell
  notepad $env:APPDATA\.spacemacs
```

  Now either add:
```elisp
  (setq straight-vc-git-default-clone-depth 1)
  (setq package-install-upgrade-built-in t)
```
  in the `dotspacemacs/user-init` section at the end of this file.
  These lines limit the number of simultaneous pipes.

  Or replace `.spacemacs` with the one I left in this repo that already has some basic features configured.

  *(don't forget to save)*

  **2. Press:**
```
  M-x
```

- **3. Enter:**
```
  package-install
```

- **4. Enter 1-3 packages that caused errors**

  In my case:
```
  helm-swoop
```
  Then restart Emacs.

---

## Other Common Windows errors

### Cyrillic or spaces in username path
If your Windows username contains non-latin characters or spaces (e.g. `C:\Users\Пользователь\`), Emacs may fail to find config files or install packages.

**Fix:** Add a `HOME` environment variable pointing to a safe path:
1. Search "Environment Variables" in Windows search
2. Add new user variable: `HOME` = `C:\emacs-home` (or any path without spaces/cyrillic)
3. Copy your `.spacemacs` there and restart Emacs

---

### Shell layer not working (`/bin/bash` not found)
Spacemacs default shell config uses `/bin/bash` which doesn't exist on Windows natively.

**Fix:** In `.spacemacs` set shell to Git bash or eshell:
```elisp
(shell :variables
       shell-default-shell 'eshell)
```
Or if you have Git for Windows:
```elisp
shell-default-term-shell "C:/Program Files/Git/bin/bash.exe"
```

---

### Slow startup / freezing on startup
Windows Defender scanning every file Emacs loads causes this.

**Fix:** Add Emacs and its config folder to Windows Defender exclusions:
1. Open Windows Security -> Virus & threat protection -> Exclusions
2. Add folders: `C:\Program Files\Emacs` and `%APPDATA%\.emacs.d`

---

### Font not found warning
Spacemacs default font `Source Code Pro` is not installed on Windows by default.

**Fix:** Either install Source Code Pro from [fonts.google.com](https://fonts.google.com/specimen/Source+Code+Pro) or change the font in `.spacemacs`:
```elisp
dotspacemacs-default-font '("JetBrains Mono"
                             :size 14.0
                             :weight normal
                             :width normal)
```
JetBrains Mono is free and available at [jetbrains.com/mono](https://www.jetbrains.com/mono/)

---

## Final notes

Spacemacs on Windows will never be as smooth as on Linux, but it's definitely usable once the initial setup is done.
If you run into issues not covered here, check the official Spacemacs FAQ at [github.com/syl20bnr/spacemacs](https://github.com/syl20bnr/spacemacs) or open an issue in this repo.

*feel free to use my ".spacemacs" file that has all usefull presets*

I'm happy if I was able to help you.
Good luck!
