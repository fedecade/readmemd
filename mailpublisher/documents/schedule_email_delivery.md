# メール配信予約
メール配信を予約します

## 提供メソッド
- [メール配信予約](#メール配信予約)

## メール配信予約

### メソッドシグネチャ
```go
ScheduleEmailDelivery(RequestId, Schedule) error
```

#### RequestId
- [メールデータ送信](./send_datas.md)で取得した、MailPublisherのAPIである`archive_upload.php`のレスポンスに`REQUST_ID`として格納される値

#### Schedule
以下の生成関数によって生成され、以下のレシーバーメソッドを持つ配信予約日時を表すユーザー定義型。
##### 生成関数
```go
ToSchedule(time.Time) Schedule
```
##### レシーバーメソッド
```go
// 配信予約日時のtime.Time値を取得する
Time() time.Time
```

#### ScheduleDeliveryStaus
- 処理の状態を返す
- エラー発生時はUndefineを返し、それ以外の場合はUndefine以外のいずれかの値を状態によって返す
```go
type ScheduleDeliveryStaus int
var ScheduleDeliveryStauses = struct{
    // リクエストが受け付けられない状態 (リトライ対象)
    Busy      ScheduleDeliveryStaus
    // リクエスト受付成功
    Done      ScheduleDeliveryStaus
    // 不定値
    Undefine  ScheduleDeliveryStaus
} {
    Busy:     ScheduleDeliveryStaus{1}
    Done:     ScheduleDeliveryStaus{0}
    Undefine: ScheduleDeliveryStaus{-1}
}
```

#### error
- 正常終了した場合はnil
- 異常終了した場合は以下のいずれかのエラーを返却する
    + [MtaError](./mta_error.md)
    + [UnhandledError](./system_error.md)

#### 要確認事項
ドキュメント "[MailPublisher連携](https://www.notion.so/MailPublisher-91cb28036211475bbc27c3ac911b3579?pvs=4)" には MTAへのリクエストパラメーターとして 'draft_id' が要求されているが、
- MC2において、この値はだれがいつどこに設定するものか
- MC2におけるこの値の取得元は何か
