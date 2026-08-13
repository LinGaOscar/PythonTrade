# CLAUDE.md

Python 練習專案：用 Jupyter Notebook 對台股（主要是 2330 台積電）做簡單的策略回測與資料處理練習。

## Commands

- 安裝依賴：`pip install pandas numpy matplotlib requests jupyterlab TA-Lib pyfolio`（本 repo 未附 requirements.txt，缺哪個裝哪個；TA-Lib 需先裝好系統層 C library，例如 macOS 用 `brew install ta-lib`）
- 啟動 Jupyter：`jupyter lab`（或執行 `run.bat`，內容就是這行）
- 所有邏輯都在 notebook 裡逐格執行，沒有可獨立執行的 `.py` 進入點

## Architecture

- `回補資料.ipynb`：向台灣證交所（TWSE）公開 CSV 端點（`MI_INDEX`）逐日爬取收盤行情，累積寫入 `price.csv`（未提交，`.gitignore` 以 `*.csv` 排除）。**無需任何 API key／登入**，純公開資料。
- `backtest.ipynb`：讀取 `price.csv`，示範「每天開盤買進、尾盤賣出」的簡單策略回測（以 2330 為例）。
- `2330回測/KD.ipynb`：以 KD（隨機指標，透過 `talib.abstract.STOCH`）對 2330 做參數網格搜尋回測，並用 `pyfolio` 產出報酬分析報表。
- `2330回測/連續跌.ipynb`：「連續三天收黑」進場策略回測，同樣針對 2330，用 `../price.csv` 相對路徑讀資料。
- `practice.ipynb`：與交易邏輯無關的 pandas 基礎操作練習（讀取 `data.csv`，欄位篩選、`loc`/`iloc` 等）。
- 資料流：先跑 `回補資料.ipynb` 產生/更新本機 `price.csv`，其餘回測 notebook 都依賴這份檔案；`price.csv`、`data.csv` 皆未提交進版控。
