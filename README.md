# PythonTrade

台股（以 2330 台積電為主）簡單策略回測練習專案，使用 Jupyter Notebook 撰寫，資料來源為台灣證交所公開行情。

## 這個專案在做什麼

- 從台灣證交所（TWSE）公開網頁 API 抓取每日收盤行情，存成本機 `price.csv`
- 用 pandas 整理資料，搭配 `talib`／`pyfolio` 做幾個簡單交易策略的回測練習：
  - 每天開盤買、尾盤賣（`backtest.ipynb`）
  - KD 指標黃金/死亡交叉（`2330回測/KD.ipynb`）
  - 連續三天收黑進場（`2330回測/連續跌.ipynb`）
- 另有一份與交易無關的 pandas 基礎操作練習 notebook（`practice.ipynb`）

## 環境需求

- Python 3
- Jupyter Lab
- 套件：`pandas`、`numpy`、`matplotlib`、`requests`、`TA-Lib`（含系統層 C library）、`pyfolio`

本 repo 未附 `requirements.txt`，請依實際執行時遇到的 `ImportError` 自行安裝對應套件。

## 如何執行

```bash
pip install pandas numpy matplotlib requests TA-Lib pyfolio jupyterlab
jupyter lab
```

Windows 下也可以直接雙擊 `run.bat`（內容就是 `jupyter lab`）。

1. 先開啟 `回補資料.ipynb`，逐格執行以下載/更新 `price.csv`（第一次執行時間視回補天數而定，會逐日呼叫一次 TWSE API）
2. 再開啟 `backtest.ipynb`、`2330回測/KD.ipynb`、`2330回測/連續跌.ipynb` 等回測 notebook，皆會讀取同一份 `price.csv`

## API／設定

- 資料來源是 TWSE 公開行情端點（`https://www.twse.com.tw/exchangeReport/MI_INDEX`），**不需要任何 API key 或登入**
- 若之後要串接券商下單或其他需要驗證的 API，請務必用環境變數存放金鑰，切勿把金鑰寫進 notebook 或程式碼提交進版控
