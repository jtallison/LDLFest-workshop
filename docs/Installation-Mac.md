# Installing Python on a Mac

First, in case you didn't know it, the modern Mac operating system -- the one they insist keeping as X (as in OH ESS EX, now, "eleven") -- is really just a pretty face for Unix. That is, it is POSIX-compliant, which is probably something that will never mean much to you, except when you want to extend the functionality of the OS and you discover there is just a lot, a lot of stuff already built for you. 

One of the things that various flavors of Unix, including Linux, have had for a long time are package managers, something the Mac OS now has in the case of the App Store. In brief, a package manager does two things -- well at least these two things worth pointing out here: first, a package manager knows what else you might need for a piece of software to run, and it will go ahead and install it for you, and, second, a package manager will update your software, all of it if you like, with a single click or, in the case of the command line, with a single typed line.

The best package manager I have found to use with the Mac OS, and there are a few, is MacPorts. One important feature of using MacPorts, is that we are going to install a separate version of Python than the one that comes with Mac OS. This is important: if we break anything in our little walled garden of Python, it will have zero effect on the operating system. For the record, MacPorts installs its walled garden at `/opt/local`. (Understanding Unix paths, as they are called, is for another time.)

This is a workshop with "command line" in the title, and so while I wish the first thing you were doing is getting to the command line, we are going to need to take a slight detour, to the [Mac App Store][] to install Xcode. (If that link works, then the App Store opened for you to the Xcode page. If not, you'll need to open it yourself -- which if you want to feel like you're commandlining it, you can do by typing **CMD + Space**, which opens Spotlight, and then type in "app" and highlight the App Store app, if it isn't already highlighted, and then hit return. *Badabing*. Once in the App Store, just search for "xcode" and proceed as usual.)

With that done, we now head to the command line. To get there, we need to open a terminal: **CMD + Space** and type in "term" *or* **CMD + Shift + U**, which is a Finder keyboard shortcut that takes you directly to the **Utilities** folder within the **Applications** folder (in case you want to find it for yourself). Terminal is a GUI application that gives you access to the CLI. Feel free to open up the preferences and adjust the size of the font used and the size of the window to your preferences -- *ack, my aging eyes!*. 

Now, here's everything you need to type, in the order you need to type it, with one slight diversion to download and install the MacPorts base package. In brief, we are going to:

1. Install the Xcode command line tools. 
2. Install MacPorts.
3. Use MacPorts to install everything else.

Please note that these directions assume that everything we need to do is in the most recent version of Python, which as of this date is Python 3.4 -- this means some libraries that have not yet been updated, and you may one day want to try as you become a power Python coder, may not be available and you'll need to install an older version of Python, which you can totally do in MacPorts, whose coolness in your eyes just doubled.

**Nota bene**: At various moments during this installation process you will be asked to preface a command with `sudo`, short for `super user do` (and pronounced *su - doe* -- I hope all this pronunciation guidance is appreciated), which means you have administrator privileges on the machine on which you are installing things. If this is your personal machine, then you probably do, but if this is an institutional machine, you may need to work something out with your IT folks. (It's possible to install MacPorts, I believe, into a user's `home/` directory, but let's only cross that bridge if we have to.)

With Xcode installed (**!**), install the Xcode command-line tools: 

First:

    xcode-select --install

Dumbly, this brings up a dialogue box that you have to click "okay." Do it, and it's done. Then: 

    sudo xcodebuild -license

We need these things done in order to install MacPorts, which you now can download and install: here's the [installation page][] with the various flavors of MacPorts depending on which version of Mac OS X you are running -- click the Apple in the upper lefthand corner and click on **About This Mac** if you are not sure. If you have kept your Mac up-to-date and you are running *El Capitan*, then [this link][] will start the download for you with one click. Double-click the downloaded *package* and let the install run.

Now, *back to the command line!*

With the base package installed, type the following and hit return, which will run MacPorts from the command line for the first time.

    sudo port selfupdate

Some words scrolled by, perhaps, and, in all likelihood, you were assured that you're at the latest version. Good.

Now, we need to install Python and the various libraries. Again, please note that we are going with the most up-to-date version of Python, and that is why you see `py34` appended in front of so many things: it's short for **Python 3.4**. 

The series of commands you will enter at the command line are below. In brief, you will first install Python 3.4, then you will tell your system that whenever you run Python, you want it to run this version of Python. (Your system is free to use the one that came with it.) Next, you will install the 3 libraries that are the basis for all scientific computing using Python: `numpy` (mathematical functions beyond the basic operators), `scipy` (scientific functions), and `matplotlib` (a plotting library for drawing graphs). These are big libraries, so depending upon the speed of your internet connection, the amount of ram in your computer, and your processor, this could be a good time to get a cup of coffee, grab a bite to eat, or work on that portion of that article you were supposed to have revised and resubmitted last week. 

After the big three, we will install `pandas` (Python's data analysis library) and, *Ta dah!*, the NLTK. The step in-between, with `xorg` is a bit of a workaround for a particular dependency. It's quick; it's painless; and do you really want to know the details or are you ready to move on?

    sudo port install python34
	sudo port select --set python python34
    sudo port install py34-numpy
    sudo port install py34-scipy
    sudo port install py34-matplotlib
    sudo port install py34-pandas
    sudo port install xorg-xcb-proto +python34
    sudo port install py34-nltk
	

At this point, you have a complete setup for general scientific computing -- the same setup that people at CERN use to try to create black holes in Switzerland (because they use my installation instructions, too) -- as well as for natural language processing. 

We could stop there, but a few more steps are going to make our work with Python just a bit easier. One step is to install *interactive Python*, which is great in and of itself, but the next step will install a series of libraries that will allow us to do all of this not from the command line but from a web browser where we can type in text like this between various experiments, turning our working environment into a lab notebook that can be exported to various formats, including web pages, slideshows, PDFs, Word documents, and much more. 

First, iPython:

    sudo port install py34-ipython
    sudo port select --set ipython py34-ipython
	
Finally, if you would like the option of using *Jupyter* notebooks:

    sudo port install py34-jupyter

You're done. Pour yourself a glass of your favorite relaxing beverage and smile knowingly while gazing into the distance.

[Mac App Store]: http://itunes.apple.com/us/app/xcode/id497799835?ls=1&mt=12
[installation page]: https://guide.macports.org/chunked/installing.macports.html
[this link]: https://distfiles.macports.org/MacPorts/MacPorts-2.3.4-10.11-ElCapitan.pkg