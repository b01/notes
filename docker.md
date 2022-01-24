# Docker Notes

## Docker uninstall Fix

Man, Docker REALLY gets jammed up on Windows sometimes. This is all I can do before I have to wipe windows and restore.

1. Stop all Docker services
2. Disable the startup service in task manager
3. Disable Hyper-V
4. Restart Windows
5. In Powershell (Admin): & "C:\Program Files\Docker\Docker\Docker Desktop Installer.exe" uninstall
    1. OR Manually
       ```
       Remove-Item -Recurse -Force "~/AppData/Local/Docker"
       Remove-Item -Recurse -Force "~/AppData/Local/Docker Desktop Installer"
       Remove-Item -Recurse -Force "~/AppData/Roaming/Docker Desktop"
       Remove-Item -Recurse -Force "C:\ProgramData\Docker"
       Remove-Item -Recurse -Force "C:\ProgramData\DockerDesktop"
       Remove-Item -Recurse -Force "C:\Program Files\Docker"
 
       Remove-Item -Force "C:\Users\Public\Desktop
       Registry 
       Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\Docker Desktop
       wsl --unregister docker-desktop
       wsl --unregister docker-desktop-data
       ```
6. Reinstall Docker Desktop
7. Restart Windows
8. Update Docker Desktop

C:\Users\kshabazz\src\git.rockfin.com\kshabazz\work\applications


## Add A Health Check to A Docker Container

Here's a good example of doing a `HEALTHCHECK` to a container so that it can ship properly.
It doesn't have to be a website, any command that your capp can process will work. You can even
replace this with a *.sh script.

```dockerfile

# This endpoint can do checks like test it can the database, which would a nice healthcheck.
# Any script or cammdn will work as long as it exit code is 0 or any small int.
HEALTHCHECK --interval=15m --timeout=3s --start-period=20s CMD curl -kfI http://example.com/status.php || exit 1
```