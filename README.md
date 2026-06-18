# pytest CI — GitHub Actions で pytest を走らせる最小例

`push` するたびに GitHub のサーバで `pytest -q` が走り、テスト結果が緑 ✓ / 赤 ✗ で返る最小構成です。

## 中身

```
calc.py            # サンプルの関数 (add / sub)
test_calc.py       # calc.py のテスト
requirements.txt   # pytest
pytest.ini         # pytest 設定 (空の最小)
.github/
  workflows/
    ci.yml         # push をきっかけに pip install -> pytest -q を走らせる
```

## 動かし方

1. GitHub に空のリポジトリを作る（README/.gitignore/license のチェックは外す）
2. このフォルダをローカルに置いて `git init` → 全ファイルを add → commit
3. リモートを登録して push
4. リポジトリの **Actions** タブを開くと `CI` が走っている。緑 ✓ になれば成功
5. 詳細を開くと `2 passed in 0.01s` のようなログが出ている

## 赤 ✗ を見たいとき

`calc.py` の `add` を `return a + b + 1` に書き換えて push すると、`test_calc.py::test_add` が
`assert 6 == 5` で落ちて赤 ✗ になります。元に戻して push すれば緑 ✓ に戻ります。

## ローカルで走らせる場合

```bash
pip install -r requirements.txt
pytest -q
```
