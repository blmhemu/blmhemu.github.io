+++
title = "Faster ZSH with zsh snap"
description = "My experiments with plugin managers and how I ended up using zsh-snap."
date = 2021-08-02

[taxonomies]
tags = ["zsh", "zsh-snap", "znap"]
+++

## Intro
Although not as ubiquitous as bash, zsh has many advantages over it. While fish is an even better shell than zsh, it does not offer the same level of **run any script &trade;** advantage like zsh.

## Plugins Managers
To get the features offered by fish and more, people have created many plugins to make life easier. But who manages all these plugins ? Ofcourse the plugin managers. People new to ZSH are commonly introduced to [oh-my-zsh](https://ohmyz.sh/), an excellent software, easy to use, and integrates easily with most plugins. But after some time, as the number of plugins increase, the shell startup time increases. This is the major pain point of using this framework. Many plugin managers were created to alleviate this pain point. One of which I used is [zinit](https://zdharma.github.io/zinit/wiki/). Although it is a great plugin manager, it had a complex and very elaborate syntax. Though I stuck to it for some time, I recently found out [zsh-snap](https://github.com/marlonrichert/zsh-snap)

## Enter zsh-snap
Znap (short for zsh-snap) provides you all the advantages of zinit minus the complexity. Here is a snippet of my zsh configuration
```
source ~/.znap/zsh-snap/znap.zsh

# Prompt
znap eval starship 'starship init zsh --print-full-init'
znap prompt

# Completion functions
fpath+=( ~[ohmyzsh/ohmyzsh]/plugins/{docker,fd,ripgrep} )
znap compdef _rustup 'rustup completions zsh'
znap compdef _cargo  'rustup completions zsh cargo'

# Plugins
znap source zsh-users/zsh-autosuggestions
znap source zsh-users/zsh-syntax-highlighting
znap source wfxr/forgit

znap source sorin-ionescu/prezto modules/{environment,history}
znap source ohmyzsh/ohmyzsh 'lib/(*~(git|theme-and-appearance).zsh)' plugins/{git}

# Evals
znap eval zoxide "zoxide init zsh"

# -- snipped --
```

Recent plugin managers seem to embrace the idea of time to value (loading the prompt first) and let the user use a shell while loading the plugins asynchronously in the background. The same behavior can be seen in the config as well. We first load the prompt (I use [starship](https://starship.rs/)), then install some completions, load a few plugins, run some inits, and done! Znap takes care of caching and will intelligently store data without running all commands on each run.

Love something in oh-my-zsh or prezto? You can use the libs/plugins like any other plugins.

## Plugins
* [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions) - Gives hints based on your history.
* [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting) - Why should programming langs have all the ~~fun~~ colors ? Adds syntax colors for zsh commands.
* [forgit](https://github.com/wfxr/forgit) - Forget Git ! Adds some flavour to git.

Here is my "shell" tour:
<script id="asciicast-428370" src="https://asciinema.org/a/428370.js" async></script>
