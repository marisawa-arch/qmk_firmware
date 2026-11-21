# caps_lt キーマップ（Keychron Q10 Max ANSI Encoder）

Keychron 公式の `keychron` キーマップ（`2025q3` ブランチ）をベースに、**Caps Lock キーの動作だけ**を変更したキーマップです。
Per-Key RGB など `2025q3` の機能（`KEYCHRON_RGB_ENABLE`）はそのまま使えます。

## Caps Lock キーの動作

| 操作 | 動作 |
|---|---|
| タップ | `Shift + Caps Lock` を送信（IME の英字 / 日本語切り替え用） |
| Shift を押しながらタップ | `Caps Lock` のみを送信（Shift は一時的に解除） |
| ホールド | 押している間 Fn レイヤー（Mac: `MAC_FN`、Windows: `WIN_FN`） |

- Q10 Max の公式キーマップには V8 Max の `_FN2` に当たるレイヤーがないため、ホールド先は各 OS の Fn レイヤーにしています。
- タップ / ホールドの判定は QMK 標準の `TAPPING_TERM`（既定 200ms）に従います。
- ビルド結果のキーマップは、公式 `keychron` キーマップと Caps Lock の 2 か所だけが異なることを確認しています。

## Keychron Launcher での扱い

独自動作はキーの位置ではなく**キーコード**に紐づいています。

| キーコード | 値 | 動作 |
|---|---|---|
| `LT(1, KC_CAPS)` | 16697 | Mac レイヤー用。上記の動作（ホールドで `MAC_FN`） |
| `LT(3, KC_CAPS)` | 17209 | Windows レイヤー用。上記の動作（ホールドで `WIN_FN`） |

別のキーコードに変更すると独自動作は無効になります。書き込み後、Launcher で変更したキー割り当ては初期化されることがあるため、必要に応じて事前に設定をエクスポートしてください。

## ビルド済みファームウェア

- [`keyboards/keychron/q10_max/firmware/keychron_q10_max_ansi_encoder_caps_lt.bin`](../../../firmware/keychron_q10_max_ansi_encoder_caps_lt.bin)
  - SHA-256: `25dddcf0fd432b2442cdd62e409a7672cef486e8c4a56a73486b87e2565b89fb`

## ビルド / 書き込み

```bash
make keychron/q10_max/ansi_encoder:caps_lt
```

背面スイッチを **Cable** にし、**Esc** を押しながら USB を接続して DFU モードにしてから、QMK Toolbox で `.bin` を書き込みます。
