# 失敗のはなし：あいだに現れるもの

## 1. プロローグ：寸法の更新忘れ

2D CADで流用設計をしていたときの話です。

全長を10 mmだけ伸ばせばよい。外形を矩形として選び、stretchをかけると、形状は狙いどおりに変わりました。

ところが図面が製造に回ったあと、「寸法が合っていません」と連絡が来ました。

外形線レイヤは更新されているのに、寸法レイヤは更新されず数値が古いままだったのです。疲れているとき、急いでいるとき、最後の確認が薄くなると、これは簡単に見落とします。

これは単なる確認漏れだったのか。それとも、形状と寸法が別レイヤに住み、独立にずれてしまう道具の構造的問題だったのか。

単発のミスというより、境界で生まれた失敗に感じました。私の注意は片方のレイヤに向き、図面の「真実」は、互いに乖離してしまった二つのレイヤに割れていたのです。

---

## 2. 失敗は境界で起きる

ニュースでは「操作ミス」「設計ミス」といった言い方をよく見ます。

けれど細かく見ると、多くの失敗は単一要素だけで起きていません。境界で起きます。

- across the interface between humans and machines
    
- along the fault line between design intent and shop-floor interpretation
    
- in the gap between words and actions
    

同じ構造は、CAD図面の中にもあります。

### 2D CAD boundaries

2D CADの図面には複数のレイヤがあります。

- outline layer: geometry
    
- dimension layer: dimension values
    
- text layer: notes
    
- title block layer: part number and material
    

各レイヤは独立に編集できます。片方を変えても、もう片方は自動では追従しません。

失敗は、形状と寸法の境界で立ち上がります。

### Common inconsistencies

Geometry–dimension drift

- 外形は動いたが、寸法値は動いていない
    

Title-block copy-paste errors

- 形状は新しいのに、品番が古いまま
    

Assembly–detail drawing mismatch

- 組図面は更新したが、バラシ図面への反映を忘れた
    

いずれも、境界で整合が崩れた結果です。

### 3D CAD can hide a different boundary

3D CADは、形状と寸法を結び付けることで、いくつかの不整合を消したように見せます。

しかし同時に、失敗をより後段の境界へ移動させることがあります。多くの場合それは、設計意図と製造現実のあいだの境界です。

その「移動」はSection 4でほどきます。

---

## 3. 整合が滑るとき

システムは、right thingがright placeにあり、right timeに出てくるときに動きます。

そのうちのどれかが滑ったとき、私たちは失敗を観測します。

### Three axes

Spatial alignment

- not in the right place
    
- example: 穴位置、部品配置
    

Temporal alignment

- not at the right time
    
- example: 改訂管理、反映漏れ
    

Semantic alignment

- not the right thing
    
- example: 単位の取り違え、図枠と形状の不一致
    

私の「10 mmのstretch」では、形状は最新状態を反映しているのに、寸法は古い状態に固定されていました。

一枚の図面の中に、異なる時間が共存していた。その割れ目で、失敗が可視化されたのです。

次の問いは実務的です。整合が滑ったとき、具体的に何が壊れていて、修理はどんな形を取るのか。

---

## 4. 失敗を構造として読む

失敗を「構造」として学ぶには、変換がどう壊れるかを実務の手触りで名付けるのが有効です。

私は修理の仕方が変わるので、次の3つに分けます。

**Missing** — 更新や引き継ぎが、そもそも起きていない。

**Mismatch** — 二つの状態が共存し、境界で食い違っている。

**Non-reproducible** — 後から、どの状態や前提が有効だったかを再構成できない。

|Mode|Tactile example|Minimum repair|
|---|---|---|
|Missing|新しい改訂に寸法値が引き継がれていない|Complete: 欠けた値を埋め、どの改訂を正とするかをpinする|
|Mismatch|外形は110、寸法は100|Compare on a pinned basis: 両状態をfreezeしdiffし解決し、整合した単一改訂として再発行する|
|Non-reproducible|製造へ送ったのはどの改訂か|Trace: evidence（timestamp、file hash、approval note）を添付し、artifactのidentityが再構成可能な一状態を指すようにする|

Non-reproducibleは、しばしばidentityの失敗です。artifactが「どの状態であるか」を指し示せません。

The mode shapes the repair. But detection timing shapes the cost.

このずれが私の言う _night-before structure_ を生みます。検出が最後の境界まで先送りされ、そこで人間の注意資源が最も薄い瞬間（締切、疲労、圧縮されたレビュー）と衝突するパターンです。

検出が後ろへずれるのと同時に、人間の注意は減衰します。疲労が増え、確認時間が圧縮され、見落としのコストが跳ね上がる。

fail-fastは、時間幾何としての逆です。検出を前に引き寄せ、修理を安く局所に留める。

その意味で、5Sは時間軸にも作用します。改訂を整理し、古い中間状態を捨て、「current」をpinしやすい状態に保つ。

### Failure reports are not enough

失敗報告はたいてい「再発防止策」で終わります。

- チェックリストを作る
    
- ダブルチェックを徹底する
    
- 記録を残す
    

必要ではありますが、それだけでは足りません。

失敗を構造の記録として読むと、道具そのものの設計が見えてきます。

### Parametric design as a partial solution

現代の3D CADは、形状と寸法を結び付けられます。

形状を変えれば寸法も追従する。これはレイヤ間の整合を自動化する設計です。

2D CADで起きがちな「寸法の更新忘れ」は、起こしにくくなります。

### But the failure only moved

3D CADは、buildableになるずっと前にfeasibleに見せることがあります。

画面上では組めて、干渉チェックも通る。

しかし製造では別種の制約が露出します。工具が届かない、締結工具を入れる空間がない、組立手順に成立する経路がない。

失敗は消えたのではなく移動した。しかも後ろへ移動すると、コストが上がり、「提出前夜」に顔を出しやすくなります。

### Failure migration

|Tool|Boundary where failure emerges|Typical detection timing|
|---|---|---|
|Hand drafting|geometry–dimension inconsistency|drawing review|
|2D CAD|inter-layer inconsistency|drawing review|
|3D CAD|design–manufacturing drift|fabrication / assembly|

道具が変わっても、境界で生まれる失敗は形を変えて残ります。

### Both 2D and 3D are necessary

これは優劣の議論ではありません。

2D CADの強みは解析的理解です。複雑な軸物を設計するとき、CTのスライスのように多断面を描きます。各断面を独立に読め、形状変更を論理的に整理できる。3D CADは全体を掴めますが、内部構造は読みにくいことがある。断面で切って読むのは解析の方法です。

3D CADの強みは成立性の検証です。干渉、組立手順、全体形状。これらは2D CADでは検証しにくい。

実務では目的で使い分けます。

- 2D: 構造の分析、製作用図面
    
- 3D: 成立性の検証、組図
    

単一の道具で全ては解けません。設計者の仕事は、道具間のギャップを橋渡しすることです。

### Reading as structure

私の図面の失敗を構造として読むと、こう見えます。

- slipped axes: space（geometry–dimensionのズレ）, time（改訂がレイヤ間でずれた）
    
- detection gate: 寸法と形状の自動突合
    
- repair: parametric coupling
    

この構造が見えれば、同じ失敗を観測可能なシステムへ進化させられます。

失敗は糾弾の材料ではありません。再設計の手がかりです。

---

## 5. 結び：あいだを観測する文化へ

失敗は誰か一人の過失ではありません。システムの不整合が露出する断層です。

図面と現場のあいだ。設計と製造のあいだ。あるレイヤと別のレイヤのあいだ。

境界を観測すると、システムの輪郭が見えてきます。

犯人探しの代わりに、構造を見る。そこから「betweenで起きること」を読む文化が始まります。

---

私が深く尊敬していた先輩設計者には、こんなルールがありました。

「CAD禁止。消しゴム禁止。間違えたら最初からやり直せ。」

極端に聞こえますが、意図は明確です。

間違えたら消すな。新しい紙で描き直せ。

詰まった図は、そのまま残す。

机の上には試行錯誤が物理的に蓄積します。各試行は「失敗」ですが、並べると探索のプロセスが見える。

同じ問題に対する、少しずつ違うアプローチ。少しずつ違う部品の組み合わせ。

今振り返ると、ソフトウェアでGitのbranchを並べるのに似ています。

複数の試行を並べることで、一回の試行では見えなかった構造が立ち上がる。

失敗の蓄積が、新しいアイデアを生む。

私もゼロから探索するときや、設計が詰まったときは、CADを閉じて真っ白な紙に戻ります。

淡い青の5 mm方眼は、何も主張しない。ただ静かにアイデアを受け止めてくれます。

CADは失敗を消せます。けれど意図的に痕跡を残せば、設計は探索ログになります。

3D CADは幾何の整合を保証できます。けれど探索のプロセスまでは保証しません。

道具を選ぶとは、何を守りたいかを選ぶことです。

失敗は、システムの不整合が可視化される断層です。

そして、消さないこと。試行を並べること。もう一度白紙に戻り、アイデアを拾い直すこと。

それもまた、betweenで起きることを観測する文化の一部です。

---

## Figures

### Figure A: Inter-layer inconsistency

```
[Outline layer]
  ●─────●  (geometry: new position)

[Dimension layer]
  ├─ 10 ──┤  (dimension: old value)

↓ inconsistency

Shop floor:
  geometry and dimensions contradict

Caption:
Failure emerges at the boundary called a layer
```

### Figure B: Three axes of alignment

```
Space  ──◯────× (geometry–dimension position drift)
Time   ──◯────× (revision drift across layers)
Meaning──◯────× (title block vs geometry mismatch)

Caption:
The axis where alignment breaks shapes the failure
```

### Figure C: Failure migration

```
[Hand drafting]
  failure: geometry–dimension inconsistency
  detection: drawing review ●

    ↓ to CAD

[2D CAD]
  failure: inter-layer inconsistency
  detection: drawing review ●

    ↓ to 3D

[3D CAD]
  failure: design–manufacturing drift
  detection: fabrication / assembly ●●● (moves later)

Caption:
Even as tools evolve, failures remain by changing form
Detection timing can move later
```

### Figure D: A drawing as an exploration log

```
[Try 1]       [Try 2]       [Try 3]
 ●─●          ●─●          ●─●─●
   └× stuck     └× stuck     └○ done

Keep attempts side by side physically
  ↓
Similar but slightly different shapes become visible
  ↓
A source of new ideas

Caption:
By not erasing failures, the exploration process becomes visible
This resembles Git branches
```

JP–EN mini glossary

|JP|EN|
|---|---|
|あいだ|between, boundary|
|整合|alignment|
|不整合|inconsistency|
|図枠|title block|
|寸法線|dimension line|
|外形線|outline|
|組図面|assembly drawing|
|バラシ図面|detail drawing|

---

## References

- 畑村洋太郎『失敗学のすすめ』講談社, 2000.
    
