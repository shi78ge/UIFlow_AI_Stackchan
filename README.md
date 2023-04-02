# UIFlow_AI_Stackchan
robo8080さんの[M5Unified_StackChan_ChatGPT](https://github.com/robo8080/M5Unified_StackChan_ChatGPT)のUIFlow版を作ろうとしています。  
現時点ではUIFlowのWEBエディタからテキストで質問を入力し、それに対する回答をM5Core2で喋らせるところまでできます。  
<img src=https://user-images.githubusercontent.com/67863963/229351909-7328d001-82d2-4651-819b-8c496433f2af.png width=300>  
↓動かしている様子  
https://twitter.com/shi78ge/status/1642442808182308864  

## 動作確認済みの環境  
- M5Stack Core2
- UIFlow V1.11.5  (WEBエディタ)
  
## 利用させてもらっている資産  
[M5Avatar_UIFlow](https://github.com/robo8080/M5Avatar_UIFlow)  
こちらのAvatar_startブロックを使用しています。  

## ChatGPT APIについて
こちらは本家roboさんのリポジトリにも説明があるので、取得方法は割愛します。

## Google text-to-speech APIについて
音声の発話にGoogle text-to-speech APIを利用しています。  
まずはGCPへの登録が必要になるので、[こちら](https://masa-engineer-blog.com/gcp-text-to-speech-api-python/)のサイトなどを参考にお願いします。ただし「1.2Cloud text-to-Speech API キーの取得」から少し手順が異なります。  
以下のAPIのページで認証情報を選択し、  
<img width=682 src=https://user-images.githubusercontent.com/67863963/229353347-b65aa44c-b618-4473-af13-3233357ec054.png>  
「認証情報を作成」→「APIキー」を選択します。  
<img width="682" alt="image" src="https://user-images.githubusercontent.com/67863963/229353410-3f0171ac-373a-45a7-9ebf-87d08f84d81f.png">  
このあと表示されるAPIキーを利用するので控えておきます。  
(「サービスアカウント」のほうと間違えないようにご注意ください)
  
## 使い方
### 使用例  
まず、先にUIFlowのカスタムブロックから chatgpt.m5b, google_tts.m5b, M5StackAvatar.m5b を読み込みます。  
次に chatgpt_googletts.m5f を開きます。右下のRunを押せば、しばしの待ち時間の後、promptに入力した質問に対する回答がM5Core2のスピーカーから再生されます。  
<img src=https://user-images.githubusercontent.com/67863963/229354691-45fd4249-bddf-4d73-9a11-d0447abeee46.png>  
上の画像で「XXX」の部分にChatGPTのAPIキーを、「YYY」部分にgoogle text-to-speechのAPIキーを入力してください。  
promptがChatGPTへの質問(要望)になります。  
role1~3で性格等指定できますが、回答を50文字に制限しているのが一つポイントになります。あとのtext-to-speechで生成した音声を一旦メモリに格納するのですが、WAVファイルなのでサイズが大きく、あまり長い回答だとメモリが足りずエラーになってしまいます。50文字でもエラーになる場合があるので、微調整が必要になります。roboさんのものだとmp3を再生しているので長い回答でも大丈夫なようです。micropythonでmp3を再生する方法がわからず、一旦このような仕様になっています。  
  
ChatGPTで生成した回答はget_responseというブロックに格納されるので、これをtext-to-speechブロックに渡しています。  
text-to-speechブロックでは他にもlangやspeakingRateといったパラメータを指定しています。これについては以下リンクのtext-to-speechデモを参照すればパラメータの意味がだいたいわかるかと思います。  
https://cloud.google.com/text-to-speech/?hl=ja&_ga=2.128697868.-1887006218.1679815025&_gac=1.249111157.1680418475.CjwKCAjwrJ-hBhB7EiwAuyBVXR1KyJqbKebUqz_kzYyJ_cQDrYTWteK3VoC_o_n-QhC4N9tKxuAc6RoCezEQAvD_BwE#section-2

<img src=https://user-images.githubusercontent.com/67863963/229355421-cc0cbfdc-c0ea-4be1-8567-ef14482f374e.png>  
text-to-speechブロック上では、speakingRateは1.5で通常の早さぐらいです。volumeはCore2のスピーカー設定なので0~6で音量を指定します。  
text-to-speechの利用料金については[こちら](https://cloud.google.com/text-to-speech/pricing?hl=ja) を参照ください。  
<img src=https://user-images.githubusercontent.com/67863963/229356264-18134bf1-4580-402a-8b57-60f6f9a89d3d.png width=800>
WaveNetやNeural2の音声だとStandardに比べて無料枠が少なくなっているようです。　　

## 参考にしたサイト
- Raspberry Pi Pico WでChatGPT APIを使用する方法  
https://sozorablog.com/raspberry-pi-pico-w-chatgpt/  
  
- Googleさんの Cloud Text-to-SpeechをPythonから使う  
https://qiita.com/to_obara/items/d8d5c92c2ea85a197e2d
