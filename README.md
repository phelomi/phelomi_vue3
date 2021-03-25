# Phelomi
> [網站](https://starrysky.family/)

## 現存的問題和瓶頸
1. `vendor` 過大（共用依賴包），加上託管伺服器的資源下載速度相對較慢，造成首次加載白屏時間會落在 `2 ~ 3s` 。
2. 部署流程全手動，效率低。
3. 資料來源沒有分環境，導致在修改資料時，線上的服務也會同步被改動。
4. `spa(single page application)` 的模式不利於爬蟲做 `SEO` 。

## 新版的技術棧和結構
1. 前端涉及到的部分包括: `Vue 3` , `Vite 2.x` , `Tailwindcss 2`
2. 後端涉及到的部分包括: `Prisma 2` , `SQLite`
3. 前端頁面走 `SSR` 模式。線上會啟動一個服務同時支持畫面渲染的資料獲取，取消原本存儲在 `firebase` 的內容。
4. 圖床的部分，考慮也移除出 `google` 的服務，轉向其他第三方服務。
5. 託管服務考慮遷移到 `gcp(google cloud platform)` ， 並走 `Dooker Image` 的模式。
6. `vendor` 的問題，在專案上線後，根據資源下載速度，再評估是否移除部分內容轉為走 `CDN` 服務。

## 開發流程
1. `master` 為線上部署分支，毋需更動。
2. `beta` 為開發主分支，所有 `commit` 內容皆由 `PR(pull request)` 來。
3. 其餘分支為個人開發分支，按照個人手上需求分類去開。開發完成後，通過 `PR` 提交上來，通過審核後，才會進入主分支。

## 部署流程
```sh
# 第一次
heroku container:login
heroku container:push web
heroku container:release web
```


