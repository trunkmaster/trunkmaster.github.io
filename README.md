# ![Logo](NEXTSPACE.png) NEXTSPACE News

### 21.01.2019
Last month I've spent for exercises with Linux audio subsystems. Namely ALSA and PulseAudio. For that reason I've 
created a application Mixer inside Frameworks/Tests. There some results:
* I have fully working ALSA mixer (thanks to [@alexmyczko](https://github.com/alexmyczko) for his [VolumeControl.app](https://github.com/alexmyczko/VolumeControl.app) - that was a starting point for me).
* ALSA and PulseAudio events handling implemented in separate GCD thread for both subsystems.
* PulseAudio looks like more preferred method of sound card settings tweaking:
    * I can easily determine default input and output. This is important for "Sound Preferences" panel where only 2 
    simple controls provided by design.
    * I can switch input and output on per application basis.
    * It will be possible to add comprehensive sound routing management in future "Sound Mixer". 
* NextSpace needs separate application - "Sound Mixer" - to perform more complex sound settings edidting (switching 
outputs, selecting input device for sound capturing, etc.)

I need to finish PulseAudio code inside Mixer. Next is create NXSound implementation that can manage ALSA and PulseAudio
with one set of methods.

Here are some screenshts of Mixer:

![ALSA Mixer](ALSAMixer-1.png) ![ALSA Mixer](ALSAMixer-2.png) ![ALSA Mixer](ALSAMixer-3.png)

![PulseAudio Mixer](PAMixer.png) 

### 24.12.2018

I guess now I've fixed most of the focus switch issues. Moreover, now GNUstep GUI backend correctly process "Hide" and
"Minimize Window" operations with respect to WM application state information. "Hide" sends message to WM. WM draws 
animation of hiding application and mark application windows as hidden. This is very important to have GNUstep and WM 
vision synchronized.

> For the record - there are several methods of performing such operations:
> * Hide - Cmd-h shortcut, right-click on Miniaturize window titlebar button, "Hide" right-click menu on appicon (for 
> X11 applications only).
> * Miniaturize Window - Cmd-m, left-click on Miniaturize titlebar button
> For GNUstep applications these operations are handled differently then to X11 applications.

Now I'm developing inside NEXTSPACE environment. I suppose that more bugs will be revealed. However I'm switching to 
other project tasks (Preferences, Terminal). 

### 13.12.2018

Fixes, fixes, fixes... to focus management again. 

Last couple of days I've tested focus management with IntelliJ IDEA.
This application has interesting startup sequence from focus management point of view. Now WM became more mature in 
handling such applications. 

### 11.12.2018

I've finished documenting some aspect of focus management. Although extensive testing, fixing and polishing are ahead.
Because of frequent crashes and logouts/logins, I make development inside VM. 
Once I'll be happy with focus management feature, I move to real hardware. That's where I can deal with sound, power, 
networking.

### 08.12.2018

It seems that I've completed focus management task.
Additinally I've managed to fix misterious unmap/map of appicon on double-click.

Next: I need to document all changes and describe concepts of focus management related things.

### 06.12.2018

Several major changes in focus management task:
1. GNUstep GUI backend activate application if TakeFocus message was received
   from WM.
2. When GNUstep application deactivates main menu left managed by WM now. Considering
   change to GNUstep GUI backend, main menu can now be used to activate GNUstep application
   with WM's wSetFocusTo() without direct calling of `[NSApp activateIgnoringOtherApps:]` (it's
   implemented in XWActivateApplication).
3. Cmd-Tab (Switch Panel) now creates list of applications (not windows). Switch to application
   that was openened on particular workspace switches to that workspace.
   
Next: double-click on appicon should switch to workspace where app was opened.

### 04.12.2018

Latest update to CentOS 7.6.1810 brings some big changes. What I noticed is:
- freetype library upgrade from vaersion 2.4 to 2.8. freetype 2.8 introduced new 
  version of TrueType interpreter - v40. As a result non-aliased hinted fonts 
  looks ugly. Perhaps new interpreter has broken font hints processing.
  Although antialiasing works much better - antialiased fonts looks good with 
  `hintslight` setting of `hintstyle` parameter of fontconfig (or Xft.hintstyle).
  Return to old version of interpreter is possible if you set environment 
  variable `FREETYPE_PROPERTIES` like this:
  `export FREETYPE_PROPERTIES="truetype:interpreter-version=35"`
- new kernel update 3.10.0-957 brings problem of bulding VirtualBox video driver
  for guest CentOS system. VirtualBox development build 5.2.23 fixes this.

### 23.11.2018

Last 2 weeks I was trying to marry GNUstep GUI backend focus management with WM's.
It's quite hard task... But now I know how focus management works in GNUstep and X11.
Next [Workspace project](https://github.com/trunkmaster/nextspace/projects/4) 
tasks probably require more deep integration between GNUstep and WM.
