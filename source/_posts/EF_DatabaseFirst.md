---
title: .Net Framework EF_DatabaseFirst
date: 2024-06-13
tags: .Net EF
---

## 使用環境 Visual Studio 2022

### 1.使用.Net FrameWork4.8.1

### 2.Nuget 安装 EntityFramework 6.4.4

### 參考：https://learn.microsoft.com/zh-tw/ef/ef6/modeling/designer/workflows/database-first

使用工具建立 DatabaseFirst EF

<h2><font color="red">設定EF環境</font></h2>

### 1.DatabaseFirst EF 相關内容放在一個類別庫從 WEB 端引入使用資料庫

#### 方案右鍵》加入》新增專案》類別庫（.Net Framework）》下一步 這裏取名 DataBase

<div style="display: flex;">
    <img src="/Ianblog/images/add_project1.jpg" style="width: 50px; height: 50px;margin:0px 10px;" title="" alt="">
    <img src="/Ianblog/images/add_project2.png" style="width: 50px; height: 50px;margin:0px 10px;" title="" alt="">
    <img src="/Ianblog/images/add_project3.png" style="width: 50px; height: 50px;margin:0px 10px;" title="" alt="">
    <img src="/Ianblog/images/add_project4.png" style="width: 50px; height: 50px;margin:0px 10px;" title="" alt="">
</div>

### 2.工具的方法建立模型

#### DataBase 右鍵建立資料夾 DbContext》右鍵 DbContext》加入》新增項目》選擇"來則資料庫的 EF Designer"》選擇你的目標 DataBase》在 App.config 建立 EF_DataBaseFirstEntities》選擇要建立的資料表模型使用預設命名》完成

<div style="display: flex;">
    <img src="/Ianblog/images/addEF1.png" style="width: 50px; height: 50px;margin:0px 10px;" title="" alt="">
    <img src="/Ianblog/images/addEF2.png" style="width: 50px; height: 50px;margin:0px 10px;" title="" alt="">
    <img src="/Ianblog/images/addEF3.png" style="width: 50px; height: 50px;margin:0px 10px;" title="" alt="">
    <img src="/Ianblog/images/addEF4.png" style="width: 50px; height: 50px;margin:0px 10px;" title="" alt="">
    <img src="/Ianblog/images/addEF5.png" style="width: 50px; height: 50px;margin:0px 10px;" title="" alt="">
</div>

### 3.檢查檔案

##### 1.路徑：DbContext\EF_DataBaseFirstEntities.Context.cs

##### class ：EF_DataBaseFirstEntities base("name=EF_DataBaseFirstEntities")name:對應到連線字串的 name

<div style="display: flex;">
    <img src="/Ianblog/images/check1.png" style="width: 50px; height: 50px;margin:0px 10px;" title="" alt="">
</div>

##### 2.App.config : 內容為連線資訊要在 web 端的 web.config 使用

##### 路徑：DataBase/App.Config

<div style="display: flex;">
    <img src="/Ianblog/images/check2.png" style="width: 50px; height: 50px;margin:0px 10px;" title="" alt="">
</div>

##### 3.DataBase/App.Config 連線資訊複製到 Web 端的 web.config

<h4><font color="red">因為使用Web端引入DataBase.dll 的方式 使用的連線字串是在Web端 不做這一步會找不到連線字串</font></h4>

<div style="display: flex;">
    <img src="/Ianblog/images/check3.png" style="width: 50px; height: 50px;margin:0px 10px;" title="" alt="">
   
</div>

### 4.在 Web 端安裝 Nuget 安装 EntityFramework 6.4.4

### 5.在 Web 端引入 DataBase.dll 
##### EF_DataBaseFirst右鍵》加入》參考》DataBase打√ 》確定

 <div style="display: flex;">
    <img src="/Ianblog/images/import1.png" style="width: 50px; height: 50px;margin:0px 10px;" title="" alt="">
    <img src="/Ianblog/images/import2.png" style="width: 50px; height: 50px;margin:0px 10px;" title="" alt="">
    <img src="/Ianblog/images/import3.png" style="width: 50px; height: 50px;margin:0px 10px;" title="" alt="">
</div>


### 6.using DataBase.DbContext; 就可以直接使用了

<h2><font color="red">以上完成環境設定</font></h2>
