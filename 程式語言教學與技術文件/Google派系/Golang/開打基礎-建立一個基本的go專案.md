#程式語言教學與技術文件 #Google派系 #Golang 
# 開打基礎-建立一個基本的go專案

一般來說，Golang其實只要一個go檔案就可以開始編譯，這個特性其實跟PHP可以說是有異曲同工之妙，但PHP並無法單獨執行，他必須搭配Apache來替他轉換編譯才可以，而Golang他自己就能自帶代理伺服器(類似Apache)的功能，或是開通Port後編譯成執行檔來使用，並不需要其他的東西來協助他，是非常方便的後端開發語言，我們可以來比較一下我們之前用過的程式語言。

| 程式語言與比較 | Go | C | PHP | Dart | C# |
| --- | --- | --- | --- | --- | --- |
| 主要應用範圍 | 後端與底層 | 韌體與底層 | 後端 | 前端介面 | 後端與Windows |
| 可否編譯 | 可 | 可 | 不可 | 可 | 可 |
| 平台範圍 | Windows、Linux、Mac | Windows、Linux、Mac、MCU | Windows、Linux、Mac(與Apache同步) | Windows、Linux、MacOS
(Fullter支援Android、iOS、Web) | Windows Only
(.NET Core可支援Linux跟Mac) |
| CPU架構 | Arm，x86 | Arm，x86 | Arm,x86 | Arm,x86 | Arm(.NET Core)
x86 |
| 最小編譯架構 | 單檔案 | 單檔案 | 單檔案 | 專案 | 專案 |
| 型別 | 靜態強型別 | 靜態弱型別 | 動態弱型別 | 靜態強型別 | 靜態強型別 |
| 是否是物件導向 | 否(但支援介面) | 否 | 否 | 是 | 是 |

雖然go可以單獨做編譯，但他也是可以做成專案來做使用的，接下來我們就來看一下如何手動建立一個go專案：

## 一、用單一檔案開始go

- 在你要的目錄下面直接創建一個 main.go檔案
- 寫好你的main.go程式碼
- 執行 `go run main.go` 就可以執行(編譯請看編譯章節)

## 二、用專案方式開始go

- 先建立一個資料夾當專案資料夾
- 先建立go.mod，執行 `go mod init <module name>` (模組名稱可以用專案的資料夾名稱)
- 然後執行 go mod tidy

注意事項：

1. 使用Package時，不可以放在同一個資料夾內，要建立新的Packge就要建立新的目錄
2. 使用GOPATH的套件管理方式跟mod.go那種的本地引用方式不同

ex：

GOPATH： import("./資料夾")

mod.go ： impaort("modname/資料夾")

## 三、基本範例

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

這是一個基本的 Go 語言 "Hello, World!" 程式。讓我們來解釋一下這段程式碼：

1. `package main`：這行聲明了程式所屬的包。主程式必須屬於 main 包。
2. `import "fmt"`：這行引入了 fmt 包，它包含了格式化 I/O 的函數。
3. `func main()`：這是程式的入口點。當執行程式時，會從這個函數開始。
4. `fmt.Println("Hello, World!")`：這行使用 fmt 包中的 Println 函數來輸出 "Hello, World!" 到控制台。

要執行這段程式，你可以將它保存為 main.go，然後在終端機中執行 `go run main.go`。你應該會看到輸出 "Hello, World!"。