# Установка и настройка терминала Alacritty + оболочки fish
##### Устанавливаем Alacritty и  fish
> `sudo dnf install alacritty fish`
> 
> `sudo apt install alacritty fish`
> 
> `sudo pacman -S alacritty fish`

##### Устанавливаем fish оболочкой по-умолчанию
`chsh -s /usr/bin/fish`
После релогина fish станет дефолтным шеллом.

##### Устанавливаем  `oh my fish`
> `curl -L https://get.oh-my.fish | fish`

##### Устанавливаем тему `fishbone`
> `omf install fishbone`

##### Устанавливаем шрифт `mononoki`
> `curl -O https://github.com/madmalik/mononoki/releases/download/1.3/mononoki.zip`
> 
> `unzip mononoki.zip -d mononoki`
> 
> `mv mononoki ~/.fonts`
> 
> `fc-cache -f -v`

##### Создаем конфиг Alacritty
> `nvim ~/.alacritty.yml`

Добавляем в файл следующие строки(настройка внешнего вида alacritty, установка шрифтов и цветовой схемы):

```
window:
  padding:
   x: 15
   y: 15
font:
  normal:
    family: mononoki
    style: Regular

  bold:
    family: mononoki
    style: Bold

  italic:
    family: mononoki
    style: Italic

  bold_italic:
    family: mononoki
    style: Bold Italic

  size: 11
# Colors (Gruvbox dark)
colors:
  # Default colors
  primary:
    # hard contrast: background = '0x1d2021'
    background: '0x282828'
    # soft contrast: background = '0x32302f'
    foreground: '0xebdbb2'

  # Normal colors
  normal:
    black:   '0x282828'
    red:     '0xcc241d'
    green:   '0x98971a'
    yellow:  '0xd79921'
    blue:    '0x458588'
    magenta: '0xb16286'
    cyan:    '0x689d6a'
    white:   '0xa89984'

  # Bright colors
  bright:
    black:   '0x928374'
    red:     '0xfb4934'
    green:   '0xb8bb26'
    yellow:  '0xfabd2f'
    blue:    '0x83a598'
    magenta: '0xd3869b'
    cyan:    '0x8ec07c'
    white:   '0xebdbb2'