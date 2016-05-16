---
layout: code
title: 引数全てを表す$@と$*の違いと問題
date: 2016-05-14 11:03:33 +0900
tags: [bash]
---

`$@`と`$*`は引数全てを表示します。違いはこの2つの変数をダブルクォートで囲んだ際です。`$@`は複数要素に別れますが、`$*`は1つの文字列となります。

```bash
"$@"
"$1" "$2" "$3"

"$*"
"$1 $2 $3"
```

これは`if`で`test`をする時に困ります。`$@`で引数が0だと空文字列ではなく、何もないことになります。そういう時は、`$*`を使いましょう。

```bash
function asterisk_if() {
  if [ "$@" != "" ]; then
    echo "$@"
  else
    echo asterisk empty
  fi
}
```

# 参考

* [シェルスクリプトでの$@の罠](http://rcmdnk.github.io/blog/2014/06/25/computer-bash/)