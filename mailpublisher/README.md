# MailPublisher Driver
このパッケージは[エンバーポイントホールディングス株式会社](https://emberpoint.com/)が提供するメール配信サービスである [MailPublisher Smart Edition](https://emberpoint.com/service/mailpublisher/smart-edition/)をMC2コンソールバックエンドがメール配信で使用するための機能を提供します

## メール配信サービスの利用者
このドライバーは下記の事業者様のみをメール配信の利用者として想定しています。
- [ブックオフグループホールディングス株式会社](https://www.bookoffgroup.co.jp/)

## このドライバーが提供する機能
このドライバーの機能は以下のInterfaceが提供するメソッドとして提供されます。

### パッケージ
apps/console/backend/pkg/infrastructure/mta/mailpublisher

### Interface名
Driver

### 機能
このドライバーは以下の機能を提供します。
インターフェースが提供するメソッドの詳細は各機能のドキュメントで説明しています。

#### [連携ファイル送信](documents/send_datas.md)
メール配信で使用される配信先リストと差し込みデータをMTAに送信します
#### [連携ファイル状態確認](documents/check_send_data_status.md)
[連携ファイル送信](documents/send_datas.md)で送信したデータの受信状態を確認します
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
