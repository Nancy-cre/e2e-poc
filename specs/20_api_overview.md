# 20. API 一覧・責務

## 1. API 設計方針

- REST 風エンドポイントとする
- リソース単位で URI を切る
- 認証済ユーザー情報はトークンから解決する想定
- バリデーションエラーは 400
- 認証エラーは 401
- 権限エラーは 403
- 未存在は 404
- 競合は 409
- サーバエラーは 500

## 2. 認証系

| Method | Path | 概要 |
|---|---|---|
| POST | `/auth/login` | ログイン |
| GET | `/auth/me` | ログインユーザー情報取得 |

## 3. 加入者系

| Method | Path | 概要 |
|---|---|---|
| GET | `/policyholders` | 加入者一覧取得 |
| POST | `/policyholders` | 加入者登録 |
| GET | `/policyholders/{id}` | 加入者詳細取得 |
| PUT | `/policyholders/{id}` | 加入者更新 |
| GET | `/policyholders/{id}/families` | 家族情報取得 |
| PUT | `/policyholders/{id}/families` | 家族情報一括更新 |

## 4. 契約申込系

| Method | Path | 概要 |
|---|---|---|
| GET | `/applications` | 申込一覧取得 |
| POST | `/applications` | 申込作成 |
| GET | `/applications/{id}` | 申込詳細取得 |
| PUT | `/applications/{id}` | 申込更新 |
| POST | `/applications/{id}/submit` | 申請 |
| POST | `/applications/{id}/resubmit` | 再申請 |

## 5. 契約系

| Method | Path | 概要 |
|---|---|---|
| GET | `/contracts` | 契約一覧取得 |
| GET | `/contracts/{id}` | 契約詳細取得 |
| POST | `/contracts/{id}/change-requests` | 契約変更申請作成 |
| POST | `/contracts/{id}/cancellation-requests` | 解約申請作成 |

## 6. 審査系

| Method | Path | 概要 |
|---|---|---|
| GET | `/reviews` | 審査一覧取得 |
| GET | `/reviews/{id}` | 審査詳細取得 |
| POST | `/reviews/{id}/approve` | 承認 |
| POST | `/reviews/{id}/return` | 差戻し |
| POST | `/reviews/{id}/reject` | 却下 |

## 7. 給付請求系

| Method | Path | 概要 |
|---|---|---|
| GET | `/claims` | 給付請求一覧取得 |
| POST | `/claims` | 給付請求作成 |
| GET | `/claims/{id}` | 給付請求詳細取得 |
| PUT | `/claims/{id}` | 給付請求更新 |
| POST | `/claims/{id}/submit` | 給付請求申請 |
| POST | `/claims/{id}/resubmit` | 給付請求再申請 |
| POST | `/claims/{id}/payment` | 支払確定 / 保留更新 |

## 8. 管理系

| Method | Path | 概要 |
|---|---|---|
| GET | `/admin/users` | ユーザー一覧取得 |
| POST | `/admin/users` | ユーザー登録 |
| GET | `/admin/users/{id}` | ユーザー詳細取得 |
| PUT | `/admin/users/{id}` | ユーザー更新 |
| GET | `/admin/roles` | ロール一覧取得 |
| GET | `/admin/products` | 保険商品一覧取得 |
| POST | `/admin/products` | 保険商品登録 |
| PUT | `/admin/products/{id}` | 保険商品更新 |
| GET | `/admin/audit-logs` | 監査ログ一覧取得 |

## 9. レスポンス共通例

```json
{
  "data": {},
  "message": "success"
}
```

エラー例:

```json
{
  "errorCode": "VALIDATION_ERROR",
  "message": "契約開始希望日は必須です",
  "details": [
    {
      "field": "desiredStartDate",
      "message": "required"
    }
  ]
}
```

## 10. Lambda 分割の例

以下のいずれでもよい。

### 10.1 ドメイン単位分割

- auth
- policyholder
- application
- contract
- review
- claim
- admin

### 10.2 API 単位分割

- 1 API 1 Lambda  
PoC ではコードが見通しやすい構成を優先する。

## 11. 実装上の留意点

- 一覧検索 API は検索条件未指定時に先頭 50 件程度返却でも可
- ページネーションは offset-limit 方式または cursor 方式のいずれでも可
- 監査ログは主要更新系 API の共通処理で記録する
- ステータス遷移はサービス層で集中管理する
