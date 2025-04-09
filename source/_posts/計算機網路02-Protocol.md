title: '[計算機網路 02]  Protocol'
catalog: true
author: Rex
tags:
  - 計算機網路
categories:
  - 計算機網路
date: 2025-04-08 22:08:00
subtitle:
header-img:
---
### 🔹 **Protocol（通訊協定）**

> **Protocol defines the language of transmission**  
> → 協定定義了資料傳輸的「語言」

#### 解釋：
- 通訊協定就是「不同系統之間溝通的共同語言與規則」。
- 它們定義：
  - **格式（Format）**：資料怎麼包裝（如 JSON、XML）
  - **規則（Rules）**：什麼時候傳？怎麼應答？
  - **功能（Functionality）**：例如錯誤檢查、重傳、加密等

#### 📌 舉例：
- TCP（傳輸控制協定）：可靠傳輸、重送機制
- HTTP（網頁協定）：用於網頁瀏覽器與伺服器間的資料交換

---

### 🔹 **Protocol Data Unit (PDU)**

> **PDU contains layer-specific information necessary for a message to be transmitted through a network**  
> → 協定資料單元包含了「特定層級」需要的資訊，才能正確傳輸訊息。

#### 💡 解釋：
- PDU 是「資料封包的單位」，每一層在處理資料時都會加入自己的資訊。
- 不同層有不同的 PDU 名稱：
  - 應用層 ➜ 資料（Data）
  - 傳輸層 ➜ 區段（Segment）
  - 網路層 ➜ 封包（Packet）
  - 資料鏈結層 ➜ 框架（Frame）

---

### 🔸 每一層都會加上自己的 PDU

> **Each layer adds a PDU**

- 例如你在瀏覽器輸入網址，資料從應用層一路往下，TCP 加上 port 資訊，IP 加上 IP 位址，Ethernet 加上 MAC 位址… 一層層包起來。

---

### 🔸 PDU 就像「巢狀信封」

> **PDUs act like nested envelopes**

#### 💡 解釋：
- 想像你寫了一封信（應用層資料），
- 把它裝進一個信封（TCP 區段），
- 外面再包一層大的信封（IP 封包），
- 最後貼上地址與收件人（乙太網框架）寄出。

---

### 🔸 **Encapsulation（封裝）**

> **Occurs when a higher level PDU is placed inside of a lower level PDU**

#### 💡 解釋：
- 「封裝」就是把上一層的資料當作 payload，包在下一層的 PDU 裡面。
- 每經過一層，就加上一層「包裝紙」。
- 封裝是資料往下走的過程；資料從另一端進來時則是解封裝（Decapsulation）。

#### 📌 舉例：
1. 你傳送一封 Email：
   - 應用層：你的信件內容（Email）
   - 傳輸層：加上 TCP 標頭（source/destination port）
   - 網路層：加上 IP 標頭（source/destination IP）
   - 資料鏈結層：加上 MAC 地址與 frame 頭尾

2. 對方收到封包時，從最外層開始一層層「拆信」還原資料