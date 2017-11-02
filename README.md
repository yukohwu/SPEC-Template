# SPEC information

###### SPEC的基本資訊描述

| Item | Description |
| :--- | :--- |
| Name/ID | \#3164 - 背景搜尋後自動打包，發通知信通知搜尋者 |
| easyredmine | [https://cellopoint.easyredmine.com/issues/3164](https://cellopoint.easyredmine.com/issues/3164) |
| Supported versions | **4.1.7** |

# Purposes

1. 使用者在查詢多日的信件時，會進入非同步查詢模式，也就是所謂的背景搜尋。而當搜尋完成後，需要發送一個通知給使用者，使用者才知道說這項任務已經完成，進而可以登入管理系統看結果。

2. 使用者希望在非同步查詢後，也能自動進行後續作業，譬如打包下載。

# Assumptions \| Constraints \| Standards

1. 非同步查詢進行中，使用者要可隨時得知任務進行的狀態。也就是說狀態需要反應在 UI 上。

2. 非同步查詢後若要再自動進行結果打包，這項打包任務需要同步到下載管理員的操作介面上。

# UX Control Flow

1. 相關功能的操作畫面下，每個使用者會有一個任務清單。此清單會顯示各項任務的執行狀態。

2. 當使用者下達非同步查詢後，需要讓使用者能輸入此項任務的名稱，以方便放入上述任務清單中作為識別。

3. 當任務完成後，可依設定來發送通知信給該使用者。通知信需要有一個登入連結。

4. 使用者登入系統後，在他的任務清單中，可以發現任務已經完成。並且可以點擊該任務後，相關的位置應該要呈現結果。

5. 若查詢任務中有設定要自動進行打包的話，使用者的下載管理員介面上，需要出現打包好的檔案讓使用者直接點選下載。

6. 查詢任務尚未完成的情況下，使用者登入後，若任務尚在查詢信件時，任務清單需要顯示 progress bar。若任務已經進行到打包程序，則使用者的下載管理員界面上，需要顯示打包中的 progress bar。

---

# References

* ###### 應有項目列表，若無可刪除
* ###### 有多項則add rows

| **Supplementary materials \(相關補充資料\)** | **Remarks \(註記是此SPEC的產物、抑或是實作時參考時用的；與左側項目的從屬關係等資訊\)** | **Location \(URL Link or other physical location\)** |
| :--- | :--- | :--- |
| title |  |  |
| **Used Standards \(使用到的相關標準\)** | - | - |
| standard name |  | 何謂REST\([WIKI](https://en.wikipedia.org/wiki/Representational_state_transfer#Relationship_between_URL_and_HTTP_methods)\) |
| **Related Modules \(此SPEC涉及的模組\) ** | - | - |
| module name |  | [https://hjcian.gitbooks.io/module-template/content/](https://hjcian.gitbooks.io/module-template/content/) |
| **Related Daemons \(此SPEC涉及的daemon\)** | - | - |
| daemon name |  | [https://hjcian.gitbooks.io/daemon-template/content/](https://hjcian.gitbooks.io/daemon-template/content/) |
| **API List\(此SPEC涉及的API\)** | - | - |
| API name |  | [https://hjcian.gitbooks.io/api-template/content/](https://hjcian.gitbooks.io/api-template/content/) |
| **SPEC List \(此SPEC涉及的SPEC\)** | - | - |
| SPEC\#/name |  | [https://hjcian.gitbooks.io/spec-template/content/](https://hjcian.gitbooks.io/spec-template/content/) |



