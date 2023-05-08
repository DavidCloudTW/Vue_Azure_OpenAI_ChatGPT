# 使用 Vue 與 Azure OpenAI ChatGPT 建立 AI 問答機器人

前置準備:已有AOAI帳號

第一步:設定 GitHub Action Secret
在專案中找到Settings > 左側欄位選取 Secrets and variables 中的 Actions > 點選 New repository secret

建立 3 個 Secret 資訊

第 1 個 Endpoint Secret
Name 欄位請輸入 VUE_APP_OPENAI_ENDPOINT
Secret 欄位請輸入 建立 Azure OpenAI ChatGPT 的 Endpoint

第 2 個 Model deployment name Secret
Name 欄位請輸入 VUE_APP_OPENAI_MODEL_DEPLOYMENT_NAME
Secret 欄位請輸入 建立 Azure OpenAI ChatGPT 的 Model deployment name

第 3 個 Key Secret
Name 欄位請輸入 VUE_APP_OPENAI_KEY
Secret 欄位請輸入 建立 Azure OpenAI ChatGPT 段落 Step 5 所取得的 Key
以上資訊輸入完成後請點選下方的 Add secret

第二步:建立 Azure靜態Web應用程式
Source選擇GitHub連結本專案
Build Presets選擇Vue.js，其餘設定使用預設，然後建立

第三步:修改程式碼
Web App建立完成後在GitHub專案的.github/workflows中會生成新的azure-static-web-apps-xxxxx-xxxxx-xxxxxxxxx.yml檔，
將原本舊的檔案移除並下載新的檔案內容做修改。
在第34行加入ene:並對其上面24行的with

env:
    VUE_APP_OPENAI_ENDPOINT: ${{ secrets.VUE_APP_OPENAI_ENDPOINT }}
    VUE_APP_OPENAI_MODEL_DEPLOYMENT_NAME: ${{ secrets.VUE_APP_OPENAI_MODEL_DEPLOYMENT_NAME }}
    VUE_APP_OPENAI_KEY: ${{ secrets.VUE_APP_OPENAI_KEY }}
    
修改完成後上傳

第四步:確認GitHub Action 狀況
在GitHub專案的Action確認上傳檔案後專案的執行狀況，
確認執行成功後到Azure靜態Web應用程式的概覽開啟URL就可以進行對話了
