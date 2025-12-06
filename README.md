Windows Cleaner - WinForms

Minimal tool in C# (WinForms) to clean temporary user files and optionally the Recycle Bin.

Quick Use
- Open a PowerShell Terminal
- Place yourself in the project folder

"'
Dotnet Build
Dotnet Run
"'

Important Notes
Run the application as an administrator if you want to delete files from the System Temp folder.
- The "Dry Run" mode allows you to see actions without deleting.
The Recycle Bin dump uses the Windows API (P/Invoke). No confirmation is required if the option is enabled.

Additional Options
Chrome, Edge, Firefox cache cleanup (close browsers before running to avoid locked files).
- Cleaning the folder 'C:\Windows\SoftwareDistribution\Download' (requires administrator rights).
- Deleting thumbnail files ('thumbcache_*.db') to retrieve space.
- Cleaning the 'C:\Windows\Prefetch' folder (requires administrator rights).
- Flush DNS ('ipconfig /flushdns') to clear the local DNS cache.
Interface and logs
The app now offers a more professional interface with menu, progress bar and undo button.
Logs are saved in the 'logs\windows-cleaner.log' folder next to the executable.
You can export logs via 'File -> Export logs'.

Robustness and retresses
The application now performs attempts (retries) with backoff to delete files and folders that can be locked by other processes. She tries several times before giving up and logs each attempt.
- In 'Dry Run' mode deletions are not performed but are listed in the logs.

License (MIT)
----------------
This project is distributed under the MIT license. The full text of the license is included below and in the 'LICENSE' file at the root of the project.

MIT License

Copyright (c) 2025 c.lecomte.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
the Software without restriction, including the right to the right to create a free service.
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to the right persons to whom the Software is, the Software is, and to which the Software is, the software is, which is created.
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS," WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. In No Event Shall the
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
Software.

Author
------
'c.lecomte'

Limits
This tool is minimal and does not handle all cases (file lock, multiple profiles, deep cleaning). Use with caution.

License
No special license provided here; use at your own risk.
Developer Helper
----------------

A handy PowerShell script is included to apply the format, check the build, and prepare a group commit:

- 'scripts/prepare_commit.ps1'

Use:

" Powershell "
.\scripts\prepare_commit.ps1
"'

The script:
- Runs 'dotnet format' (if installed); otherwise offers installation.
- Runs 'dotnet build' to check that everything is compiling.
- Proposes to run 'git add -A' + 'git commit -m...' to group changes into a single commit.

Tip: Use this script before you push your changes to keep a clean history.