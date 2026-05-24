@echo off
echo Opening RecruiterOS Dashboard...
echo.

:: Get the folder where this bat file is located
set FOLDER=%~dp0
set FILE=%FOLDER%index.html

:: Try Chrome in common locations
set CHROME1="C:\Program Files\Google\Chrome\Application\chrome.exe"
set CHROME2="C:\Program Files (x86)\Google\Chrome\Application\chrome.exe"
set CHROME3="%LOCALAPPDATA%\Google\Chrome\Application\chrome.exe"

if exist %CHROME1% (
    %CHROME1% --disable-web-security --user-data-dir="%TEMP%\recruiter-dashboard" --allow-file-access-from-files "%FILE%"
    goto end
)
if exist %CHROME2% (
    %CHROME2% --disable-web-security --user-data-dir="%TEMP%\recruiter-dashboard" --allow-file-access-from-files "%FILE%"
    goto end
)
if exist %CHROME3% (
    %CHROME3% --disable-web-security --user-data-dir="%TEMP%\recruiter-dashboard" --allow-file-access-from-files "%FILE%"
    goto end
)

echo Chrome not found in default location.
echo.
echo Please do this manually:
echo 1. Press Windows key + R
echo 2. Type: chrome --disable-web-security --user-data-dir=%%TEMP%%\rdash
echo 3. Press Enter
echo 4. In the Chrome window that opens, press Ctrl+O and select index.html
echo.
pause
:end
