#程式語言教學與技術文件 #Google派系 #Flutter #Flutter基本教學
# Flutter安裝教學(除Windows全平台)

大家都知道Mac/Linux是非常相像的，CPU平台也有x86/ARM架構，裝的軟體也不太一樣，但Flutter的下載平台其實只給了這三個平台的**x86**版本，所以現在要教大家整個通用的方式。

## 不管怎樣，Git clone就是無敵啦!
Git Clone包含了所有平台跟架構的Flutter支援，所以可以直接做去用，Windows也可以，就是取代了直接去官網下載的步驟改用git clone而已。

接下來，我們先來做Git clone，建議先在家目錄建立"development"這個資料夾下處理比較好喔~

```bash

git clone https://github.com/flutter/flutter.git

```

接下來他就會把flutter的原始碼Download進來，就會出現「flutter」這個資料夾，跟你去官網解壓縮的檔案是一模一樣的，這途中他也會自己去抓你是哪個平台的，CPU是哪個架構的，自動適應並下載適當的內容。

## 建立環境變數(Mac/Linux特用)

接下來就是要建立環境變數以方便你去呼叫 flutter，要把以下文字寫進去環境變數檔內，如果你是用bash，那你的環境變數就是.bashrc，如果是zsh，那就是zshrc，Windows的話自己去看Windows的基礎安裝。

```bash
export PATH="$HOME/development/flutter/bin:$PATH"
```

這段文字其實是從Flutter教學官網魔改來的，因為原本的"~/"會抓不到，所以改用$HOME來跑就會正常，這裡也可以知道為什麼當初要加development資料夾的原因了。

最後，git給的Flutter統一都是dev的版本，如果你是要穩定的stable版本，請下這個指令：

```bash
flutter channel stable
```

## 開始Flutter doctor!

接下來就可以開始Flutter doctor來檢查每個相依性元件了，就依據他的需求去做安裝跟處理就好，缺Android Studio就裝Android Studio，缺什麼元件就裝什麼元件就好了。

```bash
flutter doctor
```

## 同場加映：ARM Linux Chrome安裝(樹莓派)

Flutter doctor有一個選項就是，如果要針對Web除錯，首要的元件就是必須要安裝Google Chrome，當然對於x86的Windows、Linux，還有x86/Apple Silicon的Mac都是直接安裝就好，但Linux的Arm64版本可是沒有Chrome可以支援的，那要怎麼辦呢?

目前Linux ARM有支援的正規瀏覽器只有極度支持自由軟體的Firfox，而Chrome目前是不支援的，所幸Chrome是Google的專有版本之一，他有開放原始碼版本，與之相同核心的Chromium，很多的大陸瀏覽器、Microsoft Edge都是用Chromium的核心去做開發的，而Chromium因為是開放原始碼，所以在ARM64的Linux平台下成為了唯二能支援的瀏覽器，這也是我們有機會可以在ARM架構下原生執行的Chrome瀏覽器。

### 大正小道消息--Chromium的淫威(笑死)
Google的主力瀏覽器就是Chrome瀏覽器，當年跟著Firefox火狐橫掃Windows瀏覽器市場，讓大家使用Windows不用在屈服於IE的絕對武力下，慢慢的IE被這兩個大傢伙一舉殲滅，即使微軟不斷更新也毫無用處。

而Goolgle後期將Chrome的核心開放原始碼，成為了後來的Chromium瀏覽器，也被稱為開源的Chrome，後來很多瀏覽器都是採用他的核心做建造，大陸很多瀏覽器就是這樣搞的，後來聲名大噪後殲滅了IE，雖然微軟也不認輸開發了自家的Edge，但還是被壓在地上扁，最後放棄抵抗加入他們(打不贏就加入QQ)，現今的Microsoft Edge就是以Chromium為核心做的，可以說是Chrome的大勝利。

目前還在頑強抵抗，使用與Chromium完全不同的核心基礎的，只有支持自由軟體的Mozilla Firfox了，但現在好像也快被殲滅了的說....

### 大正小道消息講完了，那要怎麼在ARM 64 Linux安裝Chrome?

剛剛已經說過，Chromium跟FireFox是唯二支援ARM64 Linux架構的瀏覽器，**而Chromium的核心跟Chrome的核心是一模一樣的，這就代表可以利用Chromium來代替GoogleChrome**，接下來就來看怎麼代替吧

1. 安裝chromium
要安裝chromium很簡單，只要這樣就可以：
```bash
sudo apt install chromium-browser -y
```
2. 設定chroium作為預設chrome(騙flutter chromium是chrome)
```bash
export CHROME_EXECUTABLE="/usr/bin/chromium"
```
這部分可以取決於你的chromium位置在哪裡，接下來你去打flutter doctor，就可以看到綠色勾勾囉~