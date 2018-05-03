# workflow
アイデア家業案件の基本作業フロー
個別のプロジェクト毎にルールがある場合はそちらを優先

# ラベルの種類

## issue用ラベル

**ラベルの運用は変えるかも（特に進捗周り）**

* `Go!`: 作業可能状態
* `Doing`: 着手済み・進行中
* `Done`: 実装完了・完了レビュー中
* `緊急`: hotfixを当てるレベルの急ぎタスク
* `優先度高`: 優先して対応したいタスク

## PR用ラベル

* `WIP`: 作業中（Work in progress）本気レビュー禁止。相談中など。
* `Mergable`: マージ可能

# 具体的な開発の流れ（with ラベルの扱い方）

1. 仕様策定MTG：どれをIssue化するか決めて、結果Issueが作成されます。

2. TaskPlanner（一旦 @ikedanoda のみ）: issue吟味。`Go!`付与、担当者へアサイン。

3. 実装者：issue着手。issueへ`Go!`削除＆`Doing`付与
  * 新規ブランチを `dev`ブランチから **必ず** 作成して作業を行う。
    * 命名規則： `[issue番号]_[英文をアンスコ区切りで分かりやすい名前]` 
    * ex. `15_add_twitter_login`

4. 実装者：実装完了。
  * 最新のbaseになっているブランチ（master or devの場合が多い）を自身のブランチへマージ。
  * テストのタスクの場合`bundle exec rspec`する。
    * (feature specの設定 https://github.com/StreetAcademy/www.street-academy.com/pull/904)
  * `bundle exec rubocop`する。
  * コンフリクトしていたら解消する。解消に迷ったら @ikedanoda へ相談下さい。
  * まだ行っていなければbaseブランチに対してPullRequest（PRと略す場合あります）する
    * タイトルは基本的には元issueのタイトルを入れれば問題無いです。意味が伝わりにくい場合は変更も可能です。
  * 【PR】PRの最初の説明のところに`closed #issue番号`（例 closed #123）を入れてください（PRがマージされると自動でissueがCloseされます）。
  * 【PR&issue】CIが通っているのを確認したら、issueより`Doing`削除&`Done`付与
  * 【PR】レビュアー（基本的には @ikedanoda ）へアサイン&コメントしてください。

5. レビュアー：【PR】に`Doing`付与

6. レビュアー：レビュー完了。【PR】に`Mergable`付与

7. レビュアー：修正部分がある場合には、再度担当者へアサイン＆コメントする（この後、担当者、レビュアーでアサインし合う。誰が今作業すべきかが明瞭になるようにバトンを渡すイメージで）

8. アプリ責任者( @ikedanoda )：マージ。issue、PRをClose。 

9. 担当するタスクが無くなった場合はそのプロジェクトのslackで叫べ。
* 3で作業が大きそうな場合はWIPを活用する。
 * GitHubへpushしてPR作成
 * PRへ`WIP`を付与して継続。完了したら`WIP`を削除
