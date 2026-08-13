# dev.md

## 本機開發環境

- Python 3（未鎖定特定版本，用系統既有的 Python 3 即可）
- 套件管理：無 `requirements.txt`／`pyproject.toml`，純手動 `pip install`
- 需要的套件：`pandas`、`numpy`、`matplotlib`、`requests`、`talib`（TA-Lib，需先裝系統 C library，macOS 用 `brew install ta-lib`）、`pyfolio`、`jupyterlab`

## 如何跑

```bash
pip install pandas numpy matplotlib requests TA-Lib pyfolio jupyterlab
jupyter lab
```

或 Windows 下直接執行 `run.bat`（內容只有一行 `jupyter lab`）。

## 結構筆記

- 純 notebook 專案，沒有可重用的 `.py` module；每份 notebook 都是獨立、需由上而下逐格執行
- `price.csv`、`data.csv` 等資料檔都被 `.gitignore`（`*.csv`）排除，不會進版控；`回補資料.ipynb` 負責產生/更新 `price.csv`，其餘 notebook 都假設它已存在於對應相對路徑
- `2330回測/` 底下的 notebook 用 `../price.csv` 相對路徑讀資料，執行時 Jupyter 的工作目錄需對齊 notebook 所在資料夾（Jupyter Lab 從 repo 根目錄開啟時預設如此）
- 目前沒有測試、沒有 CI
