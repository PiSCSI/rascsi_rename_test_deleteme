# Introduction

If you're reading this, you may just have gotten your vintage computer online, through PiSCSI's [DaynaPORT adapter emulation](https://github.com/piscsi/piscsi/wiki/Dayna-Port-SCSI-Link), other any other means. And now you're asking yourself, what's next?

While a vintage computer is excellent for [telneting into a BBS](https://www.pcmag.com/news/7-modern-bbses-worth-calling-today) such as Level 29, or browsing websites made for vintage computers such as http://www.theoldnet.com or http://68k.news, the broader modern Web is an unforgiving place for a vintage computer and its equally vintage browsers. The sheet amount of data that they send to the user agent, javascript libraries thousands of lines long, massive images in exotic formats, multimedia, etc... It may take minutes to load a page, and minutes more to parse and reflow the DOM over and over, and you're lucky if it doesn't crash when running out of memory.

And the biggest practical hurdle: the move to enforcing encrypted https connections on a vast majority of sites (I blame Google for that) that even the last versions of classic Mac OS (or AmigaOS, Windows 98, etc.) aren't able to decrypt due to expired root certificates or other cryptographic limitations.

Vintage Web Proxy servers to the rescue! The Raspberry Pi that PiSCSI runs on is a versatile little device, and if it is not already overburdened by other software, it should be able to run a proxy server in parallel with PiSCSI. This page will cover a few options, tested in particular with older Macs.

# Macproxy

*Note:* As of PiSCSI 21.11.01, easyinstall.sh has an option to install Macproxy for you.

Despite the name, the use of Macproxy is not at all limited to Macs. It is a super light-weight proxy implemented as a Python script running a Flask app, which will translate https requests to http, and strip out the vast majority of linked contents such as style sheets and JavaScript, while suppressing inline scripts as well. It has support for binary file downloading, and will retain embedded images to be decoded by vintage browsers.

Macproxy is an excellent choice for any 68k Mac, or other retro computer of a similar vintage. But don't expect contents that rely on heavy scripting to work well.

The author has [forked Macproxy](https://github.com/rdmark/macproxy) and improved it to work with venv and Python3, more aggressive translation of https to http, adding support for embedded images and binary downloads, among other fixes.

To use it on your Raspberry Pi, clone the repository to your home folder, e.g.:

```
cd
git clone https://github.com/rdmark/macproxy.git
```

Then simply follow the instructions in the [README.md](https://github.com/rdmark/macproxy#readme) of that project to learn how to run the script stand-alone or as a systemd daemon.

By default, the proxy server will run on port 5000, so configure your vintage browser to use the Pi's ip address with port 5000 as http and https proxy. On Mac, depending on which browser you're using, you may have to install the stand-alone utility [Internet Config](https://macintoshgarden.org/apps/internet-config-202) to configure a proxy server.

On really old systems, such as 68000 Macs, it is recommended to turn off image loading in the browser altogether. Otherwise you'll have to contend with a ton of errors and slowdown as the software is struggling to deal with content it isn't able to handle.

# WebOne

[WebOne](https://github.com/atauenis/webone) is a full-featured proxy server implemented with .NET and is able to run on a Pi with Microsoft's .NET Core libraries for Linux. It translates https to http, and does pinpointed JavaScript injection and image file transcoding to deliver as close a modern web experience as possible on vintage systems.

It is a recommended solution for late-90s or early 2000s systems such as mid to late era Power Macs, or Windows 95/98 machines.

The author has tested and recommends the _0.11.1-noffmpeg_ release for ARM. By using the noffmpeg version, you avoid pulling in 500+ MB of audio and video libraries for multimedia transcoding to your Pi. See related [related discussion thread on vogons.org](https://www.vogons.org/viewtopic.php?p=1015179#p1015179).

Follow the [Linux installation](https://github.com/atauenis/webone/wiki/Linux-installation) instructions on that project's wiki to install and configure WebOne.

By default, WebOne will run on port 8080 which conflicts with the PiSCSI Web Interface. After installing the software, you'd want to edit `/etc/webone.conf` and change the `Port` line in the [Server] section to something like:

```
Port=8088
```

Then restart the WebOne service:

```
sudo systemctl restart webone
```