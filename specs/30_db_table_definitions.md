# 30. テーブル定義書

## 1. テーブル一覧

| テーブル名 | 論理名 |
|---|---|
| users | ユーザー |
| roles | ロール |
| user_roles | ユーザーロール |
| announcements | お知らせ |
| insurance_products | 保険商品 |
| insurance_plans | 保険プラン |
| policyholders | 加入者 |
| policyholder_families | 加入者家族情報 |
| applications | 契約申込 |
| application_documents | 申込添付書類 |
| contracts | 契約 |
| contract_change_requests | 契約変更申請 |
| cancellation_requests | 解約申請 |
| claims | 給付請求 |
| claim_documents | 給付請求添付書類 |
| reviews | 審査 |
| review_histories | 審査履歴 |
| payments | 支払 |
| audit_logs | 監査ログ |

---

## 2. users

| No | カラム名 | 型 | PK | NN | UK | 説明 |
|---|---|---|---|---|---|---|
| 1 | id | bigserial | Y | Y |  | ユーザーID |
| 2 | login_id | varchar(50) |  | Y | Y | ログインID |
| 3 | user_name | varchar(100) |  | Y |  | 氏名 |
| 4 | email | varchar(255) |  | Y | Y | メールアドレス |
| 5 | password_hash | varchar(255) |  | Y |  | パスワードハッシュ |
| 6 | is_active | boolean |  | Y |  | 有効フラグ |
| 7 | created_at | timestamp |  | Y |  | 作成日時 |
| 8 | created_by | bigint |  |  |  | 作成者 |
| 9 | updated_at | timestamp |  | Y |  | 更新日時 |
| 10 | updated_by | bigint |  |  |  | 更新者 |

## 3. roles

| No | カラム名 | 型 | PK | NN | UK | 説明 |
|---|---|---|---|---|---|---|
| 1 | id | bigserial | Y | Y |  | ロールID |
| 2 | role_code | varchar(30) |  | Y | Y | 例: APPLICANT, UNDERWRITER |
| 3 | role_name | varchar(100) |  | Y |  | ロール名 |
| 4 | description | varchar(500) |  |  |  | 説明 |

## 4. user_roles

| No | カラム名 | 型 | PK | NN | UK | 説明 |
|---|---|---|---|---|---|---|
| 1 | id | bigserial | Y | Y |  | ユーザーロールID |
| 2 | user_id | bigint |  | Y |  | users.id |
| 3 | role_id | bigint |  | Y |  | roles.id |
| 4 | assigned_at | timestamp |  | Y |  | 付与日時 |

制約:
- UNIQUE(user_id, role_id)

## 5. announcements

| No | カラム名 | 型 | PK | NN | UK | 説明 |
|---|---|---|---|---|---|---|
| 1 | id | bigserial | Y | Y |  | お知らせID |
| 2 | title | varchar(200) |  | Y |  | タイトル |
| 3 | body | text |  | Y |  | 本文 |
| 4 | publish_from | date |  | Y |  | 掲載開始日 |
| 5 | publish_to | date |  | Y |  | 掲載終了日 |
| 6 | is_published | boolean |  | Y |  | 公開フラグ |
| 7 | created_at | timestamp |  | Y |  | 作成日時 |
| 8 | created_by | bigint |  |  |  | 作成者 |

## 6. insurance_products

| No | カラム名 | 型 | PK | NN | UK | 説明 |
|---|---|---|---|---|---|---|
| 1 | id | bigserial | Y | Y |  | 商品ID |
| 2 | product_code | varchar(30) |  | Y | Y | 商品コード |
| 3 | product_name | varchar(100) |  | Y |  | 商品名 |
| 4 | product_type | varchar(30) |  | Y |  | MEDICAL/CANCER/INJURY |
| 5 | description | text |  |  |  | 説明 |
| 6 | min_insured_amount | numeric(12,2) |  | Y |  | 最低保険金額 |
| 7 | max_insured_amount | numeric(12,2) |  | Y |  | 最高保険金額 |
| 8 | claim_limit_amount | numeric(12,2) |  | Y |  | 請求上限額 |
| 9 | is_active | boolean |  | Y |  | 有効フラグ |
| 10 | created_at | timestamp |  | Y |  | 作成日時 |
| 11 | created_by | bigint |  |  |  | 作成者 |
| 12 | updated_at | timestamp |  | Y |  | 更新日時 |
| 13 | updated_by | bigint |  |  |  | 更新者 |

## 7. insurance_plans

| No | カラム名 | 型 | PK | NN | UK | 説明 |
|---|---|---|---|---|---|---|
| 1 | id | bigserial | Y | Y |  | プランID |
| 2 | product_id | bigint |  | Y |  | insurance_products.id |
| 3 | plan_code | varchar(30) |  | Y |  | プランコード |
| 4 | plan_name | varchar(100) |  | Y |  | プラン名 |
| 5 | premium_type | varchar(20) |  | Y |  | MONTHLY/YEARLY |
| 6 | default_insured_amount | numeric(12,2) |  | Y |  | デフォルト保険金額 |
| 7 | is_active | boolean |  | Y |  | 有効フラグ |

制約:
- UNIQUE(product_id, plan_code)

## 8. policyholders

| No | カラム名 | 型 | PK | NN | UK | 説明 |
|---|---|---|---|---|---|---|
| 1 | id | bigserial | Y | Y |  | 加入者内部ID |
| 2 | policyholder_no | varchar(20) |  | Y | Y | 加入者番号 |
| 3 | full_name | varchar(100) |  | Y |  | 氏名 |
| 4 | full_name_kana | varchar(100) |  | Y |  | 氏名カナ |
| 5 | birth_date | date |  | Y |  | 生年月日 |
| 6 | gender | varchar(10) |  | Y |  | 性別 |
| 7 | postal_code | varchar(10) |  | Y |  | 郵便番号 |
| 8 | prefecture | varchar(50) |  | Y |  | 都道府県 |
| 9 | address1 | varchar(255) |  | Y |  | 住所1 |
| 10 | address2 | varchar(255) |  |  |  | 住所2 |
| 11 | phone_number | varchar(20) |  |  |  | 電話番号 |
| 12 | email | varchar(255) |  |  |  | メールアドレス |
| 13 | identity_document_no | varchar(50) |  |  |  | 本人確認書類番号 |
| 14 | created_at | timestamp |  | Y |  | 作成日時 |
| 15 | created_by | bigint |  |  |  | 作成者 |
| 16 | updated_at | timestamp |  | Y |  | 更新日時 |
| 17 | updated_by | bigint |  |  |  | 更新者 |

## 9. policyholder_families

| No | カラム名 | 型 | PK | NN | UK | 説明 |
|---|---|---|---|---|---|---|
| 1 | id | bigserial | Y | Y |  | 家族情報ID |
| 2 | policyholder_id | bigint |  | Y |  | policyholders.id |
| 3 | family_name | varchar(100) |  | Y |  | 家族氏名 |
| 4 | relationship | varchar(30) |  | Y |  | 続柄 |
| 5 | birth_date | date |  |  |  | 生年月日 |
| 6 | is_cohabiting | boolean |  | Y |  | 同居フラグ |
| 7 | sort_order | integer |  | Y |  | 表示順 |

## 10. applications

| No | カラム名 | 型 | PK | NN | UK | 説明 |
|---|---|---|---|---|---|---|
| 1 | id | bigserial | Y | Y |  | 申込ID |
| 2 | application_no | varchar(20) |  | Y | Y | 申込番号 |
| 3 | contractor_policyholder_id | bigint |  | Y |  | 契約者加入者ID |
| 4 | insured_policyholder_id | bigint |  | Y |  | 被保険者加入者ID |
| 5 | product_id | bigint |  | Y |  | insurance_products.id |
| 6 | plan_id | bigint |  | Y |  | insurance_plans.id |
| 7 | desired_start_date | date |  | Y |  | 契約開始希望日 |
| 8 | desired_end_date | date |  | Y |  | 契約終了予定日 |
| 9 | insured_amount | numeric(12,2) |  | Y |  | 保険金額 |
| 10 | payment_cycle | varchar(20) |  | Y |  | MONTHLY/YEARLY |
| 11 | smoking_flag | boolean |  | Y |  | 喫煙有無 |
| 12 | medical_history_flag | boolean |  | Y |  | 既往歴有無 |
| 13 | hospitalization_history_flag | boolean |  | Y |  | 入院歴有無 |
| 14 | remarks | text |  |  |  | 備考 |
| 15 | status | varchar(20) |  | Y |  | DRAFT等 |
| 16 | submitted_at | timestamp |  |  |  | 申請日時 |
| 17 | last_reviewed_at | timestamp |  |  |  | 最終審査日時 |
| 18 | created_at | timestamp |  | Y |  | 作成日時 |
| 19 | created_by | bigint |  | Y |  | 作成者 |
| 20 | updated_at | timestamp |  | Y |  | 更新日時 |
| 21 | updated_by | bigint |  |  |  | 更新者 |

## 11. application_documents

| No | カラム名 | 型 | PK | NN | UK | 説明 |
|---|---|---|---|---|---|---|
| 1 | id | bigserial | Y | Y |  | 申込書類ID |
| 2 | application_id | bigint |  | Y |  | applications.id |
| 3 | document_type | varchar(30) |  | Y |  | IDENTITY 等 |
| 4 | file_name | varchar(255) |  | Y |  | ファイル名 |
| 5 | mime_type | varchar(100) |  |  |  | MIME タイプ |
| 6 | file_size | bigint |  |  |  | ファイルサイズ |
| 7 | storage_key | varchar(255) |  |  |  | 格納キー |
| 8 | uploaded_at | timestamp |  | Y |  | 登録日時 |
| 9 | uploaded_by | bigint |  | Y |  | 登録者 |

## 12. contracts

| No | カラム名 | 型 | PK | NN | UK | 説明 |
|---|---|---|---|---|---|---|
| 1 | id | bigserial | Y | Y |  | 契約ID |
| 2 | contract_no | varchar(20) |  | Y | Y | 契約番号 |
| 3 | application_id | bigint |  | Y |  | 元申込ID |
| 4 | contractor_policyholder_id | bigint |  | Y |  | 契約者加入者ID |
| 5 | insured_policyholder_id | bigint |  | Y |  | 被保険者加入者ID |
| 6 | product_id | bigint |  | Y |  | insurance_products.id |
| 7 | plan_id | bigint |  | Y |  | insurance_plans.id |
| 8 | contract_start_date | date |  | Y |  | 契約開始日 |
| 9 | contract_end_date | date |  | Y |  | 契約終了予定日 |
| 10 | insured_amount | numeric(12,2) |  | Y |  | 保険金額 |
| 11 | payment_cycle | varchar(20) |  | Y |  | 支払サイクル |
| 12 | status | varchar(30) |  | Y |  | ACTIVE等 |
| 13 | approved_at | timestamp |  |  |  | 承認日時 |
| 14 | approved_by | bigint |  |  |  | 承認者 |
| 15 | created_at | timestamp |  | Y |  | 作成日時 |
| 16 | created_by | bigint |  | Y |  | 作成者 |
| 17 | updated_at | timestamp |  | Y |  | 更新日時 |
| 18 | updated_by | bigint |  |  |  | 更新者 |

## 13. contract_change_requests

| No | カラム名 | 型 | PK | NN | UK | 説明 |
|---|---|---|---|---|---|---|
| 1 | id | bigserial | Y | Y |  | 変更申請ID |
| 2 | request_no | varchar(20) |  | Y | Y | 変更申請番号 |
| 3 | contract_id | bigint |  | Y |  | contracts.id |
| 4 | change_type | varchar(30) |  | Y |  | ADDRESS_CHANGE等 |
| 5 | effective_date | date |  | Y |  | 適用希望日 |
| 6 | reason | varchar(500) |  | Y |  | 変更理由 |
| 7 | new_postal_code | varchar(10) |  |  |  | 新郵便番号 |
| 8 | new_prefecture | varchar(50) |  |  |  | 新都道府県 |
| 9 | new_address1 | varchar(255) |  |  |  | 新住所1 |
| 10 | new_address2 | varchar(255) |  |  |  | 新住所2 |
| 11 | new_phone_number | varchar(20) |  |  |  | 新電話番号 |
| 12 | new_email | varchar(255) |  |  |  | 新メールアドレス |
| 13 | new_plan_id | bigint |  |  |  | 新プランID |
| 14 | new_insured_amount | numeric(12,2) |  |  |  | 新保険金額 |
| 15 | status | varchar(20) |  | Y |  | DRAFT等 |
| 16 | submitted_at | timestamp |  |  |  | 申請日時 |
| 17 | created_at | timestamp |  | Y |  | 作成日時 |
| 18 | created_by | bigint |  | Y |  | 作成者 |
| 19 | updated_at | timestamp |  | Y |  | 更新日時 |
| 20 | updated_by | bigint |  |  |  | 更新者 |

## 14. cancellation_requests

| No | カラム名 | 型 | PK | NN | UK | 説明 |
|---|---|---|---|---|---|---|
| 1 | id | bigserial | Y | Y |  | 解約申請ID |
| 2 | request_no | varchar(20) |  | Y | Y | 解約申請番号 |
| 3 | contract_id | bigint |  | Y |  | contracts.id |
| 4 | requested_cancel_date | date |  | Y |  | 解約希望日 |
| 5 | cancel_reason | varchar(500) |  | Y |  | 解約理由 |
| 6 | remarks | text |  |  |  | 備考 |
| 7 | status | varchar(20) |  | Y |  | SUBMITTED等 |
| 8 | submitted_at | timestamp |  |  |  | 申請日時 |
| 9 | created_at | timestamp |  | Y |  | 作成日時 |
| 10 | created_by | bigint |  | Y |  | 作成者 |
| 11 | updated_at | timestamp |  | Y |  | 更新日時 |
| 12 | updated_by | bigint |  |  |  | 更新者 |

## 15. claims

| No | カラム名 | 型 | PK | NN | UK | 説明 |
|---|---|---|---|---|---|---|
| 1 | id | bigserial | Y | Y |  | 請求ID |
| 2 | claim_no | varchar(20) |  | Y | Y | 請求番号 |
| 3 | contract_id | bigint |  | Y |  | contracts.id |
| 4 | incident_date | date |  | Y |  | 事故日 |
| 5 | claim_type | varchar(30) |  | Y |  | HOSPITALIZATION等 |
| 6 | claim_amount | numeric(12,2) |  | Y |  | 請求金額 |
| 7 | incident_summary | text |  | Y |  | 事故概要 |
| 8 | remarks | text |  |  |  | 備考 |
| 9 | status | varchar(20) |  | Y |  | DRAFT等 |
| 10 | submitted_at | timestamp |  |  |  | 申請日時 |
| 11 | approved_at | timestamp |  |  |  | 承認日時 |
| 12 | approved_by | bigint |  |  |  | 承認者 |
| 13 | created_at | timestamp |  | Y |  | 作成日時 |
| 14 | created_by | bigint |  | Y |  | 作成者 |
| 15 | updated_at | timestamp |  | Y |  | 更新日時 |
| 16 | updated_by | bigint |  |  |  | 更新者 |

## 16. claim_documents

| No | カラム名 | 型 | PK | NN | UK | 説明 |
|---|---|---|---|---|---|---|
| 1 | id | bigserial | Y | Y |  | 請求書類ID |
| 2 | claim_id | bigint |  | Y |  | claims.id |
| 3 | document_type | varchar(30) |  | Y |  | MEDICAL_CERT/RECEIPT等 |
| 4 | file_name | varchar(255) |  | Y |  | ファイル名 |
| 5 | mime_type | varchar(100) |  |  |  | MIME タイプ |
| 6 | file_size | bigint |  |  |  | ファイルサイズ |
| 7 | storage_key | varchar(255) |  |  |  | 格納キー |
| 8 | uploaded_at | timestamp |  | Y |  | 登録日時 |
| 9 | uploaded_by | bigint |  | Y |  | 登録者 |

## 17. reviews

| No | カラム名 | 型 | PK | NN | UK | 説明 |
|---|---|---|---|---|---|---|
| 1 | id | bigserial | Y | Y |  | 審査ID |
| 2 | review_type | varchar(30) |  | Y |  | APPLICATION/CHANGE/CANCELLATION/CLAIM |
| 3 | target_id | bigint |  | Y |  | 審査対象ID |
| 4 | current_status | varchar(20) |  | Y |  | IN_REVIEW等 |
| 5 | assigned_user_id | bigint |  |  |  | 担当審査者 |
| 6 | received_at | timestamp |  | Y |  | 受付日時 |
| 7 | completed_at | timestamp |  |  |  | 完了日時 |
| 8 | created_at | timestamp |  | Y |  | 作成日時 |
| 9 | created_by | bigint |  | Y |  | 作成者 |

補足:
- `target_id` は review_type に応じて applications / contract_change_requests / cancellation_requests / claims を参照するポリモーフィック設計

## 18. review_histories

| No | カラム名 | 型 | PK | NN | UK | 説明 |
|---|---|---|---|---|---|---|
| 1 | id | bigserial | Y | Y |  | 審査履歴ID |
| 2 | review_id | bigint |  | Y |  | reviews.id |
| 3 | action_type | varchar(20) |  | Y |  | APPROVE/RETURN/REJECT |
| 4 | action_comment | text |  |  |  | コメント |
| 5 | action_by | bigint |  | Y |  | 実行者 |
| 6 | action_at | timestamp |  | Y |  | 実行日時 |

## 19. payments

| No | カラム名 | 型 | PK | NN | UK | 説明 |
|---|---|---|---|---|---|---|
| 1 | id | bigserial | Y | Y |  | 支払ID |
| 2 | claim_id | bigint |  | Y | Y | claims.id |
| 3 | scheduled_amount | numeric(12,2) |  | Y |  | 支払予定金額 |
| 4 | paid_amount | numeric(12,2) |  |  |  | 支払金額 |
| 5 | payment_date | date |  |  |  | 支払日 |
| 6 | payment_method | varchar(20) |  |  |  | BANK_TRANSFER/CASH |
| 7 | payment_result | varchar(20) |  |  |  | SUCCESS/HOLD |
| 8 | payment_note | text |  |  |  | 支払備考 |
| 9 | created_at | timestamp |  | Y |  | 作成日時 |
| 10 | created_by | bigint |  | Y |  | 作成者 |
| 11 | updated_at | timestamp |  | Y |  | 更新日時 |
| 12 | updated_by | bigint |  |  |  | 更新者 |

## 20. audit_logs

| No | カラム名 | 型 | PK | NN | UK | 説明 |
|---|---|---|---|---|---|---|
| 1 | id | bigserial | Y | Y |  | 監査ログID |
| 2 | event_type | varchar(50) |  | Y |  | LOGIN/APPLICATION_SUBMIT等 |
| 3 | target_type | varchar(50) |  | Y |  | APPLICATION/CONTRACT等 |
| 4 | target_id | varchar(50) |  | Y |  | 対象ID |
| 5 | action_result | varchar(20) |  | Y |  | SUCCESS/FAILURE |
| 6 | executed_by | bigint |  |  |  | 実行者 |
| 7 | executed_at | timestamp |  | Y |  | 実行日時 |
| 8 | before_value | jsonb |  |  |  | 変更前 |
| 9 | after_value | jsonb |  |  |  | 変更後 |
| 10 | source_ip | varchar(50) |  |  |  | 送信元IP |

## 21. 主な外部キー一覧

- user_roles.user_id -> users.id
- user_roles.role_id -> roles.id
- insurance_plans.product_id -> insurance_products.id
- policyholder_families.policyholder_id -> policyholders.id
- applications.contractor_policyholder_id -> policyholders.id
- applications.insured_policyholder_id -> policyholders.id
- applications.product_id -> insurance_products.id
- applications.plan_id -> insurance_plans.id
- application_documents.application_id -> applications.id
- contracts.application_id -> applications.id
- contracts.contractor_policyholder_id -> policyholders.id
- contracts.insured_policyholder_id -> policyholders.id
- contracts.product_id -> insurance_products.id
- contracts.plan_id -> insurance_plans.id
- contract_change_requests.contract_id -> contracts.id
- cancellation_requests.contract_id -> contracts.id
- claims.contract_id -> contracts.id
- claim_documents.claim_id -> claims.id
- review_histories.review_id -> reviews.id
- payments.claim_id -> claims.id

## 22. 採番方針

- 加入者番号: `PH00000001`
- 申込番号: `AP00000001`
- 契約番号: `CT00000001`
- 変更申請番号: `CR00000001`
- 解約申請番号: `CN00000001`
- 請求番号: `CL00000001`

## 23. インデックス推奨

- users(login_id)
- policyholders(policyholder_no)
- policyholders(full_name)
- applications(application_no, status)
- contracts(contract_no, status)
- claims(claim_no, status)
- reviews(review_type, current_status, received_at)
- audit_logs(event_type, executed_at)

## 24. 実装補足

PoC では複雑な正規化よりも実装容易性を優先している。  
ただし、以下の整合性は必ず担保すること。

- 契約は承認済み申込からのみ生成される
- 変更申請、解約申請、給付請求は ACTIVE 契約に対してのみ作成できる
- 支払は承認済み給付請求に対してのみ実施できる
