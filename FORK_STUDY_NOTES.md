# Fork 研究笔记 — CompBioAgent

> 本文件是 fork 所有者（@SHzzzAyys）的研究记录，**非上游内容**。上游说明见 [README.md](./README.md)。

## 为什么 fork

学习它「LLM 驱动 scRNA-seq 探索」的架构，用于自己的 single-cell 分析（toxo / wh3wh6 RNA-seq 方向）。

## 关键认知

CompBioAgent 是 **PHP Web 应用**（需 RHEL+Apache+PHP+MySQL+Cellxgene VIP + 预制 h5ad），Windows 本机跑不起来，与 PDF 工具无关。所以没有部署，而是**只读提炼它的架构思路**。

## 提炼出的核心模式

「LLM-as-JSON-compiler」四步管道：自然语言 → LLM 生成结构化 JSON → 校验基因/分组名（`isBadGene` 思路）→ 调绘图工具。证据文件：`webapp/app/core/lib_app_ai_assistant_chat.php`、`webapp/bxaf_setup/default/5-Prompt.php`（5 种图 + 默认推断规则）。

## 移植成果

把这套模式移植成一个独立的 Python 原型（不在本仓库内），用 Scanpy 替代 Cellxgene VIP、DeepSeek 替代 OpenAI，在 pbmc3k demo 上跑通了 umap/violin/dotplot/stacked_bar + 校验拦截 + SHA256 缓存。
