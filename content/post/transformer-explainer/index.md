---
title: "Transformer Explainer"
description: "テキスト生成モデルのTransformer内部で、トークンや注意機構がどう働くかを対話的に学べる可視化ツール。"
slug: "transformer-explainer"
date: 2026-02-01
weight: 1
categories: "ai-model"
address: 
image: "images/cover.png"
---

Transformer Explainerは、テキスト生成モデルの内部処理を、トークン単位で追いながら学べるインタラクティブな可視化ツールです。入力テキストがトークン化され、埋め込み、位置情報、注意機構、フィードフォワード層を通って次のトークン予測につながる流れを確認できます。

自己注意の重みや中間表現を見ながら、Transformerが文脈をどのように参照しているのかを観察できる構成です。大規模言語モデルの基礎となるTransformerの仕組みを、数式や実装だけでなく、実際のテキスト生成の流れとして理解するための教材として使いやすいツールです。

## この記事で学べること

- GPT-2のようなテキスト生成モデルが、入力文から次の単語をどのように予測しているかの全体像
- Self-Attentionが、単語同士の「どれがどれに注目しているか」をQuery・Key・Valueという3つのベクトルからどう計算しているか
- Temperature(温度パラメータ)を変えると、モデルの出力が「予測可能」と「多様」のあいだでどう変化するか

## 操作ガイド

画面上部の入力欄と右上のTemperatureスライダーを動かしながら、左から右へ処理の流れを追ってみましょう。

1. **入力文を変える**: 上部の入力欄に好きな英文を入力するか、「例」ドロップダウンから例文を選び、「生成する」をクリックします。実際にブラウザ上で動くGPT-2(small)モデルが、その続きの単語を計算し直します。
2. **Embedding(左端)**: 入力文の各単語が、意味を表す数値ベクトルに変換される様子を確認します。
3. **Multi-head Self Attention**: 各単語がQuery・Key・Valueという3種類のベクトルに変換され、円が並んだAttention行列によって「どの単語がどの単語をどれくらい参照しているか」が計算されます。「Head n of 12」という表示は、12個ある注意ヘッドのうち1つを見ていることを示しており、それぞれのヘッドが異なる観点で単語間の関係を捉えています。
4. **MLPと残差接続(Residual)**: Attentionの出力はMLP(多層パーセプトロン)層と残差接続を経て、次のTransformer Blockに渡されます。
5. **12個のTransformer Blockが積み重なる**: 同じ構造のブロックが「11 more identical Transformer Blocks」として合計12回繰り返され、単語間の関係がより高次に処理されていきます。
6. **Probabilities(右端)**: モデルが予測する「次に来る単語」の候補が、確率の高い順にバーで表示されます。
7. **Temperatureスライダーを動かす**: 値を上げてから再度「生成する」を押すと、確率分布が均され、意外な単語も選ばれやすくなります。逆に下げると、最も確率の高い単語に予測が集中します。

## 理論的背景

Transformerアーキテクチャそのものは、2017年にVaswaniらが発表した論文「Attention Is All You Need」で提案されました。このExplainerが可視化しているのは、OpenAIが2019年に公開したGPT-2(smallモデル、約1.24億パラメータ)です。

このツール自体は、CNN ExplainerやGAN Labと同じジョージア工科大学のPolo Clubが2024年に発表した論文「Transformer Explainer: Interactive Learning of Text-Generative Models」(IEEE VIS 2024)として公開されました。Temperatureは、モデルが出力するスコアを確率分布に変換するsoftmax関数の温度パラメータで、値を上げるほど分布がフラットになり、下げるほど最大確率のトークンに出力が集中します。

## まとめ

- Transformerは、Self-Attentionで単語同士の関連度を計算し、それをMLPで変換する処理を何層も繰り返して次の単語を予測している
- 12個ある注意ヘッドは、それぞれ異なる観点で単語間の関係を捉えている
- Temperatureを調整すると、モデル出力の「予測可能性」と「多様性」のトレードオフを直接体感できる

{{< external-link-card
    url="https://transformer-explainer.explorable-explanations.com/"
    title="Transformer Explainer"
    image="images/cover.png"
    site="transformer-explainer.explorable-explanations.com"
    description="Transformerのトークン化、注意機構、中間表現、次トークン予測を対話的に追える可視化ツール。"
>}}
{{< /external-link-card >}}
