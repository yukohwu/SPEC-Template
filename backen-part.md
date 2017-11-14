# Taskd

Taskd 是一隻用來執行各種非同步任務的一隻服務。他會每秒鐘去指定的目錄下執行所有以檔案方式存在的任務。

###### /usr/local/mozart/data/task\_queue

因此對它來說，賦予一項任務就是開啟一個檔案。而任務\(檔案\)的內容，是以 JSON 的方式描述。  
任務執行的進度或是結果資訊，會更新到檔案內容以及檔名。檔名的格式如下：

###### /usr/local/mozart/data/task\_queue/&lt;user-id&gt;/&lt;task-id&gt;-&lt;runtime-info&gt;.&lt;task-type&gt;

* **&lt;task-id&gt;** 為一個 unique識別碼，用以識別這項任務。

* **&lt;runtime-info&gt; **為 taskd 在執行期間，一些主要狀態的顯示。

* **&lt;task-type&gt;** 是一個描述任務型別的字串，每個型別都需要有對應一個任務內容的schema

我們先實作兩種任務：

* [x] RETRMS：對郵件資料庫進行非同步的查詢任務

* [x] PACKMS：對郵件資料庫進行選擇郵件的非同步打包任務

---

# RETRMS

使用者 yukoh 要開啟一個搜尋的任務，這個任務需要包含：

1. 搜尋條件。
2. 搜尋結果要打包。
3. 任務結束後，寄通知信給 **yukoh@cellopoint** 跟 **hank@cellopoint.com** 兩個人。

假設 yukoh 這個帳號的 account id 是 3, 此時 UI 的動作就是去以下這個目錄 /usr/local/mozart/data/task\_queue/3  
 下開啟一個 file，/usr/local/mozart/data/task\_queue/3/0001.RETRMS。file 的內容如下：

```
{
"type": "RETRMS",
"description": "搜尋任務A計劃",
"criterion":
    {
        "session": "yukoh_XXX",
        "group": "",
        "user": "yukoh",
        "label": "",  
        "folder": "_ARCHIVE_",
        "file": ["20171025"],
        "subject": "haha"
    },
"pack": true,
"notify": ["yukoh@cellopoint.com","hank@cellopoint.com"],
}
```

另外，如果要寄發通知信，把要發送的通知信用下面的檔名格式，放在同一個目錄下。taskd 完成工作後，則會將該檔案寄出並且刪除。檔名格式為：/usr/local/mozart/data/task\_queue/&lt;user-id&gt;/&lt;task-id&gt;.notify.eml。以這個例子來說，檔名為 /usr/local/mozart/data/task\_queue/3/0001.notify.eml。之後 taskd 每秒都會去處理這個 task file，並開始作業，同時也會每秒去更新作業狀態寫回這個檔案。每次更新後，檔名也會依據執行狀態而被更改。比方由 **0001.RETRMS** 變更為 **0001-ABCXYZ\_87.RETRMS**，**ABCXYZ** 是來自以下內容的 retrieve-id，**87 **是來自以下內容的progress，更改後的內容如下：

```
{
"type": "RETRMS",
"
 
description": "搜尋任務A計劃",
"criterion":
    {
        "session": "yukoh_XXX",
        "group": "",
        "user": "yukoh",
        "label": "",  
        "folder": "_ARCHIVE_",
        "file": ["20171025"],
        "subject": "haha"
    },
"pack": true,
"notify": ["yukoh@cellopoint.com","hank@cellopoint.com"],
"retrieve-id": "ABCXYZ",
"progress":87
}
```

---

# PACKMS

使用者 yukoh 要開啟一個打包郵件的任務，這個任務需要包含：

1. 需要打包的 retrieve-id。
2. 需要打包的 mail-id list。
3. 需要打包的本地檔案清單
4. 任務結束後，寄通知信給 **yukoh@cellopoint** 跟 **hank@cellopoint.com** 兩個人。

假設 yukoh 這個帳號的 account id 是 3, 此時 UI 的動作就是去以下這個目錄 /usr/local/mozart/data/task\_queue/3  
 下開啟一個 file，/usr/local/mozart/data/task\_queue/3/0001.PACKMS。file 的內容如下：

```
{
    "type": "PACKMS",
    "description": "搜尋任務A計劃",
    "retrieve-id": "ABCXYZ",
    "mails": ["A11111", "A22222", "A33333"],
    "files": ["/tmp/file1.doc", "/tmp/file2.pdf"],
    "notify": ["yukoh@cellopoint.com", "hank@cellopoint.com"]
}
```

之後 taskd 每秒都會去處理這個 task file，並開始作業，同時也會每秒去更新作業狀態寫回這個檔案。每次  
更新後，檔名也會依據執行狀態而被更改。比方由 **0001.PACKMS** 變更為 **0001-87.PACKMS**，**87 **是來自以下內容的 progress  
。更改後的內容如下：

```
{
    "type": "PACKMS",
    "description": "搜尋任務A計劃",
    "retrieve-id": "ABCXYZ",
    "mails": ["A11111", "A22222", "A33333"],
    "files": ["/tmp/file1.doc", "/tmp/file2.pdf"],
    "notify": ["yukoh@cellopoint.com","hank@cellopoint.com"],
    "tmp-space": "/usr/local/mozart/data/work_space/3/XXX/",
    "output": "/usr/local/mozart/data/download/3/搜尋任務A計劃.tar.gz",
    "progress":87
}
```



