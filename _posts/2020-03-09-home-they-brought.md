---
layout: post
title: Running Doom on OSX 
---

**Note:** This may have been fixed, but if not, this worked for me: 

Requires: [Odamex](https://odamex.net/) (and doom)

MacOS has this "feature" where it sandboxes applications if things aren't done in a very particular way. It's called app translocation. For most applications it doesn't affect their behavior or your ability to use them. Because of the way our applications interact it causes serious issues.
If you are comfortable with typing commands into the terminal you can "untranslocate" the application.

1. Open your terminal and `cd /Applications/Odamex`
2. Run the command `xattr odalaunch.app`
3. Run this command `xattr -d com.apple.quarantine odalaunch.app` if needed.  Do the same for odamex.app and odasrv.
4. Then delete the file `~/Library/Preferences/odalaunch\ Preferences`

If you do that and you have your wads in the Odamex directory, should be able to start odalaunch and hit the yellow odamex button.
