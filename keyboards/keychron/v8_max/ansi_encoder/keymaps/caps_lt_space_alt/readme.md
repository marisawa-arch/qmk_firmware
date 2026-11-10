# caps_lt_space_alt キーマップ（Keychron V8 Max ANSI Encoder）

[`caps_lt`](../caps_lt/readme.md) キーマップに、**右スペースキーのタップ / ホールド動作**を追加したキーマップです。
Caps Lock キーの動作、Per-Key RGB、バックライト修正は `caps_lt` と同じです。

## 右スペースキーの動作

最下段・右側のスペースキー（`fn2` キーの右隣）に `LT(0, KC_SPC)` を割り当て、
`keymap.c` の `process_record_user()` でホールド時の動作を上書きしています。

| 操作 | Windows（`WIN_BASE`） | Android（`MAC_BASE` を Android 用として使用） |
|---|---|---|
| タップ | `Space` | `Space` |
| ホールド | ``Alt + ` ``（IME の英字 / 日本語切り替え） | `Ctrl + Space`（IME の英字 / 日本語切り替え） |

- どちらの動作になるかは、キーボード背面の **Mac / Win スイッチ**（デフォルトレイヤー）で決まります。
- タップ / ホールドの判定は QMK 標準の `TAPPING_TERM`（既定 200ms）に従います。ホールドと判定された時点で 1 回だけ送信します。
- タップ判定のため、Space はキーを**離したとき**に送信されます。
- 左スペースキーは通常の `Space` のままです。

## Caps Lock キーの動作（`caps_lt` と同じ）

| 操作 | 動作 |
|---|---|
| タップ | `Shift + Caps Lock` を送信（IME の英字 / 日本語切り替え） |
| Shift を押しながらタップ | `Caps Lock` のみを送信 |
| ホールド | 押している間 `_FN2`（レイヤー 4） |

## Keychron Launcher での扱い

`VIA_ENABLE = yes` のため、Keychron Launcher で通常どおり設定できます。独自動作はキーの**位置ではなくキーコード**に紐づいています。

| キーコード | 動作 |
|---|---|
| `LT(0, KC_SPC)` | 上記の右スペースの動作（任意のキーに割り当て可能） |
| `LT(4, KC_CAPS)` | 上記の Caps Lock の動作 |

- 別のキーコードに変更すると、独自動作は無効になります。
- ファームウェアを書き込むと、Launcher で変更したキー割り当ては初期化されることがあります。必要に応じて事前に設定をエクスポートしてください。
- Launcher から公式ファームウェアへ更新すると、このキーマップは上書きされます。

## ビルド済みファームウェア

- [`keyboards/keychron/v8_max/firmware/keychron_v8_max_ansi_encoder_caps_lt_space_alt.bin`](../../../firmware/keychron_v8_max_ansi_encoder_caps_lt_space_alt.bin)
  - ビルド元: `caps_lt_space_alt` ブランチ（`caps_lt` + 本キーマップ）
  - SHA-256: `e38fb1924b1d32e7964cf4b66b83c8508eb359322f18eb2c520cf4831eff12f1`

`keymap.c` を変更した場合は、下記の手順でビルドし直してください（この `.bin` は自動では更新されません）。

## ビルド

```bash
make keychron/v8_max/ansi_encoder:caps_lt_space_alt
```

## 書き込み

1. キーボード背面のモードスイッチを **Cable** にする
2. **Esc キー**（またはスペースバー下のリセットボタン）を押したまま USB ケーブルを接続し、DFU モードにする
3. [QMK Toolbox](https://qmk.fm/toolbox) で `.bin` を書き込む。または次のコマンドを実行する

```bash
make keychron/v8_max/ansi_encoder:caps_lt_space_alt:flash
```
