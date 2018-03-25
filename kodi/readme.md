
# Netflix Controller (Kodi 17)
Until such time that [Netflix works natively in Kodi](https://github.com/asciidisco/plugin.video.netflix)
use [NetflixRemoteController](http://sticky-ux.com/apps/NetflixRemoteController/docs.html)

Update and set any key mappings for closing netflix
  * [Close NetflixRemoteController](http://www.avsforum.com/forum/26-home-theater-computers/2133042-new-tool-netflix-remote-controller-10.html#post48503225)
  * [Keymappings](https://autohotkey.com/docs/KeyList.htm#Mouse)

[Create a link from Kodi](http://www.multibootpi.com/info/how-to-add-a-custom-shortcut-in-kodi/)

# Netflix (Kodi 18)
Follow the [instructions here](https://github.com/asciidisco/plugin.video.netflix)
but bear in mind that you need an alpha version of kodi. You can find the [more
stable dev builds here](http://mirrors.kodi.tv/snapshots/). It seems that the
InputStream.Adaptive plugin needs to be manually enabled.

`Add ons > My add ons > Video Player InputStream > InputStream Adptive > enable`

Now install and enable the Netflix plugin.

# Windows losing size with monitor recycle

[Best description of the problem](https://forum.kodi.tv/showthread.php?tid=213851)
but also [here](https://forum.kodi.tv/showthread.php?tid=158432) and
[here](http://www.overclock.net/t/1235582/dealing-with-displayport-hdmi-autodetect) and
[here](https://forum.kodi.tv/showthread.php?tid=172616)

There are a lot of suggested solutions:

  1. [Registry](http://rcaloca.blogspot.co.uk/2014/12/windows-changing-size-position-after.html) - `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\GraphicsDrivers\Configuration\`
  1. USB Power settings
  1. HDMI Pin 18
  1. [Remote with VNC](https://forum.kodi.tv/showthread.php?tid=172616&pid=1500888#pid1500888)
  1. Software
    * Launcher4Kodi
    * Persistent Windows
    * [RestoreWindows](https://github.com/sbs20/RestoreWindows) (please note
      this is an updated version to solve an additional windows problem)

The only thing that worked for me was RestoreWindows (although I didn't actually try Persistent Windows).

Specifically:

  1. If using Launcher4Kodi - use Windows Explorer as the shell
  1. Put RestoreWindows (or a shortcut) in the Startup folder (`win-r` then `shell:startup`)
  1. Use Display Mode: Full Screen, set correct resolution and "Use fullscreen window" = True
