# メールデータアップロード
メール配信で使用される配信先リストと差し込みデータをMTAにアップロードします

## 提供メソッド
- [ターゲットメールデータアップロード](#ターゲットメールデータアップロード)
- [レコメンドメールデータアップロード](#レコメンドメールデータアップロード)

## ターゲットメールデータアップロード

### メソッドシグネチャ
UploadTargetingMailData(TargetingMailData) (RequestId, error)

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
    ScenarioId   int    `csv:"senario_id"`
    // ステップID
    StepId       int    `csv:"step_id"`
    // ステップID
    StepPlanId   int    `csv:"step_plan_id"`
    // メールID
    EmailId      int    `csv:"mail_id"`
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
- [メールデータアップロード](./update_maildata.md)と[メール予約](./schedule_email_delivery.md)で使用する

#### error
以下のエラーを返却する可能性がある
- [MtaError](./mta_error.md)
- [UnhandledError](./system_error.md)

## レコメンドメールデータアップロード

### メソッドシグネチャ
UploadRecommendMailData(RecommendMailData) (RequestId, error)

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
    ItemAuthor   string `csv:"item_##_author"`
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
- [メールデータアップロード](./update_maildata.md)と[メール予約](./schedule_email_delivery.md)で使用する

#### error
以下のエラーを返却する可能性がある
- [MtaError](./mta_error.md)
- [UnhandledError](./unhandled_error.md)

## Note
### メソッドパラメーター構造体とドメインオブジェクトの関係
#### MailData
|構造体要素名|構造体フィールド名|対応するドメインオブジェクト|
|---|---|---|
|契約ID|ContractId|apps/console/backend/pkg/domain/ma/scenarios/Scenario.ContractId|
|シナリオID|ScenarioId|apps/console/backend/pkg/domain/ma/scenarios/Scenario.Id|
|ステップID|StepId|apps/console/backend/pkg/domain/ma/scenarios/Step.Id|
|メールID|EmailId|apps/console/backend/pkg/domain/emails/definitions/EmailDefinition.Id|
##### 要確認事項
- 各フィールドの値の元となるドメインオブジェクト値
- ContractIdをcsvカラムのcrm_idに割り当てているがそれでいいか
- ContractIdがcsvカラムのcrm_id相当である場合、csvカラム名はcrd_idのままにするのか (MailPublisher側でこの値がどの様に使われているか次第と思われる)
##### Target
|構造体要素名|構造体フィールド名|対応するドメインオブジェクト|
|---|---|---|
|顧客ID|CustomerId|apps/console/backend/pkg/domain/delivery/delivery_targets/email_delivery_targets/DeliveryTarget.CustomerId|
|メールアドレス|EmailAddress|apps/console/backend/pkg/domain/delivery/delivery_targets/email_delivery_targets/DeliveryTarget.EmailAddress|
##### 要確認事項
- 各フィールドの値の元となるドメインオブジェクト値
#### Recommend
|構造体要素名|構造体フィールド名|対応するドメインオブジェクト|
|---|---|---|
pkg/domain/template_variables/recommend.go
|レコメンドアイテムID|ItemId|apps/console/backend/pkg/domain/template_variabes/Item.ItemId|
|レコメンドアイテム名|ItemName|apps/console/backend/pkg/domain/template_variabes/Item.ItemName|
|レコメンドアイテム作者|ItemAuthor|apps/console/backend/pkg/domain/template_variabes/Item.Desc|
|レコメンドアイテム価格|ItemPrice|apps/console/backend/pkg/domain/template_variabes/Item.RealPrice|
|レコメンドアイテムURL|ItemUrl|apps/console/backend/pkg/domain/template_variabes/Item.LinkUrl|
|レコメンドアイテム商品画像URL|ItemImageUrl|apps/console/backend/pkg/domain/template_variabes/Item.ImageUrl|
##### 要確認事項
- 各フィールドの値の元となるドメインオブジェクト値
