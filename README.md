# Windows style keyboard layout for MacBook

This is a collection of scripts, instructions and utilities to make a Macbook OS X keyboard layout behave like a Windows laptop.

The primary goal is to retain muscle memory when moving between a configured Mac and and Windows machine, whether that is the VM on your Mac, or a separate Windows system. These configurations were based off of a Sony Vaio keyboard, although many other PC laptops share a similar layout.

This is a high level diagram of the resulting keyboard layout:

![Keyboard Layout](https://raw.githubusercontent.com/lynx44/Mac-to-Windows-Keymappings/master/Keyboard%20Diagram.png)

## Terminology

The phrase "keyboard key" refers to the actual physical keyboard, as if you are looking at the real keyboard in front of you.

The phrase "virtual key" refers to the semantic meaning of the newly mapped key, as if you were using a keyboard with the above layout in Windows.

## Contents

[Step 1 - Swap the Fn, Ctrl, Option, and Command keys](#step1)
[Step 2 - Update Keybindings for cursor movement](#step2)
[Step 3 (Optional) - Disable special characters when using the option key in conjunction with a letter](#step3)
[Step 4 (Optional) - Windows snap functionality](#step4)
[Step 5 (Optional) - Fix scrolling when using Windows with Parallels](#step5)

## <a name="step1"></a>Step 1 - Swap the Fn, Ctrl, Option, and Command keys

### Purpose

This will remap your keyboard to exhibit the following behaviors:

 | Symbol on keyboard | Mac Mapping                                                  | Windows Mapping |
|--------------------|--------------------------------------------------------------|-----------------|
| fn                 | command ⌘ (fn for Function Keys, like brightness adjustment) | ctrl            |
| control               | fn                                                           | fn              |
| option             | Ctrl                                                         | win             |
| command ⌘          | option/alt                                                   | alt             |

### Steps

 - Download and install [Karabiner](https://pqrs.org/osx/karabiner/).
 - Run the script at /scripts/Karabiner/karabiner_windows_mappings
  - `sudo chmod a+x /scripts/Karabiner/karabiner_windows_mappings`
  - `/scripts/Karabiner/karabiner_windows_mappings`

### Test

Open an application, ensure that keyboard keys `fn-c` and `fn-v` copy and paste a line.

If you're using [Parallels](http://www.parallels.com/) or presumably another virtual instance inside your OS X install, try using the `fn` key as the `ctrl` - this should also work as expected.

### Extending

There are a lot of options in Karabiner that you can easily update by using the GUI in the `Preferences...` dialog. You can output your preferences by using a command similar to:

 - `Karabiner.app/Contents/Library/bin/karabiner export > /Users/{yourusername}/karabiner_direct_windows_map`

Feel free to submit a pull request if you add functionality that improves compatibility or better matches a Windows style keyboard.

## <a name="step2"></a>Step 2 - Update Keybindings for cursor movement

### Purpose

 - Change the behavior of the virtual `ctrl` key (keyboard key `fn`) to jump by words, rather than lines when using the arrow key
 - Update the virtual `fn` key (keyboard key `control`) to: 
  - `page up` and `page down` when used with the up and down arrow keys
  - navigate `home` and `end` when used with the left and right arrow keys

### Steps

 - Extract `/Library/KeyBindings/DefaultKeyBinding.dict` to `~/Library/KeyBindings`
  - cp `Mac-to-Windows-Keymappings/Library/KeyBindings/DefaultKeyBinding.dict` `~/Library/KeyBindings/DefaultKeyBinding.dict`
  - Log out, then log back in

### Test

 - Open TextEdit and type a few lines of text with spaces (copy it from this readme if that's easiest)
  - Use keyboard keys `control-left` and `control-right` to navigate to the beginning and end of a line
  - Use keyboard keys `control`-up and `control`-down to page up and down

### Extending

These mappings were created by using [KeyBindingsEditor](http://www.cocoabits.com/KeyBindingsEditor/). To add or tweak the functionality, open the `DefaultKeyBinding.dict` file and save your changes. 

Feel free to submit a pull request if you add functionality that improves compatibility or better matches a Windows style keyboard.

## Optional Steps

## <a name="step3"><a>Step 3 (Optional) - Disable special characters when using the option key in conjunction with a letter

### Purpose

I'm a programmer, and I use IntelliJ to do a lot of my programming. This particular program makes a lot of use of the Alt key to perform special actions. This causes issues when using a Mac keyboard, because it inserts special characters when pressing `Option-Letter`, rather than performing the action the application has assigned it.

If you need the virtual `alt` key to function as it would in Windows, you may need to disable this feature.

Credit goes to [Peter Lamburg in this StackOverflow post](http://stackoverflow.com/questions/11876485/how-to-disable-typing-special-characters-when-pressing-option-key-in-mac-os-x)

### Steps

 - copy `Mac-to-Windows-Keymappings/Library/Keyboard Layouts/USKeylayout_custom_no_alt.keylayout` to `~/Library/Keyboard Layouts`
  - cp `Mac-to-Windows-Keymappings/Library/Keyboard Layouts/USKeylayout_custom_no_alt.keylayout` `~/Library/Keyboard Layouts`
 - Log out and log back in 
 - Open `System Preferences`->`Keyboard`->`Input Sources`
  - Click the `+` button on the bottom
  - Select `Others`->`US custom` and click `Add`
 - Go back to the Finder. In the menu bar at the top of your screen, you should see a keyboard icon (mine is to the left of the battery icon). Click on this and select the new `U.S. custom` keyboard layout.

### Test

Open an application and type virtual `alt`-z (keyboard key `command`). Verify that this does not type a symbol.

### Extending

I simply bummed this off of [Peter Lamberg's aforementioned StackOverflow post](http://stackoverflow.com/questions/11876485/how-to-disable-typing-special-characters-when-pressing-option-key-in-mac-os-x), but he mentions that he used [Ukelele](http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=ukelele).
 
Feel free to submit a pull request if you add functionality that improves compatibility or better matches a Windows style keyboard.

## <a name="step4"><a>Step 4 (Optional) - Windows snap functionality

### Purpose

I often use the `Windows-Arrow` shortcut to snap windows to the left and right sides of the screen, particularly when I need to compare documents side by side.

This step will give you that ability using the mouse or keyboard shortcuts.

### Steps

 - Install [BetterTouchTool](http://www.bettertouchtool.net/)
 - Open BTT Preferences from the Menu bar
  - Click on Basic Settings  at the top of the screen
   - At the bottom, click to "Enable Window Snapping"
   - Go back to the main Preferences dialog
  - Click on Keyboard
   - Click "Add New Shortcut" to
    - Virtual `win`-right (keyboard key `alt`) -> Maximize Window Right
    - Virtual `win`-left (keyboard key `alt`) -> Maximize Window Left
    - Virtual `win`-up (keyboard key `alt`) -> Maximize Window
    - Virtual `win`-down (keyboard key `alt`) -> Restore Old Window Size

*Note* - I actually had to modify these keyboard shortcuts to be virtual `win`+`alt` (keyboard keys `alt`+`command`) due to conflicts that I don't recall at this time.

### Extending

There are of course a lot of options in BetterTouchTool that I haven't explored too deeply.

Feel free to submit a pull request if you add functionality that improves compatibility or better matches a Windows style keyboard.

## <a name="step5"><a>Step 5 (Optional) - Fix scrolling when using Windows with Parallels

### Purpose

Scrolling was a terrible experience when I first started using my Windows applications in Parallels. It took far too much work to start scrolling, and after it started moving, it was choppy and unpredictable.

### Steps

 - In Parallels, disable smooth scrolling
  - From the Parallels Menu icon:
   - Configure...->Hardware->Mouse and Keyboard
    - Disable Smooth Scrolling
 - In Windows, change number of lines to scroll to 1
 
### Test

Open an application in Windows through Parallels, and the scrolling should be much more responsive.

## Feedback

This should be a good start, but feel free to fork this repository to match your needs.

Feel free to submit a pull request if you add functionality that improves compatibility or better matches a Windows style keyboard.
