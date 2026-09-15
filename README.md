SHIT-PKG

A package manager wrapper (or a provider) that shouldn’t exist.

SHIT-PKG is a small, experimental package-management frontend for Linux.

The goal is simple:

Give one command a package let SHIT-PKG figure out which package provider should handle it.

> shit-pkg search niri
> shit-pkg install <pkg-name>

Instead of having to remember whether a package belongs to apt, pacman, emerge, or something else, SHIT-PKG provides a common interface over multiple package managers.

# Current Status

***VERY unfinished.***

This project is currently an experiment / work in progress.

Things currently being worked on:

* [x]	Provider detection
* [x]	Provider selection
* [x]	Package searching
* [x]	Package installation handoff
* [x]	apt provider
* [x]	pacman provider
* [x]	portage provider
* [ ]	Proper package-name translation between distributions
* [ ]	Automatic provider selection
* [ ]	Better error handling
* [ ]	Dependency handling
* [ ]	Package information
* [ ]	Removal/uninstallation
* [ ]	Upgrade/update support
* [ ]	Configuration system
* [ ]	More package providers
* [ ]	Stop everything from exploding

# How It Works

SHIT-PKG doesn’t try to replace the underlying package managers.

Instead, it acts as a frontend/provider layer (i vibecoded most of it same with this shitty blueprint):

                    ┌──────────────┐
                    │   SHIT-PKG   │
                    └──────┬───────┘
                           │
             ┌─────────────┼─────────────┐
             │             │             │
             ▼             ▼             ▼
          ┌─────┐       ┌──────┐      ┌────────┐
          │ APT │       │Pacman│      │Portage │
          └─────┘       └──────┘      └────────┘
             │             │             │
             ▼             ▼             ▼
          Debian/       Arch-based      Gentoo
          Ubuntu/etc.   systems

Each provider lives in:

providers/
├── apt
├── pacman
└── portage

SHIT-PKG detects executable providers and presents them to the user.

# Providers

### APT

For Debian-based systems.

> shit-pkg install <package>

### Pacman

For Arch-based systems.

> shit-pkg install <package>

### Portage

For Gentoo systems.

> shit-pkg install <package>

## ***Searching***

You can search through the available providers:

> shit-pkg search niri

SHIT-PKG asks each detected provider to search for the package.

If multiple providers find it, you can choose which one to use.

### Installing

> shit-pkg install firefox

You’ll be presented with the available providers:

Available providers:
[1] apt
[2] pacman
[3] portage
[4] Cancel

Choose one and SHIT-PKG hands the package to that provider.

# Important

**SHIT-PKG is not currently a universal package-name compatibility layer.***

For example:

Arch:       niri
Gentoo:     gui-wm/niri

These are not necessarily interchangeable package identifiers.

Eventually SHIT-PKG should be able to understand these differences, but for now the underlying provider receives the package name you give it.

 # Installation

Clone the repository:

> git clone <repository-url>
> cd shit-pkg

Make the main script executable:

> chmod +x shit-pkg

You can run it directly:

> ./shit-pkg detect

Or put it somewhere in your PATH:

> mkdir -p ~/.local/bin
> ln -sf "$PWD/shit-pkg" ~/.local/bin/shit-pkg

Then make sure ~/.local/bin is in your PATH.

Check:

> command -v shit-pkg

For Development:

SHIT-PKG is currently written in Bash, yep.

Syntax-check the script with:

> bash -n ./shit-pkg

For debugging:

> bash -x ./shit-pkg detect

Provider scripts are intentionally kept separate so additional package managers can be added without rewriting the entire frontend.

My goals for this stupid ass project that i might not even touch it but i posted it here in case anyone wants to finish it

The eventual goal is something closer to:

shit-pkg install firefox

and SHIT-PKG handles the rest.

Potential future features:

* automatic provider selection
* package-name translation
* package metadata abstraction
* install/remove/update operations
* dependency handling
* provider priorities
* configuration files
* additional package managers
* better scripting/API support
* distro detection
* transaction logging
* dry-run mode

Maybe eventually:

shit-pkg install niri

will actually mean the same thing regardless of whether you’re running Arch, Debian, Gentoo, or another supported distribution.

🤡 Why?

Because apparently using the package manager normally wasn’t complicated enough.

Also, this started as a Linux experiment and turned into an excuse to learn how package managers, providers, repositories, executable discovery, and shell scripting actually work.

So here we are.

📜 License

See LICENSE. 

⸻

SHIT-PKG is unfinished, experimental software.

If it breaks your package database, I warned you.

If it works, pretend I planned it. (also side note: pacman isn't tested, apt isnt implemented.... yet so use it at your own risk)
