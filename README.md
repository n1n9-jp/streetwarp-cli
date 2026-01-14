使い方（ヘルプの表示）
cargo run -- --help

ビルドされたバイナリを直接実行する場合はこちらです。
./target/debug/streetwarp --help

具体的な例
リポジトリ内の res フォルダにあるサンプルファイル（例: 
Lunch_Miler.gpx
）を使用する場合は、以下のようになります：

cargo run -- [オプション] <GPXファイルへのパス>
cargo run -- res/Lunch_Miler.gpx

重要な注意点：APIキー
このソフトを実際に動作させて画像をダウンロードするには、Google Streetview Static APIのキーが必要です。APIキーを指定して実行する場合は以下のようになります：

具体例（動画生成）
実際に画像をダウンロードして動画を生成するには、`--dry-run`を外して実行します。
大量の画像がダウンロードされるため、`--output-dir`を指定して作業ディレクトリを固定することをお勧めします。

```bash
# 出力用フォルダを作成
mkdir -p out

# 実行（例：最初の50フレームのみ）
cargo run -- --api-key "AIzaSyAhsXw89rSXI6w43Tiaz-zgH60_2-h8ufA" --max-frames 50 --output-dir ./out res/arc-timeline-daily.0007-10-25.gpx
```

出力先について
`--output-dir`を指定しない場合、動画と一時画像はOSのテンポラリフォルダ（例: `/var/folders/...`）に生成されます。カレントディレクトリには書き出されないため、必ず出力先を指定して実行することを推奨します。

生成されるファイル：
- `streetwarp-lapse.mp4`: **完成版動画**。AIによるフレーム補間が行われており、動きが非常に滑らかです（72fps）。
- `streetwarp-lapse-original.mp4`: 中間ファイル。補間なしの状態の動画です。
- `0.jpg, 1.jpg...`: 各フレームの画像

補間オプション（--minterp）
動きの補間方法を以下のオプションで変更できます。
- `--minterp good`: デフォルト。高品質な補間を行います。
- `--minterp fast`: 処理速度優先で補間を行います。
- `--minterp skip`: 補間をスキップします。カクカクした質感にしたい場合に有効です。

```bash
cargo run -- --api-key "AIzaSyAhsXw89rSXI6w43Tiaz-zgH60_2-h8ufA" --output-dir ./out res/arc-timeline-daily.0007-10-25.gpx
```

