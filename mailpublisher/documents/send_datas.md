# [MailPublisher Driver](../README.md) - 連携ファイル送信
メール配信で使用される配信先リストと差し込みデータをMTAに送信します
# パッケージ
apps/console/backend/pkg/infrastructure/mta/mailpublisher
# 提供メソッド
- ターゲットメールデータ送信 SendTargetingMailData
- レコメンドメールデータ送信 SendRecommendMailData
# ターゲットメールデータ送信
## メソッドシグネチャ
SendTargetingMailData(TargetingMailData) (RequestId, error)
### TargetingMailData
以下の構造を持つ構造体
```go
type TargetingMailData struct {
    // 契約ID
    //TODO: crm_idの代わりとなると思われるが 1. この値で問題ないか, 2. csvのカラム名はcrd_idのままでよいか
    ContractId string
    // シナリオID
    SenarioId int
    // ステップID
    StepId int
    // メールID
    EmailId int
    // ac_paramのxnoの値に相当する要素
    //TODO: 全く不明->要確認
    Xno string
    // ターゲットリスト
    Targets []Target
}

type Target struct {
    // 顧客ID
    CustomerId int
    // メールアドレス
    EmailAddress string
}
```

### RequestId
- MailPublisherのAPIである`archive_upload.php`のレスポンスに`REQUST_ID`として格納される値
- [連携ファイル送信](documents/send_datas.md)と[メール予約](documents/schedule_email_delivery.md)で使用する

### error
以下のエラーを返却する可能性がある
- [MtaError](documents/mta_error.md)
- [SystemError](documents/system_error.md)
