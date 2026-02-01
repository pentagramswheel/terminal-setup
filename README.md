# Terminal Setup

**Author(s):** <a href='https://github.com/pentagramswheel'>Wil Aquino Jr.</a>

**Creation Date:** February 1, 2026

## Introduction
This repo's purpose is to store my personal terminal setup. It is currently compatible with the following CLIs:
- Zsh (macOS built-in)

## How to Install

The general setup for these settings is as follows:
1. Install the JetBrains Mono Nerd Font (NFM).
2. Install a theme for your terminal.
3. Install <a href='https://github.com/fastfetch-cli/fastfetch'>FastFetch</a>, add your own ASCII art inside of `fastfetch/ascii.txt`, and configure your terminal to run FastFetch upon startup.
4. Install any additional terminal tools.

My setup will be provided for macOS's Zsh. Any time `.zprofile` is mentioned, you may instead use <a href='https://github.com/pentagramswheel/terminal-setup/tree/main/themes'>the included .zprofile</a>.

Optionally install <a href='https://brew.sh/'>Homebrew</a> or install all of the following Homebrew steps manually.

Install the JetBrains NFM font via
```
brew tap homebrew/cask-fonts
brew install --cask font-jetbrains-mono-nerd-font
```

Import the <a href='https://github.com/catppuccin/Terminal.app'>Catppuccin</a> theme in <a href='https://github.com/pentagramswheel/terminal-setup/tree/main/themes'>the included themes folder</a> into your terminal.

Install FastFetch and test its installation via
```
brew install fastfetch
fastfetch
```

Create a FastFetch config file via
```
fastfetch --gen-config
```

Import your own ASCII art via `~/.config/fastfetch/ascii.txt` and configure the file at `fastfetch --gen-config` to use it, e.g.
```
{
  "logo": {
    "type": "file",
    "source": "/Users/YOUR_USERNAME/.config/fastfetch/ascii.txt",
    "padding": {
      "right": 2
    }
  },

  "display": {
    "separator": " : "
  },

  "modules": [
    "os",
    "kernel",
    "uptime",
    "packages",
    "shell",
    "terminal",
    "cpu",
    "memory"
  ]
}
```
> Want to add a Catppuccin gradient? Precede each `ascii.txt` line with "$LINE_NUMBER". See <a href='https://github.com/catppuccin/Terminal.app'>Catppuccin</a> for an example.

My setup uses <a href='https://github.com/pentagramswheel/terminal-setup/tree/main/fastfetch'>the included fastfetch folder</a>.

Add the following lines to `~/.zprofile` to launch fastfetch upon startup:
```
if [[ -z "$FASTFETCH_SHOWN" ]] && command -v fastfetch >/dev/null; then
  export FASTFETCH_SHOWN=1
  fastfetch
fi
```

Install the remaining following:
```
brew install --cask notunes firefox notion sublime-text
brew install zsh-autosuggestions zsh-syntax-highlighting
```

Then add these final lines to `~/.zprofile`:
```
# apps setup
firefox() {
    if [[ "$1" == "-P" || "$1" == "-p" ]]; then
        /opt/homebrew/bin/firefox "$@" 2> >(grep -v "GLD_TEXTURE")
    else
        /opt/homebrew/bin/firefox "$@"
    fi
}

alias notion="open -a Notion"
export EDITOR="subl -w"

# zsh tools setup
source /opt/homebrew/share/zsh-autosuggestions/zsh-autosuggestions.zsh
source /opt/homebrew/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
```

To finish being able to use `subl`, you must create the following symlink:
```
ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /opt/homebrew/bin/subl
```
> If you are using an Apple Intel chip or older, then you may have to switch `/opt/homebrew/bin/subl` to `/usr/local/bin/subl`.

Finally add VSCode `code` support via the <a href='https://code.visualstudio.com/docs/setup/mac#_alternative-manual-instructions'>macOS installation guide</a>.