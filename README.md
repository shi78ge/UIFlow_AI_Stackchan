# UIFlow_AI_Stackchan
robo8080さんの[M5Unified_StackChan_ChatGPT](https://github.com/robo8080/M5Unified_StackChan_ChatGPT)のUIFlow版を作ろうとしています。  
現時点ではUIFlowのWEBエディタからテキストで質問を入力し、それに対する回答をM5Core2で喋らせるところまでできます。  
<img src=https://user-images.githubusercontent.com/67863963/229351909-7328d001-82d2-4651-819b-8c496433f2af.png width=300>

## 動作確認済みの環境  
- M5Stack Core2
- UIFlow V1.11.5  
  
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
