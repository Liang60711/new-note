# 語言特點
1. 支持多線程，且多線程效率高。
2. 企業級程式語言。
3. 語法簡潔 (25個關鍵字)

<br/>

# windows安裝
1. 安裝 msi 檔案
2. 環境變數設置，預設值為`%USERPROFILE%/go`，可自訂為其他路徑。
3. 使用者環境變數 `GOPATH` 改成自訂目錄
4. 使用者環境變數 `PATH` 加入 `.go\bin` 路徑
5. 使用指令查看 `GOPATH` 和 `GOROOT`

    * `GOPATH`: 工作區 (workspace) 的概念，可以把所有的 Go 專案與第三方 package 都放在此目錄中。
    * `GOROOT`: 安裝Golang語言內建的程式庫的所在位置。

    ```shell
    # 查看 GO 配置
    go env
    ```

<br/>

# 目錄結構
* src: 存放原始碼。
* pkg: 編譯後生成的檔案。
* bin: 編譯後生成的可執行檔案。
