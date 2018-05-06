# Fish

* [fish-shell cookbook](https://github.com/JorgeBucaran/fish-shell-cookbook)
* [bat - like cat](https://github.com/sharkdp/bat)

## Config

Create `~/.config/fish/config.fish`

```
set -gx LANG en_US.UTF-8
set -gx EDITOR vi

set -gx AWS_REGION ap-southeast-1

set PATH $HOME/.rbenv/shims $PATH
set -g fish_user_paths "/usr/local/opt/mongodb@3.0/bin" $fish_user_paths
rbenv rehash >/dev/null ^&1
```

## Right Prompt

```
function fish_right_prompt
  set_color red
  echo "Ruby v"(rbenv version | awk '{print $1}')
  set_color normal
end
```

