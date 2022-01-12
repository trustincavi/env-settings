# How to install Oh My Zsh on Windows & intergrate with VS Code

## On Windows 10 Education using Cygwin

- Download and install [Cygwin](https://www.cygwin.com/), make sure the installation location is **`C:\cygwin64`**
```bash
setup-x86_64.exe -q -P git,vim,curl,wget,zsh,chere,lynx
````
- Open Cygwin terminal, install Oh My Zsh
```bash
git clone https://github.com/ohmyzsh/ohmyzsh.git ~/.oh-my-zsh
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
```
- To set zsh as default shell, open and edit file `vi ~/.bashrc` by adding the following:
```
exec zsh
```
- [*Optional*] Add cygwin to right-click context menu. Open in `Administator mode`:
```bash
chere -i -t mintty -s bash
```
- Set Oh My Zsh as default shell in VS Code
Create a file named `Cygwin-ohmyzsh.bat` under folder `C:\cygwin64`:
```
@echo off
set CHERE_INVOKING=1
C:\cygwin64\bin\bash.exe --login -i
```
then
```bash
chmod +x Cygwin-ohmyzsh.bat
```
- In VS Code, open User's `settings.json`, add the following:
```json
"terminal.integrated.profiles.windows": {
    "Oh my zsh": {
        "path": "C:\\cygwin64\\Cygwin-ohmyzsh.bat",
        "args": []
    }
},
"terminal.integrated.defaultProfile.windows": "Oh my zsh",
```
- Reload VS Code.
- Edit `~/.zshrc`, add (or update) the followings:
```
ZSH_THEME="robbyrussell"
```
```
if [[ $TERM = dumb ]]; then
    unset zle_bracketed_paste
fi
```
-  Restart VS Code and done.

### Notes:

- Currently all the themes for Oh My Zsh on Windows 10 Education perform slowly, not recommended.
- Fonts for those themes are not working too.
- Recommend extensions:
  - Install Lynx (the same as apt-get on Linux) to install packages:
    ```
    lynx -source rawgit.com/transcode-open/apt-cyg/master/apt-cyg > apt-cyg
    install apt-cyg /bin
    ```