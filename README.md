# Team Task Manager API

チームで利用することを想定したタスク管理APIです。  
プロジェクト単位でタスクを管理し、メンバーへの担当アサインや進捗管理を行うことができます。

本プロジェクトは、バックエンドAPI開発のポートフォリオとして  
**Spring Boot / PostgreSQL / AWS** を使用した実務に近いアーキテクチャを意識して開発しています。

---

# Project Overview

チーム開発では、複数のメンバーが同じプロジェクト内でタスクを共有し、  
担当者や進捗状況を管理する必要があります。

本APIでは以下のようなユースケースを想定しています。

- チームメンバーがプロジェクトを作成する
- プロジェクトにメンバーを追加する
- タスクを作成する
- タスクの担当者を設定する
- タスクの進捗状況を管理する

---

# Tech Stack

| 技術 | 用途 |
|-----|------|
Java | メインプログラミング言語 |
Spring Boot | REST API フレームワーク |
PostgreSQL | データベース |
JPA / Hibernate | ORM |
Git / GitHub | バージョン管理 |
Docker（予定） | コンテナ化 |
AWS（予定） | インフラ |

---

# Architecture

本プロジェクトでは一般的な **レイヤードアーキテクチャ** を採用しています。


Controller
↓
Service
↓
Repository
↓
Database


各レイヤーの役割

Controller  
APIエンドポイントの定義

Service  
ビジネスロジックの実装

Repository  
データベースアクセス

Database  
PostgreSQL

---

# ER Diagram

![ER Diagram](docs/er-diagram.png)

---

# Features

## User Registration

ユーザーはメールアドレスとパスワードを登録することでアカウントを作成できます。  
登録された情報はデータベースに保存され、今後の認証処理に利用されます。

---

## Login

登録されたユーザーはログイン機能を利用して認証を行います。  
将来的にはJWTを用いた認証方式を実装予定です。

---

## Project Management

ユーザーは新しいプロジェクトを作成できます。  
また、自分が所属するプロジェクト一覧を取得することができます。

---

## Project Member Management

プロジェクトにメンバーを追加することで、チーム単位でタスク管理が可能になります。

---

## Task Management

プロジェクト内でタスクを作成し、タスクの更新や削除を行うことができます。

---

## Task Assignment

タスクを特定のユーザーへアサインすることができます。  
これにより担当者ごとのタスク管理が可能になります。

---

## Task Status Management

タスクの進捗は以下のステータスで管理します。

- TODO
- DOING
- DONE

---

# API Endpoints

## User

POST /users  
ユーザー登録

POST /login  
ログイン

---

## Projects

GET /projects  
所属プロジェクト一覧取得

POST /projects  
プロジェクト作成

---

## Tasks

GET /projects/{id}/tasks  
プロジェクト内タスク取得

POST /tasks  
タスク作成

PATCH /tasks/{id}  
タスク更新

DELETE /tasks/{id}  
タスク削除（論理削除）

---

# Database Design

本プロジェクトでは以下のテーブルを使用しています。

- users
- projects
- project_members
- tasks

ユーザーとプロジェクトは **多対多の関係**になるため  
中間テーブルとして `project_members` を設計しています。

また、タスク削除時には履歴を保持するため **論理削除（deleted_at）** を採用しています。

---

# Getting Started

今後以下の手順でローカル環境で動作できるように整備予定です。


git clone
docker compose up


---

# Future Improvements

今後以下の機能を追加予定です。

- JWT認証
- Role-based access control（権限管理）
- API validation
- Docker対応
- AWSデプロイ
- CI/CD（GitHub Actions）

---

# Author

Hiroya Yamada
