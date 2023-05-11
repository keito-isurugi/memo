# Laravel

## 全てのリクエストは/public直下のindex.phpにアクセスする
- .htaccessに記載されている

### オートロードファイルの読み込み
- vendor/autoload.php
	- 名前空間が付与されたクラスを利用するためにオートロード
	
### アプリケーションインスタンスの生成
- bootstrap/app.php
	- Illuminate\Foundation\Applicationのインスタンス生成
		- Laravelの本体といえるクラス
		- サービスコンテナと呼ばれている
			- 部品を管理する入れ物
			
### HTTPカーネルによる処理
- app/Http/Kernel.php
- 設定情報や部品群よ読み込みサービスコンテナに登録
	- 「環境設定」「エラーハンドラー」「ミドルウェア」「サービスプロバイダ」など
- 必要なクラスのインスタンスを提供してくれる

### リクエストのディスパッチ
- app/Providers/RouteServiceProvider.php
- routes/web.php

## ルーティング登録
- 基本はRoute::get()とコールバック関数

## テンプレートエンジン
- Blade
- 部品の再利用
- 処理と見た目のコードを分けて書くことで可読性の向上

## コントローラークラス
- ルーターに書く処理を記載。可読性向上。
- App\Http\Controllers\Controllerを継承しておくと便利
	- middleware()やvalidate()など使えるようになる

## ミドルウェア
- app/Http/Middleware
- リクエスト処理前後に行う処理
- 各クラスのメソッドに記述せず、ルーティングで記述
	- コードの保守性や可読性が向上する
- handle()メソッドが必須
	- 引数2個
		- 第1引数：Requestインスタンス
			- Illuminate\Http\Requestクラスのインスタンス
			- リクエスト処理に関するさまざまな情報を取得
		- 第2引数：Closureインスタンス
- リクエスト処理前後の区別
	 - リクエスト処理前：return $next($request);
	 - リクエスト処理前：return $response;
- ミドルウェアの登録
	- app/Http/Kernel.phpの$routeMiddlewareに記載
- ルーティングにミドルウェアを設定
	- アロー演算子でつなげる
	- Route::get()->middleware("managerauth", "recordipaddress");
	
## サービスコンテナ
- Laravel本体
- \Illuminate\Foundation\Applicationのインスタンス
- resolve()関数
	- Laravelのグローバル関数
	- 引数にクラスの完全修飾名を渡すと該当クラスを探し出し、そのインスタンスをリターン
		- resolve("App\Codezine\Book")
- メソッドインジェクション
	- newBook3(Book $book)
- コンストラクタインジェクション
	- public function __construct(Magazine $magazine)
- インスタンスを自動生成してくれる
- サービスプロバイダ
	- 引数ありのコンストラクタがあるクラスのインスタンスを生成するために使用
	- app/Providers

## エラーハンドリング
- .envファイル
	- APP_DEBUG=false
- 本番環境でエラー画面を表示させるのはセキュリティ上まずい
	- resources/views/errors/500.blade.php
- \App\Exceptions\Handler
	- エラーハンドラーの中心
	
	
## バリデーション
### validate()メソッド
- $request->validate(["tel" => "required|numeric"])
- 条件を満たしていない場合は直前のURLにリダイレクト
- エラーメッセージは$errorsで取得できる
- エラーメッセージはセッションに一時的に保存される
	- リロードすると消える。フラッシュセッション
### バリデーションメッセージのカスタマイズ
- lang/en/validation.php
	- メッセージのカスタマイズ
- config/app.php
	- メッセージの日本語化
	

## DB処理
- 基本はPDOによるSQL処理
### Laravelのデータベース処理は3種類
- SQLクエリ実行
- クエリビルダ
- Eloquent
- PDOによるSQL処理をどこまで隠蔽するかの違い
### データベース接続設定
- config/database.php
	- .env
### SQLクエリ実行
- Raw
	- Running Raw SQL Queries
- 素のSQLを書く
### クエリビルダ
- LaravelのメソッドをつなげてでSQL文の代わりにする
- 基本はテーブル名指定
	- DB::table("users")->get();
### Eloquent
- Modelファイルをテーブルと紐付ける

## 認証機能



		
		
		
		
		
		
		
		
		
		





