# Processing command line interface
You might want to use Processing from its command line interface for several reasons, including:
- running a sketch at startup or from a script
- passing arguments when running a sketch

## Installation
1. Install and open the Processing software
1. MacOS users only: under **Tools**, click `Install "processing-java"`

## Usage
``` shell
# Show help file
processing-java --help
```

#### Basic example
``` shell
# Be careful to write the path to the sketch folder, not to the .pde file
processing-java --sketch=/absolute/path/to/sketchfolder --run
```

#### Run a sketch at startup on a Raspberry Pi
There are a lot of different ways to autostart a program on a Unix-like environment. This one waits for the desktop environment to be ready before runnning the command.
1. Create a **.desktop** file in the `~/.config/autostart` directory
``` shell
mkdir ~/.config/autostart
nano ~/.config/autostart/sketch.desktop
```
1. Paste the following text and edit the `Name` and `Exec` entries with your own name/path (blank spaces are not allowed).
```
[Desktop Entry]
Type=Application
Name=processingSketch
Exec=processing-java --sketch=/absolute/path/to/sketchfolder --run
```
1. Hit `ctrl-x`, `Y`, and `Enter` to save and quit nano

You might want your sketch to run in fullscreen mode, and to prevent the cursor from appearing. You can modify your Processing sketch with these two functions :

``` java
setup() {
  // Replaces the size() function.
  fullScreen();

  // Prevents cursor from showing
  noCursor();
}
```

If you want to prevent the Raspberry Pi from sleeping:

1. Open the `lightdm` configuration file (you may need to enter your password)
``` shell
sudo nano /etc/lightdm/lightdm.conf
```
1. Uncomment the `#xserver-command=X` line under the `[Seat:*]` section and modify it exactly as follows:
```
xserver-command=X -s 0 dpms
```
1. Hit `ctrl-x`, `Y`, and `Enter` to save and quit nano

A simpler way of preventing the Raspberry Pi would be to install the `xscreensaver` application. It provides an easy to use interface for configuring the screensaver, along with an option to disable it.

``` shell
sudo apt-get install xscreensaver
```

From the main desktop menu, under the `Preference` tab, you can click on `screensaver` and choose `disable`.
