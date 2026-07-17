# LOS Minesweeper

Minesweeper for the Lisa Office System, written with help from Claude!

# Introduction

I decided that I wanted to learn how to develop new LOS apps from the ground up (no ToolKit to help out), and I figured that there's no better way to do this than to ask an LLM to write a new app from the ground up, while heavily commenting and explaining things along the way. Then I can use the sample app as a teaching aid to learn just about everything that I need to know about LOS app development. And LOS Minesweeper is (one of) the results of these efforts!

# Installing on Your Lisa
If you don't want to build the app yourself and just want to play it on your Lisa, just download the [los_minesweeper.dc42](los_minesweeper.dc42) image from the root of this repo, and copy it to your Floppy Emu or write it to a real floppy disk. Then insert it into your Lisa and install it as you would any other app; duplicate the tool and drag it onto your hard disk!

Note that Minesweeper is a document-less tool, so there's no stationery for it; just double-click the app directly to open it up.

# Playing the Game
There's not a whole lot to say here; it's just Minesweeper. I'll go over a couple of Lisa-specific quirks/features and leave it at that.

- The Lisa doesn't have right-click, which is what most Minesweeper versions use for flagging squares, so you instead hold the Apple key while clicking on squares in order to flag them. As with real Minesweeper, the first time you "flag click" on a square, it'll put a flag icon on it, the second time it'll put a question mark icon on it, and the third time it'll revert it back to an unflagged square.
- There's also a dedicated Flag Mode (Apple-F or choose Flag Mode under the Game menu) that toggles flagging on permanently until you turn it back off again; no need to hold Apple.
- The Copy option under the Edit menu will copy a full image of your gameboard to the Scrap (Clipboard) that you can then paste into other LOS apps like LisaWrite or LisaDraw. Pretty cool, right?
- The Print option under the File/Print menu works too; it sends an image of your gameboard straight to your printer!

# Building From Source
If you're interested in building the app from source, then you'll need to copy all of the files in the [src](src/) directory over to your Lisa. The easiest way to do this is by downloading the [LOS_Compilation_Base.image.zip](LOS_Compilation_Base.image.zip) hard disk image, extracting it to your hard disk emulator's SD card, and booting into the Workshop from that image. Connect a serial cable between your Lisa's Serial B and your modern computer, clone this repo, and then run the command ```python3 tools/lisa_serial_transfer.py <my_serial_port> src/```, replacing ```<my_serial_port>``` with whatever port your serial cable is connected to on your modern machine. It'll then ask you to run a script on the Lisa.

So now move over to the Lisa Workshop and hit ```R``` for ```Run```. Now type ```<ALEX/TRANSFER``` and hit enter. Wait for the screen to clear and then hit enter on the modern machine. Give it 5-10 minutes for all of the files to transfer over, and then you'll be given control over your Lisa again!

Now for the actual build process. This is easy; just hit ```R``` for ```Run``` again, type ```<MINESWEEPER/MAKE```, and hit enter. Give it time to build and install the app, and then reboot into the graphical Office System, where you should find a nice playable copy of Minesweeper!

# Source Code Structure
The code is divided into several different files; I'll go over what each one does here.

## Build Scripts
Three of the source files are just build scripts, not actual code. They are:
- ```MINESWEEPER/MAKE.TEXT``` - The main build script that you run to make the app. It compiles and then links Minesweeper, then generates the app's alert file, and finally installs it into the LOS catalog.
- ```MINESWEEPER/COMP.TEXT``` - A helper script run by the main make script that compiles the source files.
- ```MINESWEEPER/LINK.TEXT``` - Another helper script run by the main make script that links the Minesweeper binary.

## Source Code
- ```MINESWEEPER/MAIN.TEXT``` - The main Minesweeper program itself. The event loop, initialization, and shutdown code all can be found here.
- ```MINESWEEPER/DIALOG.TEXT``` - Handles the dialog box that you use to enter custom board sizes. LOS doesn't provide any off-the-shelf facilities for displaying dialog boxes, so you have to do the whole thing manually.
- ```MINESWEEPER/DRAW.TEXT``` - Handles all of the program's graphics rendering through QuickDraw.
- ```MINESWEEPER/GAME.TEXT``` - The core game logic itself; the event loop talks to this whenever the user modifies the board, and this talks to the graphics rendering logic to update the display with new game state.
- ```MINESWEEPER/GLOBALS.TEXT``` - All of the global data types used by the rest of the program, plus the Filer operation handler.

## Alert File
- ```MINESWEEPER/ALERT.TEXT``` - An "alert file" that contains all of the text and menu items that the application uses. It's read in by the Alert Manager and allows for easy modification of the text displayed by your program without embedding the text into the source files themselves.


# Contact Me!
Feel free to email me at [alexelectronicsguy@gmail.com](mailto:alexelectronicsguy@gmail.com) if you need help, find any bugs, or have any questions/comments!

I hope you enjoy; it's nice to finally have a game that runs on the Lisa!