# vue-3-demo

## 安裝

* 要先卸載 vue-cli 版本 3 以下的 然後再安裝版本 3 以上的

* 可以通過在終端機中任意目錄下輸入 `vue -V` 查看當前 vue-cli 版本

* vue-cli 版本 3 開始安裝方式從 `npm i -g vue-cli` 改成 `npm i -g @vue/cli`


## 建立項目

打開終端機切換到要創建資料夾的位置 然後輸入 `vue create 項目名稱`

迴車後出現的第一個問題是說 你的安裝速度有點慢 要不要把安裝方式改成淘寶的 `npm`

接下來會問你執行創建項目的特性 有默認跟手動 這裏選擇手動 (唯一不是 `default` 開頭的那一個)

然後會出現一堆選項 這裏選擇 `Babel(編譯器) CSS(SASS) Linter(JS編碼風格規範)` 這三個

* 最新版本的迴車後會繼續問你 `Sass/SCSS (with dart-sass) or Sass/SCSS (with node-sass)` 這裏選 `node-sass`

然後是 `linter / formatter` 選項 這邊選規範比較不嚴謹的 `ESLint + Standard config`

然後是偵錯時機 我們選 `Lint on save` 即每次存檔時檢查

最後就是問你要把 Babel, PostCSS, ESLint 等等的設定檔放哪 先選放在 `package.json`

## 打開項目

項目創建完成後 會提示你做兩件事

- 1. 切進去項目資料夾中

- 2. 執行 `npm run serve` 讓項目在瀏覽器中運行

## 項目結構說明

- 1. 在新的版本中 `webpack` 相關設定檔被放在 `node_module` 資料夾中 且設定內容最好不要改動

- 2. 在新的版本中 `main.js` 的 `import App from './App.vue'` 這個後綴名 `.vue` 預設不可省略 當省略時 在 `ESLint` 中會出現錯誤提示 但實際上編譯後不會有問題

- 3. `index.html` 原本放在項目結構本身的最外層上 現在改成放在 `public` 資料夾中

    * 在 `public` 資料夾中的內容基本上全都是不會被編譯的檔案 唯獨 `index.html` 例外

- 4. 打開 `package.json` 可以看到 `script` 中有 `serve build lint` 三個屬性 他對應的就是 `npm run xxx`

    * `npm run build` 與在舊版本中的 `npm run build` 一樣 都是用來打包項目創建 `dist` 資料夾的

    * `npm run serve` 類似在舊版本中的 `npm run dev`

## 環境變量

在 `vue-cli v2` 版本的時候我們是在 config 資料夾下的 `dev.env.js` 與 `prod.env.js` 中修改環境變數的

但在 `vue-cli v3^` 版本若要設定環境變數 則是在項目目錄中直接新增 `.env` 檔案

  * `.env` 中直接寫入 `VUE_APP_自定義變數名=值` 在任意 `.vue` 檔案中 通過 `process.env.VUE_APP_自定義變數名` 即可獲取該環境變量

  * `.env.production` 檔案是 `npm run build` 的環境變量 權重比 `.env` 高

  * `.env.development` 檔案是 `npm run serve` 的環境變量 權重比 `.env` 高

  * `.env.xxx` 檔案可以通過在 `package.json` 中的 `build/serve` 後面加上 `--mode xxx` 來指定環境變量的檔案
  
  ```json
  
  "scripts": {
    "serve": "vue-cli-service serve --mode xxx",
    "build": "vue-cli-service build --mode xxx",
    "lint": "vue-cli-service lint"
  },
  
  ```

**每次修改或設定了環境變量後都需執行 `npm run xxx` 重啟服務器 才可生效**

另外如果在 `.env` 檔案的檔案名稱最後面加上 `.local` 則該環境變量檔案會直接被 `git` 忽略 如：`.env.abc.local` `.env.local` 等

## Vue-cli v3^ GUI 介面

打開終端機 切換到項目目錄中 輸入 `vue ui` 即可打開 GUI 介面

執行完畢後電腦會自動開啟 `http://localhost:8000/project/select`

打開後可以在首頁的 `新增` 中點擊 `新增專案` 新增專案的過程與使用終端機創建項目的過程一樣 只是從輸入指令改成點選

創建完成後瀏覽器畫面會切進 `專案控制台` 在其左邊選單中可以看到`拼圖/書/設定/清單` 等 icon

  * 拼圖對應的是 `vue-cli` 使用的 `vue` 插件 如：`vue-router` `vuex` 等

  * 書對應的是 `node_modules` (即依賴項) 可以直接在上方的搜索欄中安裝依賴項 如 `jquery bootstrap` 等

  * 設定對應的是 `vue` 插件使用的一些設定檔 如：原本在 `vue-cli v2` 時我們把檔案傳到 `gh-pages` 時需修改的專案引用路徑即是在 `Vue Cli` 中的第一個 `公開路徑` 做設定

  * 清單對應的是 `vue-cli` 的 `npm run xxx` 那幾個選項 我們可以直接點擊清單中的 `serve build lint` 裡面的 `執行` 來啟動對應的服務器

按下啟動後 在控制台終有一個 `啟動 app` 點擊即可開啟專案頁面 即 `http://localhost:8080/` 

若要查看原本在終端機中顯示的執行過程代碼可以點擊控制台左邊的 `輸出` 按鈕

另外在執行的右邊有一個 `變量` 按鈕 就是控制環境變量的 在 `serve` 中默認是 `development` 可以在這裡用下拉選單切換其他環境變量

現在切換回 `拼圖` 即 `vue插件` 在最上面可以看到 `新增vue-router` 按鈕 點下去後他會自動幫我們創建 `vue-router` 且在 `App.vue main.js index.js` 等檔案中都會幫我們寫好代碼

完成後我們回到專案頁面就可以看到在最上方多了 `Home | About` 點擊後也可以直接切換路由 這部分是跟 `vue-cli v2` 比較不一樣的地方 也是在版本3以上產生的一個便捷功能

另外在 `vue-cli v3^` 中可以不用先 `@import` 改成直接在需要的地方使用 `() => import('xxx')` 即可

最後補充一個知識點：在 `vue-cli v3^` 中 `src` 資料夾裡面提供了一個 `views` 資料夾 這個 `views` 資料夾也是用來放置 `.vue` 檔的 只是它建議我們拿來放要作為頁面的檔案 而要作為元件的檔案則一樣放在 `components` 資料夾中

## 快速原型開發

開啟終端機輸入 `npm install -g @vue/cli-service-global` 安裝全局依賴

然後我們就可以通過 `vue serve xxx.vue` 來快速生成 `webpack` 服務器

生成完成後也可以通過 `vue build xxx.vue` 來打包它

該功能是 `vue-cli v3^` 所提供 專門用來對**單個**文件做開發的工具 非常好用