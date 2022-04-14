# Make MAC Keyboard feel like Windows

Guide from April 2022, macOS Monterey
## First step

The first thing you wanna do is go to System Preferences on your Mac and go to keyboard. Under the very first keyboard tab click on Modifier Keys.

Once there:
1. Select your keyboard
2. Change Control to Command
3. Change Command to Control

What this will do is that now you can copy/paste with CTRL+C and CTRL+V on your keyboard, so you use the very left bottom key on your keyboard.


## Second step 

...for those who use CTRL+Backspace and co.

I use CTRL+Backspace to delete one word a lot, which is helpful if you don't feel like hitting backspace 8 times to delete an 8 character word. I also use CTRL+LeftArrow and CTRL+SHIFT+LeftArrow to traverse/select through words faster.

This is a bit more complicated. Go to your User/YourUserName directory and show all hidden files with CTRL+SHIFT+. (it's a dot at the end). CTRL in our case is of course the CMD button which we moved to CTRL key in First step above.

Now you should see the folder Library. Go inside and create a folder called KeyBindings, inside which you create a file called DefaultKeyBinding.dict

To create a file open KeyBindigs file in Terminal and enter `touch DefaultKeyBinding.dict`

Open this file with TextEdit which your Mac comes with and paste this

```
/* ~/Library/KeyBindings/DefaultKeyBinding.Dict
This file remaps the key bindings of a single user on Mac OS X 10.5 to more closely
match default behavior on Windows systems.  This particular mapping assumes
that you have also switched the Control and Command keys already.

This key mapping is more appropriate after switching Ctrl for Command in this menu:
Apple->System Preferences->Keyboard & Mouse->Keyboard->Modifier Keys...->
Change Control Key to Command
Change Command key to Control
This applies to OS X 10.5 and possibly other versions.

Here is a rough cheatsheet for syntax.
Key Modifiers
^ : Ctrl
$ : Shift
~ : Option (Alt)
@ : Command (Apple)
# : Numeric Keypad

Non-Printable Key Codes

Up Arrow:     \UF700        Backspace:    \U0008        F1:           \UF704
Down Arrow:   \UF701        Tab:          \U0009        F2:           \UF705
Left Arrow:   \UF702        Escape:       \U001B        F3:           \UF706
Right Arrow:  \UF703        Enter:        \U000A        ...
Insert:       \UF727        Page Up:      \UF72C
Delete:       \UF728        Page Down:    \UF72D
Home:         \UF729        Print Screen: \UF72E
End:          \UF72B        Scroll Lock:  \UF72F
Break:        \UF732        Pause:        \UF730
SysReq:       \UF731        Menu:         \UF735
Help:         \UF746

NOTE: typically the Windows 'Insert' key is mapped to what Macs call 'Help'.  
Regular Mac keyboards don't even have the Insert key, but provide 'Fn' instead, 
which is completely different.
*/

{
"\UF729"   = "moveToBeginningOfLine:";                       /* Home         */
"@\UF729"  = "moveToBeginningOfDocument:";                   /* Cmd  + Home  */
"$\UF729"  = "moveToBeginningOfLineAndModifySelection:";     /* Shift + Home */
"@$\UF729" = "moveToBeginningOfDocumentAndModifySelection:"; /* Shift + Cmd  + Home */
"\UF72B"   = "moveToEndOfLine:";                             /* End          */
"@\UF72B"  = "moveToEndOfDocument:";                         /* Cmd  + End   */
"$\UF72B"  = "moveToEndOfLineAndModifySelection:";           /* Shift + End  */
"@$\UF72B" = "moveToEndOfDocumentAndModifySelection:";       /* Shift + Cmd  + End */
"\UF72C"   = "pageUp:";                                      /* PageUp       */
"\UF72D"   = "pageDown:";                                    /* PageDown     */
"$\UF728"  = "cut:";                                         /* Shift + Del  */
"$\UF727"  = "paste:";                                       /* Shift + Ins */
"@\UF727"  = "copy:";                                        /* Cmd  + Ins  */
"$\UF746"  = "paste:";                                       /* Shift + Help */
"@\UF746"  = "copy:";                                        /* Cmd  + Help (Ins) */
"@\UF702"  = "moveWordBackward:";                            /* Cmd  + LeftArrow */
"@\UF703"  = "moveWordForward:";                             /* Cmd  + RightArrow */
"@$\UF702" = "moveWordBackwardAndModifySelection:";   /* Shift + Cmd  + Leftarrow */
"@$\UF703" = "moveWordForwardAndModifySelection:";    /* Shift + Cmd  + Rightarrow */
"@\U007f"   = "deleteWordBackward:";                  /* C-Del        Delete word backward */
"^\U007f"   = "deleteWordBackward:";                  /* C-Del        Delete word backward */
}
```

### Congratulations

- Now you can CTRL+Left or right to jump through words in text
- You can now CTRL+Shift+Left or right to select one word
- And the last like as it says deleteWordBackward will make your CTRL+Backspace delete one word

#### Misc

Your VSCode editor will not respect these changes, because VSCode has their own shortcuts, which you will be able to easily change yourself. Search for deleteWordLeft in VSCode shortcut settings to bind it to CTRL+Backspace and unbind deleteAllLeft from the same shortcut if you want the Windows behavior.

Alternatively you can use Karabiner app and better touch tool which did not work for me. Karabiner would just not run on computer start and I would have to restart until it starts working and I could not even install BetterTouchTool. You can try these two programs and see if it works. Happy hacking.