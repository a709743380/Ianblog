---
title: .Net Framework EF_CodeFirst
date: 2024-06-12
tags: .Net EF
---
## 使用環境 Visual Studio 2022
### 1.使用.Net FrameWork4.8.1
### 2.Nuget 安装 EntityFramework 6.4.4
<hr />

#### 確認安裝EntityFramework
#### Web.config > configuration 出現entityFramework相關資訊

<h2><font color="red">Web.config設定</font></h2>

``` xml
<configuration>
  <configSections>
    <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
    <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
  </configSections>
  
```
<hr />

### 在configSections下方加入DB connectionStrings用於連綫DB
##### (這裡用Windows登錄)
##### name="MyDbContext"  連綫名稱
##### connectionString: 連續目標資訊字串
##### Data Source 連綫主機 (可能是ip / localhost / .) 這裏使用本地SSMS
##### Initial Catalog = EF_CodeFirst （使用的database名稱）

``` xml
<connectionStrings>
    <add name="MyDbContext" connectionString="Data Source=.;Initial Catalog=EF_CodeFirst;Integrated Security=True;" providerName="System.Data.SqlClient" />
</connectionStrings>
```
<h2><font color="red">以上完成Web.config設定</font></h2>
<hr />

<h2><font color="green">Models 建立</font></h2>

#### 因為是CodeFirst 所以要先建立好model
##### 路徑：~/Models/Post.cs(在Models下建立Post.cs檔案)
``` C#

    //這是準備建在資料庫table的Model 
    public class Post
    {
        public int PostId { get; set; }

        public string Title { get; set; }

        public string Content { get; set; }
    }
```
#### 建立和DbContext的關係
##### 路徑：~/Models/Post.cs(在Models下建立Post.cs檔案)
##### 要繼承 DbContext （使用EF）
```  C#
using System.Data.Entity;

      public class MyDbContext : DbContext
    {
        //做base 對應到Web.config connectionStrings>><add name="MyDbContext".....
        public MyDbContext() : base("name=MyDbContext")
        { }
        //宣告
        //DbSet  表示與資料表建立關係
        //<Post> 使用此class内的欄位
        //Posts  名稱是Table名稱
        public DbSet<Post> Posts { get; set; }
    }
```
### 多個model ： DbContext的關係只有一個 DbSet對應的model變多
<h2><font color="green">以上完成Models 建立</font></h2>
<hr />

<h2 id="InitialCreate"><font color="Purple">第一次建立語法建立Table</font></h2>

##### 執行環境：（Visual Studio 2022上面那一排） 工具》》Nuget套件管理員》》套件管理員主控台
##### 套件管理員主控台 快捷鍵 : ALT + T  然後 N 然後 O
#### 1 Enable-migrations 建立Configuration
#### 2 Add-Migration InitialCreate 建立紀錄（跑完應該是可以刪掉的
#### 3 Update-Database 實際同步到SQL

## Enable-migrations 建立Configuration
``` 
 執行 Enable-migrations 建立Configuration
 會在專案建立一個資料夾Migrations 
 內有一個檔案Configuration.cs 

 成功建立
```
## Add-Migration InitialCreate 
```
 執行 Add-Migration InitialCreate (記錄檔案名稱)
 會在資料夾Migrations 中建立一個檔案 檔案名稱： 時間格式 + _ + InitialCreate (記錄檔案名稱) + .cs
 裡面有建立的table資訊（欄位格式）

 成功建立
```

## Update-Database 
```
 執行 Update-Database 
 會根據此 Add-Migration InitialCreate 這時候的檔案資訊對資料庫做實際的更新 
 資料庫此時會建立一個EF_CodeFirst的database
 database名稱為Web.config 設定 Initial Catalog=EF_CodeFirst
 裡面會有你的model 還有一個更新記錄檔案

 成功建立
```

<h2><font color="Purple">以上完成建立Table</font></h2>

<hr />

<h2><font color="blue">語法更新自己的Table</font></h2>

#### 修改model
##### 路徑：~/Models/Post.cs
``` c#
    public class Post
    {
        public int PostId { get; set; }
        //修改欄位長度
        [MaxLength(50)]
        public string Title { get; set; }

        public string Content { get; set; }
    }
```
#### 加入model UserInfo
##### 路徑：~/Models/UserInfo.cs
``` c#
    public class UserInfo
    {
        [Key]
        public int UserId { get; set; }

        [MaxLength(50)]
        public string Name { get; set; }

        public DateTime CreateDate { get; set; } = DateTime.Now;
    }
```
## Migrations 檔案還在的時候
##### 執行環境：（Visual Studio 2022上面那一排） 工具》》Nuget套件管理員》》套件管理員主控台
##### 套件管理員主控台 快捷鍵 : ALT + T  然後 N 然後 O
### Update-Database AlterModel
```
 執行 Add-Migration AlterModel （AlterModel 像備註一樣給一個名稱）
 此時在Migrations資料夾下會建立一個 時間格式 + _ + AlterModel (記錄檔案名稱) + .cs 的檔案
 裡面有這次更新欄位的資訊
 成功執行
```
### Update-Database 更新資料
```
 Update-Database時要指定是哪個Migrations檔案 （get-help Update-Database 查看語法是什麼）
 執行 Update-Database -TargetMigration AlterModel 指定AlterModel
 
 成功執行

 檢查資料表
 多了table ：UserInfoes 
 table :Posts title長度被限制到50了
```
## Migrations 檔案不在的時候

<a href="#InitialCreate">回到第一次建立語法建立Table</a>

<h2><font color="blue">以上完成更新Table</font></h2>
