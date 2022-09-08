# Fedora Workstation setup

I switched to fedora not too long ago and it has worked like a charm, therefore i wanted to make a guide mainly for my own benefit, to remember what i use on a daily basis.

## DNF config file

There are some small changes i make in the DNF config file to make it perform a little bit better.

```
[main]
gpgcheck=True
installonly_limit=3
clean_requirements_on_remove=True
best=False
skip_if_unavailable=True
fastestmirror=True
max_parallel_downloads=10
defaultyes=True
keepcache=True
```

## DNF installation

```
sudo dnf install \
alacritty \
git \
bat \
jq \
httpie \
zsh \
vim \
gnome-tweaks \
gnome-extensions-app \
remmina \
util-linux-user \
sqlite \
starship
```

## Oh-My-ZSH

```
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

## Flatpak

```
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

## Flatpak install

```
flatpak install -y discord spotify
```

## Albert Launcher

```
dnf config-manager --add-repo https://download.opensuse.org/repositories/home:manuelschneid3r/Fedora_36/home:manuelschneid3r.repo
dnf install albert
```

## VSCode

```
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
```

```
dnf check-update
sudo dnf install code
```

## Kubectl

```
cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-\$basearch
enabled=1
gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF
sudo yum install -y kubectl
```

## Helm

```
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

## Alacritty Config

Alacritty uses a yaml file to configure its settings, the file should be stored at ~/.config/alacritty/alacritty.yaml

```
selection:
  save_to_clipboard: true

window:
  padding:
    x: 5
    y: 5

  opacity: 0.9

font:
  normal:
    family: Inconsolata
    style: Regular

  size: 15

cursor:
  style:
    shape: Beam

scrolling:
  history: 10000
  multiplier: 3

key_bindings:
  - {key: Return, mods: Super|Shift, action: SpawnNewInstance}
```

## ZSH Config

zshrc config

```
# If you come from bash you might have to change your $PATH.
# export PATH=$HOME/bin:/usr/local/bin:$PATH

# Path to your oh-my-zsh installation.
export ZSH="$HOME/.oh-my-zsh"

# Set name of the theme to load --- if set to "random", it will
# load a random theme each time oh-my-zsh is loaded, in which case,
# to know which specific one was loaded, run: echo $RANDOM_THEME
# See https://github.com/ohmyzsh/ohmyzsh/wiki/Themes
ZSH_THEME="eastwood"

# Set list of themes to pick from when loading at random
# Setting this variable when ZSH_THEME=random will cause zsh to load
# a theme from this variable instead of looking in $ZSH/themes/
# If set to an empty array, this variable will have no effect.
# ZSH_THEME_RANDOM_CANDIDATES=( "robbyrussell" "agnoster" )

# Uncomment the following line to use case-sensitive completion.
# CASE_SENSITIVE="true"

# Uncomment the following line to use hyphen-insensitive completion.
# Case-sensitive completion must be off. _ and - will be interchangeable.
# HYPHEN_INSENSITIVE="true"

# Uncomment one of the following lines to change the auto-update behavior
# zstyle ':omz:update' mode disabled  # disable automatic updates
# zstyle ':omz:update' mode auto      # update automatically without asking
# zstyle ':omz:update' mode reminder  # just remind me to update when it's time

# Uncomment the following line to change how often to auto-update (in days).
# zstyle ':omz:update' frequency 13

# Uncomment the following line if pasting URLs and other text is messed up.
# DISABLE_MAGIC_FUNCTIONS="true"

# Uncomment the following line to disable colors in ls.
# DISABLE_LS_COLORS="true"

# Uncomment the following line to disable auto-setting terminal title.
DISABLE_AUTO_TITLE="true"

# Uncomment the following line to enable command auto-correction.
ENABLE_CORRECTION="true"

# Uncomment the following line to display red dots whilst waiting for completion.
# You can also set it to another string to have that shown instead of the default red dots.
# e.g. COMPLETION_WAITING_DOTS="%F{yellow}waiting...%f"
# Caution: this setting can cause issues with multiline prompts in zsh < 5.7.1 (see #5765)
COMPLETION_WAITING_DOTS="true"

# Uncomment the following line if you want to disable marking untracked files
# under VCS as dirty. This makes repository status check for large repositories
# much, much faster.
# DISABLE_UNTRACKED_FILES_DIRTY="true"

# Uncomment the following line if you want to change the command execution time
# stamp shown in the history command output.
# You can set one of the optional three formats:
# "mm/dd/yyyy"|"dd.mm.yyyy"|"yyyy-mm-dd"
# or set a custom format using the strftime function format specifications,
# see 'man strftime' for details.
# HIST_STAMPS="mm/dd/yyyy"

# Would you like to use another custom folder than $ZSH/custom?
# ZSH_CUSTOM=/path/to/new-custom-folder

# Which plugins would you like to load?
# Standard plugins can be found in $ZSH/plugins/
# Custom plugins may be added to $ZSH_CUSTOM/plugins/
# Example format: plugins=(rails git textmate ruby lighthouse)
# Add wisely, as too many plugins slow down shell startup.
plugins=(git sudo kubectl zsh-autosuggestions terraform)

source $ZSH/oh-my-zsh.sh
source <(kubectl completion zsh)
# User configuration

# export MANPATH="/usr/local/man:$MANPATH"

# You may need to manually set your language environment
# export LANG=en_US.UTF-8

# Preferred editor for local and remote sessions
# if [[ -n $SSH_CONNECTION ]]; then
#   export EDITOR='vim'
# else
#   export EDITOR='mvim'
# fi

# Compilation flags
# export ARCHFLAGS="-arch x86_64"

# Set personal aliases, overriding those provided by oh-my-zsh libs,
# plugins, and themes. Aliases can be placed here, though oh-my-zsh
# users are encouraged to define aliases within the ZSH_CUSTOM folder.
# For a full list of active aliases, run `alias`.
#
# Example aliases
# alias zshconfig="mate ~/.zshrc"
# alias ohmyzsh="mate ~/.oh-my-zsh"
#
# Custome Aliases
alias dc='docker-compose'
export KUBECONFIG=./kubeconfig
eval "$(starship init zsh)"
export USE_GKE_GCLOUD_AUTH_PLUGIN=True
ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=3'
alias fjson="jq -R -r -C '. as \$line | try fromjson catch \$line'"
```

## Starship config

I use the following config file, file should be located at ~/.config/starship.toml

```
format = """
$username\
$hostname\
$shlvl\
$directory\
$kubernetes\
$git_branch\
$git_commit\
$git_state\
$git_status\
$hg_branch\
$package\
$golang\
$helm\
$kotlin\
$nim\
$nodejs\
$rust\
$terraform\
$vagrant\
$nix_shell\
$memory_usage\
$env_var\
$custom\
$cmd_duration\
$line_break\
$lua\
$jobs\
$battery\
$time\
$status\
$character"""

# Don't print a new line at the start of the prompt
add_newline = false

# Replace the "❯" symbol in the prompt with "➜"
[character]                            # The name of the module we are configuring is "character"
success_symbol = "[➜](bold green)"     # The "success_symbol" segment is being set to "➜" with the color "bold green"
error_symbol = "[➜](bold red)"     # The "success_symbol" segment is being set to "➜" with the color "bold green"

[directory]
truncation_length = 3
truncation_symbol = "…/"

[kubernetes]
format = '[$symbol\[$namespace\] $context](blue) '
disabled = false
```

## Gnome beautification

Default gnome leaves a lot to be desired for me at least, this section basically makes gnome look like MacOS

### Fonts

```
sudo dnf install google-roboto-fonts
```

### Icons

https://github.com/vinceliuice/WhiteSur-icon-theme

### Theme

https://github.com/vinceliuice/WhiteSur-gtk-theme

### Cursor

https://github.com/varlesh/volantes-cursors

## Uninstallation

```
sudo dnf remove \
gnome-terminal
```
