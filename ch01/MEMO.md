- [コンピュータシステムの理論と実装――モダンなコンピュータの作り方](https://www.oreilly.co.jp/books/9784873117126/)
  で紹介されている
  [「Nand2tetris Software Suite」のチュートリアル](https://www.nand2tetris.org/software) の[Setup Guide for Apple MacOS](https://drive.google.com/file/d/1QDYIvriWBS_ARntfmZ5E856OEPpE4j1F/view)を読んでインストールを進めた
- 付録 A の A.1 節から A.6 節を読んだ
- [ハードウェアシミュレータ・チュートリアル](https://b1391bd6-da3d-477d-8c01-38cdf774495a.filesusr.com/ugd/44046b_bfd91435260748439493a60a8044ade6.pdf)の 1 ~ 3 に目を通す
  - 付録 A の a.1~A.6 と同等の内容がより具体的に書かれていた

## メモ

### なぜ現代の回路は NAND を基に設計するのか?

- 時代がそうだから

#### 参考

- https://okwave.jp/qa/q1681463.html

### 配布ファイル群 nand2tetris について

- ハードウェアシミュレータは `nand2tetris/tools/HardwareSimulator.sh` で起動

## 実装

全て Nand のみで実装していく。

### Nand

```
x Nand y
= Not(x And y)
```

### Not

```
Not x
= (Not x) Or (Not x)
= Not(x And x)
= x Nand x
```

### And

```
x And y
= Not(Not(x And y))
= Not(x Nand y)
= (x Nand y) Nand (x Nand y)  (∵ 上のNotの変換より)
```

### Or

```
x Or y
= Not(Not(x Or y))
= Not(Not(x) And Not(y))
= Not(x) Nand Not(y)
= (x Nand x) Nand (y Nand y)  (∵ 上のNotの変換より)
```

### Xor

x Xor y = (Not(x) And y) Or (x And Not(y))
式変形しなくとも Not, And, Or を使って表せる（式変形していったほうがより少ないチップで組めるかも？？）
