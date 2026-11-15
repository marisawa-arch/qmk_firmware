# jis_user キーマップ（Keychron Q10 Max JIS Encoder）

Keychron Launcher で設定していた**自分用のキー配列を、初期キーマップとして組み込んだ**キーマップです。
Launcher から書き出したキーマップファイル（`Keymap-Q10_MAX_JIS`、4 レイヤー + ノブ）を元に生成しており、
ビルドしたファームウェアのキーマップ・ノブ設定は書き出しファイルの値と完全に一致することを確認しています。

書き込んだ直後から、この配列で使えます（Launcher でのインポートは不要です）。
Per-Key RGB の色設定は書き出しファイルに含まれないため、Launcher で設定し直してください。

## 公式配列（`keychron` キーマップ）との主な違い

Mac 用レイヤー（`MAC_BASE` / `MAC_FN`）は公式配列と同じです。Windows 用レイヤーを変更しています。

### WIN_BASE

| 位置 | 公式 | jis_user |
|---|---|---|
| 最上段右端 2 キー | `Insert` / `Delete` | `PgUp` / `PgDn` |
| 数字段右端 | `PgUp` | `Home` |
| Tab 段右端 | `PgDn` | `Delete` |
| Home 段右端 | `Home` | `End` |
| Caps Lock | `Caps Lock` | `LT(WIN_FN, KC_CAPS)`（タップ = Caps Lock、ホールド = `WIN_FN`） |
| 右手側の `B` | `B` | `MO(WIN_FN)` |
| 無変換 | `無変換`（`KC_INT5`） | `左 Shift` |
| Fn（左スペース右） | `MO(WIN_FN)` | `Backspace` |
| 変換 / 右 Alt | `変換` / `右 Alt` | `` ` `` / `` ` ``（`KC_GRV`） |

### WIN_FN

| キー | 動作 |
|---|---|
| `Y` `U` / `H` `J` `K` `L` / `I` | `Home` `End` / `Backspace` `←` `↓` `→` / `↑` |
| `N` `M` `,` | `Delete` `PgUp` `PgDn`（公式では `N` = `NK_TOGG`） |
| `T` | `RGB オン/オフ` |
| `B`（右） | 透過（公式では `BAT_LVL`） |
| `C` `V` | `RGB 速度 −` / `RGB 速度 +` |
| 左スペース | `Backspace` |
| `0` / `Home` 段右端 | `NK_TOGG`（NKRO 切り替え） |
| 最上段右端 | `Print Screen` |

## ビルド

```bash
make keychron/q10_max/jis_encoder:jis_user
```

ビルド済み: [`keyboards/keychron/q10_max/firmware/keychron_q10_max_jis_encoder_jis_user.bin`](../../../firmware/keychron_q10_max_jis_encoder_jis_user.bin)
