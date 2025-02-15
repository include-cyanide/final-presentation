# 智匯方舟 - 資料的最佳歸宿
16 張投影片, 約19分鍾

[簡報](https://docs.google.com/presentation/d/1wvh-DmrOGys18R4rcZVq60cQsfx7G6JfBUT9D2pDuBc/edit?usp=sharing)
- 故事待補


> [GPT 改進建議 - ver1](https://chatgpt.com/share/67af1298-43e0-800c-85a4-51066d872cdf)
> 1. 痛點闡述和產品價值這兩部分加入更多實例與故事性敘述
> - 目標用戶，痛點，產品比較變成故事
> 2. 根據聽眾背景適當調整各部分時間

> 教授改進建議
> 1. A後，聚焦於想解決的問題，和解決這個問題的困難度
> 2. GPT 是否可以解釋圖所表達的概念


# 1 `Q:(30s)`
在llm發展的時代，重要的能力是什麼
(deep research, notebooklm, o3, learnabout)

# 2 `A:(30s)`
1. 提出問題的能力
  - 前知識很重要(決定問題的品質)
2. 個人知識庫
  - 避免做白工
  - 累積前知識(你問問題之前就知到的知識)
ex: CORS 如果不知道是前端還是後端的問題的話，直接搜找不到答案

# 3 `我們想要解決的問題`(30s)

1. 資料過於零散
    - ex: hackmd, notion, chatgpt問答紀錄
2. 資料整理的問題

:::spoiler `食知無味，棄之可惜的詢問紀錄`
![CleanShot 2025-02-14 at 18.50.09](https://hackmd.io/_uploads/rJIlxs3F1e.png)

![CleanShot 2025-02-14 at 18.52.20](https://hackmd.io/_uploads/rkq_lshYkx.png)
:::


# 4 `困難點`(30s)

1. 要怎麼打通各個程式之間的資料轉移問題
    -  可以以很低的成本銜接未來的新產品
2. 很好的適應未來可能的出現的新應用程式
    - 要有很好的彈性

# 5 `我們的解法`

1. api server
    - 只要寫簡單的插件調用api，就可以快速整合新的方法
2. 良好的架構設計

---

# 6`目標用戶(30s)` - 故事
1. 大量接觸新領域的人
  - 記大量筆記的人
:::spoiler 圖片 - 架設ruby on rails 專案時做的筆記(沒有同時記錄下綱址所以不知道原因，只有操作步驟)
![CleanShot 2025-02-14 at 18.04.04](https://hackmd.io/_uploads/rkULBqht1g.png)
:::
ex: 需要存下分析報告的入, 解決環境問題的系統工程師

故事
- 目標用戶
- 痛點
- 其他產品使用體驗


<!--
1. 照片1 -- chatgpt 尋問topic雜亂
2. 照片2 -- google 搜尋結果對搜尋詞很敏感

:::spoiler 照片1,2
## 痛點1(問了很多輪，但問完之後不知道那裡才是真正需要的答案)


- 照片(chatgpt 問)
![CleanShot 2025-02-13 at 23.08.42](https://hackmd.io/_uploads/SkWGjFjKyg.png)

## 痛點2(因為google對關鍵詞很敏感，想找之前找的資料的時候找不到)

- 照片x2(google search)
![CleanShot 2025-02-13 at 23.23.28](https://hackmd.io/_uploads/HJ50CtiFyx.png)
![CleanShot 2025-02-13 at 23.23.20](https://hackmd.io/_uploads/BJTCRtoF1g.png)
:::

**故事**
:::success


:::

# 5 `目前可以用的工具(兩類)(30s)`
1. 直接存到筆記軟體(ex: notion)
2. 存到資料庫裡面，用rag搜(ex: supermemory)

故事
:::success

:::

# 6 `共有的問題(30s)`
1. 遷移成本高
    - 很難轉移現有的資料庫
3. 只是存下來，少了一個好的結構
    - 資料是一個list, 沒有任何的架構或標注
-->


# 簡介

# 7 `總覽(1min)`
![32128870-2118-41FB-AD06-F34168666197](https://hackmd.io/_uploads/r1zuM9ot1g.jpg)
:::spoiler `gpt`
這張圖片似乎是在描述一個資訊處理與存儲的流程，可能與知識管理或筆記應用（如 Notion）有關。  

大致流程如下：  
1. **資料（暫存記錄）**：這是原始資訊的來源，可能是日常記錄或臨時筆記。  
2. **儲存（save）** 到 **智慧存舟（well-structured data）**：這表示將原始資訊轉化為結構化數據，使其更具組織性與可用性。  
3. **儲存至 Notion（super memory）**：將這些整理好的資訊進一步保存到 Notion 或類似的應用，以作為「超級記憶」的存儲庫。  
4. **應用產品（super memory, Notion, notebook, LLM）**：這些資訊可以被導出（export）到不同的應用，例如 Notion、筆記本（notebook），甚至是 LLM（大型語言模型），以便進一步應用或分析。  

整體而言，這張圖描述了一個從「原始資料」到「結構化存儲」，再到「應用與導出」的知識管理流程。
:::


做為一個中間層

# 8 `產品介紹(1min)`
為了展示整個的流程，我們總共做了以下三個事

1. 資料收集
   - google extension 
   - 直接匯入markdown
2. data base
   - well strcuture databse
3. 資料使用
   - 前端查詢界面
   - 讓gpt調用api獲取資料
   - ex: https://chatgpt.com/share/67af06c0-c70c-800c-9a58-8ea27fdabf08


![CleanShot 2025-02-14 at 17.03.42](https://hackmd.io/_uploads/B1xWDF3Ykx.png)
:::spoiler `gpt`
這張圖片顯示了一個對 Kubernetes（K8s）的基本介紹，並且是來自某個聊天機器人或 AI 助手的回應。  

### 內容概述：
- **問題**：使用者 `guosw` 提出了請求 `/answer 10`，並要求獲取 Kubernetes 的基本概述。  
- **回應**：
  - **Kubernetes (K8s) Overview**（Kubernetes 概述）
  - **What is Kubernetes?**（什麼是 Kubernetes?）  
  - 解釋了 Kubernetes 是一個用於自動化部署、擴展和管理容器化應用的系統。  
  - 提到了 Kubernetes 的幾個核心功能：
    - 在單台或多台機器上部署多個容器。
    - 管理容器的狀態。
    - 在機器之間遷移容器。
    - 為應用提供高擴展性。

### 其他觀察：
- 這可能是一個 AI 驅動的回答系統，如基於 LLM（大型語言模型）的聊天機器人，能夠提供技術知識的簡要回應。
- 背景顯示了一些與 `api.driseam.com` 的交互，可能是與 API 進行溝通的記錄。

### 結論：
這張圖的主要內容是 Kubernetes 的基本介紹，顯示了如何使用 Kubernetes 來管理容器化應用，並且是由某個 AI 助手或自動化系統生成的回應。
:::

![image](https://hackmd.io/_uploads/Hkk_BYhYkx.png)
:::spoiler `gpt`
這張圖片描述了一個資訊處理與應用的流程，核心概念圍繞著「智慧存舟」，可能是一個知識管理系統或數據處理平台。  

### **流程解析**
1. **輸入來源**（左側）：
   - **Chrome extension**（瀏覽器擴展）
   - **Markdown**（標記語言，用於記錄與格式化文本）
   - **ChatGPT**（AI 生成內容或對話）
   - 以及其他可能的數據來源（「...」表示還有更多）。

2. **核心處理系統**（中央）：
   - **智慧存舟**（可能是一個智能知識管理系統），負責整合來自不同來源的資訊並進行存儲與處理。

3. **輸出與應用場景**（右側）：
   - **Frontend UI**（前端介面）
   - **GPT**（可能是 AI 相關應用，例如與 ChatGPT 進一步交互）
   - **Notebook/LM**（筆記應用或大型語言模型的存儲與應用）
   - **Blog**（用於發布文章或知識分享）
   - 以及其他可能的應用（「...」表示更多用途）。

### **總結**
這張圖概述了一個數據處理與應用的架構：
- 來自不同來源（如 Chrome 擴展、Markdown、ChatGPT）的信息被輸入到「智慧存舟」。
- 然後，這些信息可以被導出到不同的應用，如前端 UI、GPT 交互、筆記管理、博客發布等。
- 這可能是一個整合 AI、生產力工具與知識管理的系統。
:::


# 9~11 `程式架構(1m30s)`
![image](https://hackmd.io/_uploads/HkB9FFnFyg.png)

1. nodepool
  - 存下許多的`node`
2. `node`
  - 一個知識單元，可以有很多個知識點在裡面
  - 裡面有`important`,`relate`,`other`這三種類別
3. Project
  - 只負責處理`node`之間的連接

:::spoiler `node structure`
```json
{
  "ID": "GCyyG",
  "title": "12 `demo time(3min)`",
  "important_Data": [
    {
      "url": "<some url>",
      "title": "<Title>",
      "content": "<Content>"
    }
  ],
  "relate_Data": [],
  "other_Data": [],
  "Summary": ""
}
```
:::

:::spoiler `project structure`
```json
{
  "YWmpG": [
    "DoWZO"
  ],
  "nodeTitle": {
    "YWmpG": "Root",
    "DoWZO": "Cors"
  },
  "DoWZO": []
}
```
:::


# 12 `架構優勢(30s)`
1. 將node內資料分成`important`, `relate`, `other`
  - 對於資料更有彈性
 
3. NodePool
  - 不同的project可以共用一個node
# 13 `實際例子`
chrome extension 就可以對於特定網站(ex: stackoverflow) 直接存下來到`relate`或`other`

# 14 `demo time(3min)`
1. import markdown(30s)
2. chrome extension auto load(30s)
3. show the front end ui(1min)
4. chatgpt ability show(1min)

# 15 `未來展望(1min)`
1. 和llm provider一樣的api, 然後篩選有價值的存近database
![image](https://hackmd.io/_uploads/HkJAaFhYye.png)
2. 自動判斷要存在那一個project下
3. 可以存下文檔



# 結論
## 16 `小結(1min)`
當LLM可以直接讓我們獲取答案的時候，如何更好的存取知識會直接決定我們的上限
![32128870-2118-41FB-AD06-F341686661972](https://hackmd.io/_uploads/ryuCE9itJl.jpg)

## 17~18  `我們學到了什麼&使用的工具(1min)`
1. Vue , python, prompt engine
2. 快速迭代
  - 快速做出產品，試用後看有沒有新的突破口
3. 深刻的體會到了"不要只專注於當前AI模型的不足之處，因為這些短板可能隨時會被解決"
- 原本是想要做llm樹狀搜詢問題的，但`deep research`突然出現，後來有感而發，認真思考簡報開頭的問題後才得以改目標


# 16  `QA(5min)`

## Q1: 問題定位與用戶需求

### 你在報告中提到「提出問題的能力」與「個人知識庫」的重要性，能否舉例說明這兩者如何在實際應用中幫助用戶解決具體問題？

**A:**

---

## Q2: 現有工具比較

### 當前市場上像 Notion 或 Supermemory 等工具已經存在，請問「智匯方舟」在解決資料散亂、結構化管理方面有什麼獨到之處？
**A:**

### 你的產品如何降低遷移成本，讓用戶從現有工具順利轉換？

**A:**

---

## Q3: 技術架構與易用性

### 報告中提到的 node、nodepool 與 project 結構是否會讓非技術用戶感到複雜？有沒有設計相應的引導或介面來降低學習曲線？
**A:**

### 在大規模資料管理的情境下，這樣的架構如何保證查詢速度和穩定性？

**A:**


> ## Q4: Demo 展示

> ### 3 分鐘的 demo 時間較短，你如何保證能夠涵蓋產品的核心功能，並且讓聽眾清楚理解產品的價值？

> **A:**

---

## Q5: 未來展望與整合

### 你提到未來會與 LLM provider 整合，能否具體說明整合的技術路線和可能面臨的挑戰？

**A:**

### 在產品迭代和新功能推出方面，有沒有一個明確的時間表或路線圖？

**A:**

---

## Q6: 資料安全與隱私

### 對於儲存和管理用戶知識的過程中，資料安全和隱私保護是非常重要的一環，你有哪些具體措施來保護用戶資料？

**A:**
對於`api`的部份，我們將來會使用`Oauth`等使用`google`帳戶驗證的方式

---

## Q7: 用戶反饋與市場驗證

### 目前是否已經有實際用戶試用這個產品？從用戶反饋中學到了哪些關鍵點，有沒有改進的具體案例？

**A:**
目前是我們組內的組員都試用過了，其中一個改進點是原本我們的`extension`

