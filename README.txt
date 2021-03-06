See the screenshot.
Direct download of EXE is available: https://github.com/vxiiduu/SnippingToolEx

This Snipping Tool is from Windows 10 1507 (the RTM release). The SHA-256 hash
of the original SnippingTool.EXE is:

 fccf231e0e4437baba86f64752e13562c9a2aa2d699a8dae7fafc85b48da4aa8

Porting requires 3 hex edits: one to change the NT version from 10.0 to 6.0 in
order to trick Windows into running it, the second to bypass some licensing/
permission check that Microsoft put in, and the third to change the 0-second
delay in order to avoid an artifact of the context menu that shows up on Vista
and 7 under certain conditions. This is a bug which occurs on all versions of
Windows up to the latest version of Windows 10. So, Windows 10 users can now
gain a very minor benefit from this patch. See the included screenshot which
demonstrates the bug (zoom in on the middle of the image).

These instructions ONLY WORK FOR x64 Snipping Tool. If there is a big demand I
can also work out how to do it for the 32-bit Snipping Tool as well.

1. Obtain Windows 10 1507 RTM x64 ISO, open with 7-Zip, then open
   sources\install.wim with 7-zip
2. Go to Windows\system32 and drag SnippingTool.exe to desktop (or some other
   location)
3. Next to SnippingTool.exe, make a folder called "en-US" (or whatever your
   language code)
4. From your 7-zip window, go to Windows\system32\en-US (or whatever your
   language code) and drag SnippingTool.exe.mui into the "en-US" folder you
   made in step 3
5. Open SnippingTool.exe in HxD or some other hex editor
6. At offset 0x120, change "0A 00 00 00 0A 00 00 00 0A 00 00 00" to
   "06 00 00 00 06 00 00 00 06 00 00 00"
7. At offset 0x1D19C, change "40 55 41 54 41 55" to "B8 01 00 00 00 C3"
8. At offset 0xF6B0, change "B8 FA 00 00 00" to "B8 2C 01 00 00"
9. Save file and exit hex editor

At this point, you can simply open the edited SnippingTool.exe and get the
Windows 10 snipping tool as pictured. You may also replace the Windows Vista/7
stock snipping tool with this one if you desire. 
For reference, the SHA-256
hash of the modified SnippingTool.exe is supposed to be:

  c60898fb4ea6984aaee1f2d3c9b73560bf0aaff64b9855e3d58e9855f3836433

FAQ:
"It runs but only displays an error box with no text!"
This is caused by incorrect MUI file, or incorrect placement of the MUI file.
As in picture, en-US folder should be next to SnippingTool.exe, and
SnippingTool.exe.mui should be inside that folder. And keep in mind, everywhere
I say "en-US", this means the language code used by your system. For example,
ja-JP or fr-FR for Japanese and French respectively.
