# MailPublisher Driver
このパッケージは[エンバーポイントホールディングス株式会社](https://emberpoint.com/)が提供するメール配信サービスである [MailPublisher Smart Edition](https://emberpoint.com/service/mailpublisher/smart-edition/)をMC2コンソールバックエンドがメール配信で使用するための機能を提供します

## メール配信サービスの利用者
このドライバーは下記の事業者様のみをメール配信の利用者として想定しています。
- [ブックオフグループホールディングス株式会社](https://www.bookoffgroup.co.jp/)

## このドライバーが提供する機能
このドライバーの機能は以下のInterfaceが提供するメソッドとして提供されます。

### パッケージ
```go
apps/console/backend/pkg/infrastructure/mta/mailpublisher
```

### Interface名
```go
Driver
```

### 機能
このドライバーは以下の機能を提供します。
インターフェースが提供するメソッドの詳細は各機能のドキュメントで説明しています。

#### [メールデータアップロード](documents/upload_maildata.md)
メール配信で使用される配信先リストと差し込みデータをMTAにアップロードします
#### [メールデータアップロード状態取得](documents/get_uploaded_maildata_status.md)
[メールデータアップロード](documents/upload_maildata.md)でアップロードしたデータの状態を取得します
#### [メール予約](documents/schedule_email_delivery.md)
メール配信を予約します

## このドライバーの使用方法
このドライバーを使用する際は、以下の関数によってInterfaceオブジェクトを入手します。

### パッケージ
`apps/console/backend/pkg/infrastructure/mta/mailpublisher`

### 関数名 
`NewDriver`

### 関数のシグネチャ
```go
NewDriver(RequestUrl, LoginId, LoginPassword) Driver
```
#### RequestUrl リクエスト先URL
以下の生成関数によって生成され、以下のレシーバーメソッドを持つユーザー定義型。
フルスペックのURL文字列が期待されます。
##### 生成関数
```go
ToRequestUrl(string) RequestUrl
```
##### レシーバーメソッド
```go
// リクエストURLの文字列値を取得する
String() string
```
#### LoginId MailPublisher Smart EditionのログインID
以下の生成関数によって生成され、以下のレシーバーメソッドを持つユーザー定義型。
##### 生成関数
```go
ToLoginId(string) LoginId
```
##### レシーバーメソッド
```go
// リクエストURLの文字列値を取得する
String() string
```
#### LoginPassword MailPublisher Smart Editionのログインパスワード
以下の生成関数によって生成され、以下のレシーバーメソッドを持つユーザー定義型。
##### 生成関数
```go
ToLoginPassword(string) LoginPassword
```
##### レシーバーメソッド
```go
// リクエストURLの文字列値を取得する
String() string
```
