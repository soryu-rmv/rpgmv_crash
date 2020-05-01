# Tips to save our project data from RPGMV crash

by @soryu_rpmakermv

-------------------------------------------------

<br>

## 1. Introduction

RPGMakerMV has potentially unstable behavior after it has been roled out in 2015.  
The most significant feature of RPGMV is its portability for various platforms.   
Instead, several faults in RPGMV editor are seen which were hardly in previos series of RPGMakers.   

What I worry the most is high frequency of crash and force termination of RPGMV.   
Though number of items in database which can be handled in RPGMV editor got fewer compared to old series,   
we often encounter force termination of RPGMV when we are using almost maximum items in the database.
Especially, termination during the save of current working project is tragedy, which devastates the data file at worst.   

![json](https://user-images.githubusercontent.com/64351233/80788333-c5b3cd00-8bc3-11ea-9d11-bd549341cf43.png)   

Above figure shows a dialog which notifies that Animations.json has been destroyed    
after force termination of RPGMV has occurred. In this time, Animations.json becomes empty.
We never open RPGMV game project unless we fix Animations.json for designated format.   
Even if we succeeded to open a project, we hardly can restore the animation data without its copy in advance.   

When we launch RPGMV, RPGMV extract data (events, playing bgm, map data, database, and so on)     
from every .json files into memory (Here, memory is a space allocated for RPGMV to save project data.)     
until it is terminated. Note that, items in database are also written in corresponding files 
as the project is saved **even if there are no changes in database**.     

Installing additional physical memory into our PC absolutely does not help this behavior.    
We never can fix the problem in RPGMV by using js plugins. Only we can do is just waiting.    
However, it is not still fixed after more than 5 years passed when RPGMV is released.
On the contrary, the developement has been directed another maker series such as Visual Novel Maker and   
Pixel Game Maker. Actually, RPGmakerMV is poted to PlayStation 4 and Nintendo Switch as "RPGmakerMV Trinity"   
in Japan, which has been condemned by purchasers due to serious bugs in a editor.



During my works with RPGMV, I have experienced many times of force termination and being destroyed data    
and lost much time for the work. I was greatly disappointed as if I heard a revelation that   
"RPGMaker MV is not a tool for making professional RPGs". To defy this damned situation,    
I began to consider methods of self-protection for current working project data from frequently causing RPGMV crash.   




<br>

## 2. Situation RPGMV crashes
著者が遭遇した、RPGツクールMV強制終了が発生した主な瞬間を列挙する。

- 「プロジェクトの保存」を実行したとき
- データベースやイベント編集画面でOKを押したとき
- イベントの作成中 (イベントコマンド選択操作など)
- bgmフォルダに入れた楽曲を、サウンドテストで再生している状況下での作業

プロジェクト保存によるデータ破壊は以ての外であるが、イベント作成中の強制終了は  
作業データを退避させる暇もなく、作成したイベントが無に帰すため非常に厄介である。


<br>

## 3. Countermeasures

### 3.1. Migration of database files which have large number of items temporary 

Animations.jsonの破損によく遭遇するというのならば、戦闘テストを必要としない作業をしている間は
RPGツクールMVに読み込ませるAnimations.jsonをわざと空にしてしまうという方法もある。    
ただし、はじめに述べたように**「全くの白紙」ではプロジェクトを起動できない**ので最小限の準備が必要である。  
以下は、空のAnimations.jsonを利用してエディタを開くまでの手順である。   

- 1. 現在のプロジェクトの ./data/Animations.json を適当に名前を変更する、あるいはコピーで別の場所へ退避
- 2. RPGツクールMVのデータベース上で、アニメーションを全て削除（空の状態にする）
- 3. プロジェクトを保存する（ここでRPGツクールMVを1度終了させておくとよい）
- 4. 実質的な空のAnimations.jsonを以後、バックアップとしておくために別の名前(Animations_.json等)へ変更する
- 5. RPGツクールMVを開き直す（ほぼ空のAnimations.jsonが読み込まれる）

<br>

![animations](https://user-images.githubusercontent.com/64351233/80791751-92763b80-8bcd-11ea-8d2e-072a3610efbc.png)

上図は実際の運用例である。   
Animations.jsonは、エディタ上で編集可能な1000データ全てを使い込むと、10MB近くになる。   
ところが会話イベントを作成する作業が目的ならば、（アニメーションの表示をしない限り）この作業にAnimations.jsonは必要ない。   
無駄に読み込ませてクラッシュされるぐらいなら、ほぼ空のデータを読み込ませておけば    
保存時のクラッシュのリスクが減るどころか、プロジェクトの起動時間も短くなる。  
 
戦闘テストを含めた通しプレイをする時は、ダミーとして用意した（ほぼ）空のAnimations.jsonを  
再度Animations_.json等にしておいて、**退避しておいた本物のAnimations.jsonを元に戻す（./data/に置く）**。　　　

<br>

バックアップを作成することを心掛けておくことはこういった制作作業においては当然気をつけるべきことだが、    
RPGツクールMVに関してはいささか性質が悪いので、   
（アニメーションデータが数個失われてしまっただけでも再現・復元、再作成は手間である）    
エディタをアテにしない自衛手段としては有効である。


<br>

なお、ダミーのAnimations.jsonを読み込んでツクールを起動している間は、    
既にプロジェクト内で作成していたイベント内の「アニメーションの表示」における表示アニメーションは　　  
　　**？**　　となってしまっているが、表示させるアニメーションの情報は、各マップのデータを持つ   
MapXXX.jsonファイルが記憶しているのでAnimations.jsonを元に戻せば直ちに復活する（ので、不安になって迂闊に触らないこと）。   



### 3.2. Refrain to play BGM files in RPGMV 

ツクールのエディタ上（サウンドテスト）でBGMを再生すると、もちろん曲のデータもメモリに格納される。   
曲データのファイルサイズ(ビットレートや長さ)にもよるが、**長く壮大な曲はそもそも再生できていないこともある**。   
oggファイルのループ再生のチェックに有用ではあるが、再生しながらの作業継続は強制終了のリスクを高める。   

作業BGMとしての試聴など、再生だけが目的なら他のツールを使って再生させた方が安全である。


### 3.3. Have a copy of created events for backup before saving project

「保存したいが、保存するとクラッシュするかもしれない」となると、    
割としっかりとしたストーリー部分のイベントを書き上げた直後のプロジェクト保存には勇気が必要である。    

そこで、RPGツクールMVを**もう１つ起動する**という方法がある。    
開かれた直後のRPGツクールMVでいきなり強制終了してしまうということはまず起こらない。    
（もちろん、ツクール多重起動のためにPCそのもののメモリは必要なので、古いPC等の環境によっては厳しいかもしれないが…）   


まず、作業中のプロジェクトを新たに起動したRPGツクールMVで開いた状態にしておく。
下図では、もともと作業していたRPGMVを左側に、今新規に開いたRPGMVを右側に並べている。

![rpgmv](https://user-images.githubusercontent.com/64351233/80790807-be43f200-8bca-11ea-897c-4efac99e5442.png)

作成されているイベントは、なんと**ツクールのウィンドウやプロジェクトをまたいでコピー・ペーストできる**。     
しかも同じマップであってもなくてもよく、更には全く違うゲームに対してのペーストも可能である。

これを利用して、作業していたRPGMV画面から今作ったばかりのイベントをコピーする。   
ショートカットでCtrl+Cをしてもよいし、右クリック→コピーでもよい。   

コピーができたら、新たに立ち上げた方のRPGMV画面（もちろん、同じマップを開いていた方が良い）にペーストする。   
こちらもショートカットでCtrl+Vをしてもよいし、右クリック→ペーストでもよい。  

この状態で、もともと作業していたRPGMV側に戻って改めてプロジェクト保存を試みる。  
成功したなら、もうそれでもう一方は閉じてしまって構わないし、    
万が一強制終了になってしまったとしても、新たに開いておいたツクールに作成したイベントは生きているので、
精神的ダメージを受けずに保存の再チャレンジができる。   
（たとえ成功した場合でも、その後に再び大きな作業を続けるならツクールMVを開き直す事も検討されたい。）


※ 間違っても、同じプロジェクトを開いた状態で異なる作業を同時に進めてはいけない     
（それらを保存する行為はゲーム制作状態の整合性を失う）   
※ あくまで、ツクールで同じデータを**読み込むだけ**は作業上問題ない、というだけである
