
ピクセルからプランへ：ゲームプレイAIエージェントのためのベンチマーク環境に関する包括的調査


序論：人工知能とゲームの共進化的関係


ベンチマークの根源的重要性

定量的ベンチマークは、人工知能（AI）モデルやシステムの性能、能力、安全性を評価するための基本的なツールとして登場し、現在ではAI開発の方向性を形成し、さらには規制の枠組みにおいてもますます重要な役割を果たしています 1。これらは単なる受動的な測定ツールではなく、AI開発の方向性を積極的に形成する力となっています。ベンチマークは、研究者や開発者にとって重要なフィードバックシグナルを提供し 1、健全な競争を促進します 2。その重要性は非常に高く、高いベンチマークスコアを達成することは、商業的にも研究的にも主要な目標となっています。例えば、市場の主要プレイヤーであるOpenAIは、ARC-AGIベンチマークで高スコアを得るために数十万ドルもの計算資源を費やしたと推定されています 1。
さらに、ベンチマークの役割は技術開発の領域を超え、社会政治的な次元にも及んでいます。EUのAI法（EU AI Act）のような規制の枠組みでは、高リスクAIシステムの精度や堅牢性、サイバーセキュリティ要件への準拠を評価する上で、ベンチマークが中心的な役割を果たすことが期待されています 1。これは、ベンチマークが単に世界を記述するだけでなく、それを積極的に形成するという「遂行性（performativity）」を持つことを示唆しています 1。しかし、この影響力の増大は、ベンチマーク自体が透明性、公平性、説明可能性といった、AIモデルに求められるのと同じ厳格な基準に服さなければならないという新たな要求を生み出しています 1。

AI研究の「ショウジョウバエ」としてのゲーム

AI研究の歴史において、ゲームは理想的な実験場、いわば「ショウジョウバエ」としての役割を果たしてきました。ビデオゲームは、明確に定義された目標とスコアリングシステムを持つ、自己完結した環境を提供するというユニークな組み合わせを持っています 3。現実世界のシナリオが持つ曖昧さや複雑さとは対照的に、ゲームは成功を客観的に測定できる構造化された課題を提供します 3。この特性により、ゲームはAIアルゴリズムが複雑な問題を解決する方法を訓練するための理想的なプラットフォームとなります。
AIにおけるゲームプレイの歴史は、チェスのような決定論的で完全情報なゲームから始まり、現代のビデオゲームが提供する、不完全情報で確率的な、より複雑な環境へと進化してきました 3。これらの現代的なゲーム環境は、知覚、戦略的計画、そしてリアルタイムの意思決定といった、現実世界の課題を解決するために不可欠な能力の組み合わせをAIに要求します 3。DeepMindによる画期的なAtari実験以降、ゲームは汎用AI能力を開発するための本格的な研究ツールとして確立されました 3。ゲーム環境は、AIが視覚情報を処理し、戦略的に先を読み、正確な行動をリアルタイムで実行するという、人間が当たり前に行っている能力を再現するための試金石であり続けています。
AIとベンチマークの歴史を振り返ると、それは単なる線形の進歩ではなく、共進化的なループとして捉えることができます。新しいベンチマークの登場が、特定のAI技術のブレークスルーを可能にします。例えば、Arcade Learning Environment（ALE）は、深層強化学習（Deep Reinforcement Learning, DRL）の分野でDQN（Deep Q-Network）のようなアルゴリズムの成功を後押ししました 3。しかし、コミュニティがそのベンチマークを「解決」または飽和させるにつれて、そのベンチマークの限界が明らかになります。ALEの場合、固定されたゲームセットに対する過剰適合が、エージェントが真に汎用的なスキルを学習しているのかという疑問を提起しました 7。この認識された限界、すなわち汎化能力を測定する手段の欠如が、次世代のベンチマークであるProcgen Benchmarkの創設を直接的に動機付けました。Procgenは、手続き的生成を用いて訓練セットとテストセットを明確に分離し、汎化能力を直接測定することを目的としています 7。同様に、2Dアーケードゲームの単純さは、部分的な観測可能性や記憶を要求する、より複雑な3D環境の必要性を浮き彫りにし、DeepMind Labのようなプラットフォームの開発へとつながりました 10。このように、AIの能力と評価方法論は、互いに互いを前進させるサイクルの中で発展してきました。この共進化的プロセスこそが、この分野における進歩の主要な原動力となっているのです。

I. 基礎の時代：強化学習のためのプレイフィールドの標準化


Arcade Learning Environment (ALE): 深層強化学習の夜明け

Arcade Learning Environment（ALE）は、深層強化学習革命の触媒となった評価プラットフォームです 12。数百種類に及ぶAtari 2600ゲームへのインターフェースを提供することで、ALEは汎用的かつドメイン非依存のAI技術のための、多様で挑戦的なテストベッドを研究コミュニティに提示しました 13。その登場は、異なるアルゴリズムを比較するための共通の土台を確立し、AI研究における極めて重要な瞬間となりました 14。

目的とインパクト

ALEの主な研究目的は、単一のタスクに特化するのではなく、広範なゲームをプレイすることを学習できる「汎用エージェント」のための評価プラットフォームとして機能することです 13。これは、ドメイン固有の調整をほとんど必要とせずに、多様なタスクで能力を発揮できるアルゴリズムを開発するという、AIの長年の目標に合致しています 13。ALEは、強化学習、模倣学習、転移学習といった分野に重要な研究課題を提示し、それらのアプローチを評価・比較するための厳密なテストベッドを提供しました 13。

技術的アーキテクチャ

ALEは、オープンソースのAtari 2600エミュレータであるStellaを基盤として構築されています 12。エミュレーションの詳細をエージェントの設計から切り離すことで、研究者がエミュレーションの複雑さに煩わされることなく、エージェント開発に集中できるクリーンなフレームワークを提供します 12。さらに、100以上のゲームについて、ゲームスコアやゲーム終了シグナルを自動的に抽出する機能を備えており、標準的な強化学習問題として各ゲームを扱うことを可能にしています 12。

主要な特徴と研究課題

ALEが深層強化学習の研究に与えた最も大きな影響の一つは、エージェントが高次元の感覚入力から直接学習する必要がある環境を提供した点です。
観測空間: エージェントは、人間プレイヤーが見るものと同様のRGB画像（210×160×3ピクセル）やグレースケール画像、あるいはコンソールのRAM状態（128バイト）を直接観測として受け取ります 15。これにより、エンドツーエンドの学習、すなわち生のピクセルデータから直接ポリシーを学習するアプローチの開発が促進されました。
行動空間: 標準化された18種類の離散的な行動空間が定義されていますが、各ゲームではそのサブセットが使用されます 15。研究者は、ゲームに影響を与えない行動を除外した縮小行動空間を使用するか、
full_action_space=True引数によって全ての可能な行動を使用するかを選択できます 15。近年では、連続的な行動空間もサポートされるようになり、より繊細な制御が求められる研究にも対応しています 15。
確率性: Atari 2600のゲームは本質的に決定論的であるため、エージェントが最適な行動系列を単に「記憶」してしまうリスクがありました 15。この問題を回避し、より頑健なポリシーの学習を促すため、ALEは2つの確率的要素を導入しました。一つは「スティッキーアクション（sticky actions）」で、これは直前の行動が一定の確率（v0およびv5環境では25%）で繰り返されるというものです。もう一つは「フレームスキッピング（frame-skipping）」で、1つの環境ステップ内で同じ行動がランダムな回数のフレームにわたって繰り返されます 15。

限界と遺産

ALEは深層強化学習の分野を切り拓きましたが、その静的なゲームセットは、エージェントがベンチマーク自体に過剰適合し、未知の環境に対する汎化能力を欠いているのではないかという懸念を生み出しました。また、全57ゲームのスイートで結果を出すには膨大な計算コストがかかるため、Atari-5のような、より小さく代表的なサブセットを選択する研究も行われました 14。ALEの最大の遺産は、汎用エージェントの評価プロトコルを標準化し、その後のベンチマーク開発の基礎を築いた点にあります 13。

OpenAI Gym APIとGymnasiumの台頭：強化学習のための普遍的言語

ALEが深層強化学習のための「課題」を提供したとすれば、OpenAI Gymは、その課題に取り組むための「言語」を標準化したと言えます。Gymは、学習アルゴリズムと環境との間のコミュニケーションのための標準APIを提供し、瞬く間にこの分野の標準となりました 16。

目的と標準化

Gymの核心は、環境をシンプルなPythonのenvクラスとしてモデル化し、make、reset、stepという3つの主要なメソッドを通じて操作するという、エレガントで直感的なAPIにあります 16。この標準化により、研究者は特定のアルゴリズムを、環境の詳細を気にすることなく、多種多様なタスクで迅速にテストできるようになりました。
gym.make("Environment-vX"): 指定されたIDの環境インスタンスを作成します。
observation, info = env.reset(): 環境を初期状態にリセットし、最初の観測を返します。
observation, reward, terminated, truncated, info = env.step(action): エージェントが選択した行動を環境内で実行し、次の観測、報酬、エピソードの終了状態（terminatedまたはtruncated）、および診断情報を返します。

主要な環境ファミリー

Gymは、それ自体が多様な参照環境のコレクションを提供しており、それぞれが異なるタイプの研究課題に対応しています。
Classic Control: CartPole-v1やPendulum-v1のような、物理学に基づいた古典的な制御問題です。これらは状態空間が低次元であるため、新しい強化学習アルゴリズムのデバッグや教育目的に理想的です 18。
Box2D: LunarLander-v2やBipedalWalker-v1など、Box2D物理エンジンを使用した2Dのトイゲームです。より複雑な連続制御タスクを扱います 18。
Toy Text: FrozenLake-v1のように、状態空間と行動空間が小さく離散的で、非常にシンプルなテキストベースの環境です 18。
MuJoCo: Ant-v4やHumanoid-v4など、より複雑で高次元な物理ベースのシミュレーション環境で、多関節ロボットの制御タスクが含まれます 16。
Atari: ALEフレームワークを統合し、Atari 2600ゲームの広範なスイートへのアクセスを提供します 18。

Gymnasiumへの移行

Gymの成功は、それを単なるベンチマークから、強化学習コミュニティ全体にとって不可欠なインフラストラクチャへと昇華させました。しかし、この成功は同時に「メンテナンス負債」という課題も生み出しました。Gymは2016年にOpenAIによってリリースされ、瞬く間に分野の標準となりました 16。数え切れないほどの研究論文、ライブラリ（KerasRL, Tensorforce, RLlibなど 23）、チュートリアル 20 がその安定したAPIに依存するようになりました。しかし、公式ドキュメントによると、Gymは2022年以降メンテナンスされておらず、公式ウェブサイトも閉鎖されました 19。これにより、Numpy 2.0のような新しいソフトウェアバージョンへの対応が欠如するなど、コミュニティにとって深刻な問題が生じました 19。
この状況に対応するため、2021年以降Gymのメンテナンスを行っていたチームが、Gymnasiumという「ドロップイン・リプレースメント（そのまま置き換え可能な代替品）」を作成し、将来のすべての開発をそちらに移行しました 16。これはFarama Foundationの管理下で行われたコミュニティ主導の取り組みであり 17、元の作成者が残したメンテナンス負債を返済するものでした。この一連の出来事は、成功したベンチマークが経験するライフサイクルを示唆しています。すなわち、研究プロジェクトとして始まり、コミュニティのインフラとなり、そして最終的には元の組織の目標を超えた、献身的で長期的な管理体制を必要とするようになるのです。

サードパーティエコシステム

Gymの標準化されたAPIがもたらした最大の功績の一つは、巨大なサードパーティ製環境のエコシステムを育んだことです。研究者や開発者は、金融取引 25、ロボット工学 27、あるいはカスタムデザインのビデオゲーム 28 など、特定のドメインに合わせた独自のGym互換環境を容易に作成し、共有できるようになりました。これにより、強化学習の応用範囲は飛躍的に拡大しました。

II. 複雑性の次元の拡大：3D世界と手続き的生成

基礎的なフレームワークが確立されると、AI研究の関心は、より複雑で現実世界に近い課題へと移行しました。この動きは、ベンチマーク設計における2つの主要な方向性、すなわち環境の忠実度を高める3D化と、汎化能力を直接問う手続き的生成によって特徴づけられます。

DeepMind Lab: 3次元への挑戦

DeepMind Labは、id SoftwareのQuake III Arenaエンジンを基盤とする3D学習環境であり、深層強化学習の研究のためのテストベッドとして設計されました 10。このプラットフォームは、従来の2Dアーケードゲームが主眼としていた反応ベースのゲームプレイから、一人称視点での3Dナビゲーション、記憶、そしてパズル解決へと、研究の焦点を劇的にシフトさせました 10。

中核となる研究課題

DeepMind Labは、それまでのベンチマークでは十分に探求されていなかった、AIエージェントの新たな能力を試すためのフロンティアを開拓しました。
一人称視点からの3Dビジョン: エージェントは、2Dスプライトよりもはるかに複雑な3Dシーンを、生のピクセル入力から解釈することを学ばなければなりません。これは、現実世界のロボットが直面する視覚的課題に一歩近づくものです 11。
ナビゲーションと記憶: 複雑な迷路を探索したり、手続き的に生成される環境の構造を記憶したりするタスクは、エージェントの空間認識能力と長期記憶能力に強い重点を置いています 11。
部分観測可能性: 一人称視点であるため、エージェントは世界の完全な状態を一度に観測することができません。これにより、エージェントは観測履歴から世界の内部モデルや記憶を構築し、見えない部分を推論する必要が生じます。

技術的特徴

DeepMind Labは、Luaスクリプトを通じて高度なカスタマイズが可能です。研究者は、新しいレベル、タスク、報酬体系を自由に設計し、特定の研究仮説を検証することができます 10。特に、30の多様なタスクを含む「DMLab-30」スイートは、学習、記憶、ナビゲーションといった異なる能力を試し、共通の行動空間を持つことで、マルチタスク学習の研究を促進するために開発されました 29。

関連研究

このプラットフォームの要求する高い計算スループットとデータ効率に応えるため、IMPALA（Importance Weighted Actor-Learner Architecture）のようなスケーラブルな分散学習アーキテクチャが開発されました。IMPALAは、DMLab-30スイートでの訓練に必要な膨大なデータ処理を可能にするために設計されたものです 29。

Procgen Benchmark: 汎化能力のリトマス試験紙

ALEのような静的なベンチマークに対する最大の批判は、エージェントが特定のゲームセットに過剰適合してしまうリスクでした。Procgen Benchmarkは、この問題を正面から解決するために設計されました。その目的は、エージェントがどれだけ速く「汎用的な」スキルを学習するかを直接測定することにあります 7。

中核メカニズム：手続き的コンテンツ生成 (PCG)

Procgenの核心は、手続き的コンテンツ生成（PCG）を全面的に活用している点です。PCGを用いることで、ほぼ無限に近い数の、高度にランダム化されたレベルをアルゴリズム的に生成します 7。レベルのレイアウト、アセット、難易度といった重要な要素がエピソードごとにランダム化されるため、エージェントはこれまで一度も見たことのない状況に常に対応しなければなりません。これにより、訓練セットとテストセットを明確に分離することが可能となり、汎化能力を評価するための理想的なベンチマークとなっています 7。

環境スイート

このベンチマークは、CoinRun、StarPilot、Maze、Jumperなど、16種類のユニークなゲームライクな環境で構成されています 7。これらの環境は、計算コストが低く、使いやすいように設計されており、共通のGymインターフェースと15次元の離散行動空間を共有しています 7。

評価プロトコル

Procgenにおける性能評価は、単一のレベルでのスコアではなく、訓練中には遭遇しなかったレベルの分布全体に対する平均的な性能によって行われます。主要な評価指標は、多くの場合、16の環境すべてにわたる正規化された平均リターンです 7。
DeepMind LabとProcgenは、AIの評価を進める上で、2つの異なる、そして時には対立する哲学的アプローチを体現しています。DeepMind Labは、Quake IIIエンジンをベースにした「リッチなサイエンスフィクション風のビジュアル」と3D物理演算によって、環境の「複雑性」と「忠実度」を高めるアプローチを取ります 10。この設計の背後にある暗黙の仮説は、このようなリッチで現実的な感覚入力をマスターすることによって、より汎用的な知性が生まれるというものです。研究課題も、ナビゲーション、記憶、3Dビジョンといった、この複雑な世界内部での高度な認知タスクに焦点が当てられています 11。
一方、Procgenは、視覚的・物理的な忠実度を意図的に単純化し、代わりに「手続き的な多様性」という別の軸で複雑性を追求します 7。Procgenの複雑さは、単一のインスタンスの忠実度にあるのではなく、考えられるインスタンスの広大な分布にあります。その研究目標は、エージェントが多様な状況に適応する能力、すなわち「汎化」を直接ベンチマークすることです 7。
この対比は、ベンチマーク設計における戦略的な分岐を示しています。一方の道（DeepMind Lab）は「深さ」に賭けています。つまり、知性は高忠実度のシミュレーションを深くマスターすることから生まれるという考えです。もう一方の道（Procgen）は「広さ」に賭けています。つまり、知性は、より単純だが多様で未知の状況に適応する能力によって示されるという考えです。この「深さ」と「広さ」の二項対立は、現代のベンチマーク設計においても影響を与え続けている重要なテーマです。

III. 高忠実度シミュレーションと階層的挑戦

AI研究がさらに進むにつれて、ベンチマークは単なる抽象的な課題から、現実世界の問題をより忠実に反映する高忠実度のシミュレーションへと進化しました。この動きは、最新のゲームエンジンを活用するUnity ML-Agentsと、長期的かつ階層的な計画能力を問うMineRLによって代表されます。

Unity ML-Agents Toolkit: 研究とゲーム開発の架け橋

Unity ML-Agents Toolkitは、世界で最も人気のあるゲームエンジンの一つであるUnityで作成されたゲームやシミュレーションを、知的エージェントの訓練環境として利用可能にするオープンソースプロジェクトです 32。このツールキットは、ゲーム開発者とAI研究者の双方に利益をもたらすことを目的としています。開発者はより賢いNPCの作成やゲームビルドの自動テストに活用でき、研究者はUnityが提供するリッチで物理ベースの3D環境にアクセスできます 32。

アーキテクチャ

ML-Agentsは、5つの主要コンポーネントで構成されています 32。
学習環境 (Learning Environment): エージェントが活動するUnityシーンそのものです。
Python低レベルAPI: Unity環境と外部の学習アルゴリズムを接続するインターフェースです。
外部コミュニケーター: 学習環境とPython API間の通信を担います。
Pythonトレーナー: PPO（Proximal Policy Optimization）やSAC（Soft Actor-Critic）といった最先端の学習アルゴリズムの実装を含みます。
GymおよびPettingZooラッパー: 既存の強化学習フレームワークとの互換性を提供します。

能力と応用

ML-Agentsは、その柔軟なアーキテクチャにより、多様な訓練パラダイムをサポートします。単一エージェントの学習はもちろん、協調的・競合的なマルチエージェントシステムや、敵対的自己対戦（adversarial self-play）のような高度なシナリオも構築可能です 32。特に、Unityの高度な物理エンジンとフォトリアリスティックなレンダリング能力は、ロボット工学や自動運転車のシミュレーションにおいて強力なツールとなります 35。現実のロボットを訓練する前に、シミュレーション内で安全かつ効率的にモデルを開発する「sim-to-real」アプローチで広く活用されています。

セットアップと利用フロー

典型的な開発フローは、まずUnityエディタ内で環境（床、ターゲット、エージェントなど）を構築することから始まります 42。次に、C#で
Agentクラスを継承したスクリプトを作成し、観測の収集（CollectObservations）、行動の実行（OnActionReceived）、報酬の計算、エピソードのリセット（OnEpisodeBegin）といったロジックを実装します 42。訓練の準備が整ったら、コマンドラインから
mlagents-learnコマンドを実行し、Unityエディタの再生ボタンを押すことで学習が開始されます 43。訓練が完了すると、学習済みのニューラルネットワークモデルが
.onnxファイルとして出力され、これをUnityのSentis推論エンジンを用いてプロジェクトに組み込むことで、訓練されたエージェントをゲーム内で実行できます 34。

MineRL: 長期計画とサンプル効率学習のためのベンチマーク

MineRLは、サンドボックスゲーム「Minecraft」を舞台にした、AI研究における特異な挑戦を提供します。Minecraftは、単なるゲームを超えた、複雑で、視覚的に豊かで、階層的な技術ツリーを持つ3Dボクセル世界です 46。

Minecraftがもたらす挑戦

MineRLの中心的な課題であるObtainDiamondタスクは、AIエージェントにとって極めて困難です。このタスクを達成するためには、エージェントはまず木を伐採し、作業台を作り、木のツルハシ、石のツルハシ、鉄のツルハシを順にクラフトし、最終的にダイヤモンドを採掘するという、長く複雑な一連のサブタスクをこなさなければなりません 47。このプロセスは、報酬が非常にスパース（まばら）であり、長期的な計画能力が不可欠であるという、強化学習における2つの根源的な問題を浮き彫りにします 46。

中核となる研究焦点

この困難さから、MineRLコンペティションは、特に「サンプル効率の良い」強化学習アルゴリズムの開発を促進するために設計されました 47。標準的な強化学習アルゴリズムが人間レベルの性能に達するために数百年分のプレイ時間を要するのに対し、MineRLは、人間のデモンストレーションデータを「事前知識（human priors）」として活用することで、訓練に必要な環境とのインタラクション回数を劇的に削減することを目指しています 48。

MineRL-v0データセット

この研究目的を達成するための鍵となるのが、6000万フレームを超える人間のプレイデータを収録した大規模データセット「MineRL-v0」です 50。このデータセットの存在は、模倣学習や、模倣学習と強化学習を組み合わせたハイブリッドなアプローチの研究を強く奨励します 49。

技術的実装と関連研究

MineRLは、Minecraft（Java版）と対話するためのOpenAI Gym互換のPythonライブラリを提供します 50。この環境はMalmoプラットフォーム上に構築されており 52、複数のバージョンが存在します。新しいバージョン（v1.0.0以降）では、より新しいMinecraftバージョン（1.16.5）が使用され、自動クラフト機能がなくなるなど、より現実的な行動空間が採用されています 53。このプラットフォームは、マルチタスク・カリキュラム学習 46 や、コンペティションの優勝チームが開発した模倣学習と階層的強化学習を組み合わせた手法など、数多くの先進的な研究を生み出しています 47。

IV. 新しいパラダイム：推論エージェントとしての大規模言語モデルの評価

AIエージェントの研究は、近年、劇的なパラダイムシフトを経験しています。従来の強化学習エージェントが、主にピクセルのような低レベルの状態から低レベルの行動へのマッピングを学習していたのに対し、大規模言語モデル（LLM）を基盤とするエージェントは、より高い抽象度で動作します。この新しいエージェントは、テキストで与えられたルールを理解し、複数ステップの計画を立案し、自然言語や構造化された形式で戦略的な行動を生成する能力によって評価されます 56。

LLMエージェントのベンチマークにおける課題

既存のゲーム環境にLLMを直接適用することは、いくつかの根源的な課題により困難であることが判明しています。
脆弱な視覚認識: 最新の視覚言語モデル（VLM）でさえ、複雑なゲームのUIや動的なシーンを正確に解釈するのに苦労することがあります。視覚情報の微妙なニュアンスを理解する能力が、しばしばボトルネックとなります 56。
プロンプトへの感受性: LLMの性能は、その行動をガイドするために使用されるプロンプトの具体的な言葉遣いや構造に大きく依存します。これにより、異なるモデル間の公平な比較が困難になります 56。
データ汚染の可能性: 多くの人気ゲームには、攻略法、議論、画像など、広範なオンライン情報が存在します。LLMが訓練データとしてこれらの情報に触れていた場合、その性能は真の問題解決能力ではなく、記憶を反映しているに過ぎない可能性があります 56。
これらの問題により、LLMはしばしばランダムな行動を取るのと同程度の性能しか示せず、モデル間の能力差を正確に評価することが困難になっています 56。

最新のLLM中心ゲームベンチマークの概観

これらの課題に対応するため、LLMの能力をより正確に評価することを目的とした新しいベンチマークが次々と登場しています。
LMGAME-BENCH: 上記の問題点に対処し、より信頼性が高く洞察に満ちた評価方法を確立するために開発されたベンチマークです。LLMがゲームをどの程度「本当に」プレイできるかを評価するための、より安定したフレームワークを提供することを目指しています 56。
グリッドベースのゲーム競技会: 三目並べ、コネクトフォー、五目並べといった古典的なボードゲームを利用して、GPT-4o、Claude 3.5、Gemini 1.5 Proなどの最新LLMのルール理解能力と戦略的思考を評価する、拡張可能なベンチマークです 57。オープンソースのシミュレーションコードと公開リーダーボードが提供されており、研究者が自身のモデルをテストし、結果を共有することを奨励しています 60。
ゲームにおけるエージェント的推論（Balrog-AI, Snake-Bench）: これらのベンチマークは、テキストベースのアドベンチャーゲームや、動的な環境でエージェントを制御するタスクをLLMに課します。特に、長期的な視野に立った計画、記憶、そして意思決定能力を評価することに焦点を当てています 61。
調査とコレクション: この分野は急速に拡大しており、アドベンチャー、クラフト、シミュレーション、対戦ゲームなど、様々なジャンルにわたるLLMベースのエージェントを分類・整理する調査研究も登場しています 58。
LLMベースのゲームエージェントにおける中心的な課題は、もはや単にポリシーを学習することではなく、「解釈のギャップ（Interpreter Gap）」を埋めることにあります。このギャップとは、LLMの持つ高レベルな推論能力（自然言語や思考プロセスとして表現される）と、環境が要求する低レベルで具体的な行動空間との間の翻訳プロセスを指します。新しいベンチマークは、この解釈層の頑健性をテストするために、暗黙的または明示的に設計されています。
この解釈のプロセスは、LLMへのクエリと、それを補助する「スキャフォールディング・プログラム」の組み合わせとして定義できます 63。このスキャフォールディングこそが、LLMの出力を実行可能な行動に変換し、環境からの観測（例えば、視覚シーンのテキスト記述）をLLMが理解できる形式でフィードバックする「解釈器」の役割を果たします。LMGAME-BENCHで指摘された視覚の脆弱性やプロンプトへの感受性といった失敗点は、まさにこの解釈層の失敗です 56。視覚モデルがピクセルを正確にテキストに変換できなかったり、プロンプトがLLMの一般的な意図を次のステップに必要な正確な形式に変換できなかったりするのです。
VideoGameBenchのようなフレームワークは、異なるエミュレータ（ゲームボーイ、MS-DOS、ブラウザ）にまたがる標準化されたインターフェースを作成することで、この問題に明示的に取り組んでいます。これは、一種の汎用的な解釈層を提供する試みです 3。グリッドベースのゲームでLLMエージェントが成功を収めている一因は、この解釈のギャップが小さいことにあります。ゲームの状態はテキスト（グリッド）として曖昧さなく完璧に表現でき、行動もシンプルで離散的（座標にトークンを置く）だからです 57。したがって、この分野における次なる進歩は、より強力なLLMだけでなく、ノイズの多い知覚、複雑な行動空間、そして長期的な記憶管理を扱える、より洗練され頑健なスキャフォールディング、すなわち「解釈器」の開発にかかっていると言えるでしょう。そして、ベンチマークはまさにこの構成要素をストレステストするために進化しているのです。

V. 次なるフロンティア：インタラクティブな世界における身体性知能

AI研究の最前線は、ゲームを「勝つ」ことから、シミュレートされた現実世界で物理的に接地された複雑なタスクを遂行できるエージェントを訓練することへと移行しつつあります。これは、ゲームAIと身体性AI（Embodied AI）の融合領域であり、その最終的な目標は、現実世界のロボット工学へと直接つながる知能の創出です 64。

EmbodiedBench: MLLMのための包括的フレームワーク

EmbodiedBenchは、この新しいフロンティアにおける評価フレームワークのギャップを埋めるために設計された、包括的なベンチマークです。その目的は、マルチモーダル大規模言語モデル（MLLM）を用いた「視覚駆動型」の身体性エージェントを評価することにあります 65。

階層的タスク

このベンチマークは、4つの異なる環境にまたがる多様なタスクセットを特徴としています。これらのタスクは、アクションレベルの階層性という点で区別されます。
高レベルタスク: EB-ALFREDやEB-Habitatのような環境では、「本を机の上に置く」といった高レベルの指示に基づき、タスクを分解し計画する能力が試されます 65。
低レベルタスク: EB-NavigationやEB-Manipulationのような環境では、並進や回転といった低レベルの原子的な行動を計画する必要があり、エージェントには正確な知覚と空間推論能力が要求されます 65。

きめ細かい評価

EmbodiedBenchは、単一の成功指標を超え、身体性エージェントに不可欠な6つの重要な能力を評価するための、きめ細かいフレームワークを導入しています 65。
基本的なタスク解決能力
常識的推論
複雑な指示の理解
空間認識
視覚的知覚
長期的な計画能力
評価には、自己中心的な視覚認識、少数ショットの文脈例、インタラクション履歴を統合して意思決定を行う、統一されたエージェントパイプラインが使用されます 65。

その他の身体性ベンチマーク

EmbodiedBench以外にも、この分野の研究を推進する重要なベンチマークが存在します。
ALFRED (Action Learning From Realistic Environments and Directives): 自然言語の指示と自己中心的な視覚情報から、家庭内でのタスク（マグカップを温める、塩入れを棚にしまうなど）を達成するための一連の行動を学習するエージェントのための、よく知られたベンチマークです 64。
EmbodiedCity: 北京の実際の都市地区をベースにした、非常にリアルな3Dシミュレーション環境でエージェントを評価するプラットフォームです。歩行者や車両の流れを含む屋外環境でのナビゲーションやインタラクションに焦点を当てています 66。
これらのベンチマークは、シミュレーションと現実世界のギャップ（sim-to-real gap）を埋めるために、シーンやオブジェクトの多様性、そして基礎となるシミュレーション環境の現実性を重視して設計することの重要性を強調しています 64。

VI. 統合、推奨、そして今後の展望

本調査は、AI研究におけるゲームベンチマークの進化の軌跡を、単純で標準化された環境から、複雑でオープンエンドなマルチモーダル世界へと至る道筋として描き出してきました。この進化は、AIが解決すべき課題の性質の変化と、それを測定するための方法論の洗練を反映しています。

ベンチマーク哲学の比較分析

AIゲームベンチマークの歴史は、異なる設計哲学間のダイナミックな相互作用として理解することができます。初期のALEは、多様なタスクにおける「汎用的な性能」を測定するための標準化されたプラットフォームを提供することに焦点を当てました。これに対し、Procgenは、静的な環境への過剰適合という問題を解決するため、「汎化能力」を直接評価する手段として手続き的生成を導入しました。一方、DeepMind LabやUnity ML-Agentsは、「環境の忠実度と複雑性」を高めることで、より現実世界に近い課題を提示しました。Minecraftを舞台とするMineRLは、「長期計画」と「サンプル効率」という、特に困難な課題に焦点を当てています。そして最新のLLMベースおよび身体性AIのベンチマークは、高レベルの「推論」や「物理的インタラクション」を評価の対象としています。
これらの異なるアプローチは、AIの「知能」をどの側面から測定しようとしているのかという、根本的な問いに対する多様な答えを示しています。以下の表は、本調査で取り上げた主要なベンチマーク環境を、その中核的な研究焦点と技術的特徴に基づいて比較したものです。
表1：主要AIゲームベンチマーク環境の比較マトリクス
ベンチマーク
主要なゲーム/環境タイプ
中核となる研究焦点
エージェントのインターフェース/入力
主要な挑戦
代表的なプラットフォーム
ALE
2Dアーケード (Atari 2600)
ピクセルからの汎用エージェント性能
ピクセル (RGB/グレースケール), RAM
高次元入力, 反応時間
Stella Emulator, Gymnasium API
Gymnasium
多様 (制御, 物理, テキスト)
標準化されたRLアルゴリズム比較
状態ベクトル, ピクセル
基礎的なRL問題
Python, Box2D, MuJoCo
DeepMind Lab
3D一人称パズル/ナビゲーション
3Dビジョン, 記憶, ナビゲーション
一人称視点ピクセル
部分観測可能性, 長期記憶
Quake III Arena Engine
Procgen
2D手続き的生成ゲーム
汎化能力
ピクセル (RGB)
未知のレベルへの汎化
Custom C++ Environments, Gym API
Unity ML-Agents
高忠実度3Dシミュレーション
マルチエージェントシステム, ロボティクス, 複雑な物理
状態ベクトル, カメラ入力, レイキャスト
Sim-to-real, マルチエージェント協調
Unity Engine
MineRL
3Dボクセルサンドボックス (Minecraft)
サンプル効率, 階層的RL, 事前知識からの学習
一人称視点ピクセル, インベントリ状態
スパース報酬, 長期計画
Minecraft (Java), Malmo, Python API
LMGAME-BENCH
多様 (クラシック, モダン)
LLM/VLMゲームエージェントの頑健な評価
視覚フレーム, テキストプロンプト
視覚の脆弱性, プロンプト感受性
PyBoy, JS-DOS, Browser Emulation
EmbodiedBench
3Dリアルなシミュレーション (家庭, ロボティクス)
視覚駆動型の身体性知能
自己中心視点, テキストフィードバック
高/低レベル計画, sim-to-real
AI2-THOR, Habitat, Isaac Gym


ベンチマーク選択のための推奨事項

研究者や開発者が自身の目的に最適なベンチマークを選択できるよう、以下に具体的な指針を示します。
新しい強化学習アルゴリズムのデバッグや基礎的な検証には、 GymnasiumのClassic Control環境が最適です。低次元で解釈しやすいため、迅速なイテレーションが可能です。
手続き的に生成される多様な環境に対する汎化能力をテストするには、 Procgen Benchmarkを使用すべきです。これは、エージェントが未知の状況に適応する能力を直接測定するために設計されています。
人間のデモンストレーションデータを活用したサンプル効率の良い、長期的な計画能力を評価するには、 MineRLが唯一無二の選択肢です。その階層的なタスク構造は、複雑な問題解決能力を試す上で非常に価値があります。
LLMの戦略的推論能力を制御された環境で評価するには、 グリッドベースのゲーム競技会のようなベンチマークが有効です。これにより、視覚認識の複雑さを排除し、純粋な論理・戦略能力を分離して評価できます。
ロボット工学への応用を視野に入れた、視覚駆動型の身体性エージェントをテストするには、 EmbodiedBenchが最も包括的なフレームワークを提供します。高レベルのセマンティックなタスクから低レベルの操作まで、幅広い能力をきめ細かく評価できます。

AIゲームベンチマークの未来

AIの能力が進化し続けるにつれて、それを評価するベンチマークもまた進化し続けなければなりません。

批判と未解決問題

現在のベンチマーク手法には依然として限界が存在します。指標を「ハック」する、すなわち真の能力向上を伴わずにスコアだけを最適化してしまうリスクは常に存在します 2。また、LLMの時代においては、訓練データにベンチマークの解法が含まれてしまう「データ汚染」が深刻な懸念となっています 2。さらに、ベンチマークスコアと現実世界での有用性との間には依然としてギャップがあり 2、ベンチマーク自体の透明性、公平性、説明可能性を確保する必要性が高まっています 1。

新たなトレンド

今後のベンチマークは、よりオープンエンドで、マルチモーダルで、社会的に複雑な環境へと向かうでしょう。これには、複数のエージェントが協調したり、コミュニケーションをとったりする能力を評価するベンチマーク 62 や、人間の社会行動をモデル化する生成エージェントのシミュレーション 70 が含まれます。これらの新しい評価軸は、AIが技術的なタスクをこなすだけでなく、人間社会の中で効果的に機能するために必要な能力を測定することを目指しています。

結論

ベンチマークは、AIエコシステムにおける根源的で、動的で、そして非常に影響力のある構成要素です。それらは研究の方向性を定め、進歩を測定し、次なる挑戦を定義します。本調査が明らかにしたように、ピクセルを認識することから複雑な計画を立てることまで、ベンチマークの進化はAI自身の進化の物語を映し出してきました。より有能で、汎用的で、安全なAIの開発を導くために、ベンチマークの継続的な進化は今後も不可欠であり続けるでしょう。
引用文献
Can We Trust AI Benchmarks? An Interdisciplinary Review of Current Issues in AI Evaluation, 7月 28, 2025にアクセス、 https://arxiv.org/html/2502.06559v1
The Race to Measure Machine Minds: Understanding AI Benchmarks - Sandgarden, 7月 28, 2025にアクセス、 https://www.sandgarden.com/learn/benchmarks
From Atari to AGI: Why Video Games Challenge Our Smartest AI Models | by Greg Robison, 7月 28, 2025にアクセス、 https://gregrobison.medium.com/from-atari-to-agi-why-video-games-challenge-our-smartest-ai-models-aabcd48a3faa
Game Playing in Artificial Intelligence - GeeksforGeeks, 7月 28, 2025にアクセス、 https://www.geeksforgeeks.org/artificial-intelligence/game-playing-in-artificial-intelligence/
Exploration of Game Artificial Intelligence: Key Technologies and Case Analysis - SciTePress, 7月 28, 2025にアクセス、 https://www.scitepress.org/Papers/2024/135175/135175.pdf
Mastering Game Playing in AI - Number Analytics, 7月 28, 2025にアクセス、 https://www.numberanalytics.com/blog/mastering-game-playing-in-ai
Leveraging Procedural Generation to Benchmark ... - OpenAI, 7月 28, 2025にアクセス、 https://cdn.openai.com/procgen.pdf
Measuring Sample Efficiency and Generalization in Reinforcement Learning Benchmarks: NeurIPS 2020 Procgen Benchmark - Proceedings of Machine Learning Research, 7月 28, 2025にアクセス、 http://proceedings.mlr.press/v133/mohanty21a/mohanty21a.pdf
ProcGen Dataset | Papers With Code, 7月 28, 2025にアクセス、 https://paperswithcode.com/dataset/procgen
google-deepmind/lab: A customisable 3D platform for agent ... - GitHub, 7月 28, 2025にアクセス、 https://github.com/google-deepmind/lab
Open-sourcing DeepMind Lab - Google DeepMind, 7月 28, 2025にアクセス、 https://deepmind.google/discover/blog/open-sourcing-deepmind-lab/
The Arcade Learning Environment (ALE) -- a platform for AI research. - GitHub, 7月 28, 2025にアクセス、 https://github.com/Farama-Foundation/Arcade-Learning-Environment
The Arcade Learning Environment: An Evaluation Platform for ..., 7月 28, 2025にアクセス、 https://arxiv.org/abs/1207.4708
Atari-5: Distilling the Arcade Learning Environment down to Five Games - OpenReview, 7月 28, 2025にアクセス、 https://openreview.net/pdf?id=xRDHjO0YBo
Environments - ALE Documentation, 7月 28, 2025にアクセス、 https://ale.farama.org/environments/
openai/gym: A toolkit for developing and comparing reinforcement learning algorithms. - GitHub, 7月 28, 2025にアクセス、 https://github.com/openai/gym
Farama-Foundation/Gymnasium: An API standard for single ... - GitHub, 7月 28, 2025にアクセス、 https://github.com/Farama-Foundation/Gymnasium
Gym Documentation, 7月 28, 2025にアクセス、 https://gymlibrary.ml/
Gym Documentation, 7月 28, 2025にアクセス、 https://www.gymlibrary.dev/
Getting Started With OpenAI Gym: The Basic Building Blocks ..., 7月 28, 2025にアクセス、 https://www.digitalocean.com/community/tutorials/getting-started-with-openai-gym
Getting Started with OpenAI's Gym for Reinforcement Learning | by Amnah Ebrahim, 7月 28, 2025にアクセス、 https://medium.com/@amnahhmohammed/getting-started-with-openais-gym-for-reinforcement-learning-e0aa2914874d
A Gentle Introduction to OpenAI Gym | intro_to_gym – Weights & Biases - Wandb, 7月 28, 2025にアクセス、 https://wandb.ai/mukilan/intro_to_gym/reports/A-Gentle-Introduction-to-OpenAI-Gym--VmlldzozMjg5MTA3
The Best Tools for Reinforcement Learning in Python You Actually Want to Try - Neptune.ai, 7月 28, 2025にアクセス、 https://neptune.ai/blog/the-best-tools-for-reinforcement-learning-in-python
Tutorials - Gym Documentation, 7月 28, 2025にアクセス、 https://www.gymlibrary.dev/content/tutorials/
16 Reinforcement Learning Environments and Platforms You Did Not Know Exist - MLK, 7月 28, 2025にアクセス、 https://machinelearningknowledge.ai/reinforcement-learning-environments-platforms-you-did-not-know-exist/
List of Reinforcement Learning Environments | by Mauricio Fadel Argerich | Medium, 7月 28, 2025にアクセス、 https://medium.com/@mauriciofadelargerich/reinforcement-learning-environments-cff767bc241f
clvrai/awesome-rl-envs - GitHub, 7月 28, 2025にアクセス、 https://github.com/clvrai/awesome-rl-envs
Gymnasium/docs/environments/third_party_environments.md at main - GitHub, 7月 28, 2025にアクセス、 https://github.com/Farama-Foundation/Gymnasium/blob/main/docs/environments/third_party_environments.md
Scalable agent architecture for distributed training - Google DeepMind, 7月 28, 2025にアクセス、 https://deepmind.google/discover/blog/scalable-agent-architecture-for-distributed-training/
lab/docs/developers/minimal_level_tutorial.md at master · google-deepmind/lab - GitHub, 7月 28, 2025にアクセス、 https://github.com/deepmind/lab/blob/master/docs/developers/minimal_level_tutorial.md
Procgen — DI-engine 0.1.0 documentation, 7月 28, 2025にアクセス、 https://opendilab.github.io/DI-engine/13_envs/procgen.html
ML-Agents Toolkit Overview - GitHub Pages, 7月 28, 2025にアクセス、 https://unity-technologies.github.io/ml-agents/ML-Agents-Overview/
Unity-Technologies/ml-agents: The Unity Machine Learning Agents Toolkit (ML-Agents) is an open-source project that enables games and simulations to serve as environments for training intelligent agents using deep reinforcement learning and imitation learning. - GitHub, 7月 28, 2025にアクセス、 https://github.com/Unity-Technologies/ml-agents
ML Agents | 3.0.0 - Unity - Manual, 7月 28, 2025にアクセス、 https://docs.unity3d.com/Packages/com.unity.ml-agents@3.0/manual/index.html
Unity Technologies Unveils Machine Learning Agents; Turns Unity Creation Engine Into Artificial Intelligence Powerhouse, 7月 28, 2025にアクセス、 https://unity.com/news/unity-technologies-unveils-machine-learning-agents-turns-unity-creation-engine
[2503.05146] Unity RL Playground: A Versatile Reinforcement Learning Framework for Mobile Robots - arXiv, 7月 28, 2025にアクセス、 https://arxiv.org/abs/2503.05146
[1809.02627] Unity: A General Platform for Intelligent Agents - arXiv, 7月 28, 2025にアクセス、 https://arxiv.org/abs/1809.02627
Made with Unity: Soccer robots with ML-Agents, 7月 28, 2025にアクセス、 https://unity.com/blog/games/made-with-unity-soccer-robots-with-ml-agents
Simulated Autonomous Driving Using Reinforcement Learning: A Comparative Study on Unity's ML-Agents Framework - ResearchGate, 7月 28, 2025にアクセス、 https://www.researchgate.net/publication/370795300_Simulated_Autonomous_Driving_Using_Reinforcement_Learning_A_Comparative_Study_on_Unity's_ML-Agents_Framework
Reinforcement Learning for Obstacle Avoidance Application in Unity Ml-Agents - CEUR-WS.org, 7月 28, 2025にアクセス、 https://ceur-ws.org/Vol-3575/Paper23.pdf
Reinforcement Learning of Robot Behavior based on a Digital Twin - SciTePress, 7月 28, 2025にアクセス、 https://www.scitepress.org/Papers/2020/88809/88809.pdf
Making a New Learning Environment - Unity ML-Agents Toolkit, 7月 28, 2025にアクセス、 https://unity-technologies.github.io/ml-agents/Learning-Environment-Create-New/
ML-agents/docs/Basic-Guide.md at master - GitHub, 7月 28, 2025にアクセス、 https://github.com/gzrjzcx/ML-agents/blob/master/docs/Basic-Guide.md
Getting Started Guide - Unity ML-Agents Toolkit - GitHub Pages, 7月 28, 2025にアクセス、 https://unity-technologies.github.io/ml-agents/Getting-Started/
How To Setup The Unity ML-Agents ToolKit (on Mac), 7月 28, 2025にアクセス、 https://www.erikaagostinelli.com/post/how-to-setup-the-unity-ml-agents-toolkit-on-mac
Multi-task curriculum learning in a complex, visual, hard-exploration domain: Minecraft - arXiv, 7月 28, 2025にアクセス、 https://arxiv.org/pdf/2106.14876
Retrospective Analysis of the 2019 MineRL Competition on Sample Efficient Reinforcement Learning, 7月 28, 2025にアクセス、 http://proceedings.mlr.press/v123/milani20a/milani20a.pdf
arXiv:2111.08857v1 [cs.LG] 17 Nov 2021, 7月 28, 2025にアクセス、 https://arxiv.org/pdf/2111.08857
(PDF) The MineRL Competition on Sample Efficient Reinforcement Learning using Human Priors - ResearchGate, 7月 28, 2025にアクセス、 https://www.researchgate.net/publication/332603991_The_MineRL_Competition_on_Sample_Efficient_Reinforcement_Learning_using_Human_Priors
MineRL: Towards AI in Minecraft — MineRL 0.4.0 documentation, 7月 28, 2025にアクセス、 https://minerl.readthedocs.io/
[R] NeurIPS 2019: The MineRL Competition for Sample-Efficient Reinforcement Learning : r/MachineLearning - Reddit, 7月 28, 2025にアクセス、 https://www.reddit.com/r/MachineLearning/comments/bngj3n/r_neurips_2019_the_minerl_competition_for/
arXiv:2005.03374v1 [cs.AI] 7 May 2020, 7月 28, 2025にアクセス、 https://arxiv.org/pdf/2005.03374
MineRL Versions — MineRL 0.4.0 documentation, 7月 28, 2025にアクセス、 https://minerl.readthedocs.io/en/latest/notes/versions.html
[2106.14876] Multi-task curriculum learning in a complex, visual, hard-exploration domain: Minecraft - arXiv, 7月 28, 2025にアクセス、 https://arxiv.org/abs/2106.14876
Links to papers and projects - MineRL - Read the Docs, 7月 28, 2025にアクセス、 https://minerl.readthedocs.io/en/latest/notes/useful-links.html
How Good Are Large Language Models At Playing Games ..., 7月 28, 2025にアクセス、 https://dataconomy.com/2025/05/28/how-good-are-large-language-models-at-playing-games/
(PDF) Evaluating Large Language Models with Grid-Based Game Competitions: An Extensible LLM Benchmark and Leaderboard - ResearchGate, 7月 28, 2025にアクセス、 https://www.researchgate.net/publication/382144980_Evaluating_Large_Language_Models_with_Grid-Based_Game_Competitions_An_Extensible_LLM_Benchmark_and_Leaderboard
\benchmarkname : A Benchmark for LLMs as Intelligent Agents - arXiv, 7月 28, 2025にアクセス、 https://arxiv.org/html/2310.01557v5
GameBench: Evaluating Strategic Reasoning Abilities of LLM Agents | OpenReview, 7月 28, 2025にアクセス、 https://openreview.net/forum?id=VVDewLcVkx
research-outcome/LLM-Game-Benchmark: Evaluating Large Language Models with Grid-Based Game Competitions: An Extensible LLM Benchmark and Leaderboard - GitHub, 7月 28, 2025にアクセス、 https://github.com/research-outcome/LLM-Game-Benchmark
40 Large Language Model Benchmarks and The Future of Model Evaluation - Arize AI, 7月 28, 2025にアクセス、 https://arize.com/blog/llm-benchmarks-mmlu-codexglue-gsm8k
A Survey on Large Language Model-Based Game Agents - GitHub, 7月 28, 2025にアクセス、 https://github.com/git-disl/awesome-LLM-game-agent-papers
Survey of Multi-agent LLM Evaluations - LessWrong, 7月 28, 2025にアクセス、 https://www.lesswrong.com/posts/tGcLA596E8g3KnphE/survey-of-multi-agent-llm-evaluations
A collection of benchmarks for emboided robotic agent based on LLMs - Medium, 7月 28, 2025にアクセス、 https://medium.com/@yananchen1116/a-collection-of-benchmarks-for-emboided-robotic-agent-based-on-llms-40482ecef189
EmbodiedBench: Comprehensive Benchmarking Multi-modal Large Language Models for Vision-Driven Embodied Agents - arXiv, 7月 28, 2025にアクセス、 https://arxiv.org/html/2502.09560v1
EmbodiedCity: A Benchmark Platform for Embodied Agent in Real-world City Environment, 7月 28, 2025にアクセス、 https://openreview.net/forum?id=y15LAM4u0A
EmbodiedBench: Comprehensive Benchmarking Multi-modal Large ..., 7月 28, 2025にアクセス、 https://embodiedbench.github.io/
I'm starting to think ai benchmarks are useless : r/LocalLLaMA - Reddit, 7月 28, 2025にアクセス、 https://www.reddit.com/r/LocalLLaMA/comments/1i4vwm7/im_starting_to_think_ai_benchmarks_are_useless/
What Makes a Good AI Benchmark? | Stanford HAI, 7月 28, 2025にアクセス、 https://hai.stanford.edu/what-makes-good-ai-benchmark
Simulating Human Behavior with AI Agents | Stanford HAI, 7月 28, 2025にアクセス、 https://hai.stanford.edu/policy/simulating-human-behavior-with-ai-agents
(PDF) Generative Agent Simulations of 1,000 People (2024) | Joon Sung Park - SciSpace, 7月 28, 2025にアクセス、 https://scispace.com/papers/generative-agent-simulations-of-1000-people-31sj9byjex26
LLMs: the new frontier in generative agent-based simulation | AWS HPC Blog, 7月 28, 2025にアクセス、 https://aws.amazon.com/blogs/hpc/llms-the-new-frontier-in-generative-agent-based-simulation/
