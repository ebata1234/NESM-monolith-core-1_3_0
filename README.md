# NESM モノリスコア版 (1.20.1 / Forge 47) v1.3.0

StockiesLad/NESM のソースに「モノリスコア」(旧: モノリスコア) を追加した改造版です。
MOD ID は元のまま (`nightmareesm`) なので、**今の NESM の jar と入れ替えて使います**
(両方 mods フォルダに入れると重複エラーになります)。

## 追加されるもの
- ブロック「モノリスコア」(見た目はロードストーン。独立した別ブロックなので、元からあるロードストーンには効果なし。発光しません)
- レシピ (定形):
  ```
  . 金 .
  金 ダイヤ 金
  鉄 鉄ブロック 鉄
  ```
  (金インゴット3 / ダイヤ1 / 鉄ブロック1 / 鉄インゴット2)
- クリエイティブタブ「機能ブロック」にも入っています

## 効果
1. モノリスコアがあるチャンクでは、NESMのモブによるブロックの設置・破壊が止まります。
   ゾンビの採掘 (前・上・下)、丸石の柱積み、橋かけ、TNT設置、火つけ、クモの巣。
2. クリーパーなどの爆発、プレイヤーの建築・破壊は今までどおりです。
3. 世界にあるモノリスコア1個につき、全プレイヤーの L2Hostility 追加難易度 (`l2hostility:extra_difficulty`) が +5。
   全ディメンションの合計で、置く・壊す・爆発で壊れる、のたびに即反映されます。
   すでに湧いているモブのレベルは変わらず、新しく湧くモブから反映されます。

## 設定 (config/esm-config.toml、初回起動後に作られます)
- `protectionLanternRadius` : 0 = モノリスコアのいるチャンクのみ (初期値) / 1 = 3x3 チャンク / 2 = 5x5 チャンク
- `protectionLanternDifficulty` : 1個あたりの難易度 (初期値 5、0で無効)

## 動作確認のしかた
- `/give @s nightmareesm:protection_lantern` で入手
- `/attribute @s l2hostility:extra_difficulty get` : 置くと 5.0、2個で 10.0、壊すと戻る

## v1.2.0 で追加: ナパームクリーパー
クリーパーが爆発すると、爆発地点の周囲の地面に火がまき散らされ、爆発に巻き込まれた生き物は5秒間燃えます。
爆発の威力や範囲は変わりません。mobGriefing が false のときは火も出ません。
- `creeperNapalm` : true/false (初期値 true)
- `creeperNapalmRadius` : 火をまく範囲(ブロック) (初期値 6)
- `creeperNapalmFires` : 1回の爆発でまく火の数 (初期値 25)
- `creeperNapalmIgnitesEntities` : 巻き込まれた生き物に着火 (初期値 true)
※ 爆発由来なので、モノリスコアの保護範囲内でも火は出ます。

## 寝られるようにする
config/esm-config.toml の `allowSleep = false` を `true` にして、ゲームを再起動します。


## v1.3.0 の注意
ブロックIDを `protection_lantern` から `monolith_core` に変えたため、旧版で置いた保護のランタンはワールドから消えます (開発中ワールド向け)。
睡眠: `allowsleep = true` でも、ベッドの周囲8x5x8に敵対モブがいるとバニラ仕様で眠れません。
