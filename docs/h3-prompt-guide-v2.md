Hailuo H3 画像参照プロンプト・ガイダンス

初版調査日：2026年8月20日  
改訂日：2026年10月31日  
版：v2.0（公式資料照合・肯定形プロンプト方針追加）
対象：MiniMax H3 / Hailuo H3、ComfyUIのI2V・R2V（Reference to Video）

1. 先に結論

H3の画像参照で最も重要なのは、各画像から何を採用し、何を採用しないかを分けて書くことです。

基本形は次の順序です。

1. 各参照画像の担当を決める
2. 維持する特徴を具体化する
3. 採用対象を肯定形で限定する（必要な場合だけ非採用要素を簡潔に記す）
4. 動作を再生順に書く
5. 1ショットにつきカメラ指示を1つに絞る
6. 最後の状態を明記する

短い実用形なら、まず次の型から始めます。

<Picture 1> supplies the main character's identity, face, hairstyle, body proportions, and clothing.
Preserve these features consistently throughout the entire video.

<Picture 2> supplies only [採用する要素].
Use <Picture 1> for the character, environment, lighting, viewpoint, framing, and pose; use <Picture 2> exclusively for [採用する要素].

[Shot 1] [画面の開始状態].
[動作を発生順に記述].
The camera remains [カメラの状態].
End with [最後の構図・姿勢・状態].

2. I2VとR2Vを混同しない

| 目的 | 適したモード | 画像の扱い |
|---|---|---|
| 添付画像を動画の正確な開始画面にする | I2V / first frame | 画像をfirst_frameへ接続 |
| 2枚の画像間をつなぐ | I2V / first + last frame | 開始画像と終了画像を別々に接続 |
| 顔・服・小物・背景・画風などを借りる | R2V / Ref2VA | 画像を参照素材として接続 |
| 画像の人物と参照動画の動きを組み合わせる | R2V / Ref2VA | 画像＝人物、動画＝動作など役割を分担 |

R2Vに画像を入れただけでは、その画像が自動的に「正確な最初のフレーム」になるとは限りません。開始構図を最優先する場合はI2Vのfirst_frameを使う方が確実です。R2Vは、人物の同一性、服装、背景、画風、動作、カメラ、声などを複数素材から組み合わせる用途です。

3. 公式形式のラベル

MiniMax公式ガイドでは、参照ファイルと、その中から再利用する要素を分けています。

| ラベル | 意味 | 主な用途 |
|---|---|---|
| <Picture N> | アップロードした画像自体 | 開始・終了・キーフレーム、構図、絵コンテ |
| <Subject N> | 画像や動画から取り出して再利用する要素 | 人物、服、物体、背景、表情、ポーズ、画風 |
| <Video N> | 参照動画全体 | 動作、カメラ、編集、テンポ、継続元 |
| <Audio N> | 参照音声 | 声質、話し方、効果音、音楽、音声の再利用 |

画像の接続順と番号を一致させます。ComfyUIでは、最初に接続した画像が<Picture 1>、次が<Picture 2>です。

PictureとSubjectの使い分け

<Subject 1> is the woman shown in <Picture 1>.
Preserve her facial identity, shoulder-length black hair, dark brown eyes, slim build, and navy jacket.

これは「Picture 1の画像全体を再現する」のではなく、「Picture 1に写っている女性を再利用する」という意味です。

一方、開始構図そのものを使う場合は次のようにします。

<Picture 1> is the exact opening frame and composition anchor for [Shot 1].

4. 参照画像の準備

人物用の推奨構成

- 1枚目：顔が鮮明な正面または斜め前
- 2枚目：全身または別角度。体型、髪の長さ、服装、シルエットが分かる画像
- 3枚目：必要な場合だけ、アクセサリー、手、小物、衣装の細部

画像間で年齢、顔型、髪型、服、画風が食い違うと、H3が中間的な人物を作りやすくなります。枚数を増やすより、矛盾しない画像を少数使う方が安定します。

ComfyUIのref_image_size

- match：出力解像度に合わせて参照画像を縮小。速いが、顔や細部の一致が弱くなる場合があります。
- max：参照画像の短辺を最大2048pxまで保持。遅くなりますが、人物の同一性や細部を優先するときに向きます。

人物・手・衣装の細部を重視する今回の用途では、まずmaxを基準にするのが適しています。

5. プロンプトを組む順序

5-1. 参照の担当を先に書く

<Picture 1> supplies the woman's identity, face, hairstyle, body proportions, clothing, and the main environment.
<Picture 2> supplies only the right-hand shape and palm orientation.
<Video 1> supplies only the action timing, body movement, and camera movement.

5-2. 維持する特徴を3〜7個に絞る

「同じ女性」だけではなく、認識しやすい特徴を指定します。

Preserve her oval face, dark brown eyes, shoulder-length black hair, small mole below the left eye, slim build, and black jacket.

全特徴を何度も繰り返す必要はありません。最初に定義し、後は<Subject 1>として参照します。

5-3. 補助画像から採用しない要素を書く

補助画像はまず「何を使うか」「残りの要素をどの参照から使うか」を肯定形で明記します。競合が解消しない場合だけ、非採用要素を短く補足します。

Use <Picture 2> only for the hand configuration.
Retain the person, face, body, clothing, background, lighting, camera angle, crop, and overall pose from <Picture 1>.

5-4. 動作は目に見える順序で書く

悪い例：

She acts confidently and naturally.

改善例：

She looks down at the object, moves her right hand toward it, places her palm against its surface, closes her fingers around the edge, then looks back toward the camera.

感情や雰囲気だけでなく、画面で確認できる動作に分解します。

5-5. カメラは1ショットにつき1種類を基本にする

The camera remains completely static in a locked-off middle shot.
The camera holds its original position, orientation, focal length, and framing for the entire shot.

static cameraとfast orbitのような矛盾した指示を同じ場面に入れないようにします。動かす場合は軌道・速度・被写体との距離・開始と終了の位置を肯定形で記述します。

6. 秒数を固定しない実用テンプレート

動画尺を毎回変える場合は、単一ショット内で「開始→進行→終了」を書く方法が扱いやすいです。公式の厳密な複数ショット形式は2ショット目以降にカット時刻を付けますが、尺を使い回す用途では、まず単一ショットにします。

subject_definitions:
<Subject 1> is the main character shown in <Picture 1>. Preserve [顔・髪・体型・服装など].
<Subject 2> is [Picture 2から借りる要素]. Transfer only [具体的な特徴] to <Subject 1>.

summary:
[reference generation] Create one continuous shot using <Subject 1> as the main character and transferring only the specified feature from <Subject 2>.

retention_analysis:
<Subject 1> (appears in [Shot 1]): fully_preserved - preserve [維持する特徴].
<Subject 2> (appears in [Shot 1]): attribute_transfer - transfer only [借りる特徴]; do not copy the source person or scene.

detailed_description:
[画風、照明、全体の雰囲気].
[Shot 1] Begin with [開始構図]. <Subject 1> [最初の動作]. Then [次の動作]. As the action continues, [変化]. Near the end, [終了動作]. The camera remains [カメラ指示]. End with [最終状態].

overall_soundscape:
[環境音・物理音。不要なら N/A]

non_diegetic_music:
[BGM。不要なら N/A]

7. 具体例1：Picture 1の人物・背景を維持して動かす

用途：1枚目の人物、服、背景を主参照にする。ただし画像を厳密な開始フレームにはしないR2V。

subject_definitions:
<Subject 1> is the adult woman shown in <Picture 1>. Preserve her facial identity, shoulder-length black hair, dark eyes, body proportions, white blouse, and dark skirt.
<Subject 2> is the room shown in <Picture 1>. Preserve the window position, pale wall, wooden table, soft daylight direction, and restrained neutral colors.

summary:
[reference generation] Create one continuous realistic shot of <Subject 1> standing naturally inside <Subject 2> and performing a small controlled action.

retention_analysis:
<Subject 1> (appears in [Shot 1]): fully_preserved - retain her identity, hair, body proportions, and clothing.
<Subject 2> (appears in [Shot 1]): fully_preserved - retain the room layout, table, window, daylight direction, and color palette.

detailed_description:
Natural live-action realism with soft daylight and stable anatomy.
[Shot 1] A stable middle shot shows <Subject 1> inside <Subject 2>, with her full face clearly visible in the upper part of the frame and her torso visible below. She looks toward the table, slowly reaches for the cup, lifts it to chest height, glances toward the camera, and settles into a relaxed pose. The camera remains completely static and locked off. Keep her face at the same upper-frame position and keep her apparent body size unchanged. Maintain the original camera position, focal length, subject scale, and framing, with only the main character visible. End on a stable middle shot with the cup held at chest height.

overall_soundscape:
Quiet indoor room tone with soft fabric movement and one light ceramic contact sound.

non_diegetic_music:
N/A

8. 具体例2：Picture 1を主画像、Picture 2を手だけの参照にする

用途：Picture 1の人物・背景・構図を中心にし、Picture 2から手の形と向きだけを移す。

subject_definitions:
<Subject 1> is the adult woman and main scene shown in <Picture 1>. Preserve her facial identity, hairstyle, body proportions, clothing, background, lighting direction, and middle-shot composition.
<Subject 2> is only the right-hand configuration shown in <Picture 2>: the palm faces the body surface, the back of the hand faces outward, the wrist remains in neutral rotation, and the fingers keep the referenced arrangement. Transfer only this hand configuration to <Subject 1>. Keep the person, face, arm proportions, clothing, background, lighting, camera angle, crop, and overall pose from <Picture 1>.

summary:
[reference generation] Create one continuous shot based primarily on <Subject 1>. Transfer only the right-hand configuration from <Subject 2> while preserving the person, scene, and composition from <Picture 1>.

retention_analysis:
<Subject 1> (appears in [Shot 1]): fully_preserved - retain the woman's identity, clothing, scene, lighting, and middle-shot composition.
<Subject 2> (appears in [Shot 1]): attribute_transfer - transfer only the palm orientation, wrist rotation, and finger arrangement to <Subject 1>'s right hand.

detailed_description:
Natural live-action realism with stable anatomy, consistent identity, and restrained motion.
[Shot 1] Begin in a stable middle shot based on <Subject 1>. Her face remains fully visible near the top of the frame while her torso and right arm remain visible below. She moves her right hand slowly toward the target surface. Her palm stays continuously oriented toward the surface, the back of the hand stays outward, and the wrist does not roll or reverse. Her fingers maintain the arrangement defined by <Subject 2> throughout the contact and following motion. The palm continuously faces the target surface with stable wrist alignment. The camera stays fixed at the original position, keeping the same focal length, crop, and framing. Keep the background and lighting from <Picture 1>. End with the hand in the specified orientation and the woman's identity unchanged.

overall_soundscape:
Quiet room tone with subtle clothing movement.

non_diegetic_music:
N/A

この例の要点

- Picture 2を独立した場面や構図として扱わない
- attribute_transferで局所的な特徴だけを移す
- 手の向きを、手の平・手の甲・手首の3点で定義する
- 動作中も向きが維持されることを書く

9. 具体例3：画像の人物にVideo 1の動きだけを移す

用途：キャラクター置き換え。Picture 1の人物を使い、Video 1から動作・タイミング・カメラを借りる。

subject_definitions:
<Subject 1> is the adult woman shown in <Picture 1>. Preserve her exact facial identity, hairstyle, skin tone, body proportions, and clothing throughout.
<Subject 2> is the complete body action performed by the main person in <Video 1>, including the head turns, eye direction, facial expressions, arm movement, hand movement, walking rhythm, and final pose.
<Video 1> supplies only the action order, body mechanics, timing, framing, and camera movement. Use the identity, face, hair, body, and clothing of <Subject 1> from <Picture 1>.

summary:
[reference generation] Generate a new video starring <Subject 1>. Transfer the motion and camera structure from <Video 1> while keeping <Subject 1>'s appearance consistent.

retention_analysis:
<Subject 1> (appears throughout [Shot 1]): fully_preserved - retain her identity, face, hair, proportions, and clothing.
<Subject 2> (appears throughout [Shot 1]): attribute_transfer - transfer the visible body and facial performance to <Subject 1>.
<Video 1> (motion, timing, framing, and camera): fully_preserved - follow its temporal structure without copying its original person's appearance.

detailed_description:
Realistic live-action style with natural anatomy and stable facial identity.
[Shot 1] Replace only the main person from <Video 1> with <Subject 1>. Reproduce the visible action in the same playback order: the same initial stance, head movement, eye direction, facial performance, body movement, arm and hand movement, walking rhythm, and final pose. Follow the camera path, framing changes, and action timing from <Video 1>. Preserve the environment and lighting from <Video 1> unless otherwise specified. Reproduce only the referenced gestures, steps, actors, cuts, and camera path in their original sequence. Keep <Subject 1>'s face, hair, body proportions, and clothing consistent throughout the entire shot.

overall_soundscape:
Follow the physical sound timing from <Video 1>, but do not copy speech or music unless separately assigned as an audio reference.

non_diegetic_music:
N/A

音声を分ける場合

Video 1の映像だけを使うなら、音声まで自動的に引き継ぐ指定をしません。声質だけを参照する場合は<Audio 1>: reference、元の音声信号をそのまま使う場合はfully_copyまたはpartially_copyとして別に定義します。

10. 具体例4：Picture 1を正確な開始フレームにする

ComfyUIでは、画像をMiniMaxH3ImageToVideoノードのfirst_frameに接続します。プロンプトだけでR2V画像を開始画面として強く指定するより、I2Vの入力で固定する方が適しています。

For the target video, at 0.00 seconds, <Picture 1> is the fully preserved opening frame.

integrated_multimodal_description:
[Shot 1] Begin exactly from <Picture 1>. Preserve the same person, face, hair, clothing, environment, lighting, camera angle, crop, and subject placement at the opening. After the opening frame, the woman slowly turns her eyes toward the camera, lifts her right hand to chest height, gives one restrained smile, and becomes still. Keep one continuous shot. The camera maintains its original position, orientation, focal length, and composition throughout. End with the same composition and the woman holding the final pose.

overall_soundscape:
Quiet indoor room tone with subtle fabric movement.

non_diegetic_music:
N/A

冒頭の0.00 secondsは開始フレームとの対応を示すための固定表記です。動画全体の尺を指定するものではありません。

11. 絵コンテ画像を使う場合

<Picture 3> is a storyboard reference for [Shot 1], [Shot 2], and [Shot 3].
Use it only for shot order, viewpoint, subject placement, and approximate framing.
Use the storyboard panels for spatial and temporal guidance; render the final footage as full-frame scenes.

絵コンテは完全なフレーム再現ではなく、順序と構図のガイドとして扱います。短い動画では2〜3カット程度から試し、成立後に増やします。

12. よくある失敗と修正方法

| 症状 | 主な原因 | 修正 |
|---|---|---|
| Picture 1と違う構図から始まる | R2Vの参照画像を開始フレームだと考えている | 正確な冒頭が必要ならI2Vのfirst_frameへ接続 |
| Picture 2の人物や背景まで混ざる | 補助画像の担当が広すぎる | onlyで採用要素を限定し、採用しない要素も列挙 |
| 顔が途中で別人になる | 顔が小さい、画像同士が矛盾、参照解像度不足 | 鮮明な正面・斜め前を使い、ref_image_size=max、特徴を具体化 |
| 手が反転する | 「手を置く」だけで掌・甲・手首の関係が未定義 | 掌の向き、手の甲、手首回転、動作中の維持を別々に記述 |
| 勝手にズームする | カメラ指示が曖昧、構図変化を動作として解釈 | locked-offと禁止する運鏡を具体的に記述 |
| Video 1の人物までコピーする | 動作と人物の役割分離がない | 画像＝identity、動画＝motion/cameraと明記し、動画人物の外見を除外 |
| 指示の一部が抜ける | 動作、カメラ、音、複数参照、複数カットを一度に追加 | 参照と指示を1要素ずつ増やして検証 |
| 遠景の人物が崩れる | 顔の画面占有率が低い | 最初の検証はミドルショット以上にし、遠景は別テストにする |

13. 検証の進め方

1. Picture 1だけで、人物と背景が維持できるか確認
2. 小さな動作を1つだけ加える
3. Picture 2を追加し、局所要素だけが移るか確認
4. Video 1を追加し、動作とカメラだけを移す
5. 最後に音声、カット、複雑な動作を追加

比較時はseed、解像度、steps、schedulerを固定し、一度に変える項目を1つにします。今回の基準は、通常品質なら20 steps、比較用に25 steps、16:9なら1344×768前後、人物参照はref_image_size=maxです。

14. 実用上の推奨方針

現在の主な用途には、次の役割分担が合っています。

Picture 1 = 主人物、服装、背景、基本構図
Picture 2 = 手・小物・局所ディテールだけ
Video 1   = 動作、順序、タイミング、カメラだけ
Audio 1   = 必要な場合だけ、声質または元音声

秒数を毎回変える場合は、まず[Shot 1]だけの連続ショットにし、Begin... / Then... / As the action continues... / Near the end... / End with...で順序を作ります。正確なカット位置が必要になった場面だけ、動画尺に合わせた時刻入り版を作ります。

15. 調査から分かったこと

公式情報として確認できた点

- R2Vは画像・動画・音声を混ぜ、人物、画風、動作、カメラ、声などを参照できます。
- ComfyUIのR2Vでは、参照素材を接続順どおり<Picture 1>、<Video 1>などで呼びます。
- 画像は最大9枚、動画は最大3本、単独音声は最大3本です。
- ref_image_size=maxは速度と引き換えに人物同一性を強める設定です。
- 公式の高度な形式は、subject_definitions、summary、retention_analysis、detailed_description、overall_soundscape、non_diegetic_musicの6部構成です。
- 高度な形式は英語で書き、会話や歌詞、画面に見せる文字だけ元の言語を維持します。

X・コミュニティの実例から確認できた傾向

- Picture 1 supplies identity only, not pose or framingのように、画像が担当しない要素まで明記する例が多く見られます。
- 正確な開始画面を狙う投稿では、exact first frame、only visual anchorのように、冒頭と参照範囲を強く限定しています。
- 補助参照が1枚だけの場合も、ONLY visual referenceと明記し、維持対象を列挙する例があります。
- 参照動画を使った人物置き換えでは、画像側に人物同一性、動画側に動作・タイミング・カメラを割り当てる書き方が実用例として使われています。

これらは再現を保証する魔法の単語ではなく、H3に参照関係を誤解させにくくする整理方法です。

16. 主な参照先

公式・一次情報

- MiniMax H3 Full-Reference Mode Prompt Guide (https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/docs/VIDEO_PROMPT_WRITING_GUIDE_ref_en.md)
- ComfyUI公式 MiniMax H3 T2V / I2V / R2Vガイド (https://docs.comfy.org/tutorials/video/minimax/minimax-h3)
- ComfyUI公式 MiniMax H3 Reference to Video workflow (https://comfy.org/workflows/46a303cbccf9-46a303cbccf9/)

詳細解説

- RunDiffusion MiniMax H3 Prompt Guide (https://www.rundiffusion.com/minimax-h3-prompt-guide)
- ComfyUI MiniMax H3 Guide（GitHub） (https://github.com/ethanfel/ComfyUI-MiniMax-H3-Guide)

X・コミュニティ実例

- Picture 1をidentity onlyとして分離する例 (https://x.com/IamEmily2050/status/2084274703489790372)
- Picture 1を唯一の参照として維持対象を列挙する例 (https://x.com/LoveUolanda/article/2088867546464473474)
- 2枚の画像を正確な開始・終了フレームとして扱う例 (https://x.com/Dheepanratnam/status/2087136564316877152)
- Picture 1をexact first frameとする例 (https://x.com/Cardoso/status/2088296385422455165)
- 開始フレームの公式形式を使ったモーショングラフィックス例 (https://x.com/ponzponz15/status/2086681966917939218)
- R2V画像を固定開始フレームにしない指定例 (https://x.com/Vtuber7144/status/2090030495921033313/photo/1)
- 画像の人物と参照動画の動きを分けるコミュニティ例 (https://www.reddit.com/r/StableDiffusion/comments/1vfzyxv/how_to_replace_char_with_minimax_h3/)

17. 【v2追加】最重要：肯定形・映像記述優先ルール

原則：ユーザーの希望を「禁止リスト」へ機械的に書き換えない。モデルへ伝えるのは、視聴者が実際に見る映像、カメラが実際に辿る経路、維持される状態である。

運用ルール：
1. 「カットせずに」「ズームしないで」「顔を変えないで」などの否定的な日本語は、まず肯定形の英語に変換する。
2. 変換時に意図を変えない。ワンカット撮影を「固定カメラ」に置き換えない。ワンカットでもカメラは動ける。
3. camera, subject, action, duration, final frame の順に映像を具体化する。
4. No cuts / No zoom / Don't change ... といった禁止句の列挙を既定出力にしない。
5. 参照素材が競合する場合、何を採用し、残りをどの素材から採用するかを先に明示する。否定的な制約が技術上必須であれば、理由を把握した上で最小限だけ使う。
6. 同一の禁止句をsummary、retention_analysis、detailed_descriptionに繰り返さない。
7. プロンプト出力前に「ユーザー意図を禁止語の羅列へすり替えていないか」を確認する。

変換例：
日本語：カットを切り替えず、一連のカメラワークで人物の横から背後まで映す。
推奨：A single continuous moving-camera shot. The camera starts beside the subject, follows a smooth clockwise arc around the subject, passes behind the shoulder, and settles at a rear three-quarter viewpoint. The movement is physically continuous, with consistent subject scale and natural parallax throughout.

日本語：ズームせず人物の大きさを保つ。
推奨：The camera tracks parallel to the subject at a constant distance, maintaining the same focal length and apparent subject size throughout the shot.

日本語：顔を別人にしない。
推奨：<Subject 1> retains the facial identity, hairstyle, and distinctive features defined by <Picture 1> throughout the motion.

注意：肯定形にすれば必ず成功するという保証はない。公式ComfyUIガイドはBasicGuider / cfg 1の構成でnegative branchを使わず、禁止語の羅列を避けることを推奨している。これは主に文章設計上の原則であり、技術的な制約入力全般を禁止する意味ではない。

18. 【v2追加】単一連続ショットと複数ショットを区別する

・単一連続ショット：原則[Shot 1]のみ。カメラ移動をそのショット内の時間順の軌道で記述する。
・複数ショット：画面の切替が意図される場合だけ[Shot 2]以降を作成し、後続ショットには明確なカット時刻を入れる。
・「カメラが人物の正面から背後へ回る」は、カメラが移動する指示であって、視点の切替・編集カットを意味しない。
・動きが複雑なときは start viewpoint → camera path → passing position → end viewpoint を記す。
・カメラ位置の変化に応じた背景の視差（parallax）を明記すると、実際に移動する意図を説明しやすい。

連続移動のテンプレート：
detailed_description:
[Shot 1] A single continuous live-action shot. Begin at [開始位置・構図]. The camera then [方向・軌道・速度] while tracking [被写体]. As it passes [中間地点], maintain [距離・画角・被写体サイズなど]. The camera arrives at [終了位置・構図] and holds the final view. Realistic spatial continuity and background parallax accompany the entire camera movement.

19. 【v2追加】I2V / R2V / Multiframe / ControlNetの使い分け

・I2V first_frame：冒頭画面を入力で拘束。要求するアスペクト比とクロップ、入力画像の画角の一致を確認する。文章だけでピクセル単位の一致を保証できない。
・I2V first + last：始点と終点を与える。途中経路、身体動作、映像の連続性はプロンプトで補う。
・R2V：人物同一性、衣服、背景、動作、カメラ、声などの参照役割を区別する。参照画像をつなぐだけで冒頭フレームが固定されるとは限らない。
・Multiframe Reference：MiniMaxH3AddGuide等で任意のframe_idxに画像/音声のガイドを配置。画像ガイドのみの入力は文章側の<Picture N>参照として自動認識されない場合があるので、必要に応じてref_imagesへも接続する。これはガイド条件付けであり、入力動画全体をそのまま編集するV2Vとは異なる。
・Fun ControlNet Union：Canny、Depth、HED、MLSD、Poseまたはマスクによる構造・姿勢制御。プロンプトだけで姿勢が安定しないときの別手段として扱う。
・既存のComfyUI環境に該当ノードがあるかを確認する。新機能の存在だけで、現在のRunPod構成に導入済みと判定しない。

20. 【v2追加】動画尺、FPS、設定の実装上の注意

・公式ComfyUIテンプレートは24fpsを前提とする。lengthは秒数ではなくフレーム数。
・公式ガイドに記載される有効フレーム数は17k+5の形にスナップされる。例：124フレームは約5.17秒。設定値と最終出力の秒数を混同しない。
・標準16:9のネイティブ目安は1344×768。サイズは32の倍数というテンプレートの条件を守る。
・参照動画は24fpsとして読まれるため、別FPSの入力は必要に応じて事前変換する。
・R2Vはref2va系、T2V/I2Vはfl2va系を使用。ワークフローに適合するモデルを選ぶ。
・ref_image_size=matchは出力に合わせる既定選択肢、maxは短辺最大2048pxを保持する高負荷選択肢。小画像を自動的に高精細化するわけではない。
・20～25 stepsは参照忠実度重視の検証基準。Turbo/Lightning LoRAの4-step構成は高速化できる一方、参照・音声・動きの品質が低下する場合がある。比較時には設定を分ける。
・スタイルLoRAは画像参照と競合しうる。必要時は低強度から個別検証し、設定は固定値として決めつけない。
・FastH3等の高速ワークフローは別条件として測定する。品質比較と生成速度比較を混在させない。

21. 【v2追加】音声・セリフの整理

・overall_soundscape：環境音、効果音、非言語音。
・non_diegetic_music：場面外BGM。不要ならN/A。
・セリフや歌詞は公式形式の<d>タグに原語で記述する。発話内容と声質参照は別概念。
・動画に付随する音声は映像参照と自動的に同じ扱いとは限らず、対応する音声入力への接続を確認する。
・R2Vの音声参照はfully_copy / partially_copy / reference / weak_referenceなどの保持属性を用途に応じて区別する。
・動画から動作のみを借りる場合、声・環境音・BGMまで無条件に流用する指定を避ける。

22. 【v2追加】検証と運用ルール

確認順序：
1. 入力モードと参照画像の役割が一致するか。
2. 開始フレームの固定が必要ならノード側で設定されているか。
3. カメラ指示は固定/移動、連続/編集カットを正しく区別しているか。
4. 肯定形によって移動経路や被写体の状態を具体化しているか。
5. identity / pose / framing / environment を不用意に他画像から混ぜていないか。
6. 既存のseed、解像度、fps、length、steps、scheduler、LoRAを比較条件として記録したか。
7. 結果が崩れた場合、変更する要因を一つずつ比較しているか。

失敗時の切り分け：
・カットが挿入される → [Shot 1]に統一し、カメラ軌道を連続動作として書き直す。
・カメラが固定される → 開始・通過・終了の3つの位置と視差を明記する。
・画角が急に変わる → カメラと被写体の距離・焦点距離・被写体サイズを具体化する。
・開始画像に一致しない → I2V first_frame接続とクロップ条件を先に確認する。
・姿勢が破綻する → 動作を小さく分解し、必要ならPose/Depthガイドを検討する。
・人物が変わる → 主参照の優先順位、画像の矛盾、参照解像度、LoRAの強さを確認する。

23. 【v2追加】根拠と注意

一次資料（2026-10-31参照）：
・MiniMax R2V Full-Reference Guide:
  https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/docs/VIDEO_PROMPT_WRITING_GUIDE_ref_en.md
・ComfyUI H3総合案内:
  https://docs.comfy.org/tutorials/video/minimax/minimax-h3
・ComfyUI H3 Prompt Guide:
  https://github.com/Comfy-Org/docs/blob/main/tutorials/video/minimax/minimax-h3-prompt-guide.mdx
・ComfyUI H3 Native R2V Guide:
  https://github.com/Comfy-Org/docs/blob/main/tutorials/video/minimax/minimax-h3-native.mdx
・ComfyUI H3 Multiframe:
  https://github.com/Comfy-Org/docs/blob/main/tutorials/video/minimax/minimax-h3-multiframe.mdx

注意：公式仕様、推奨ベストプラクティス、本ガイド独自の運用ルールは同一ではない。特に肯定形への変換、ワンカット指示の構成、検証順序は推奨される実践的手法であり、個々の生成の成功を保証しない。旧章に含まれる数値・事例は当時の検証設定として残しているため、環境更新時は再検証する。
