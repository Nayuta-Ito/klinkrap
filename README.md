**これは脇本壬です。**

GitHubを使っているのはバージョン管理を簡単にするためです。

2022/06/16 15:15頃追記: 後でシミュレータを作るかもしれません。そのときは言語ごとにディレクトリを設け、その下に実際のプログラムを置くことにします。

* 注釈その1: Javascriptは言語として数えます。

# 定義

## ギアル

「ギ」「グ」「ゲ」「ゴ」「ア」「ル」の6個の文字からなる集合をSとし、S上の文字列全体の集合をTとする。

Tの要素が**ギアル**であるとは、Tが正規表現/^[ギグゲゴ]+アル$/にマッチすることである。

Tの要素の文字数は1オリジン、すなわち左端を1文字目と数える。

### 例

ギアルである例
- ギアル
- ギギアル
- ギギギアル
- ギギギギアル
- ギグゲゴアル
- ゴアル

ギアルでない例
- ガアル
- アルアル
- アルギアル
- ルギア

## 比較

Tの元同士の比較は文字の順序をル<ア<ギ<グ<ゲ<ゴとしたときの辞書的順序とする。

## 定義

ギアルgに対し、0個以上の「自然数とTの要素の順序対」の配列からなる**部分ギアル**を以下の手順で定義する。

1. a=[]とする。
2. lをgの長さとする。
3. for i in 1 to l, repeat this process:
    1. cをgのi文字目とする。
   　2. もしcが「ギ」であれば、aに(i,空文字列)を追加する。
    3. もしcが「グ」または「ゲ」または「ゴ」であれば、
        1. もしaが空であれば、aに(0,空文字列)を追加する。
        2. aの末尾の要素の第2要素の末尾にcを追加する。
    4. もしcがそれ以外の文字なら、何もしない。
4. 最終的に得られたaを部分ギアルとする。

配列は0オリジンとする。すなわち、左端の要素を0と数える。

文字列Mに対し、M{a..b}でMのa文字目からb文字目までの部分を指す。
文字列Mに対し、M{a}でMのa文字目を指す。

Rubyとは添え字が1つずれていることを表すために、あえて別の括弧を用いていることに注意せよ。

ギアルの列A=[G_0,G_1,...,G_n]に対し、A.joinを以下で定義する:
```
A.join=G_0+"ギ"+G_1+"ギ"+..."ギ"+G_n
```

ギアルの列A=[G_0,G_1,...,G_n]に対し、A.join(true)を以下で定義する:
```
A.join(true)="ギ"+G_0+"ギ"+G_1+"ギ"+..."ギ"+G_n
```
実際にはこれは使わない。

ギアルの列A=[G_0,G_1,...,G_n]に対し、A.join(false)を以下で定義する:
```
A.join(false)=A.join
```

## ギアルいえるかな?

以下の手順でギアルからなるリストである **ギアルいえるかな?** を構成する。

## 手順

### 準備

1. 空のリストLを用意する。
2. Lに「ゴゴゴアル」を追加する。
3. Lの最後の要素が「ギアル」になるまで、以下の「繰り返し手順」を繰り返す。
4. Lの最後の要素が「ギアル」になったら、Lの全体を逆順にする。
5. 以上の手順で得られるLがギアルいえるかな?である。

### 繰り返し手順

1. Lの最後の要素をGとする。
2. Gの末尾によって分岐する。
    1. Gの末尾が「ギアル」のとき
        1. Gからその中で最も右にある「ギ」だけを取り除いた文字列はギアルなのでそれをG'とする。
        2. G'をLに追加する。
    2. そうでないとき
        1. Gの部分ギアルをPとする。
        2. Gの長さをlとする。
        3. Gの末尾が「グアル」のとき
            1. 値qを以下を満たす最大のrとして定める。
                1. Pの最後の要素の第2要素をpとする。
                2. Pの長さをlとする。
                3. このとき、P[q]の第2要素<pであり、かつ任意のq<q'<lに対してP[q']の第2要素>=pである。
            2. もしそのようなqが存在すれば、
                1. gをG{1..(P[q]の第1要素)}とする。
                2. bをG{(P[q]の第1要素+1)..(l-2)}に「ギ」を足した文字列とする。
                3. rを「アル」とする。
                4. G'=g+b+b+b+b+rとする。
            3. もしそのようなqが存在しなければ、
                1. gを空文字列とする。
                2. bをG{(P[q]の第1要素+1)..(l-2)}に「ギ」を足した文字列とする。
                3. rを「アル」とする。
                4. G'=g+b+b+b+b+rとする。
        4. Gの末尾が「ゲアル」か「ゴアル」のとき // 変数名に一貫性がないのは英語で使用頻度の低い文字を適当に使っているからである
            1. Gの末尾の「アル」の直前の文字をcとする。
            2. 文字の順序をギ,グ,ゲ,ゴとする。
            3. cの1つ前の文字をc'とする。
            4. Gの部分ギアルを[(z_0, G_0), (z_1, G_1), ..., (z_x, G_x)]とする。
            5. kは後述のサブモジュールで定める。
            6. もし、G_xの中にc未満の文字が存在すれば、
                1. jを「G_x{j}<cかつ全てのj<v<lに対してG_x{v}>=c」を満たす最大のjとする。
                2. k<=v<=xと自然数yに対し、G'_{v,y}を以下で定める。
                    1. l'をG_vの長さとする。
                    2. X_v=G_v{1..j}とする。
                    3. Y_v=G_x{(j+1)..(l'-1)}+c'とする。
                    4. Z_v=G_v{(j+1)..l'}とする。
                    5. もしv=xであれば、Z_vの末尾の文字をc'に変える。
                    5. G'_{v,y}=X_v+(Y_v)*y+Z_vとする。
                3. 自然数yに対し、B_yを以下の手順で得られるBとして定める。
                    1. B=""とする。
                    2. k<=i<=xについて、以下を繰り返す。
                      1. もし後述のサブモジュール2なら、BにG'_{i,y}を追加する。
                4. G'=[G_0, G_1, ..., G_(k-1), B_0, B_1, B_2, B_3].joinとする。
            7. そうでなければ、
                1. k<=v<=xと自然数yに対し、G'_{v,y}を以下で定める。
                    1. l'をG_vの長さとする。
                    2. Y_v=G_x{1..(l'-1)}+c'とする。
                    3. Z_v=G_v{1..l'}とする。
                    4. もしv=xであれば、Z_vの末尾の文字をc'に変える。
                    5. G'_{v,y}=(Y_v)*y+Z_vとする。
                2. 自然数yに対し、B_yを以下の手順で得られるBとして定める。
                    1. B=""とする。
                    2. k<=i<=xについて、以下を繰り返す。
                      1. もし後述のサブモジュール2なら、BにG'_{i,y}を追加する。
                3. G'=[G_0, G_1, ..., G_(k-1), B_0, B_1, B_2, B_3].joinとする。
        5. G'をLに追加**しない**。

#### サブモジュール
1. もし、G_xの中にc未満の文字が存在すれば、
   1. jを「G_x{j}<cかつ全てのj<v<lに対してG_x{v}>=c」を満たす最大のjとする。
   2. kを、「全ての乙<=甲<=xに対してG_甲{1..j}=G_x{1..j}が成り立つ最小の乙とする。
2. そうでなければ、
   1. kを、「全ての乙<=甲<=xに対してG_乙≠""」が成り立つ最小の乙とする。

#### サブモジュール2
文字列S,Tに対し、先頭から見て等しい文字の長さをf(S,T)とする。

1. QをQ'_{i,y}とする。
2. Rを以下で定める。
   1. i+1<x+1なら、R=G'_{i+1,y}である。
   2. そうでなければ、R={k,y+1}である。
3. Pを以下で定める。
   1. i-1>=kなら、P=G'_{i-1,y}である。
   2. i-1<kかつy>0なら、P=G'_{x,y-1}である。
   3. それ以外なら、P=G_{k-1}である。
4. f(P,Q)<=f(Q,R)を返す。
