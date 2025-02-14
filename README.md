# 🧾 Windows-terminal-context-menu 

![](https://raw.githubusercontent.com/kerol2r20/Windows-terminal-context-menu/master/Preview.png)

Inspired from Windows terminal issue [Add "open Windows terminal here" into right-click context menu #1060](https://github.com/microsoft/terminal/issues/1060). Thanks to you all giants ❤

Windows terminal is an excellent terminal. But it does not offer a basic function which is **right click context menu**!  
Without it, I have to `cd` to my working directory everytime. It's inefficient.  

So I wrote this script to deal with it.

# Feature
* Two layers of context menu
* Auto parse settings.json to contruct menu
* With uninstaller

# Todo
- [x] Custom icon for profile

# Install
1. Clone this repo
`git clone https://github.com/kerol2r20/Windows-terminal-context-menu`

2. Run powershell (no need to get admin access right)
3. Change the execution policy `Set-ExecutionPolicy Unrestricted -scope CurrentUser`
4. Run `SetupContextMenu.ps1` script

⚠️ If you find no item in your context menu, it may be caused by the old style profiles.json. You can delete `%LocalAppData%\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\LocalState\profiles.json` and restart Windows terminal. The new one will be generated. Ref to [microsoft/terminal#4556](https://github.com/microsoft/terminal/pull/4556) 

# Uninstall
1. Run `SetupContextMenu.ps1 -uninstall:$true`

# Config
This script will parse the `settings.json` file to generate menu items. However you can customize it.  
You can also specify a custom path for the JSON via a `customJsonPath` entry.  
Put any icon file into `icon` folder and modify the `config.json` like the following.

```json
{
    "global": {
        "extended": false
    },
    "profiles": {
        "{a5a97cb8-8961-5535-816d-772efe0c6a3f}": {
            "icon": "arch.ico",
            "label": "Arch Linux"
        },
        "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}": {
            "showRunAs": true
        },
        "{b453ae62-4e3d-5e58-b989-0a998ec441b8}": {
            "hidden": true
        }
    }
}
```

**Config reference**
- global
  - extended[bool]: if set this to true, context menu will only show up when right click with `shift`
- profiles
  - guid[string]: this GUID of your profile defined in `settings.json`
    - hidden[bool]: overwrites the visibility of the profile, if defined
    - icon[string]: filename of your ico file, **you must put this file in icon folder**
    - label[string]: context menu label
    - showRunAs[bool]: add `run as administrator` item for this profile

# Misc
I'm not sure that icons file are legal or not. If you feel it is not ok, please tell me. Thanks.
