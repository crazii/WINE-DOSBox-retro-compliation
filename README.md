# WINE-DOSBox-retro-compilation

what it is: a collection of customization notes to improve the retro gaming experience for WINE and DOSBox  

what it is NOT: there might be guide to workaround problems. but it is not a step-by-step stup guide.

## Fluidsynth

fluidsynth (https://github.com/fluidsynth/fluidsynth) is a software synthesizer using SoundFont2,
it works for DOSBox and Wine. Some Linux distro include the package in the installation, you only need to add & enable a user service for it.  

For retro-gaming, the recommended SoundFont file is ``SC-55`` or ``Yamaha-XG`` sound font, those can be obtained online.

## CDEmu

CDEmu (https://github.com/cdemu/cdemu) is a a software suite designed to emulate an optical drive and disc (including CD-ROMs and DVD-ROMs) on the Linux operating system.

CDEmu works for WINE and also provide CD Music playing that can used by DOSBox.

For configuration, you can fllow the manual for CDEmu on unbuntu or Arch (e.g. https://manpages.ubuntu.com/manpages/stonking/man8/cdemu-daemon.8.html)  

NOTE: DOSBOX uses SDL1, modern distribution of SDL1 (sdl12_compat via SDL2) removes CDROM support. For DOSBox to work with CDEmu, you need to remove ``sd12_compat`` and install the original sdl package.

NOTE: CDEmu uses libao to play CD music, on some systems the default config of libao doesn't have music for CDEmu, you may need to comment out the ``dev=default`` line in ``/etc/libao.conf``. Here is a sample of libao.conf:

```
#default_driver=alsa #uncomment this line if you prefer alsa
default_driver=pulse
#dev=default
quiet
```


## WineVDM patch

The patch for WineVDM is to pass ``-t cdrom`` and ``usecd #n`` to DOSBox, so that the emulated CD-ROM by CDEmu can be directly usable by runing a MZ EXE via WINE.

## Look and Feel

### Themes

Chicago95 (https://github.com/grassmunk/chicago95) is a win9x theme for XFCE, recommended for a retro-gaming dedicated setup.

### Icons

icoextract (https://github.com/jlu5/icoextract) provide thumbnailers for PE exes.  
I added thumbnailers for ``.desktop`` files which is linked to a PE/MZ, and a simple tool ``exe-shortcut`` to create shortcut for MZ/PE.  You can add it to your filemanager. Examples for Thunar (XFCE):  

- Open a Thunar window
- Menu ``Edit`` => ``Config custom actions...``
- Add a new action by click the "PLUS" sign
- Set Name, e.g. "Create desktop shortcut (for EXE)", 
- Set command ``exe-shortcut %d/%n``
- Set optional hotkey shortcut and menu icon, and click OK

After thant you can right click an EXE (PE/MZ) and create a .desktop file for it, the file is placed on destktop.  
NOTE for MZ: exe-shortcut will first search the folder of the DOS MZ to find a valid ico to use for the .desktop, if not found an old "MS-DOS" icon will be used.


