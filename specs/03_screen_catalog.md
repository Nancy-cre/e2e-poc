# 03. 画面一覧

## 1. 画面一覧表

| 画面ID | 画面名 | 区分 | 主ロール |
|---|---|---|---|
| SCR-001 | ログイン | 共通 | 全ロール |
| SCR-002 | ダッシュボード | 共通 | 全ロール |
| SCR-003 | お知らせ一覧 | 共通 | 全ロール |
| SCR-004 | 加入者一覧 | 加入者 | 申込担当者、審査担当者、管理者 |
| SCR-005 | 加入者詳細 | 加入者 | 申込担当者、審査担当者、管理者 |
| SCR-006 | 加入者新規登録 | 加入者 | 申込担当者、管理者 |
| SCR-007 | 加入者編集 | 加入者 | 申込担当者、管理者 |
| SCR-008 | 家族情報登録・編集 | 加入者 | 申込担当者、管理者 |
| SCR-009 | 契約申込一覧 | 契約 | 申込担当者、審査担当者、管理者 |
| SCR-010 | 契約申込詳細 | 契約 | 申込担当者、審査担当者、管理者 |
| SCR-011 | 新規契約申込作成 | 契約 | 申込担当者 |
| SCR-012 | 契約一覧 | 契約 | 申込担当者、審査担当者、管理者 |
| SCR-013 | 契約詳細 | 契約 | 申込担当者、審査担当者、管理者 |
| SCR-014 | 契約変更申請作成 | 契約 | 申込担当者 |
| SCR-015 | 解約申請作成 | 契約 | 申込担当者 |
| SCR-016 | 審査一覧 | 審査 | 審査担当者、管理者 |
| SCR-017 | 審査詳細 | 審査 | 審査担当者、管理者 |
| SCR-018 | 給付請求一覧 | 給付請求 | 申込担当者、審査担当者、支払担当者、管理者 |
| SCR-019 | 給付請求詳細 | 給付請求 | 申込担当者、審査担当者、支払担当者、管理者 |
| SCR-020 | 給付請求作成 | 給付請求 | 申込担当者 |
| SCR-021 | 支払処理 | 給付請求 | 支払担当者 |
| SCR-022 | ユーザー一覧 | 管理 | 管理者 |
| SCR-023 | ユーザー登録・編集 | 管理 | 管理者 |
| SCR-024 | ロール一覧 | 管理 | 管理者 |
| SCR-025 | 保険商品一覧・編集 | 管理 | 管理者 |
| SCR-026 | 監査ログ一覧 | 管理 | 管理者 |

## 2. 画面遷移方針

- ログイン後はダッシュボードへ遷移する
- 左メニューから機能遷移する
- 一覧画面から詳細画面へ遷移する
- 登録・編集完了後は対象詳細または一覧へ戻る
- 審査案件は審査一覧 → 審査詳細の流れを基本とする

## 3. ルーティング例

- `/login`
- `/dashboard`
- `/announcements`
- `/policyholders`
- `/policyholders/:policyholderId`
- `/policyholders/new`
- `/policyholders/:policyholderId/edit`
- `/policyholders/:policyholderId/family`
- `/applications`
- `/applications/:applicationId`
- `/applications/new`
- `/contracts`
- `/contracts/:contractId`
- `/contracts/:contractId/change`
- `/contracts/:contractId/cancel`
- `/reviews`
- `/reviews/:reviewId`
- `/claims`
- `/claims/:claimId`
- `/claims/new`
- `/claims/:claimId/payment`
- `/admin/users`
- `/admin/users/:userId/edit`
- `/admin/roles`
- `/admin/products`
- `/admin/audit-logs`

## 4. 画面設計共通ルール

- 一覧画面は検索条件、検索結果一覧、ページネーションを持つ
- 詳細画面は参照項目セクション、関連情報セクション、操作ボタンを持つ
- フォーム画面は必須項目を明示し、保存、申請、取消ボタンを持つ
- ステータスに応じて活性ボタンを制御する
- 主要操作ボタンには確認ダイアログを出す
- E2E テストのため、フォーム・ボタン・テーブル行には data-testid を付与する
