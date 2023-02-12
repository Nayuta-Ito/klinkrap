**これは脇本壬です。**

これがこのリポジトリの唯一のファイルです。

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
        2. Gの末尾が「グアル」のとき
            1. 値qを以下を満たす最大のrとして定める。
                1. Pの最後の要素の第2要素をpとする。
                2. Pの長さをlとする。
                3. このとき、P[q]の第2要素<pであり、かつ任意のq<q'<lに対してP[q']の第2要素>=pである。
            2. もしそのようなqが存在すれば、
                1. gをGの左端からGの「「P[q]の第1要素」文字目」までの部分とする。
                2. bをGの「「P[q]の第1要素+1」文字目」からGの「右端から4文字目」までの部分に「ギ」を足した文字列とする。
                3. rを「アル」とする。
                4. G'=g+b+b+b+b+rとする。
            3. もしそのようなqが存在しなければ、
                1. gを空文字列とする。
                2. bをGの左端からGの「右端から4文字目」までの部分に「ギ」を足した文字列とする。
                3. rを「アル」とする。
                4. G'=g+b+b+b+b+rとする。
        3. Gの末尾が「ゲアル」か「ゴアル」のとき
            1. TODO
