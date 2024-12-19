#程式語言教學與技術文件 #好用工具
# Linux/Mac 的漂亮終端機- oh my zsh

既然微軟有漂亮的 oh my posh，那 Mac/Linux 怎麼能少漂亮終端介面呢?這種漂亮終端介面還是 Mac/Linux 先開始的，我們一起來看看這個新的東西--oh my posh

## oh-my-zsh 跟 oh-my-posh 的不同

oh-my-zsh 跟 oh-my-posh 其實是差不多的東西，<span class="red-text"><u>只是 oh-my-zsh 是特別針對終端服務為 zsh 來做設計，而 oh-my-posh 則是特別針對終端服務為 pwsh 來做設計的</u></span>，也就是 Windows 的 PowerShell，所以才會有在微軟 Windows 使用 oh-my-posh，而在 MacOS 使用 oh-my-zsh 的狀況，因為 MacOS 主要的使用終端服務為 zsh，但請注意，<span class="red-text">Linux 的主要終端服務其實是 bash</span>，他也有一個漂亮終端機套件為 oh-my-bash，只是因為 zsh 與 bash 有幾乎相近的能力，zsh 還更加強大。且 Linux 可以輕鬆安裝 zsh，所以就一起用了，這是三大系統的終端表格：

| 作業系統 | 主終端服務 | 可加裝服務 | 使用套件 |
| --- | --- | --- | --- |
| Windows | Power Shell | 無   | oh-my-posh |
| Linux | bash | zsh | oh-my-bash/oh-my-zsh |
| MacOS | zsh(早期 bash) | bash(已內建) | oh-my-bash/oh-my-zsh |

這樣你就知道為什麼很多前後端都喜歡用 Mac 了，因為 Linux 跟 Mac 非常像，所以才有人說 Mac 根本是漂亮、主流軟體支援最多、最適合跟 Windows 比拚桌面電腦的 Linux 阿~~(其實是 Linux 像 Mac)

備註：以前的 MacOS 也是用跟 Linux 同根同源的 bash，因 Apple 政策才改為 zsh，但其實 MacOS 在 Recovery 的主終端服務跟私底下還是有 bash 可以用喔~

## 如何安裝 oh-my-zsh

看這個就好

[Ubuntu 安裝 Zsh + Oh My Zsh + Powerlevel10k 與各種插件](https://www.kwchang0831.dev/dev-env/ubuntu/oh-my-zsh)

## 同場加映：zsh 沒有 bash 的 command-not-found 的提示怎麼辦?

加上這個：

```bash
    $ sudo apt install command-not-found
    $ echo "source /etc/zsh_command_not_found" >> ~/.zshrc
    $ exec zsh
```

這樣就會有沒安裝但會給 install 提示的功能了