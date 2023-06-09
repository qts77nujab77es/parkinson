# Parkinson

## Goal of the competition
本大会は、パーキンソン病患者さんの進行度を測るMDS-UPDRスコアを予測することを目的としています。Movement Disorder Society-Sponsored Revision of the Unified Parkinson's Disease Rating Scale（MDS-UPDRS）は、パーキンソン病に関連する運動症状と非運動症状の両方を総合的に評価するものである。あなたは、パーキンソン病の被験者と年齢をマッチさせた正常な対照被験者のタンパク質およびペプチドレベルの経時的なデータから学習させたモデルを開発します。

あなたの研究は、パーキンソン病の進行に伴って変化する分子について、重要なブレークスルー情報を提供することにつながるでしょう。

## Context
パーキンソン病（PD）は、運動、認知、睡眠、その他の正常な機能に影響を及ぼす脳疾患です。残念ながら、現在のところ治療法はなく、時間の経過とともに病状は悪化していきます。2037年までに、米国では160万人がパーキンソン病に罹患し、その経済的コストは800億ドルにのぼると推定されています。この病気の発症や悪化には、タンパク質やペプチドの異常が重要な役割を果たすことが研究により明らかになっています。このことをデータサイエンスによってより深く理解することは、パーキンソン病の進行を遅らせたり、治癒させるための新しい薬物療法を開発するための重要な手がかりになると考えられます。

現在の取り組みでは、1万人以上の被験者の複雑な臨床・神経生物学的データを取得し、研究コミュニティと広く共有しています。このデータを用いて多くの重要な知見が発表されていますが、明確なバイオマーカーや治療薬はまだ見つかっていません。

コンペティションの主催者であるAccelerating Medicines Partnership® Parkinson's Disease（AMP®PD）は、政府、企業、非営利団体による官民パートナーシップで、National Institutes of Health（FNIH）財団を通じて運営されています。このパートナーシップは、パーキンソン病の診断、予後、および/または疾患進行のバイオマーカーを特定し、検証することを目的として、パーキンソン病患者の深い分子特性評価と長期的な臨床プロファイリングを含むAMP PDナレッジプラットフォームを作成しました。

あなたの研究が、パーキンソン病の治療法の探索に役立ち、この病気の患者さんの苦しみや医療費を軽減することができます。

## Dataset Description
このコンペティションの目的は、タンパク質の存在量データを用いてパーキンソン病（PD）の経過を予測することです。PDに関与するタンパク質の完全なセットは、まだ未解決の研究課題であり、予測価値を持つタンパク質は、さらに調査する価値があると思われます。このデータセットの中核は、数百人の患者から採取した脳脊髄液（CSF）サンプルの質量分析から得られたタンパク質存在量値である。各患者は、PDの重症度評価と同時に、複数年にわたり複数のサンプルを提供しました。

テストセットのデータを受け取り、Kaggleの時系列APIを使用して予測を行う、時系列コードコンペティションです。

## Files
### train_peptides.csv 
ペプチドレベルの質量分析データです。ペプチドはタンパク質の構成サブユニットである。

- visit_id - 訪問のIDコード。
- visit_month - 患者による初診からの相対的な来院月。
- patient_id - 患者のIDコード。
- UniProt - 関連するタンパク質のUniProt IDコード。1つのタンパク質に複数のペプチドが存在することが多い。
- Peptide - ペプチドに含まれるアミノ酸の配列。関連するコードについては、この表を参照してください。稀なアノテーションは、この表に含まれない場合もある。テストセットには、トレーニングセットに含まれていないペプチドが含まれることがあります。
- PeptideAbundance - サンプルに含まれるアミノ酸の頻度です。

### train_proteins.csv ペプチドレベルのデータから集約したタンパク質発現頻度。
- visit_id - 訪問のIDコード。
- visit_month - 患者の初診からの相対的な来院月。
- patient_id - 患者のIDコード。
- UniProt - 関連するタンパク質のUniProt IDコード。1つのタンパク質につき数個のペプチドが存在することが多い。テストセットには，トレーニングセットに含まれていないタンパク質が含まれる場合がある。
- NPX - Normalized protein expression（正規化タンパク質発現量）。サンプルに含まれるタンパク質の出現頻度。ペプチドを繰り返し含むタンパク質もあるため、構成ペプチドと1対1の関係にはない可能性があります。

### train_clinical_data.csv
- visit_id - 訪問のIDコード。
- visit_month - 患者の最初の訪問から相対的に見た、訪問の月。
- patient_id - 患者のIDコード。
- updrs_[1-4] - 統一パーキンソン病評価尺度のパートNに対する患者のスコア。数値が高いほど症状が重いことを示す。パート1では気分や行動、パート3では運動機能など、各サブセクションは症状の異なるカテゴリーをカバーしています。
- upd23b_clinical_state_on_medication - UPDRS評価時にレボドパなどの薬物を服用していたかどうか。主にパート3（運動機能）のスコアに影響を及ぼすと予想される。これらの薬はかなり早く（1日単位で）切れるので、患者は1ヶ月に2回、薬の服用と未服用の両方で運動機能検査を受けることが一般的です。

### supplemental_clinical_data.csv 
CSF サンプルが添付されていない臨床記録。このデータは、パーキンソン病の典型的な進行に関する追加的な文脈を提供することを意図している。train_clinical_data.csvと同じカラムを使用する。

### example_test_files/ 
APIがどのように機能するかを説明するためのデータ。APIが提供するカラムと同じカラムが含まれる（つまり、updrsカラムはない）。

### amp_pd_peptide/ 
APIを有効にするためのファイルです。APIが5分以内にすべてのデータ（1,000人未満の追加患者）を配信し、0.5GB未満のメモリを確保することを期待する。APIが提供するデータの簡単なデモは、こちらでご覧いただけます。

### public_timeseries_testing_util.py 
カスタムオフラインAPIテストの実行を容易にすることを目的としたオプションファイルです。詳細はスクリプトのdocstringを参照してください。