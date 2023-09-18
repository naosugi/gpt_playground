# gpt_playground
https://digital-gov.note.jp/n/nc24c2f70feda のデモアプリを改修したもの

ChatGPTのAPIをcallするいわゆるplayground環境

## 参照用Github Pagesのリンク

- [プレーン](https://naosugi.github.io/gpt_playground/main.html)
- [日本語の校正](https://naosugi.github.io/gpt_playground/example/%E6%97%A5%E6%9C%AC%E8%AA%9E%E3%81%AE%E6%A0%A1%E6%AD%A3.html)
- [補助金・助成金・支援金の情報ラベル付け](https://naosugi.github.io/gpt_playground/example/補助金・助成金・支援金の情報ラベル付け.html)
- [確定申告が必要か判定](https://naosugi.github.io/gpt_playground/example/%E7%A2%BA%E5%AE%9A%E7%94%B3%E5%91%8A%E3%81%8C%E5%BF%85%E8%A6%81%E3%81%8B%E5%88%A4%E5%AE%9A.html)
- [キャラなりきり](https://naosugi.github.io/gpt_playground/example/LLMintoLUM.html)
- [SQL作成補助](https://naosugi.github.io/gpt_playground/example/WriteSQL.html)



## 改修点
1. OpenAI のAPIに対応
2. gpt3.5のコストを最新化
3. HTML保存機能を追加

# License
MIT License (/exampleを除く)

# 使い方

1. OpenAIのAPIキーを入手する

https://openai.com/product


2. APIキーをapi keyと書かれているテキストボックスに入力する

3. プロンプトを書き換える

参考 [ChatGPTを業務に組み込むためのハンズオン](https://www.digital.go.jp/assets/contents/node/information/field_ref_resources/5896883b-cc5a-4c5a-b610-eb32b0f4c175/82ccd074/20230725_resources_ai_outline.pdf)

注: assitant response となっている箇所は、事前に何か書いてあればassistant promptとしてGPTの入力となり、何も書いてなければGPTの出力がはいる

4. 「GPTに聞く」ボタンを押す

5. 画面下方のuser promptに入力フォームのテキストが、その直下のassistant responseの箇所に出力されたテキストが入る。APIの利用料金が画面上部に表示される

6. 気に入ったプロンプトができたら「HTMLに保存」ボタンを押す。各種入出力が初期値になったHTML(api keyを除く)がローカルにダウンロードされる


# 実例の解説

[example](example/) 下に幾つかの利用例のサンプル（HTML保存機能で実行結果を複製したもの）をアップロード済み

## 1. [日本語の校正](example/%E6%97%A5%E6%9C%AC%E8%AA%9E%E3%81%AE%E6%A0%A1%E6%AD%A3.html)

事務作業の補助に有用な例として提示

入力した日本語をよりわかりやすくする書き方を提案してくれる。これの出力結果をそのまま使うというよりは自身の文章作成の参考にする、といった使い方が望ましい

そのまま使うさいは user promptとassistant responseを削除して利用。system promptをコピペして使う方を推奨

元の文章は [市内保育所における非常災害発生時等の対応について](https://www.city.kodaira.tokyo.jp/kurashi/085/085691.html) より引用。個人的には元の文章も特にわかりにくいと感じなかったが、GPTが細かいところまで提案する様子がわかる良いサンプルだったため利用。本当に酷すぎる文章の場合はGPTにそもそもの文意が伝わらずに動かないケースもある。

## 2. [補助金・助成金・支援金の情報ラベル付け](example/補助金・助成金・支援金の情報ラベル付け.html)

システムに組み込む場合の例として提示

文章を解してなんらかのラベリングをする作業が半自動化できる。完全自動化せず、最後に人間のチェックを行うことを推奨。またラベリングの理由を付与した。これは(1)あとで人間で確認(2)検索システムなどに組み込んだときのユーザ体験の改善に有益。

そのまま使うさいは user promptとassistant responseを削除して利用。system promptをコピペして使う方を推奨

元の文章と利用目的一覧は[補助金ポータル](https://hojyokin-portal.jp/subsidies/33489)から引用。入力に与える補助金情報から「目的」のカラムを除外している。このサイトではすでに利用目的が補助金情報に紐づけてあるため、今回の処理は本質的には不要。あくまでデモの一環として

## 3. [確定申告が必要か判定](example/%E7%A2%BA%E5%AE%9A%E7%94%B3%E5%91%8A%E3%81%8C%E5%BF%85%E8%A6%81%E3%81%8B%E5%88%A4%E5%AE%9A.html)

知識をプロンプトに埋め込む例として提示

ルールが短くまとまっていれば、system promptにそのまま書きこまば良いという実例。ルールが長大な場合は事前に箇条書きや要約するなどして圧縮するか、promptだけでなんとかするのを諦めてRetrieval-Augmented Generation や LLM自体の事後学習などの別の方法を検討する必要がある。

そのまま使うさいは user promptとassistant responseを削除して利用。system promptをコピペして使う方を推奨

system promptに入れ込んだルールは[国税庁のページ](https://www.nta.go.jp/taxes/shiraberu/shinkoku/tebiki/2022/01/1_06.htm)をコピペして作成。個人的には人工無能のチャットボットより柔軟に回答してくれるのでこちらの方が好みだが、この方法でもハルシネーション（いわゆるAIが嘘をつく問題）のリスクはゼロではない。QA表の大量自動作成（人間が確認することを前提とした）などには明らかに有益

## 4. [LLMintoLUM](/example/LLMintoLUM.html)

few shot learningによる例示と知識の与え方の例として提示

Qiitaのこの[記事](https://qiita.com/naosugi1987/items/059fb69a15a3dc06f33d)を参照。わかりやすさとインパクトを優先させ既存の商用キャラクタを実例にしているため、著作権元からの指摘があれば即消す。[本リポジトリの製作者への連絡先](https://twitter.com/oosugi_naoya)。普通に会話を楽しんで、明らかに事実誤認があればfew shotに追加していく。あえて嘘（例えば、ダーリンとは？に対する回答を面堂終太郎にする）を入れ込むことによって回答がどう変化するかを楽しむこともできる。

## 5. [WriteSQL](/example/WriteSQL.html) 

コード作成補助の例として提示。2023/09/18に追記

テーブルの情報をWITH句で与え、その続きを書かせるといった形で指示。今回の例のテーブルは適当にそれっぽいものを書いた。GPTへの入力に与える指示が明確であればあるほど正しいSQLが返ってきやすい。今回の例ではやっていないが最終的にSQLから出力されるもののカラム名を指定するなどして要件を明確化する。要件の明確化が求められるのでテーブルにどんなものが入っているかを意識できないと良い結果は得られにくい（ただしSQLを書く時間は大幅に軽減されるしSQL初心者にとっての良いお手本にもなる）

# readme(English ver)

--- translated by gpt3.5-turbo ---

## Usage

1. Obtain an API key from OpenAI.

https://openai.com/product

2. Enter the API key in the text box labeled "api key".

3. Modify the prompt.

Reference: [Hands-on for incorporating ChatGPT into business](https://www.digital.go.jp/assets/contents/node/information/field_ref_resources/5896883b-cc5a-4c5a-b610-eb32b0f4c175/82ccd074/20230725_resources_ai_outline.pdf)

Note: If "assistant response" is already written, it will be used as the assistant prompt for GPT input. If nothing is written, the output from GPT will be used.

4. Click the "GPTへ聞く" button.

5. The text from the input form will appear in the user prompt at the bottom of the screen, and the text from the output will appear in the assistant response section. The API usage cost will be displayed at the top of the screen.

6. Click the "Save to HTML" button to download an HTML file with the default values for various inputs and outputs (excluding the API key).

## Explanation of Examples

Several sample examples (replicated using the HTML save function) are uploaded under [example](example/).

1. [Japanese Proofreading](example/%E6%97%A5%E6%9C%AC%E8%AA%9E%E3%81%AE%E6%A0%A1%E6%AD%A3.html)

Presented as a useful example for assisting office work.

It suggests ways to make the inputted Japanese text more understandable. It is recommended to use the output as a reference for creating your own sentences, rather than using it directly.

When using it directly, delete the user prompt and assistant response. It is recommended to copy and use the system prompt.

The original text is quoted from [City of Kodaira's website](https://www.city.kodaira.tokyo.jp/kurashi/085/085691.html). Personally, I didn't find the original text particularly difficult to understand, but it was a good sample to demonstrate how GPT suggests improvements in detail. In cases where the original text is truly terrible, GPT may not work because the intended meaning of the text may not be conveyed to GPT.

2. [Labeling Information on Grants and Subsidies](example/補助金・助成金・支援金の情報ラベル付け.html)

Presented as an example for incorporating into a system.

It semi-automates the process of understanding the text and labeling it in some way. It is recommended to perform a final human check instead of fully automating the process. The reasons for labeling are also provided. This is beneficial for (1) later human confirmation and (2) improving the user experience when integrating into a search system, etc.

When using it directly, delete the user prompt and assistant response. It is recommended to copy and use the system prompt.

The original text and the list of purposes are quoted from [Subsidy Portal](https://hojyokin-portal.jp/subsidies/33489). The "purpose" column was excluded from the subsidy information given as input. This processing is essentially unnecessary because the purpose is already linked to the subsidy information on this website. It is purely part of the demonstration.

3. [Determining the Need for Filing a Tax Return](example/%E7%A2%BA%E5%AE%9A%E7%94%B3%E5%91%8A%E3%81%8C%E5%BF%85%E8%A6%81%E3%81%8B%E5%88%A4%E5%AE%9A.html)

Presented as an example of embedding knowledge in the prompt.

For cases where the rules are concise and well-organized, it is good to directly write them in the system prompt. If the rules are lengthy, it is necessary to compress them by creating a list or summary in advance, or to consider other methods such as Retrieval-Augmented Generation or post-training of LLM if it is not feasible to handle them with just the prompt.

When using it directly, delete the user prompt and assistant response. It is recommended to copy and use the system prompt.

The rules included in the system prompt were copied from the [National Tax Agency's page](https://www.nta.go.jp/taxes/shiraberu/shinkoku/tebiki/2022/01/1_06.htm). Personally, I prefer this method because it provides more flexible responses than a typical chatbot. However, even with this method, there is still a risk of hallucination (the problem of AI telling lies). It is clearly beneficial for tasks such as creating a large number of QA tables (assuming human confirmation).

4. [LLMintoLUM](/example/LLMintoLUM.html)

Presented as an example of few-shot learning and how to provide knowledge.

Refer to this [Qiita article](https://qiita.com/naosugi1987/items/059fb69a15a3dc06f33d). If there are any copyright issues with using existing commercial characters as examples, they will be removed immediately. Contact the creator of this repository [here](https://twitter.com/oosugi_naoya). Enjoy the conversation and add few-shot examples if there are obvious factual errors. It is also possible to have fun by deliberately including lies (e.g., changing the answer to "Who is Darling?" to "Mendou Shuutarou") and observing how the responses change.





