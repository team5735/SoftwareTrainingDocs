# Tools and Setup

Welcome! If you weren't here last lesson, you can read it [here](https://github.com/team5735/SoftwareTrainingDocs/blob/main/lessons/000_intro_to_software.md). Today we will download and prepare various tools on your MacBooks.

This lesson is easier to follow if you have the Markdown version open in your browser. The easiest way to go there is to type the following into your browser's address bar exactly:
`github.com/team5735/SoftwareTrainingDocs`
Then, click on the `lessons` folder, followed by `001_tools_and_setup.md` (this document).

## WPILib

WPILib, developed at WPI, is a package of most necessary tools for FRC programming. It comes with VSCode, various Java APIs, and many additional programs that we will explore in the future. For now, it should be a quick install, all in one folder. It's what we'll use instead of IntelliJ, if you took APCSA. If you're advanced enough to have something else you prefer, you still need to install this.

1. Follow [this link](https://github.com/wpilibsuite/allwpilib/releases/latest) 
2. Scroll down and click the link that ends in 'Mac (Arm)'.
3. Open the downloaded file. It's large, so get ready to wait for the download.
4. This should open a new window. Drag the app named WPILibInstaller and the other zip-like file contained in the .dmg (disk image) onto your desktop.
5. Open the new "WPILibInstaller" application (it should be the only thing named that that's new to your desktop) by double-clicking it, then selecting "Open" and "Allow" when your computer gives popups.
6. In the window opened by the installer, select "Start," "Install for this User," and "Download for this computer only" as the buttons appear.
7. Wait for VSCode to install. It should take a few seconds.
8. Click "Next" once the first progress bar is finished and wait for other installations to finish. This will take some time. Click "Finish" when it's done.
9. A Finder window should open. Drag the file named Visual Studio Code (selected) onto the dock. You will know you've done this correctly if you can see two copies of the icon like in this screenshot:
<img width="903" height="608" alt="VSCode: both the .app and the link in the Dock are visible after installation." src="https://github.com/user-attachments/assets/68c65012-fdb1-4df8-8663-bc67cec39984" />

10. You don't need anything on your desktop anymore; you can remove the following three files if you'd like to clean up:
<img width="120" height="342" alt="WPILibInstaller mounted dmg, executable, and artifacts file from top to bottom." src="https://github.com/user-attachments/assets/7cf3ecd6-a07d-43b8-b981-d9f4c6618eee" />

11. Open VSCode from your dock and check for a little red and black "w" symbol around the top right like pictured. If you do not see one, come and see a software member for help or try the instructions again.
<img width="134" height="83" alt="Screenshot 2025-09-02 at 9 41 07 PM" src="https://github.com/user-attachments/assets/a77fc53a-54d5-46cd-8f3b-4736256be1aa" />

If that's present, congratulations, you've installed WPILib and VSCode! You're almost ready to write robot code.

## A Terminal

A terminal program is a program that lets you type in terminal commands. It's generally the most efficient and fast method of accomplishing tasks, despite being noticeably harder to set up. kitty and iTerm2 are two popular terminal editors that this document explains how to install if you'd like, but most tasks in these documents don't need a terminal, so if you're ok with sacrificing an admittedly small amount of productivity and efficiency for ease of use, feel free to use a GUI (for FRC purposes, you can do most of your tasks with the VSCode GUI).

The VSCode terminal is the easiest to set up as you've already done so. kitty is Sebastian's preferred terminal, but the differences between the three are relatively nonexistent for our purposes.

### VSCode terminal

As an alternative to a standalone terminal program, the VSCode terminal is a good entry point for learning the ways of the terminal. You can open it by going to View > Terminal from the menu bar in the top left of your screen.

### iTerm2

1. Navigate to https://iterm2.com/downloads.html (or search "iTerm2 install" and click the link titled "Downloads").
2. Click the link to download the latest version of iTerm2 (right now it should be 3.5.5), select your downloading location (again, I recommend Desktop) and click "Save" to start downloading.
3. Open the downloaded ".zip" file.
4. Check that an application named "iTerm" is now in place of the zipped file.

### kitty

You can skip to step 3 by clicking on [this link](https://github.com/kovidgoyal/kitty/releases/latest).

1. Search "kitty docs"
2. Click the link titled something like "kitty - Kovid Goyal"
3. Navigate to Quickstart > Install kitty on the left sidebar
4. Click the link titled "GitHub releases page"
5. Scroll down to the "Assets" section of the first version, it should say "Latest" next to the version number
6. Click "show all 36 assets" (scroll down a couple screens)
7. Scroll down to the bottom of the link overrun and click the "macOS dmg" file
8. Open your Downloads folder and open the downloaded kitty-\<version>.dmg, where \<version> is the latest version
9. Drag the "kitty" app to your desktop. Do not drag it into the Applications folder that shows up next to kitty, as you can't.
10. You can "eject" the "kitty-\<version>" drive-looking thing from your desktop now (right click or drag into trash)

## Set Up Your Git Info

You need to do this before writing code. This needs to be done in a terminal even if you'd rather use the GUI.

1. Open a terminal (any of kitty, iTerm2, or the VSCode integrated terminal)
2. Type `git config --global user.name "` \<your name> `"` and press enter
3. Type `git config --global user.email "` \<your email> `"` and press enter

## Make a GitHub Account

This will be the most important step in all of this, creating an account for yourself on GitHub, and having that account added into our team's organization.

1. Navigate to https://github.com and click "Sign Up."
2. Enter your email (can be any email of your choice, you can add others to your account in the future).  
3. Create a password (make it strong!).
4. Create a username (preferably one with your name in it, but any should be fine).
5. Press "Continue."
> [!NOTE]
> If you get an error stating that GitHub cannot verify your captcha results, **try again on a home wifi network**.
7. Copy over the code sent to your email (should be a string of numbers).
8. GitHub should now prompt you to log in with your new account by entering email and password, do so!
9. You may be prompted to "personalize" your experience, if you really want to do so, then do, otherwise look for a button labelled "skip personalization" (it may be a bit hidden).
10. Join the organization
    - If you're at home, send your account name to one of the returning Software members (whoever is running the lesson if in person, otherwise ask on the team Discord). This is a necessary step because it will let you access the team's code.
    - Otherwise, leads and/or mentors should be able to let you into the organization.

If you weren't able to make a GitHub account while at school, it's no problem. You can still clone and should sign in later.

## Clone the Sample Repo

Now for the most important step, getting yourself connected to the rest of the team via Git. We will go over all sorts of important and interesting information about Git and GitHub in future lessons, but for now you'll just be copying down and syncing yourself to code from the team's database.

1. Open VSCode.
2. On the welcome page, select "Clone Git Repository..."
3. In the text box that appears at the top of the screen, paste in "https://github.com/team5735/SampleRobotCodebase"
4. Select a suitable file location.
5. When prompted, select "Allow" to sign in with GitHub. If you are already signed in on your browser, then it should immediately sign you in. Otherwise, sign in to GitHub.
6. VSCode should start working to download the repository now.

Alternatively, if you'd like to get used to the terminal from the start, you can use the terminal. It really isn't scary at all. You do need to sign in using VSCode first, however.

> [!WARNING]
> If you want help, you'll have to ask Sebastian.

1. Open VSCode using the shortcut you just created.
2. Click on the person in the bottom left of the window and try your darndest to sign in (will update with details when MacOS stops bullying me).
3. Access your terminal of choice.
4. Run these commands (the bit before the ->) (the bolded bits are mnemonics to help you remember the commands):
   - `mkdir robotics` -> this command **m**a**k**es the 'robotics' **dir**ectory
   - `cd robotics` -> **c**hange **d**irectory to 'robotics'; 'robotics' should now be in your prompt (replacing ~, your home directory), which tells you that you're in that directory.
   - `git clone https://github.com/team5735/SampleRobotCodebase` -> this uses **git** to **clone** (download a copy of) the repository at that URL. You can get the URL by copying it from the search bar after navigating to it on GitHub, or by copying it from here; whichever's easier.
   - `cd SampleRobotCodebase` -> the above git command 'clones' (downloads) the repository into the 'SampleRobotCodebase' directory, into which you can `cd`.

> [!TIP]
> If you choose to the continue learning the terminal, you can familiarize yourself with `mkdir` and `cd`, as well as other commands by using them alongside a Finder window to see what they do.
> If demand is high, I'll write a terminal cheat sheet.

You can now work on the robot code.
