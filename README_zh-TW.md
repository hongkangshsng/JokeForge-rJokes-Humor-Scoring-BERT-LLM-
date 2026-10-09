# JokeForge：BERT 幽默分數預測與 LLM 回饋式生成管線

> [English](README.md) ｜ **繁體中文**

JokeForge 是一項 Agentic AI 專題，以 BERT 文字回歸模型預測笑話的幽默分數代理訊號，再把預測分數用於 LLM 生成笑話候選的排序與篩選。

## 專題重點

- **任務：** 由英文笑話文字預測連續型 humor-score proxy。
- **資料基礎：** r/Jokes 資料集與 Reddit 社群回饋訊號。
- **模型定位：** BERT 是獨立的**評分器**，不是笑話生成器。
- **生成流程：** LLM 提出候選笑話，再由 BERT scorer 評分、排序與過濾。
- **迭代紀錄：** 整理 Epoch 1、2、4、4.5、5 等 checkpoint，作為訓練歷程比較依據。

## 系統流程

    r/Jokes 笑話文字 + Reddit 社群回饋
                     |
                     v
            資料清理與對數化分數標籤
                     |
                     v
            BERT 回歸評分模型 --> 預測 humor score
                                        |
    LLM 生成笑話候選 --------------------|
                                        v
                           排序 / 篩選 / 人工檢視
                                        |
                                        v
                                互動式展示網站

這個分數是**社群回饋的代理指標**，不是客觀或放諸所有文化皆準的笑不笑判斷。Reddit 的投票也可能受曝光量、發布時間、受眾與版規影響。

## 目前 Repo 狀態

這一版先建立作品集所需的說明文件、可重現專案架構、資料處理規範與模型發布規畫。

- 不重新散布完整 r/Jokes 原始資料。
- 不把大型 checkpoint 直接提交至 Git。
- 未完成可重現評估前，不宣稱任何模型效能數字。
- 互動網站原始碼會在展示版清理、驗證後再放入 app 資料夾。

## 資料集與標籤

本專題參考 Weller 與 Seppi 提出的 humor-level regression 任務：以 Reddit upvote 的對數化分數作為幽默程度的代理標籤。

- 資料集：[orionw/rJokesData](https://github.com/orionw/rJokesData)
- 參考文獻：[The r/Jokes Dataset: a Large Scale Humor Collection（LREC 2020）](https://aclanthology.org/2020.lrec-1.753/)

r/Jokes 包含超過 55 萬則英文笑話。詳細資料取得方式與使用限制請見 [data/README.md](data/README.md)。

## 模型與評估

BERT 評分器預定採用 Transformer encoder 加上單一連續值 regression head。評估會以論文常用的下列指標呈現：

| 指標 | 用途 |
|---|---|
| RMSE | 衡量預測分數與標籤的誤差 |
| Pearson correlation | 衡量線性關聯程度 |
| Spearman correlation | 衡量排序一致性 |

原始論文提供 BERT、RoBERTa 與 XLNet 的研究基準；本 Repo 只會呈現本專題實際重跑或實測得到的結果，不混用論文的 baseline 成績。

## 本機執行

目前公開的是專案文件與環境骨架。程式碼加入後可使用：

    git clone https://github.com/hongkangshsng/JokeForge-rJokes-Humor-Scoring-BERT-LLM-.git
    cd JokeForge-rJokes-Humor-Scoring-BERT-LLM-
    python -m venv .venv
    pip install -r requirements.txt

## 使用限制

- 原始語料可能含有冒犯性、成人或高度文化脈絡化的內容。
- Reddit 投票不能視為幽默品質的絕對標準。
- 本 Repo 不散布第三方原始資料。
- LLM 生成內容在公開使用前仍應經人工檢視。

## 授權與致謝

本 Repo 中的原創程式碼與文件採用 [MIT License](LICENSE)。資料集、論文、預訓練模型與其他第三方素材各自保有原本的授權條款。

詳見 [參考資料與歸屬](docs/references.md)。
