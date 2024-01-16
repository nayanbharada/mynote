@echo off
REM Wait for 4 hours (14400 seconds)
timeout /t 14400 /nobreak

REM Check if Chrome is running, and if so, close it
tasklist /fi "imagename eq chrome.exe" | find ":" > nul
if errorlevel 1 (
    REM Chrome is not running, open Chrome and your HTML file
    start chrome.exe "http://your-website.com"  # replace with your URL
) else (
    REM Chrome is running, close the existing browser
    taskkill /f /im chrome.exe
)

REM Add a delay before closing the batch file (optional)
timeout /t 5
