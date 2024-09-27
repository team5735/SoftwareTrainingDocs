# Tools and Setup

> This lesson should be simple and middle-range, anywhere from 1-2hr, simply because it will be a collective process and people will need individual help. If finished early, we can probably just chill.

Welcome, new Software members! Today we will download and prepare various tools on your MacBooks, discussing their purposes as we go.

## WPILib

WPILib, developed at WPI (a college in Worcester), is a package of most necessary tools for FRC robot control. It comes with VSCode, various Java APIs, and many additional programs that we will explore in the future. For now, it should be a quick install, all in one folder.

 1. Navigate to https://docs.wpilib.org/en/stable/docs/zero-to-robot/step-2/wpilib-setup.html (or search "WPILib Install" and click the first link).
 2. Scroll until the first Download, verify that it is for MacOS, and click the installation link.
 3. Select your downloading location (I personally recommend Desktop for ease of use) and wait for it to finish installing.
4. Open the downloaded ".dmg" file (this stands for Disk Image!) and move  "WPILibInstaller" and "WPILib_MacArm-2024.3.2-artifacts.tar.gz" out, onto your Desktop.
5. Eject the "WPILibInstaller" *Disk Image* (It looks like a little hard drive in the icon) by right clicking and selecting eject. Doing this is not strictly necessary, but there is no reason to leave it around.
6. Open the new "WPILibInstaller" *Application* (It looks like a W surrounded by a red hexagon, it is annoying that all of these files are named the same) and select "Open" and "Allow" when your computer gives popups.
7. In the window opened by the installer, select "Start," "Everything," "Install for this User," and "Download for this computer only." 
8. Wait for VSCode to install.
9. Select "Next" and wait for other installations to finish. Then select "Finish" when prompted.
10. Navigate to the "vscode" folder (located under your account -> WPILib -> [year]), right click the VSCode application file, and select "Make Alias."
11. Rename the alias (shortcut) to whatever you want, and move it to your Desktop.
12. Delete and eject whatever installation files are left on the Desktop, excluding VSCode. 

Congratulations, you have now installed WPILib (and by proxy VSCode)!

## iTerm2

iTerm2 is a simple Terminal emulator, allowing us to access the MacOS Terminal in a more restricted manner, where it would otherwise be blocked.

1. Navigate to https://iterm2.com/downloads.html (or search "iTerm2 install" and click the link titled "Downloads").
2. Click the link to download the latest version of iTerm2 (right now it should be 3.5.5), select your downloading location (again, I recommend Desktop) and click "Save" to start downloading.
3. Open the downloaded ".zip" file.
4. Check that an application named "iTerm" is now in place of the zipped file.

Congratulations, you have now installed iTerm2!

## Set Up Your Git Info

Very simple, just giving some identification for git to use when referring to you, but very much needed for everything we will be doing going forwards.

1. Open iTerm2
2. Type `git config --global user.name "` [your name] `"` and press enter
3. Type `git config --global user.email "` [your email] `"` and press enter
4. Verify that both have been properly configured by typing `git config --get user.name`, pressing enter, and checking for the name you provided, then typing `git config --get user.email` and doing the same.

You now have id on git!

## Clone the Sample Repo

Now for the most important step, getting yourself connected to the rest of the team via Git. We will go over all sorts of important and interesting information about Git and GitHub in future lessons, but for now you'll just be copying down and syncing yourself to code from the team's database.

1. Open VSCode.
2. On the welcome page, select "Clone Git Repository..."
3. In the text box that appears at the top of the screen, paste in "https://github.com/team5735/SampleRobotCodebase"
4. Select a suitable file location.
5. When prompted, select "Allow" to sign in with GitHub. If you are already signed in on your browser, then it should immediately sign you in. Otherwise, sign in to GitHub.
6. VSCode should start working to download the repository now.

Congratulations! You now have code on your computer that is able to track, across the internet, the overall team's progress! We will go more into detail on why and how this works during future lessons, but for now you should know that this is no small feat.
