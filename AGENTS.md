# imozuru の保守

配布する Codex スキルは `skills/imozuru/`。Python 3.10 以上の標準ライブラリで動き、外部コマンドは任意。調査成果物はこのスキルのソースに混ぜない。

- スキルの振る舞いを変える場合は `skills/imozuru/SKILL.md` と該当モードの参照資料を見る。理論の検討時だけ `references/theory.md` を参照する。
- 原文の取得を変える場合は、取得失敗時の既存ファイル保全と UTF-8 / Python 3.10 互換性を維持する。
- 抜き書きの形式を変える場合は `scripts/report.py`、`references/report.md`、`examples/demo/extracts.json` を揃える。原文との照合を省かない。
- 配布物は `skills/imozuru/` 単体で使える形を保つ。リポジトリ外の個人用設定や特定のモデルには依存させない。

ローカルテストは `python3 -m unittest discover -s tests -v`。一時ファイル・モック・ループバック HTTP サーバーのみを使い、本番環境や外部サービスに接続しない。変更に関係するテストの実行・失敗の修正・再実行は追加確認なしで進めてよい。抜き書きの例は `python3 skills/imozuru/scripts/report.py examples/demo --check` で確認できる。
