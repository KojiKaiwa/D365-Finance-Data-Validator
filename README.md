# D365 Finance Data Validator (Python/Pandas)

## 概要
Dynamics 365 Finance & Operations へのデータ移行を効率化するための検証ツールです。
会計コンサルタントの視点で、インポート前に発生しやすいデータの不備を自動検知します。

## 主な機能
- 貸借一致チェック（Debit/Credit balance check）
- 必須項目（勘定科目コード等）の欠損値チェック
- 二重入力の防止ロジック
- 列名の空白（スペース）自動クレンジング

## 開発の背景
Microsoftの面接フィードバックに基づき、技術課題を克服するために自力で構築しました。
概要 / Overview
Microsoft Dynamics 365 Finance & Operations (D365 F&O) へのデータ移行（Data Migration）を効率化・正確化するためのデータ検証ツールです。
会計コンサルタントの視点で、インポート前に発生しがちなデータの不備や整合性エラーを自動検知することを目的としています。

主な機能 / Key Features
- ・貸借一致チェック (Debit/Credit Balance Verification): 伝票ごとの貸借合計が一致しているか自動検証します。
- ・必須項目バリデーション (Mandatory Field Check): 勘定科目コードなどの未入力（欠損値）を特定します。
- ・二重入力防止 (Double-Entry Detection): 同一行内の借方・貸方両方への重複入力を検知します。
- ・データクレンジング (Data Cleansing): 列名やデータ内の不要な空白（スペース）を自動除去し、インポートエラーを未然に防ぎます。

追加新機能 / Adding features
- ・減価償却スケジュールの自動生成
- ・月次償却スケジュールの生成ロジックを追加
- ・銀行勘定照合ロジックを追加
- ・為替損益の計算を追加
- ・税務ロジックの実装
- ・外貨差損益
- ・連結会計・内部取引消去の自動化シミュレーションを追加
- ・予算対実績分析（予実管理）と異常検知ロジックを追加
- ・Added Data Visualization (Budget vs Actual) using Matplotlib
- ・Added Duplicate Transaction Detection for Audit Data Integrity
- ・Implemented Audit Log Monitoring for Weekend and Late-night Transactions
- ・Implemented Burst Detection for Monitoring Abnormal System Usage
- ・Added Visualization for User Transaction Burst Peaks
- ・Added Time-Series Trend Analysis for Daily Transaction Volumes
- ・Implemented Master Data Integrity Check (Orphaned Record Detection)
- ・Implemented Master Data Consistency Check (Detecting multi-name mapping per ID)
- ・Implemented Master Data Validation with Business Rule Checks
- ・Added Data Format Validation (Length, Numeric check, and Prefix rules)
- ・Developed a Unified Error Dashboard for multi-point data validation
- ・Added Excel Export functionality for easy sharing of validation results
- ・Developed a Master Data Comparison (Diff) and Cleansing tool for system migration
- ・Enhanced Number Sequence Integrity check with Gap detection and formatting
- ・Developed a Text Sanitization tool to remove/replace invalid characters for D365 imports
- ・Finalized Data Migration Pipeline: From data cleaning to CSV export for D365 Import
- ・Added Incident Analysis tools: Transaction Spike Detection and Error Pattern Analysis
- ・Improved log parsing logic to handle keyword variations (e.g., 'timeout' vs 'timed out')
- ・Added Pie Chart visualization for Error Category Distribution
- ・Implemented Cross-Validation logic to detect transactions by 'Ghost Users' (non-existent employees)
- ・Developed a Weighted Risk Intelligence model combining Statistical, Business, and Organizational audit flags
- ・Implemented Fraud Detection tool using Benford's Law for auditing financial transaction data
- ・Developed a Round Number Detection tool for identifying suspicious financial transactions
- ・Developed an Integrated Fraud Detection Dashboard by combining Benford's Law and Round Number Analysis
- ・Visualized Integrated Risk Scores using Heatmaps to prioritize audit investigations
- ・Implemented Multi-dimensional Pivot Analysis and Automated Error Reporting for ERP transaction logs
- ・Visualized Departmental Spending Patterns using Stacked Bar Charts from Pivot Data
- ・Developed a Device Compliance Analysis Tool for Intune MDM (Mobile Device Management) scenarios

開発の背景 / Background
前回の面接において、Dynamics 365 の製品知識（MB-310保持）に加え、実装現場での技術的理解（Python/C#等）の重要性を再認識いたしました。
指摘いただいた技術課題を短期間で克服し、実務で即戦力として貢献できることを証明するため、本ツールを自力で構築・公開いたしました。

使用技術 / Tech Stack
・Python 3.x
・Pandas (Data Analysis Library)
・Google Colaboratory (Development Environment)

新機能　/ Adding Function
- **銀行勘定照合ロジック (Bank Reconciliation Logic):** 銀行明細データと内部元帳データを「日付・金額」の複数条件で突合し、未照合（アンマッチ）な仕訳を自動抽出します。
- **日付のズレの許容 Fuzzy Matching）:** 照合時のロジックを実装しました。
- **外貨差損益 （Exchange Gain/Loss）:** 外貨差損益に対するチェックを行うロジックを実装しました。
- **消費税額計算 (Sales Tax Check logic):** 売上価額に対する消費税額のチェックを行うロジックを実装しました。
- **外貨差損益 （Exchange Gain/Loss）:** 外貨差損益に対するチェックを行うロジックを実装しました。
- **モニタリングとアラート（Monitaring & Alerting) :** システムの利用ログからユーザー別のバースト（突発的負荷）を可視化し、異常な操作パターンを特定するモニタリング機能を実装しました。
- **しきい値の可視化（Threshold Visualization) :** 単なるグラフ化にとどまらず、アラートの閾値を視覚的に示すことで、迅速な意思決定（エスカレーション）を支援する設計にしました。
- **文字変換（Handling Character Normalization Logic) :** 半角カタカナが正規化プロセス（NFKC）を経て全角へと変換される特性を考慮し、マッピング辞書を最適化することで、名寄せの精度を 100% に高めました。
- **形式が根本的に異なるデータ間の名寄せ（Legacy Data Transformation) :** 旧システム特有の『半角カナ』と新システムの『漢字名称』という、形式が根本的に異なるデータ間の名寄せを自動化しました。
