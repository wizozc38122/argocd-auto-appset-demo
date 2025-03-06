# Overview

刻意切成 bootstrap 及 deploy

bootstrap 設計為自動讀取 deploy 目錄結構生成 app

後續開發人員不需要關注該目錄，僅需要關注 deploy 即可

PS. 
此範例僅設定 dev 環境，要多環境複製appset將環境改一下就好

**Tips**

AppSet 預設3分鐘掃描一次，剛添加可能不會馬上出現新的App

## bootstrap

bootstrap-app.yaml 單純用於 app of apps 管理所有 env-appset

env-appset 則是負責動態掃描，特定環境的部屬檔

基礎的資源名稱 透過目錄結構 /ns/app/env 代表 命名空間 應用名稱 環境 (這點配合helm的template value規劃好)

## deploy

**/apps**

放置主要不同 /ns/app/env 服務部屬檔案
只有兩個檔案
1. template.yaml (自訂)
    ```
    template: 指定templates目錄內的特定範本(Chart)
    ```
2. values.yaml
目標Chart的values值替代

**/templates**

放置各類範本(Chart)，預設 values 當作範例提供使用者參考

# 啟用

```shell
# 後續透過 Argo Sync 即可
kubectl apply -f /bootstrap/bootstrap-app.yaml 
```
