# Tools and Setup

> This lesson should be simple and middle-range, anywhere from 1-2hr, simply because it will be a collective process and people will need individual help. If finished early, we can probably just chill.

Welcome, new Software members! Today we will download and prepare various tools on your MacBooks, discussing their purposes as we go.

## WPILib

WPILib, developed at WPI (a college in Worcester), is a package of most necessary tools for FRC robot control. It comes with VSCode, various Java APIs, and many additional programs that we will explore in the future. For now, it should be a quick install, all in one folder.

1. Navigate to https://docs.wpilib.org/en/stable/docs/zero-to-robot/step-2/wpilib-setup.html (or search "WPILib Install" and click the first link).
2. Press the big blue "Downloads" button about one screen down the page. If this opens a new tab, then scroll down and click the link that ends in 'Mac (Arm)'.
4. Open the downloaded file however you'd like. On some browsers it shows up in the top right and you can click it while downloading, and the browser will open it when it's downloaded. If your browser doesn't feel like cooperating today, you can find it in your Downloads folder (open Finder and find it on the left).
5. This should open a new Finder-looking window. Drag the file named WPILibInstaller onto your desktop. It should take a moment or two to copy; it's quite large.
6. On your desktop you should find a silver drive-looking file *also* called WPILibInstaller. Drag that into the Trash (or right-click it with two fingers and select 'Eject "WPILibInstaller"').
7. Open the new "WPILibInstaller" *Application* (It looks like a W surrounded by a red hexagon, it should be the only new thing remaining on your desktop) by double-clicking the app on your desktop and select "Open" when your computer gives popups.
8. In the window opened by the installer, select "Start," "Everything" (should be selected), "Install for this User," and "Download for this computer only," in that order. 
9. Wait for VSCode to install. It should take a few seconds.
10. Click "Next" once VSCode is downloaded (the window should say "Done Downloading") and wait for other installations to finish. This will most likely take a while. Then click "Finish" when prompted.
11. Yet another Finder window should open. Select the file named "Visual Studio Code" in the folder that was opened and either drag it to the Desktop while holding Alt or drag it to your Dock. This ensures you can access it easier. You can rename the one on your desktop if you'd like.
13. You can drag anything left over from this process into the Trash, including the installer (but obviously not the app we just worked so hard to install).

Congratulations, you've installed WPILib and VSCode! You're almost ready to write robot code.

## A Terminal

There's two options for a terminal program on a Mac, and both are equally good for what we're doing. Historically iTerm2 has been used, but Kitty is a newer (and faster) option that has all the same features but can also be run on any computer.

### Kitty

Kitty may seem to be a simple terminal emulator that gets out of your way and just works, but when you need it to be more powerful, it can do anything others can and more, such as having tabs or split-screen.

1. Either type in the following link: https://github.com/kovidgoyal/kitty/releases
  Or, for those averse to link-typing, you can
  1. Search "kitty docs"
  2. Click the link titled something like "kitty - Kovid Goyal"
  3. Navigate to Quickstart > Install kitty on the left sidebar
  4. Click the link titled "GitHub releases page"
2. Scroll down to the "Assets" section of the first version, it should say "Latest" next to the version number
3. Click "show all 36 assets"
4. Scroll down to the bottom of the link overrun and click the "macOS dmg" file
5. Open your Downloads folder and open the downloaded kitty-\<version>.dmg, where \<version> is the latest version
6. Drag the "kitty" app to your desktop or wherever you'd like it
7. You can "eject" the "kitty-<version>" drive-looking thing from your desktop now (right click or drag into trash)

Run the app from your desktop (or wherever)! You've installed Kitty!

### iTerm2

iTerm2 is a simple Terminal emulator, allowing us to access the MacOS Terminal in a more restricted manner, where it would otherwise be blocked.

1. Navigate to https://iterm2.com/downloads.html (or search "iTerm2 install" and click the link titled "Downloads").
2. Click the link to download the latest version of iTerm2 (right now it should be 3.5.5), select your downloading location (again, I recommend Desktop) and click "Save" to start downloading.
3. Open the downloaded ".zip" file.
4. Check that an application named "iTerm" is now in place of the zipped file.

Congratulations, you have now installed iTerm2!

## Set Up Your Git Info

This is a very simple and vital procedure that gives some identification to git (our version control system) for it to use when referring to you, but doing this is very much needed for everything we will be doing going forwards.

1. Open iTerm2
2. Type `git config --global user.name "` [your name] `"` and press enter
3. Type `git config --global user.email "` [your email] `"` and press enter
4. Verify that both have been properly configured by typing `git config user.name`, pressing enter, and checking for the name you provided, then typing `git config user.email` and doing the same.

Git now understands that you are, in fact, you!

## Clone the Sample Repo

Now for the most important step, getting yourself connected to the rest of the team via Git. We will go over all sorts of important and interesting information about Git and GitHub in future lessons, but for now you'll just be copying down and syncing yourself to code from the team's database.

1. Open VSCode.
2. On the welcome page, select "Clone Git Repository..."
3. In the text box that appears at the top of the screen, paste in "https://github.com/team5735/SampleRobotCodebase"
4. Select a suitable file location.
5. When prompted, select "Allow" to sign in with GitHub. If you are already signed in on your browser, then it should immediately sign you in. Otherwise, sign in to GitHub.
6. VSCode should start working to download the repository now.

Alternatively, if you'd like to get used to git from the start, you can use the terminal. It really isn't scary at all. You do need to sign in using VSCode first, however.

1. Open VSCode.
2. 

Congratulations! You now have code on your computer that is able to track, across the internet, the overall team's progress! We will go more into detail on why and how this works during future lessons, but for now you should know that this is no small feat.
