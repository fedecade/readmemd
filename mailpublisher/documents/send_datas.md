# [MailPublisher Driver](../README.md) - 連携ファイル送信
メール配信で使用される配信先リストと差し込みデータをMTAに送信します

## 提供メソッド
- ターゲットメールデータ送信 SendTargetingMailData
- レコメンドメールデータ送信 SendRecommendMailData

## ターゲットメールデータ送信

### メソッドシグネチャ
SendTargetingMailData(TargetingMailData) (RequestId, error)

#### TargetingMailData
以下の構造を持つ構造体
```go
type TargetingMailData struct {
    // メール配信基礎データ (コンポジション)
    MailData
    // ターゲットリスト
    Targets      []Target
}

type MailData struct {
    // 契約ID
    ContractId   string `csv:"crm_id"`
    // シナリオID
    SenarioId    int    `csv:"senario_id"`
    // ステップID
    StepId       int    `csv:"step_id"`
    // メールID
    EmailId      int    `csv:"mail_id"`
    // ac_paramのxnoの値に相当する要素
    Xno          string `csv:""`
}

type Target struct {
    // 顧客ID
    CustomerId   int    `csv:"customer_id"`
    // メールアドレス
    EmailAddress string `csv:"email"`
}
```

#### RequestId
- MailPublisherのAPIである`archive_upload.php`のレスポンスに`REQUST_ID`として格納される値
- [連携ファイル送信](documents/send_datas.md)と[メール予約](documents/schedule_email_delivery.md)で使用する

#### error
以下のエラーを返却する可能性がある
- [MtaError](documents/mta_error.md)
- [SystemError](documents/system_error.md)

## レコメンドメールデータ送信

### メソッドシグネチャ
SendRecommendMailData(RecommendMailData) (RequestId, error)

#### RecommendMailData
以下の構造を持つ構造体
```go
type RecommendMailData struct {
    // メール配信基礎データ (コンポジション)
    MailData
    // レコメンドリスト
    Targets      []TargetWithRecommend
}

type TargetWithRecommend struct {
    // ターゲット (コンポジション)
    Target
    // レコメンド
    Recommends   []Recommend
}

type Recommend struct {
    // レコメンドアイテムID
    ItemId       int    `csv:"item_##_id"`
    // レコメンドアイテム名
    ItemName     string `csv:"item_##_title"`
    // レコメンドアイテム作者
    IteAuthor    string `csv:"item_##_author"`
    // レコメンドアイテム価格
    ItemPrice    int    `csv:"item_##_price"`
    // レコメンドアイテムURL
    ItemUrl      string `csv:"item_##_url"`
    // レコメンドアイテム商品画像URL
    ItemImageUrl string `csv:"item_##_image"`
}
```

#### RequestId
- MailPublisherのAPIである`archive_upload.php`のレスポンスに`REQUST_ID`として格納される値
- [連携ファイル送信](documents/send_datas.md)と[メール予約](documents/schedule_email_delivery.md)で使用する

#### error
以下のエラーを返却する可能性がある
- [MtaError](documents/mta_error.md)
- [SystemError](documents/system_error.md)

## Note
### メソッドパラメーター構造体とドメインオブジェクトの関係
#### MailData
|構造体要素名|構造体フィールド名|対応するドメインオブジェクト|
|---|---|---|
|契約ID|ContractId|apps/console/backend/pkg/domain/ma/scenarios/Scenario.ContractId|
|シナリオID|SenarioId|apps/console/backend/pkg/domain/ma/scenarios/Scenario.Id|
|ステップID|StepId|apps/console/backend/pkg/domain/ma/scenarios/Step.Id|
|メールID|EmailId|apps/console/backend/pkg/domain/emails/definitions/EmailDefinition.Id|
|ac_paramのxnoの値に相当する要素|Xno|全く不明->要確認|
##### 要確認事項
- 各フィールドの値の元となるドメインオブジェクト値
- ContractIdをcsvカラムのcrm_idに割り当てているがそれでいいか
- ContractIdがcsvカラムのcrm_id相当である場合、csvカラム名はcrd_idのままにするのか (MailPublisher側でこの値がどの様に使われているか次第と思われる)
##### Target
|構造体要素名|構造体フィールド名|対応するドメインオブジェクト|
|---|---|---|
|顧客ID|CustomerId|apps/console/backend/pkg/domain/ma/cuscustomer_lists/CustomerList.CustomerId もしくは apps/console/backend/pkg/domain/ma/email_email_delivery_lists/EmailDeliveryList.CustomerID|
|メールアドレス|EmailAddress|シナリオの配信対象メールアドレスカラムIDを元に顧客毎スキーマの会員マスタから取得したメールID もしくは apps/console/backend/pkg/domain/ma/email_email_delivery_lists/EmailDeliveryList.EmailAddress|
##### 要確認事項
- 各フィールドの値の元となるドメインオブジェクト値
#### Recommend
|構造体要素名|構造体フィールド名|対応するドメインオブジェクト|
|---|---|---|
|レコメンドアイテムID|ItemId|apps/console/backend/pkg/domain/recommend_items/RecommendItem.Id|
|レコメンドアイテム名|ItemName|apps/console/backend/pkg/domain/recommend_items/RecommendItem.Name|
|レコメンドアイテム作者|IteAuthor|apps/console/backend/pkg/domain/recommend_items/RecommendItem.Descriptions[0].Title|
|レコメンドアイテム価格|ItemPrice|apps/console/backend/pkg/domain/recommend_items/RecommendItem.RealPrice|
|レコメンドアイテムURL|ItemUrl|apps/console/backend/pkg/domain/recommend_items/RecommendItem.CurtUrl|
|レコメンドアイテム商品画像URL|ItemImageUrl|apps/console/backend/pkg/domain/recommend_items/RecommendItem.Descriptions[?].ImageURL|
##### 要確認事項
- 各フィールドの値の元となるドメインオブジェクト値
- レコメンドアイテム作者とレコメンドアイテム商品画像のDescriptionsインデックス
