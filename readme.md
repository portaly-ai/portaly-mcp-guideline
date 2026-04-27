# **Portaly MCP \- AI 串接工具** 

**分類：**AI 工具 / 電商應用 / 生產力工具　閱讀時間：約 8 分鐘

## **什麼是 MCP？**

MCP（Model Context Protocol）是由 Anthropic 提出的開放協議，讓 AI 模型可以安全地連接並操作外部服務。

*如果說語言模型是一個聰明的顧問，那 MCP 就是給顧問配了一雙手，他可以直接幫你打開系統、建立資料、完成任務。*

## **Portaly MCP 能做什麼？**

透過 Portaly MCP，你可以對 AI 說：

*「幫我建立一個商品，名稱是『十年店家經營心得』，定價 NT$1,280，附上商品描述。」*

AI 就會直接呼叫 Portaly API，在你的後台建立商品，你甚至不需要打開 Portaly 管理介面。

目前支援的功能包括：

* 建立商品（設定名稱、價格、描述等）  
* 查詢商品列表  
* 取得單一商品資訊  
* 更新商品內容  
* 切換商品開關狀態

## **設定教學：三步驟 5 分鐘完成 Portaly MCP 串接**

### **第一步：取得 MCP Token**

* 前往 Portaly 後台 \>「經營工具 \> MCP 管理」  
* 點擊「建立 MCP Token」  
* 複製產生的 Token（格式類似 mcp\_ptly\_xxxxxxxx）

  ***⚠️ 安全提醒：**Token 等同帳號存取權限，請勿分享給他人或公開在程式碼中。*

### **![](.\/images/1.jpg)**

![](.\/images/2.jpg)

### **第二步：選擇你的 AI 工具並設定**

你可以選擇用 Claude Desktop 或 OpenAI Codex 來使用 Portaly MCP，兩者都支援。以下分別說明設定方式。

#### **方法 A：使用 Claude Desktop**

* 打開 Claude Desktop 應用程式  
* **前往 Settings → Developer**  
* 找到「Edit Config」或直接開啟設定檔案「 claude\_desktop\_config.json」


* 新增 Portaly MCP 設定，在設定檔中貼上以下內容（mcpServers 區塊）：


  {                                                                                                       

  	"mcpServers": {                                                                  

      "portaly": {

        "command": "npx",

        "args": \["-y", "@portaly-ai/portaly-mcp"\],

        "env": {

          "PORTALY\_API\_TOKEN": "mcp\_ptly\_xxx"

        }

      }

    }

  }


* 重新啟動 Claude Desktop

儲存設定檔後，完全關閉 Claude Desktop 再重新開啟。

![](.\/images/3.jpg)![](.\/images/4.jpg)

#### **方法 B：使用 OpenAI Codex CLI**

* 打開 GPT Codex → Settings → MCP 伺服器  
* 選擇 “標準輸入/輸出” tab ，輸入以下資訊  
* 啟動指令輸入：npx  
* 引數輸入：-y @portaly-ai/portaly-mcp  
* 環境變數：PORTALY\_API\_TOKEN \= \<在後台請求的 MCP Token\>  
  *   
  * ![](.\/images/5.jpg)

### **第三步：確認連線成功**

在對話框中輸入：

你可以使用 Portaly MCP 嗎？列出目前可用的工具。

如果看到 AI  列出 listProducts、createProduct 等工具，代表設定成功！

#### **![](.\/images/6.jpg)**

## **實戰演示：用 AI 建立商品**

設定完成後，直接在對話框輸入自然語言指令，AI 就會幫你完成操作。

### **範例 1：建立一個新商品**

**你輸入：**

幫我在 Portaly 建立一個新商品：- 名稱：十年店家經營心得- 價格：NT$550- 描述：餐飲店家涵蓋選址、定價、客群分析等全攻略 150 頁電子書精華

商品連結:https://docs.google.com/document/d/testproduct

接著去 Portaly 後台，就能看到新商品已經出現了。  
![](.\/images/7.jpg)

### **範例 2：查詢並更新商品**

**你輸入：**

列出我目前所有商品，然後把「十年店家經營心得」的價格改成 NT$980

AI 會取得商品列表，找到目標商品 ID，再完成更新——全程你只需要說一句話。

![](.\/images/8.jpg)

### **範例 3：批次管理商品上下架**

**你輸入：**

把目前所有售價低於 NT$1000 的商品暫時關閉

這種需要判斷 \+ 批次操作的任務，以往需要人工一筆一筆處理；有了 MCP，AI 可以自動篩選並執行。

![](.\/images/9.jpg)

## **常見問題 FAQ**

### **Q：設定完重啟後還是連不到，怎麼辦？**

試試看用工作管理員（Windows）或活動監控器（macOS）把 Claude 的所有背景程序完全關掉，再重新啟動。有時候 Claude 會有背景程序殘留。

### **Q：Token 安全嗎？會不會被盜用？**

Token 只存在你的本機設定檔中，不會傳送到 Portaly 以外的服務。但還是建議不要把包含 Token 的設定檔上傳到 GitHub 等公開平台，可以用環境變數管理取代明文儲存。

## **總結**

**Portaly MCP 能讓 AI 代替你操作介面。**

透過這篇教學，你可以：

* 在 5 分鐘內完成 Claude Desktop 或 Codex 的 MCP 設定  
* 用自然語言建立、更新、管理 Portaly 商品  
* 把重複性的後台操作交給 AI，專注在更有價值的事情上

**立即開始：**

* Portaly 後台 → [MCP 管理](https://portaly.cc/admin/mcp) — 取得你的 MCP Token  
* Claude Desktop  → [claude.ai/download](http://claude.ai/download) — 安裝 Claude 桌面版  
* Codex Desktop →  [https://chatgpt.com/codex/cloud](https://chatgpt.com/codex/cloud) — 安裝 Codex 桌面版

如果想了解更多數位商品的內容，可以參考：

* [創作者「數位商品」怎麼賣？新手完整攻略與五大平台比較](https://portaly.cc/blog/digital-products-sell)  
* [Portaly 教學：如何使用「數位商品」功能進行實體商品預購？](https://portaly.cc/blog/preorder)  
* [Portaly 教學：如何使用數位商品](https://portaly.cc/blog/digital-goods)

## **作者介紹**

Portaly 台灣團隊開發的創作者商務平台，提供 Link-in-Bio 個人頁面、數位商品銷售與品牌合作媒合工具，幫助創作者將內容影響力轉化為收入。