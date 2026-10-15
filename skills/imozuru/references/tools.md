# 道具

以下の `scripts/` は `<skill_dir>` からの相対パス。すべて `python3` と絶対パスで呼び出す。

スクリプトは Python 3.10 以上の標準ライブラリだけで動く。外部コマンドは、あれば使う（無いときの動きは各行に書いた）。

- `scripts/fetch.py <sources_dir> <name> <url>` — 落として本物か確かめる。PDF は .pdf と .txt（`pdftotext -layout`・poppler か Xpdf）、HTML は .md、YouTube は字幕を `[分:秒] 文` の .md（`yt-dlp`・動画は落とさない）。文字の層が無い PDF は `pdftoppm` と `tesseract` で OCR する。要るコマンドが無いときは、無いコマンドの名前を書いて `FAIL` する。HTML は [ax](https://github.com/yusukebe/ax) があれば ax で、無ければ標準ライブラリで本文を文字にする（見出しや表の形は ax のほうが残る）。取ってきたものは作業用のフォルダで検査し、通ったものだけを sources_dir へ移す。404・壁・短すぎる本文は `FAIL`（同じ名前の原文がすでにあれば、そのまま残る）。X は本文が取れないので取りに行かず `FAIL`＝URL と、検索で拾った抜粋を（未確認）で map.md に残す
- 動画の場所は行番号の代わりに時刻で指す（`sources/x.md [12:34]`）
- `scripts/report.py <topic_dir> [--check]` — extracts.json の抜き書きを原文と照合し、合えば report.html にする。`--check` は照合だけ
- `scripts/watch.py add|list|check` — 見張り。RSS / Atom を引いて前回からの新着を出す。検索ではなく配信元のフィードを取得する。DOCTYPE・ENTITY を含むフィードは安全のため読まない
- `scripts/chain.py find|refs|cites|author` — OpenAlex で引用と著者をたどる。認証やレート制限で利用できなければ本文の参考文献と Web 検索へ切り替える。**API キーや支払いの登録はしない**。古めの論文に強く、新しい論文と同名の多い著者に弱い（author は同名の別人を掴むことがある）
- ファイル名は `<著者>-<年>-<短い題>`、arXiv は `arxiv-<番号>-<短い題>`

OpenAlex の題名検索は候補の題名・年・著者を確認し、できれば DOI で指定する。新しい論文の引用は登録が遅れることがあるため、0件を「引用なし」と判断しない。本文の参考文献と Web 検索を補助に使う。
