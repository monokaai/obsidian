## Obsidianとは？
Obsidianは、ローカルファイル（主にMarkdown形式）を使って知識やメモをリンクしながら管理できる、パーソナルナレッジマネジメント（PKM）ツールです。ノート同士を相互にリンクすることで、情報のネットワーク（知識グラフ）を構築できるのが特徴です。自分のPC上で完結するため、プライバシーやカスタマイズ性にも優れています。

- 公式ドキュメント: [https://help.obsidian.md/](https://help.obsidian.md/)

### プライベートページの作成方法
[[Git]]でルートリポジトリと別のリポジトリを作成し、サブモジュールとして扱うことで単一のVault内でプライベートなページ群を作成できる。
1. プライベート用の新しいリポジトリをGitHub等で作成する（Cloneはしない）
2. ローカルでプライベートリポジトリに対応するディレクトリを作成し、連携させる
	```shell
    cd root_repo/private
	git init
	git remote add origin git@github.com:yourname/your-private-repo.git
	git add .
	git commit -m "initial commit for private notes"
	git push -u origin master
	```
3. 元のリポジトリに戻ってサブモジュールに追加する
	```shell
    cd path/to/root_repo
    git submodule add git@github.com:yourname/your-private-repo.git ./private
    git submodule # 追加の確認（.gitmodulesが作成されているはず）
	```
4. 上記が完了していればサブモジュール配下のファイルに対する変更はメインモジュール側のGit管理外になる
   1. 正確にはサブモジュールに対する変更の有無はcommitID単位で管理することになるが、ファイルの中身は把握しない
5. Obsidian側でコミュニティプラグインのGitを追加しAdvanced→Update submodulesを有効化する
6. commit-and-syncを実行するとサブモジュール含めてPushされる
   1. Stage all & Commit & PushではメインモジュールしかPushされない（設定の説明に記載あり）

### 使ってみたい
- **[[S3_image_uploader]]**

#### 参考
- [Obsidian逆引きレシピ](https://minerva.mamansoft.net/%F0%9F%93%97Obsidian%E9%80%86%E5%BC%95%E3%81%8D%E3%83%AC%E3%82%B7%E3%83%94/%F0%9F%93%92Obsidian%E9%80%86%E5%BC%95%E3%81%8D%E3%83%AC%E3%82%B7%E3%83%94)
- [Cursorにobsidian-mcpを設定する時にハマること](https://zenn.dev/shuzon/articles/15027f04d1b642)
- [Obsidian・Cursorをフル活用してAI駆動でアウトプットしていく](https://note.com/shu127/n/n61115b0b8c64)