## GitHub

`t`  でファイル名の曖昧検索ができる

コメントやreadmeはマークダウンに対応しているが、`<kbd>`タグで囲むとボタンみたいな表示にできる
e.g    <kbd>ESC</kbd>


バッククオートで色コードを囲むと色を表示してくれる `#C6E48B`

![スクリーンショット 2021-10-21 18 33 01](https://user-images.githubusercontent.com/13535662/138251309-da73126f-4b1d-4cc7-bb5d-fe59d2575f99.png)


diffで囲み、行頭に-や+をつけると緑と赤のハイライトで差分表示ができる
```diff
+add code
-delete code
```

```<details>``` and ```<summary>``` タグで複数行をトグルにまとめることができる

```<div align="center">```を使えば中央揃えができる。READMEのトップにアイコン画像などをおく時に便利そう

`<sup>`<sup>タグで文字を小文字にできる。画像の下に説明を追記したり、表が横にはみ出ないようにするのに使える</sup>

`git shortlog -sn`でコミット数ランキングが見れる

`brew install hub` ->
```hub browse```コマンドでリモートレポジトリのgithubページ開ける

alias貼るなら

```bash
alias hub='hub browse'
```

`.`でブラウザ上でVSCodeを開ける

## fish

`ctrl + w`  単語ごとに削除する

`ctrl + f`  過去の履歴の補完ができる

## html
apple-touch-icon.pngを読み込むと、ホーム画面に追加した際のアイコンを変更できる(for iPhone)

