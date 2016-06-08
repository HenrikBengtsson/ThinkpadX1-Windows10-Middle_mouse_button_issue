# Thinkpad X1 Windows 10 Middle Mouse Button Issue

The middle mouse button on Thinkpads can be used together with the TrackPointer to scroll windows without having to move the pointer to the scrollbar.  This is an awesome feature that has worked on Thinkpads with MS Windows for several years.

## Issue

Unfortunately, this feature clashes with Windows 10 Cortana on my fresh Thinkpad X1 Carbon (2016).  Scrolling does work as previously, but it also triggers the big Cortana search window/panel to pop up, which renders the system nearly useless to anyone used to middle mouse button scrolling.  More precisely, Cortana pops up as soon as you press the middle mouse button.  I made a brief [Youtube screencast](https://www.youtube.com/watch?v=6OrSnRtoT6w) illustrating the extremely annoying problem.  Others [report the same problem](https://forums.lenovo.com/t5/forums/searchpage/tab/message?q=thinkpad+x1+middle+button+cortana+opens), e.g. [Thinkpad X1](https://forums.lenovo.com/t5/ThinkPad-X-Series-Laptops/X1-middle-button-keeps-opening-Cortana-diver-updated-disabled/m-p/3322230/highlight/true#M69979), [Thinkpad X260](https://forums.lenovo.com/t5/ThinkPad-X-Series-Laptops/x260-ultranav-middle-button-opens-Cortana/m-p/3322349), [Thinkpad T460s](https://forums.lenovo.com/t5/ThinkPad-T400-T500-and-newer-T/T460s-Middle-button-keeps-opening-Cortana/m-p/3314561/highlight/true#M108863).


## Workarounds

### Workaround \#1 - Disable Win + \<key\>
It turns out that the middle mouse button on Thinkpads sgenerates the equivalent key presses as `Win + S`, which is also the sequence that opens Cortana on Windows 10.  Fortunately, it is possible to [disable the `Win` in Explorer](http://www.isumsoft.com/it/disable-win-keyboard-shortcuts-in-windows-10/), but making a single edit to the Windows Registry.  I created two Windows Registry files that disables and enables (to undo the fix) for this:s

* [Windows10-WinKey-disable.reg](https://raw.githubusercontent.com/HenrikBengtsson/ThinkpadX1-Windows10-Middle_mouse_button_issue/master/Windows10-WinKey-disable.reg?token=ABir0tylzqjty1TrRaEdStljO-9qDMciks5XYQi1wA%3D%3D) - right click and save with extension *.reg and doubleclick to apply fix.
* [Windows10-WinKey-enable.reg](https://raw.githubusercontent.com/HenrikBengtsson/ThinkpadX1-Windows10-Middle_mouse_button_issue/master/Windows10-WinKey-enable.reg?token=ABir0r7Kx-giYAzz7MvFDaE6GDepBGH_ks5XYQlFwA%3D%3D) - undo fix.

Know problems with this fix:
* Pressing the middle mouse button while the cursor is over a text field / in an editor, will cause a (lower case) `s` to be typed.
* All `Win + <key>` actions are suppressed in Windows, e.g. `Win + D` will no longer open the Desktop.


### Workaround \#2 - Uninstall / Disable Cortana
By disabling Cortana will avoid the problem while scrolling with TrackPoint and middle mouse button will still work.  Unforturtunately, it is not fully straightforward to disable Cortana.  The best I could find was [to uninstall Cortana or to make Windows not find it](https://superuser.com/questions/949569/can-i-completely-disable-cortana-on-windows-10).

Know problems with this fix:
* Windows logins using a Microsoft account no longer works.
* Windows Store won't work.
* Breaks the Windows 10 Start Menu and probably Search. Note: [Classic Shell](http://www.classicshell.net/) provides a very nice alternative Start Menu with Search.
* ...?

Since it's not clear to me what other problems there are by uninstalling Cortana, I personally prefer the `Win+<key>` workaround.


## Not a Workaround / Fix
Lenovo has released Synaptics ThinkPad UltraNav Driver 19.0.17.77 (2016-03-04) which [claims](https://download.lenovo.com/pccbbs/mobiles/n1cgx21w.txt) to "Fixed an issue where middle button click opened Cortana".  Importantly, this also causes scrolling using the middle mouse bottom to no longer work as [reported by several](https://forums.lenovo.com/t5/ThinkPad-T400-T500-and-newer-T/T460s-Middle-button-keeps-opening-Cortana/m-p/3314561/highlight/true#M108863).  I have tried this, but it makes sense given that the middle mouse button generates key code sequence `Win + S` - it sounds like Lenovo has simply disabled the middle mouse button completely.  Could someone please confirm this by checking with [KeyCodes](http://delphiforfun.org/programs/utilities/KeyCodes.htm#Download) (see below).


## Troubleshooting
Using the [KeyCodes](http://delphiforfun.org/programs/utilities/KeyCodes.htm#Download) software, I found that when I click the middle mouse button on my Thinkpad X1 Carbon (2016) the following key code sequence is generated:

1. OnKeyDown Key code=91, Control keys=, Key name Left Windows key (MS Natural Kb)
2. OnKeyDown Key code=83, Control keys=, Key name s
3. OnKeyPress s
4. OnKeyUp Key code=83, Control keys=, Key name s
5. OnKeyUp Key code=91, Control keys=, Key name Left Windows key (MS Natural Kb)

This is seen when the `Win+<key>` feature is disabled in Windows (the above workaround).  Without the workaround, we will only see:

1. OnKeyDown Key code=91, Control keys=, Key name Left Windows key (MS Natural Kb)
2. OnKeyUp Key code=83, Control keys=, Key name s
3. OnKeyUp Key code=91, Control keys=, Key name Left Windows key (MS Natural Kb)

which is probably because the Explorer grabs the other two (and opens Cortana).

I observed this with Windows 10 Pro (x64) with Synaptics ThinkPad UltraNav Driver 19.0.17.43 (2015-11-19).
