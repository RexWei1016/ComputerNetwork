title: 網路模型的層級化設計（Layered Architecture）
catalog: true
author: Rex
tags:
  - 計算機網路
categories:
  - 計算機網路
date: 2025-04-08 22:22:00
subtitle:
header-img:
---
### ✅ **Advantages of Layers（層級架構的優點）**

---

#### 1. **模組化設計（Modularity）**
> Networking functionality is modular and the software/hardware at any layer can be more easily substituted

##### 💡 說明：
- 每一層只專注在自己的功能，比如：
  - 實體層：負責實際傳輸（例如光纖、電纜）
  - 資料鏈結層：處理 MAC 位址、錯誤偵測
  - 傳輸層：處理可靠傳輸、流量控制

- **模組化代表：** 一層改變不會影響其他層

##### 📦 範例：
> **Substitute wired for wireless at the physical layer**  
你可以把原本用網路線的 LAN，換成 Wi-Fi，只需改變**實體層硬體**，上層像 TCP、HTTP 都不受影響。

---

#### 2. **方便除錯與維護**
> Easier to troubleshoot or make changes to one layer at a time

##### 💡 說明：
- 有問題時，只需針對那一層進行檢查與修正。
  - 比如：若 TCP 連線斷掉，只查「傳輸層」的連線狀態。
- 類似物件導向中的封裝與責任分離。

---

#### 3. **讓開發者專注在應用層**
> Application developers only need to worry about the application layer in their programs

##### 💡 說明：
- 你寫 Web 應用程式時，只要懂 HTTP、API，根本不需處理底層封包、路由、MAC。
- 上層不需知道底層是 IPv4、IPv6、光纖或電纜，**抽象化帶來開發效率提升。**

---

### ❌ **Disadvantages of Layers（層級架構的缺點）**

---

#### 1. **效率不佳：每層封裝都需處理**
> Inefficient because the encapsulation/de-encapsulation at each layer requires processing

##### 💡 說明：
- 傳送端：資料要一層層「包裝」（Encapsulation）
- 接收端：要一層層「拆封」（Decapsulation）
- 每一層都需 CPU 處理，增加延遲與資源使用

##### 📦 範例：
- 一個小訊息，經 TCP 加標頭、IP 加標頭、Ethernet 加標頭……處理時間累積起來，效能下降

---

#### 2. **封裝導致的額外負擔（Overhead）**
> Inefficient because encapsulation in a PDU increases overhead at each layer

##### 💡 說明：
- 每層 PDU 都會加上額外資訊（如標頭 Header）
- 傳輸一個小訊息時，「控制資訊」可能比實際資料還多！

##### 📦 範例：
- 傳送「OK」兩個字，實際封包可能有 40~60 byte 的 header，加總超過內容本身。

---

## 🧠 小結（整理成表格）

| 分層優點 | 說明 |  
|--------|------|
| 模組化 | 每層獨立、可替換 |
| 易於維護 | 問題可侷限在單一層處理 |
| 易於開發 | 上層應用程式不需懂底層 |

| 分層缺點 | 說明 |  
|--------|------|
| 處理負擔重 | 每層封裝/拆封需 CPU 處理 |
| 效能浪費 | 各層 Header 增加封包大小，浪費頻寬與延遲 |