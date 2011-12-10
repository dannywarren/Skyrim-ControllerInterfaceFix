ControllerInterfaceFix

Allows you to remap controller buttons without breaking the interface menus

version:	1.00
author:		Danny Warren
email:		danny@dannywarren.com


--

ABOUT:

In the 1.2.12.0 patch, bethesda introduced a change to the way the control
mappings worked.

In the original release, the buttons you use to interact with the user
interface menus were hardcoded.  This allowed you to remap your in-game actions
(such as jump, sheath, interact, etc) while still leaving the user interface
buttons consistent (a is always accept, b is always cancel, etc).

Now, the mappings are set up such that changing the button used for an in-game
action will also swap the buttons used in the user interface menus.

Not only do the user interface buttons get swapped around, but several actions
in the menus stop working when remapped.  There are several cases where you are
unable to accept or cancel menus.  You must unplug your controller and take
over with the mouse or force quit skyrim.

This fix restores the hardcoded button mappings found in the original skyrim
release, allowing you to once again remap the in-game actions without breaking
the user interface menus.

I posted a quick fix for this in the bethesda forums when the 1.2.12.0 patch
came out.  Unfortunately, the same behavior is present in 1.3.7.0 as well so it
looks like bethesda is sticking with this behavior.  Might as well make the fix
official, too.

Please note that this fix does not change any of the keyboard mappings, it only
applies to the controller.  If there is interest in doing a similar fix for the
keyboard, please let me know.  I play with a controller so I have no idea which
new mapping tweaks work better and which would need restored to the original
release settings.


--

INSTALLING:

To install this mod, extract it to your skyrim data folder.

You should end up with:

  Data\Interface\controls\pc\controlmap.txt
  Data\ControllerInterfaceFix-Readme.txt

Since a lot of people who don't normally mod bethesda games have been applying
this fix and having trouble, please note that the data folder is *not* located
in the same location as your save games and configuration files.

It is located in the skyrim application directory, which on windows xp would
be found here:

  C:\Program Files\steam\steamapps\common\skyrim\Data

Also, please make sure that the above files are copied in to your data folder
instead of overwriting it.  Several people have had this issue, and I'm not
sure which archiver they are using that is doing this.


--

TROUBLESHOOTING:

Not really related to this mod, but handy if your controller configuration is
stuck or not behaving correctly.

The button mappings for skyrim are not stored in the configuration files, but
instead are located in a file called ControlMap_Custom.txt that lives in the
skyrim application directory.

So, on windows xp the file would be located here:

  C:\Program Files\steam\steamapps\ControlMap_Custom.txt

If you delete this file, you button mappings will be reset and you can remap
them again as you see fit.

Also note, for anyone that attempts to open the controlmap.txt file and edit
it themselves, that the tab stops in the file *must* remain in place or else
skyrim will crash when launched.  It looks like the parser that reads in the
controlmap.txt file doesn't have any fallback for tabs as spaces, etc.


--

DIFFS:

Here is a diff of the changes made to controlmap.txt from the stock file found
in "Skyrim - Interfaces.bsa" as of version 1.3.7.0:

  60,61c60,61
  < Accept    !0,Activate             !0,Activate             !0,Activate     0  0  0  0x8
  < Cancel    !0,Tween Menu,!0,Pause  !0,Tween Menu,!0,Pause  !0,Tween Menu   0  0  0  0x8
  ---
  > Accept    !0,Activate             !0,Activate             0x1000    0  0  0  0x8
  > Cancel    !0,Tween Menu,!0,Pause  !0,Tween Menu,!0,Pause  0x2000    0  0  0  0x8
  
  85,86c85,86
  < XButton    !0,Ready Weapon  !0,Ready Weapon   !0,Ready Weapon   0  0  0  0x8
  < YButton    !0,Toggle POV    !0,Toggle POV     !0,Jump           0  0  0  0x8
  ---
  > XButton    !0,Ready Weapon  !0,Ready Weapon   0x4000    0  0  0  0x8
  > YButton    !0,Toggle POV    !0,Toggle POV     0x8000    0  0  0  0x8
  
  101,102c101,102
  < Accept    !0,Activate                           !0,Activate                           !0,Activate     0  0  0  0x8
  < Cancel    !0,Favorites,!0,Tween Menu,!0,Pause   !0,Favorites,!0,Tween Menu,!0,Pause   !0,Tween Menu   0  0  0  0x8
  ---
  > Accept    !0,Activate                           !0,Activate                           0x1000    0  0  0  0x8
  > Cancel    !0,Favorites,!0,Tween Menu,!0,Pause   !0,Favorites,!0,Tween Menu,!0,Pause   0x2000    0  0  0  0x8
  
  107c107
  < Cancel        !0,Tween Menu,!0,Pause    !0,Tween Menu,!0,Pause    !0,Tween Menu   0  0  0  0x8
  ---
  > Cancel        !0,Tween Menu,!0,Pause    !0,Tween Menu,!0,Pause    0x2000          0  0  0  0x8
  
  188c188
  < Cancel        !0,Tween Menu,!0,Pause    !0,Tween Menu,!0,Pause    !0,Tween Menu   0  0  0  0x8
  ---
  > Cancel        !0,Tween Menu,!0,Pause    !0,Tween Menu,!0,Pause    0x2000          0  0  0  0x8
  
  191c191
  < Cancel    !0,Tween Menu,!0,Pause    !0,Tween Menu,!0,Pause    !0,Tween Menu   0  0  0  0x108
  ---
  > Cancel    !0,Tween Menu,!0,Pause    !0,Tween Menu,!0,Pause    0x2000          0  0  0  0x108

The gamepad.txt file, also in "Skyrim - Interfaces.bsa", explains which hex
codes correspond to which buttons.  I'll include the contents of that file here
to help explain the above diff and in case you wish to tweak controlmap.txt
yourself:

  // 1st field: Gamepad button name.  DO NOT ALTER!  This field is used to ID events in the code
  // 2nd: Key hardware value.  Matches XINPUT_GAMEPAD_* enum values on 360
  Up        0x0001
  Down      0x0002
  Left      0x0004
  Right     0x0008
  360_Start 0x0010
  360_Back  0x0020
  360_L3    0x0040
  360_R3    0x0080
  360_LB    0x0100
  360_RB    0x0200
  360_A     0x1000
  360_B     0x2000
  360_X     0x4000
  360_Y     0x8000
  
  // NOTE: The below hardware values are arbitrary, since there are no XINPUT_GAMEPAD values for them
  360_LT    0x0009
  360_RT    0x000a
  360_LS    0x000b
  360_RS    0x000c


--

CHANGELOG:

1.00  2011.12.09
  
  * initial release

