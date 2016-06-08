# Thinkpad X1 Windows 10 Middle Mouse Button Issue

The middle mouse button on Thinkpads can be used together with the TrackPointer to scroll windows without having to move the pointer to the scrollbar.  This is a feature that has worked on Thinkpads with MS Windows for several years.

## Issue

Unfortunately, this feature clashes with Windows 10 Cortana on my fresh Thinkpad X1 Carbon (2016).  Scrolling does work as previously, but it also triggers the big Cortana search window/panel to pop up.  More precisely, Cortana pops up as soon as you press the middle mouse button.  I made a brief [Youtube screencast](https://www.youtube.com/watch?v=6OrSnRtoT6w) illustrating the problem.  Others [report the same problem](https://forums.lenovo.com/t5/forums/searchpage/tab/message?q=thinkpad+x1+middle+button+cortana+opens), e.g. [Thinkpad X1](https://forums.lenovo.com/t5/ThinkPad-X-Series-Laptops/X1-middle-button-keeps-opening-Cortana-diver-updated-disabled/m-p/3322230/highlight/true#M69979), [Thinkpad X260](https://forums.lenovo.com/t5/ThinkPad-X-Series-Laptops/x260-ultranav-middle-button-opens-Cortana/m-p/3322349), [Thinkpad T460s](https://forums.lenovo.com/t5/ThinkPad-T400-T500-and-newer-T/T460s-Middle-button-keeps-opening-Cortana/m-p/3314561/highlight/true#M108863).


## Workarounds

### Workaround \#1 - Disable Win + \<key\>
It turns out that the middle mouse button on Thinkpads [generates the equivalent key presses](http://delphiforfun.org/programs/utilities/KeyCodes.htm#Download) as `Win + S`, which is also the sequence that opens Cortana on Windows 10.  Fortunately, it is possible to [disable the `Win` in Explorer](http://www.isumsoft.com/it/disable-win-keyboard-shortcuts-in-windows-10/), but making a single edit to the Windows Registry.  I created two Windows Registry files that disables and enables (to undo the fix) for this:

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
* ...?

Since it's not clear to me what other problems there are by uninstalling Cortana, I personally prefer the `Win+<key>` workaround.
