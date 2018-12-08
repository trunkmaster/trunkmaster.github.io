## ![Logo](NEXTSPACE.png) NEXTSPACE News

### 06.12.2018

Several major changes in focus management task:
1. GNUstep GUI backend activate application if TakeFocus message was received
   from WM.
2. When GNUstep application deactivates main menu left managed by WM now. Considering
   change to GNUstep GUI backend, main menu can now be used to activate GNUstep application
   with WM's wSetFocusTo() without direct calling of [NSApp activateIgnoringOtherApps:] (it's
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
