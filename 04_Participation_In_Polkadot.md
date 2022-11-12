4. Participation in Polkadot

Polkadotネットワークの維持には、コレーター、フィッシャーマン、ノミネーター、バリデーターという4つの基本的な役割が存在する。Polkadot のある実装では、後者の役割は、実際には、基本的な検証者と利用可能性の保証者の 2 つの役割に分解されるかもしれない; これについては 6.5.3 節で説明する。

4.1. Validators.

バリデータは最高額で、Polkadotネットワーク上の新しいブロックの封印を支援する。バリデータの役割は、十分に高い債券が預け入れられることを条件とするが、他の被保証者が1人以上の バリデータを指名して代理させることができるため、バリデータの債券の一部は必ずしもバリ データ自身ではなく、これらの指名者によって所有される可能性がある。

バリデータは、高い可用性とバンド幅を持つリレーチェーンクライアントの実装を 実行しなければならない。各ブロックにおいて、ノミニー・パラチェーン上の新しいブロックを批准する 役割を引き受けられる状態でなければならない。このプロセスには、候補ブロックの受信、検証、再パブリッシュが含まれます。ノミネートは決定論的であるが、事実上、ずっと前から予測できない。バリデータはすべてのパラチェーンの完全な同期データベースを維持することは不可能なので、 バリデータは新しいパラチェーンのブロック案を作成する作業を、 コレーターと呼ばれる第三者に委ねることが予想される。

新しいパラチェーンブロックがすべて指定されたバリデータ部会で適切に批准されると、 バリデータはリレーチェーンブロックそのものを批准しなければならない。これには、トランザクションキューの状態を更新し(基本的にデータをパラチェーンの出力キューから別のパラチェーンの入力キューに移動する)、批准済みのリレーチェーン トランザクションセットのトランザクションを処理し、最後のパラチェーンの変更を含む最終ブロックを批准することが含まれる。

我々が選んだコンセンサスアルゴリズムのルールのもとで合意を見出す義務を果たさないバリデ ータは罰せられる。最初の、意図的でない失敗に対しては、バリデータの報酬を差し控える。失敗が繰り返されると、セキュリティボンドが削減される（バーニング）。二重署名や無効なブロックを提供するための共謀など、証明可能な悪意ある行為は、 保証金全体を失うことになる(保証金は一部焼却されるが、大部分は情報提供者と誠実な行為者に 渡される)。ある意味でバリデーターは、現在のPoWブロックチェーンのマイニングプールに似ている。

4.2. Nominators.

ノミネータとは、バリデータのセキュリティボンドに出資する利害関係者である。彼らは、リスクキャピタルを預け、特定のバリデータ(またはその集合)がネットワークの維持に 責任を持って行動することを信頼していることを示す以外には、何の役割も持たない。バリデータは、債券の成長に応じて、預託金の比例配分による増減を受ける。

次に、ノミネーターは、コレーターとともに、ある意味で現在のPoWネットワークにおける採掘者と似ている。

4.3. Collators.

トランザクションコレーター（略してコレーター）は、有効なパラチェーンブロックを生成するバリデーターを支援する当事者である。つまり、現在のPoWブロックチェーンで採掘者が行うのと同じように、新しいブロックを作成し、取引を実行するために必要なすべての情報を保持しているのです。通常の場合、彼らは取引を照合・実行して封印されていないブロックを作成し、それをゼロ知識証明とともに、現在パラチェーンブロックを提案する責任を負う1人以上のバリデーターに提供することになる。

コレーター、ノミネーター、バリデーターの関係の正確な性質は、おそらく時間の経過とともに変化する。当初は、取引量の少ないパラチェーンが少数（おそらく1つ）しか存在しないため、照合人と検証人が非常に緊密に連携することが予想される。初期のクライアント実装には、パラチェーンコレーターノードが（リレーチェーン）バリデータノードに証明可能な有効なパラチェーンブロックを無条件で提供するためのRPCが含まれる予定です。このようなすべてのパラチェーンの同期バージョンを維持するコストが増加するにつれて、経済的に動機づけられた独立したパーティに義務を分離するのに役立つ追加のインフラが設置されることを期待しています。

最終的には、取引手数料を最も多く徴収するために競い合うコレーター・プールが現れると予想されます。このような照合人は、特定のバリデータに一定期間サービスを提供する契約を結び、継続的に報酬を受け取ることができる。あるいは、「フリーランス」の照合人は、有効なパラチェーンブロックを提供する市場を創設し、 その見返りとして直ちに支払われる報酬を競争的に分け合うこともできる。同様に、分散型ノミネーター・プールを利用すれば、複数の絆で結ばれた参加者がバリデーターの任務を調整し、分担することができる。このプール機能により、より分散化されたシステムへとつながるオープンな参加が保証される。

4.4. Fishermen.

fishermanは、他の二人の活動家と違って、ブロックオーサリングのプロセスとは直接関係がない。むしろ彼らは、一回限りの大きな報酬に動機づけされた独立した「賞金稼ぎ」なのです。まさにfishermanの存在のために、我々は、不品行がめったに起こらないこと、そして起こったとしても、悪意によるものではなく、ボンドパーティが秘密鍵のセキュリティに不注意であることによるものであることを期待しているのである。名前の由来は、期待される報酬の頻度、参加するための最小限の条件、最終的な報酬の大きさである。

漁師は、少なくとも1人の被保証者が違法行為を行ったことを適時に証明することで、報酬を得ることができる。違法行為とは、同じ批准親を持つ2つのブロックにそれぞれ署名することや、パラチェーンの場合、無効なブロックの批准を手助けすることなどが含まれる。過剰な報酬や、セッションの秘密鍵の漏洩と不正使用を防ぐため、1人のバリデータ が不正に署名したメッセージを提供した場合の基本報酬は最小である。この報酬は、他のバリデータから本物の攻撃を示唆する不正な署名が提供されるほど、 漸近的に増加する。バリデータの少なくとも3分の2が善意で行動しているという、我々の基本的なセキュリティの主張に従って、漸近線は66%に設定される。

フィッシャーマンは、現在のブロックチェーンシステムにおける「フルノード」に類似しており、必要なリソースが比較的小さく、安定した稼働時間や帯域幅を約束する必要はない。フィッシャーマンは、少額の保証金を支払う必要がある点が異なります。このボンドは、バリデータの時間と計算資源を浪費させるシビル攻撃を防ぐ。この保証金はすぐに引き出すことができ、おそらく数ドル程度であろうが、悪さをするバリデータを発見することで、高額な報酬を得ることができるかもしれない。
