pythonによる対話型自律学習AI(python2.7)
======================
これはpythonで作られたAIです。  
自律学習型なので、自分で言葉を覚え、覚えた言葉を組み合わせて色々なことを喋ります。

予め形態素の候補として文章を読ませることもできますし、何もないところからあなたの入力した文章のみをもとに学習させることもできます。
 
使い方
------
### AIと対話する ###
AIと対話してみましょう！  

`` save/alice.txt ``という空のファイルを用意して下さい。もちろんこれは書き込み可能なものでなければいけません。  
そして``AI/`` のフォルダに移り `` python Alice_AI.py ``のようにして実行して下さい。  
`` save/alice.txt ``を読み込んだら`` Aliceさんがログインしました ``のように表示されるので、`` You: ``のあとに続けて何か入力して下さい。

終了のコマンドなどは特に用意していませんので`` Ctrl + C ``などで終了して下さい。

 
### AIとAIで対話させる ###
次はAIとAIで喋らせましょう！

`` save/alice_2.txt `` と `` save/bob_2.txt `` という2つの空のファイルを用意して下さい。もちろん書き込み可能なものでなければいけません。
先ほどと同じように``AI/``のフォルダで`` python ai2ai.py ``のようにして実行して下さい。
`` Aliceさんがログインしました `` ``Bobさんがログインしました`` のメッセージが出ればあとは自動でAI達が喋ってくれます！
 

### あらかじめファイルを読ませる ###
予めファイルを読ませることもできます。その場合は文章が書かれたファイルを形態素に分解しておく必要があります。  
まずはファイルを用意しましょう（私が青空文庫からいくつか引っ張って来たものが`` text/ ``のフォルダ内にあります）。

これを次に`` python Cutmorph.py [ファイル名] ``として実行して下さい。  
すると`` save/m_[ファイル名].txt ``(もともとテキストファイルであれば``~.txt.txt``)のようになります。

あとはこれを上のように``alice.txt``や``bob_2.txt``のようにリネームしてAIを実行すれば、自動的にもとの文章から自分で会話を創りだしてくれます！好きなキャラクターなどにAIを模倣させると面白いかも知れませんね。


### Twitterのログを用いる場合 ###
twitterのログを用いてAIに喋らせたい場合、[twilog](http://twilog.org/)からログを持ってくるのが速いと思われます。  
twilogの管理ページより適当な文字コードでCSVファイルを落とすことができます。今は全てutf-8で開発を行なっているのでutf-8で落として下さい。

ログファイルが用意できたら、``python text/non_number.py [ログファイル]``として実行して下さい。ログファイルで不必要な数字などが省かれて``[ログファイル].txt``の形で出てきます。

あとはこれを上と同じように``python Cutmorph.py [[ログファイル].txt]``などとしてAIに読ませれば、Twitterログを通してあなたと会話することができます。


プログラムの改変
------- 

### 読み込むファイルを変更する ###
最初に読み込ませるファイルの設定は`` ./Alice_AI.py ``であれば一番下、

```python
if __name__ == "__main__":
    alice = AliceEngine("save/alice.txt") # ← ココです
    while True:
        input = raw_input("You：").decode('utf-8')
        if input == '': continue
        alice.mainloop(input)
```

``./ai2ai.py``であれば真ん中辺りの

```python
AI.append(Alice_AI.AliceEngine("save/alice_2.txt",u"Alice"))  # ← ココです
AI.append(Alice_AI.AliceEngine("save/bob_2.txt",u"Bob"))      # ← ココです
```

のファイル名を適当に変更して下さい。


-------
楽しいAIライフを！  
なお、このプログラムはpython2.7.3を用いています。python3.x系列では動かない部分がありますのでご了承下さい（その場合は適当にfolkして改変してくださいね！）。

