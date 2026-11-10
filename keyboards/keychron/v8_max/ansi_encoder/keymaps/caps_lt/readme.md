# caps_lt キーマップ（Keychron V8 Max ANSI Encoder）

`via` キーマップをベースに、**Caps Lock キーの動作だけ**を変更したキーマップです。
Caps Lock の位置に `LT(_FN2, KC_CAPS)`（Keychron Launcher / VIA 上の表記は `LT(4, KC_CAPS)`）を割り当て、
`keymap.c` の `process_record_user()` でタップ時の動作を上書きしています。

## Caps Lock キーの動作

| 操作 | 動作 | 用途 |
|---|---|---|
| タップ | `Shift + Caps Lock` を送信 | IME の英字 / 日本語入力モード切り替え |
| Shift を押しながらタップ | `Caps Lock` のみを送信（Shift は一時的に解除） | 本来の Caps Lock（大文字固定） |
| ホールド | 押している間 `_FN2`（レイヤー 4）に切り替え | F1〜F12 などの利用 |

- タップ / ホールドの判定は QMK 標準の `TAPPING_TERM`（既定 200ms）に従います。
- Mac 用レイヤー（`MAC_BASE`）でも同じ動作になります。`Shift + Caps Lock` で入力モードが切り替わるかどうかは OS・IME の設定に依存します。

## レイヤー構成

レイヤー数・その他のキー配置は `via` キーマップと同一です。

| 番号 | 名前 | 内容 |
|---|---|---|
| 0 | `MAC_BASE` | Mac 用ベースレイヤー |
| 1 | `WIN_BASE` | Windows 用ベースレイヤー |
| 2 | `MAC_FN1` | Mac 用 Fn レイヤー（メディア・RGB・Bluetooth 切り替えなど） |
| 3 | `WIN_FN1` | Windows 用 Fn レイヤー |
| 4 | `_FN2` | F1〜F12、`~`、バッテリー残量表示など。Caps Lock ホールドまたは `MO(_FN2)` キーで有効 |

## Keychron Launcher での扱い

`VIA_ENABLE = yes` のため、書き込み後も Keychron Launcher で通常どおり設定できます。

- 独自動作はキーの**位置ではなくキーコード**に紐づいています。
  - 任意のキーに `LT(4, KC_CAPS)` を割り当てると、そのキーで上記の動作になります。
  - Caps Lock の位置を `KC_CAPS` など別のキーコードに変更すると、独自動作は無効になります（通常の Caps Lock になり、ホールドでのレイヤー切り替えもなくなります）。
  - `LT(3, KC_CAPS)` や `LT(4, KC_ESC)` のように数字・キーが異なる場合は、QMK 標準の Layer-Tap として動作します。
- ファームウェアを書き込むと、Launcher で変更したキー割り当ては初期化されることがあります（VIA の EEPROM はビルド日付で有効性を判定するため）。必要に応じて事前に設定をエクスポートしてください。
- Launcher から公式ファームウェアへ更新すると、このキーマップは上書きされます。

## ビルド

```bash
make keychron/v8_max/ansi_encoder:caps_lt
```

または

```bash
qmk compile -kb keychron/v8_max/ansi_encoder -km caps_lt
```

## 書き込み

1. キーボード背面のモードスイッチを **Cable** にする
2. **Esc キー**（またはスペースバー下のリセットボタン）を押したまま USB ケーブルを接続し、DFU モードにする
3. [QMK Toolbox](https://qmk.fm/toolbox) で `.bin` を書き込む。または次のコマンドを実行する

```bash
make keychron/v8_max/ansi_encoder:caps_lt:flash
```
