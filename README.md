# 🩺 半監督式肝腫瘤圈選輔助與全自動化肝腫瘤辨識系統

一款結合半監督式學習（Semi-Supervised Learning）與全自動深度學習（Full-Automation）的醫療影像 AI 系統，旨在輔助放射科醫師更高效、精準地進行 CT 影像中的肝腫瘤辨識與圈選。

## 👥 團隊成員 (Team Members)
* 吳嘉尉、邱柏驊、歐冠廷、王泓翔

---

## 📌 01. 前言與創作動機 (Introduction & Motivation)

### ▍ 研究背景
根據衛福部統計，癌症已連續多年高居國人首位死因，其中**肝癌**在癌症死因中高居男性第 2 位、女性第 4 位。利用深度學習技術進行早期診斷，已成為輔助放射科醫師辨識腫瘤的熱門工具。

### ▍ 痛點與動機：獲取訓練資料困難
1. **醫師行程繁忙**：專業醫療標註（Annotation）需要耗費醫師大量時間與精力。
2. **腫瘤形狀多元複雜**：肝腫瘤邊界模糊、形態各異，傳統自動化標註精準度有限。

本專案提出**「半監督式肝腫瘤圈選輔助」**技術，讓醫師只需進行簡單的點選或小部分圈選，AI 即可自動擴展生成精準的腫瘤遮罩（Tumor Mask），大幅降低標註成本。

<p align="center">
  <img width="1602" height="902" alt="image" src="https://github.com/user-attachments/assets/40356470-c7f0-4cce-96a7-5c29b8e21432" />
</p>

---

## 🛠️ 02. 系統功能與開發技術 (System Architecture & Technologies)

本系統主要分為兩大核心模塊：

### 1. 半監督式肝腫瘤圈選輔助 (Semi-Supervised Tumor Segmentation)
當醫師點選或框選未知 CT 影像中的腫瘤後，系統透過以下技術交叉融合，生成最終的半自動結果：
* **自適應二值化 (Adaptive Thresholding)**：結合多元迴歸模型（針對腫瘤點 HU 值、周圍 HU 值進行平均與標準差計算），透過公式 $Threshold = avg + 0.5 \times std$ 進行動態門檻值計算，並持續擴散直到邊緣。
* **定錨式 Mask R-CNN**：精確鎖定腫瘤邊界並進行實例分割。
* **YOLOv8 模組**：快速定位腫瘤區域。

### 2. 全自動肝腫瘤辨識 (Fully Automated Tumor Detection)
* **未知 CT 影像輸入** ➡️ **肝臟切割預處理** ➡️ **YOLOv8 模型辨識** ➡️ **全自動輸出腫瘤位置**。

<p align="center">
  <img width="1597" height="898" alt="imageq" src="https://github.com/user-attachments/assets/696457d6-a31e-4dfb-bdad-0d94a98fd067" />
</p>

---

## 📊 03. 實驗設計與結果 (Experiment & Results)

### ▍ 實驗資料集 (Dataset)
* **LiTS (Liver Tumor Segmentation Challenge)**：包含 117 位病人，具備多類型肝腫瘤影像。
* **半監督式訓練分配**：訓練 23 人 / 驗證 2 人 / 預測 92 人（比例約 2:8）。
* **全自動訓練分配**：訓練 92 人 / 驗證 2 人 / 預測 23 人（比例約 8:2）。

### ▍ 評估指標
本研究採用 **Precision**、**Recall** 以及 **F-Measure (F1-Score)** 作為模型評估標準。

### ▍ 數據表現 (Results Comparison)
1. **半監督式技術 vs. 非監督式模型**：本團隊提出的融合模型（Fusion for Liver）在 Precision、Recall 與 F-Measure 上皆顯著優於傳統的 YOLOv8、Seresnet152 Unet、Naïve Unet、ResUNet 與 UNet++。
2. **新舊技術對比**：本專案提出的改良算法（Proposed）相較於對照組（Compared），在維持高精準度的同時，大幅提升了召喚率（Recall）。

<p align="center">
  <img src="images/result_chart1.png" width="450" alt="半監督與非監督結果比較">
  <img src="images/result_chart2.png" width="350" alt="新舊技術比較">
</p>

---

## 📺 04. 專題示範 (Demo)

歡迎觀看我們的實際操作與成果展示影片：

<a href="https://www.youtube.com/watch?v=Ki3aVb2vbBc" target="_blank">
  <img src="https://img.youtube.com/vi/Ki3aVb2vbBc/maxresdefault.jpg" alt="Watch the video" width="600" style="max-width: 100%;">
</a>




