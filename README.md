# docker-php7-web
用 docker 建立 lamp 開發環境

## 簡介

1. 基礎為使用 ubuntu + apache2 + mysql + php7.2 的開發環境。
2. 使用 nginx 作為 reverse-proxy，如果需要新增網站，只需新增 container ，在docker-compose.yml 增加 VIRTUAL-HOST 即可。詳細實作可參考 [jwilder/nginx-proxy](https://github.com/jwilder/nginx-proxy)
3. 專案目錄 src 在本處只是範例，不需要放在 docker 目錄中，以個人習慣，會將專案放在 ~/Projects/
