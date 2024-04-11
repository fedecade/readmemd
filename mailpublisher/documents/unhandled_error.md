# UnhandledError
[MailPublisher Smart Edition](https://emberpoint.com/service/mailpublisher/smart-edition/)から返却されたエラー以外の対処不能なエラーを表します。

### パッケージ
apps/console/backend/pkg/infrastructure/mta/mailpublisher

### 構造体名
UnhandledError

### 生成関数
```go
NewUnhandledError(RootCase) UnhandledError
```
### レシーバーメソッド
```go
// RootCaseがErrorメソッドで提供する文字列を取得します (errors.Errorの実装)
Error() string
```
#### RootCase 元となったエラー
##### 生成関数
```go
ToRootCase(error) RootCase
```
##### レシーバーメソッド
```go
// 元となったエラーオブジェクトを取得します
Error() error
```
