# H3 LoRA Assets

H3 Mobile用LoRAの非公開保管場所です。

.safetensors はGitリポジトリへ直接コミットせず、Release h3-loras-v1 のAssetsへ追加します。

## LoRA一覧 (h3-loras-v1)

機械可読版は [loras.json](loras.json)。出典はSHA256でCivitai / CivArchiveから照合。base model: すべて MiniMax H3。トリガー・強度・例文は各ファイルのハッシュに一致する modelVersionId の記載とそのバージョンのサンプルのみで確認（2026-10-31）。「—」は配布元に記載なし。

| File | Triggers | 必須 | Strength (rec / range) | 発火のさせ方 | Source |
|---|---|---|---|---|---|
| `BJ_v3.safetensors` | `bl0w_j0b` | Yes | 1.0 / — | プロンプトに bl0w_j0b を入れ、フェラの動作を記述 | [MM-H3 - Blowjob v3](https://civarchive.com/models/2845331?modelVersionId=3285598) |
| `breastplayjiggle_h3_v2.safetensors` | — | No | — / — | 胸を掴む/揉む/持ち上げる/乳首を吸う等の動作を自然文で具体的に書く（トリガー語なし） | [Breast Play & Jiggle for MiniMax H3 v2.0](https://civarchive.com/models/2856004?modelVersionId=3278283) |
| `HMCumshot_V2.safetensors` | `cumshot` | No | — / — | 射精の瞬間・精液の量/質感・着地点・体位を平易な直接表現で詳しく書く（cumshot は任意。Female POVは避ける） | [HMCumshot V2](https://civarchive.com/models/2857340?modelVersionId=3441237) |
| `Deepthroat_Ultimate_v1.safetensors` | — | No | — / — | deepthroat / 喉奥まで咥える動作・喉の動きを時刻付きで具体的に記述 | [Ultimate DeepThroat + Frenulum Vers - MiniMax H3 - K3NK](https://civarchive.com/models/2904180?modelVersionId=3284171) |
| `deepthroat_v02.safetensors` | — | No | — / — | ディープスロート/フェラの動作を記述。'maintain eye contact' で目線固定 | [Daring's Deepthroat H3/LTX2.3 (MiniMax H3 FL2VA v0.2)](https://civarchive.com/models/2476698?modelVersionId=3226989) |
| `Finger_BEAN_v1.safetensors` | `BEANFLK` | Yes | 0.4 / — | プロンプト先頭に BEANFLK（大文字）→場面→SHOTごとに指の挿入動作 | [BEANFLK — Masturbation & Finger Insertion + Audio (H3)](https://civarchive.com/models/2829335?modelVersionId=3267091) |
| `Finger_Insert_3323149.safetensors` | `sensual_fingering` | Yes | — / — | sensual_fingering, fingering her vagina with her two middle fingers, ... を書く | [Minimax H3 - Perfect Fingering v1.0](https://civarchive.com/models/2935787?modelVersionId=3323149) |
| `h3-nipplesuck-step00007000-k3nk.safetensors` | `n1ppl3suck1ng` | No | — / — | 胸を口元へ引き寄せ自分の乳首を吸う動作を時刻付きで記述（trainedWord: n1ppl3suck1ng） | [Self Nipple Roping and Sucking LoRA - MiniMax H3 - K3NK v0.1](https://civarchive.com/models/2984096?modelVersionId=3383093) |
| `HMNSFW-AIO-V2.5.safetensors` | — | No | — / 0.5–0.9 | トリガー不要。性行為の内容・体位・カメラを詳細に書く（プロンプトの質が全て） | [HMNSFW - AIO Sex LoRA V2.5](https://civarchive.com/models/2834417?modelVersionId=3268303) |
| `HMPussyV2.safetensors` | `Pussy`<br>`vagina`<br>`anus` | ? | — / — | vagina / pussy / anus を明示し、形状・陰毛・開き方・カメラ位置を描写 | [HMPussy - Pussy/Anus LoRA V2](https://civarchive.com/models/2846342?modelVersionId=3436891) |
| `JerkOff_H3.safetensors` | `[He/She] is jerking off.` | Yes | — / — | He is jerking off. / She is jerking off. と書き、手で竿をしごく動作を記述 | [Jerking Off (Minimax H3)](https://civarchive.com/models/2933701?modelVersionId=3320556) |
| `M3_Unlocked_v2.safetensors` | `nude`<br>`topless`<br>`bare breasts`<br>`naked`<br>`completely unclothed` | No | 0.5 / 0.3–1.0 | nude / topless / bare breasts 等を被写体記述に入れる | [MiniMax H3 NSFW Unlocked (M3_V1)](https://civarchive.com/models/2925727?modelVersionId=3310653) |
| `minimax-jav-voice.safetensors` | `jpnMoans` | Yes | — / — | jpnMoans, she moans and says "気持ちいい" のように書く（台詞は日本語） | [JAV moans/喘ぎ声 - Audio Only [Minimax H3] v1.0](https://civarchive.com/models/2902825?modelVersionId=3282509) |
| `minimax-timefreeze_000003020.safetensors` | `A fifteen-second photoreal time freeze video.` | ? | — / — | A fifteen-second photoreal time freeze video. で始め、誰が停止し誰が動くかを書く | [Timefreezes (minimaxh3-timefreeze)](https://civarchive.com/models/2437696?modelVersionId=3383271) |
| `MM-H3.-.Fingering.v4.safetensors` | `She slides two fingers into her vagina. She moves her fingers in and out of her vagina.` | Yes | — / — | She slides two fingers into her vagina. She moves her fingers in and out of her vagina. をそのまま書く | [Fingering (Minimax H3 v4)](https://civarchive.com/models/2923170?modelVersionId=3342915) |
| `Motion_FL2VA_v2.safetensors` | `dynv2` | Yes | 0.7 / 0.6–0.8 | dynv2 を入れ、動きの方向・リズム・接触・反動を具体的に記述（I2V推奨） | [Faster! Harder! Shake Harder! | H3 Motion Booster V0.2](https://civarchive.com/models/2840146?modelVersionId=3228867) |
| `Mystic_FL2VA_v4.safetensors` | — | No | 1.0 / 0.2–1.0 | トリガー不要。性行為を自然文で詳細に記述 | [[MMH3] Mystic XXX v4.0](https://civarchive.com/models/2856467?modelVersionId=3266628) |
| `MysticXXX_MMH3-V5.safetensors` | — | No | — / 0.2–1.0 | トリガー不要。性行為を自然文で詳細に記述（REF2VA/FL2VA対応） | [[MMH3] Mystic XXX v5.0 (FL2VA & REF2VA)](https://civarchive.com/models/2856467?modelVersionId=3416478) |
| `Nipple_v2.safetensors` | — | No | 1.0 / — | 指先で乳首を弾く/つまむ/転がす動作を具体的に書く | [Nipple Play - MiniMax H3 v2.0](https://civarchive.com/models/2888071?modelVersionId=3295051) |
| `Orgasm_Masturbate_v1.4.safetensors` | `she is sitting with open legs while masturbating with a wand massager / massage gun / her hand`<br>`her pussy and anus to have strong orgasmic contractions visibly tightening and releasing rhythmically`<br>`She has an orgasm that causes her to ...`<br>`she falls back into a relaxed state, audibly catching her breath` | Yes | — / — | 開脚で座りオナニー→ She has an orgasm that causes her pussy and anus to have strong orgasmic contractions... の流れで書く | [H3 Female Masturbation/Orgasmic Contractions v1.0](https://civarchive.com/models/2926109?modelVersionId=3311155) |
| `Panties_v1.safetensors` | `She has her hand in her panties.`<br>`She slides her hand in her panties.`<br>`She rubs her vagina.` | Yes | — / — | She slides her hand in her panties. She rubs her vagina. と書く | [Hand in Panties Masturbation (Minimax H3)](https://civarchive.com/models/2839440?modelVersionId=3205014) |
| `Passionate_Kiss.safetensors` | `They kiss passionately.` | Yes | 1.0 / 0.7–1.0 | They kiss passionately. と書く | [Passionate Kissing (Minimax H3)](https://civarchive.com/models/2908508?modelVersionId=3289478) |
| `Penis_HM_v2.safetensors` | `HMPenis`<br>`penis` | Yes | — / — | HMPenis で始め、向き（Front/Back/Side）を指定 | [HMPenis - Penis/Cock LoRA v2.0](https://civarchive.com/models/2849923?modelVersionId=3247473) |
| `Pussy_HM_v1.safetensors` | `pussy` | ? | 1.0 / — | pussy を含め、女性器の形状・陰毛・角度を具体的に描写 | [HMPussy V1 - Stills only](https://civarchive.com/models/2846342?modelVersionId=3252213) |
| `Rough.Sex.safetensors` | `This is a cgi video depicting a rough, intense, penetrative sex with male character performing, intense, fast thrusting motion penetrating female character with his erect penis` | Yes | — / — | 先頭にトリガー文（CGI video depicting a rough, intense, penetrative sex ...）を入れ、体位を記述 | [Rough Sex/Fucked Silly (H3-3D-V1)](https://civarchive.com/models/1332917?modelVersionId=3402996) |
| `Squirt_HM_v2.safetensors.safetensors` | — | No | — / — | 指挿入オナニー→潮吹きを具体的に描写。HMPussy併用 | [HMMasturbation - Squirting and Female Masturbation v2.0](https://civarchive.com/models/2893742?modelVersionId=3310312) |
| `H3_speed_slider_1.1.safetensors` | `slow`<br>`fast` | No | — / -8–8 | トリガー不要。強度の符号で速度を指定（−で遅く、＋で速く）。動作は普通に記述 | [✦ Motion speed slider for H3 MiniMax - by FoS v1.0](https://civarchive.com/models/2951265?modelVersionId=3342524) |

## 使い方メモ

- **BJ_v3.safetensors** — フェラ(口淫)動作LoRA。トリガー bl0w_j0b 必須（元ページ記載）。強度1.0。サンプルはT2Vだが Ref2Vでも動作報告あり。元作者 kermitfrog1202 はBAN済、CivArchive経由で確認。
- **breastplayjiggle_h3_v2.safetensors** — v2.0（v1から新規学習）。v2.0は揺れ/バウンドより胸を揉む・吸う等の「ブレストプレイ」重視、吸う動作は良好・舐めは不安定（モデル説明のV2.0節）。トリガー語なし。FL2V向け学習、Ref利用時は強度を下げる。v2.0の推奨強度は配布元に記載なし（サンプルメタデータでは0.75–0.85）。
- **HMCumshot_V2.safetensors** — 射精シーン用アクションLoRA（V2）。データセット拡大で対応ポジションが増えた。トレーニング方針はv1と同じ。Female POV（女性視点）は弱い（ときどき効く）。trainedWords は cumshot だが作者V2サンプルには含まれず、射精の自然文記述で発火。推奨強度は配布元に記載なし（サンプルにも強度メタデータなし）。
- **Deepthroat_Ultimate_v1.safetensors** — ディープスロート+裏筋。トリガー語なし（配布元に記載なし）、動作記述で発火。推奨強度は配布元に記載なし。作者サンプルは integrated_multimodal_description 形式＋時刻指定の詳細プロンプト。ワークフローは作者動画に埋め込み。
- **deepthroat_v02.safetensors** — 映像+音声同時生成のディープスロートLoRA（FL2VA v0.2）。トリガー語なし（配布元に記載なし）。'maintain eye contact' が有効フレーズ。15秒まで動作維持。MMF/FFM対応。音量は小さめ（後で正規化）。シード差が大きいので書き直す前にリロール推奨。推奨強度は配布元に記載なし。
- **Finger_BEAN_v1.safetensors** — 指挿入オナニー（音声付き）。トリガー BEANFLK を全大文字で先頭に置く（必須）。H3では0.40で挿入が発火（サンプルメタデータでは0.7使用例も）。手が触れていない初期フレームからでも動作開始可。（サンプル実使用強度: [0.4, 0.7]）
- **Finger_Insert_3323149.safetensors** — 指挿入（Perfect Fingering）。作者記載のプロンプト先頭 sensual_fingering を使用。任意で潮吹き描写追加可。推奨強度は配布元に記載なし。
- **h3-nipplesuck-step00007000-k3nk.safetensors** — 自分の乳首を吸うLoRA（v0.1）。trainedWords は n1ppl3suck1ng だが作者サンプルプロンプトには含まれず、自然文の動作記述（固定カメラ・時刻指定）で発火している→トリガーは任意（作者サンプル13件すべて未使用）。推奨強度は配布元に記載なし。
- **HMNSFW-AIO-V2.5.safetensors** — 汎用NSFW（AIO）V2.5。トリガー語なし。強度0.5–0.9（バージョン説明）。設定: Euler/simple, 12 steps, shift 6, Turbo LoRA 0.5。I2Vが特に良好。プロンプトの質が結果を左右、埋め込みワークフローの例を参考に。（サンプル実使用強度: [0.5]）
- **HMPussyV2.safetensors** — 女性器/肛門の解剖学補正（V2, pruned基準で再学習）。trainedWords: Pussy, vagina, anus。指・広げる・見せる動作で学習。V2の推奨強度は配布元に記載なし（旧版説明: 静止画版1.0、動画版0.35）。
- **JerkOff_H3.safetensors** — 手コキ/オナニー（男性器）。トリガー文 '[He/She] is jerking off.'。ペニスLoRA併用推奨（作者）。推奨強度は配布元に記載なし（サンプルメタデータでは1.0/0.35）。（サンプル実使用強度: [0.35, 1]）
- **M3_Unlocked_v2.safetensors** — 汎用NSFWアンロック。コアトリガー: nude, topless, bare breasts, naked, completely unclothed（被写体・動作記述に混ぜる）。強度0.3–1（開始0.5）。Euler_ancestral + 4–8 turbo steps。
- **minimax-jav-voice.safetensors** — 音声専用：日本語の喘ぎ声。トリガー jpnMoans。セリフは日本語で（英語は未検証）。推奨強度は配布元に記載なし（サンプルメタデータで1.0使用）。（サンプル実使用強度: [1]）
- **minimax-timefreeze_000003020.safetensors** — 時間停止（minimaxh3-timefreeze版）。作者推定トリガー文 'A fifteen-second photoreal time freeze video.'（学習キャプションで最頻出のため、と作者）。H3は元々time freeze概念を持ち、151本の15秒動画で強化した実験版。性器描写が弱いので他LoRA併用推奨。H3版の推奨強度は配布元に記載なし。
- **MM-H3.-.Fingering.v4.safetensors** — 指挿入（v4）。トリガー文をそのまま記述。推奨強度は配布元に記載なし（サンプルメタデータでは1.0）。元作者BAN、CivArchiveで確認。（サンプル実使用強度: [1]）
- **Motion_FL2VA_v2.safetensors** — H3 Motion Booster V2（V0.2, 実写版）。トリガー dynv2。推奨0.6–0.8（開始0.7）。I2V推奨：正しいポーズの参照画像から、動きの方向・リズム・接触・反動・音を記述。音声対応（喘ぎは overall_soundscape でなくアクション内のセリフとして書くと口が動く）。
- **Mystic_FL2VA_v4.safetensors** — 汎用リアル系NSFW（V4, FL2VA）。トリガー語なし。推奨開始1.0、低めも可。
- **MysticXXX_MMH3-V5.safetensors** — 汎用リアル系NSFW＋音声（V5）。トリガー語なし。強度0.2–1。Turboで見た目が変わるので調整。V5はREF2VA（参照画像）にも対応。
- **Nipple_v2.safetensors** — 乳首を指先で弾く・つまむ。トリガー語なし。強度1.0（他は未検証、溶けたら下げる）。吸う動作は不安定→吸引系LoRAと併用。（サンプル実使用強度: [1]）
- **Orgasm_Masturbate_v1.4.safetensors** — 女性オナニー＋絶頂時の収縮。trainedWordsの文を流れに沿って使う。収縮/肛門は出たり出なかったり。機械音対策に 'Background audio is her breathing and sighing only. No mechanical hum. No engine noise.' を追加。推奨強度は配布元に記載なし（サンプルメタデータで1.0）。（サンプル実使用強度: [1]）
- **Panties_v1.safetensors** — パンツの中に手を入れてのオナニー。トリガー文3種。推奨強度は配布元に記載なし（サンプルメタデータで0.5–0.7）。元作者BAN、CivArchiveで確認。（サンプル実使用強度: [0.5, 0.7]）
- **Passionate_Kiss.safetensors** — 情熱的なキス。トリガー文 'They kiss passionately.'。男女/女女は1.0、男男は約0.7。元作者BAN、CivArchiveで確認。（サンプル実使用強度: [0.75, 1]）
- **Penis_HM_v2.safetensors** — 男性器の解剖学補正（v2）。トリガー HMPenis を先頭に（モデル説明）、バージョンtrainedWordsは penis。向き Front(POV)/Back/Side を明記。中〜大サイズ向き。推奨強度は配布元に記載なし（サンプルメタデータで0.5–0.6）。（サンプル実使用強度: [0.5, 0.6]）
- **Pussy_HM_v1.safetensors** — 女性器補正 V1（静止画学習）。trainedWords: pussy。静止画版は1.0（動作の保持には動画版 0.35 を併用、と作者）。シェーブ/有毛・肛門にも対応。
- **Rough.Sex.safetensors** — 3D/CGI風の激しいセックス。trainedWordsの長文をプロンプト先頭に。推奨強度は配布元に記載なし（サンプルメタデータで0.3–1.0、0.8が多い）。（サンプル実使用強度: [0.3, 0.6, 0.8, 1]）
- **Squirt_HM_v2.safetensors.safetensors** — オナニー＋潮吹き（v2.0、実験的）。トリガー語なし。本体の推奨強度は配布元に記載なし。Turbo LoRA 0.5、HMPussy 0.4–0.8 を併用（必須級）。
- **H3_speed_slider_1.1.safetensors** — 動きの速さスライダー（作者 FrogOnStilts）。トリガー語不要（slow / fast は任意）。マイナスで遅く（作者例: 'a woman runs quickly along a sunny park path' を -16 で歩きに）、プラスで速く（プラス側の具体例は配布元に記載なし）。最適範囲 -8〜+8、±10付近からプロンプト追従が低下。他LoRA併用で効果が弱まることあり。サンプルに強度メタデータなし。

