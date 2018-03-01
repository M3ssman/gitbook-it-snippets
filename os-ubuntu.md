# Ubuntu

### Create Launcher for external Applications

Files in  
/usr/local/share or \(as overwrite usr local defaults?\) in ~/.local/share/applications

eclipse.desktop

```
[Desktop Entry]
Version=1.b
Terminal=false
Name=EclipseOxygenEE
Exec="/opt/eclipse-oxygen/eclipse"
Icon=/opt/eclipse-oxygen/icon.xpm
Categories=Development;IDE;
Type=Application
```

intellij.desktop

```
[Desktop Entry]
Version=1.0
Type=Application
Name=IntelliJ Community Edition 2016.3
Icon=/opt/idea-IC-163.7743.44/bin/idea.png
Exec="/opt/idea-IC-163.7743.44/bin/idea.sh" %f
Comment=Develop with pleasure!
Categories=Development;IDE;
Terminal=false
StartupWMClass=jetbrains-idea
```

* make files executable ?

### Conky

* [http://www.linuxandubuntu.com/home/what-is-conky-and-how-to-configure-conky-on-ubuntu-1604](http://www.linuxandubuntu.com/home/what-is-conky-and-how-to-configure-conky-on-ubuntu-1604)
* sudo apt-get install conky-all

Conky-Manager \(optional\)

```
$ sudo apt-add-repository -y ppa:teejee2008/ppa
$ sudo apt-get update
$ sudo apt-get install conky-manager
```

#### Conky Autostart

* see 
  * https://www.lifewire.com/beginners-guide-to-conky-4043352
  * https://www.linux.com/learn/how-install-and-configure-conky
* create shellscript that starts conky in ~ Folder
* add desktop entry to ~/.config/autostart \(or open "Startprogramme", select script\)
  ```
  [Desktop Entry]
  Type=Application
  Exec="~/.conkystartup.sh"
  Hidden=false
  NoDisplay=false
  X-GNOME-Autostart-enabled=true
  Comment=AutoStart for Conky
  ```

### Launcher Position

* [http://ubuntuhandbook.org/index.php/2016/03/ubuntu-16-04-move-unity-launcher-to-bottom/](http://ubuntuhandbook.org/index.php/2016/03/ubuntu-16-04-move-unity-launcher-to-bottom/)

```
gsettings set com.canonical.Unity.Launcher launcher-position Bottom
```



