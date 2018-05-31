# 最初にSchemeを勉強しよう

## 動作環境はどうする？
Schemeのいちばん人気な処理系はGaucheらしいのだけれど、WindowsだとインストールがめんどくさいしMacと環境を合わせるのもこれまた面倒なので、Paiza.ioでSchemeを選んで動作確認することにした。  
ちなみにLispはたくさん（別の人が作った）実装があって、この実装のことを”処理系”とよんでいる。

https://paiza.io/

## まず最初に何が出来ないとだめなんだ？
プログラムコンテストは標準入力でパラメータを受け取り、標準出力でパラメータに対する処理結果を返すスタイルとなる。  
まずはinputとprintを覚えることにした。

Lispは処理系ごとに標準入出力を実装するようになっているため、ここではGaucheの命令を覚えなければならない。  
Paiza.ioの中身はGaucheなのだ。
さっそくググって下記のコードを書いてみた。

defineで関数mainを宣言してread-lineで標準入力を取得してprintで出力って感じだと思う。  
最後の0は関数の戻り値だと思う。  
paiza.ioで実行するとちゃんと動く。

    (define (main args) 
        (print (read-line))
        0)


次に標準入力をstring->numberにて文字列を数値に変換してn×２するコードを書いた  
これも正常に動作した。

    (define (main args) 
        (define n (string->number (read-line)))
        (print (* n 2))
        0)


## お次はループだ
n回printするコードを書く。  
よくわからないがSchemeにはCommon Lispのようなloopマクロすなわちfor文がないのでループは再帰で書かなければならないらしい。  

loop-printというテキトーなネーミングの関数を定義して再帰でカウントダウンしていくだけのコードを書いた。  
再帰は終了条件を書かないと無限ループになるのでnが0未満になったときに0を返却するようにした。  
Common Lisp知識だとifはtrueの場合とfalseの場合で一行しか式を書けなかったのでfalseにはbeginを入れて逐次実行するようにした。  

    (define (loop-print n)
        (if (< n 0)
               0
               (begin 
                      (print n)
                      (loop-print (- n 1)))
        )
    )
    
    (define (main args) 
        (define n (string->number (read-line)))
        (loop-print n)
        0)



フィボナッチ数列を（おそらく）Lisp的な書き方を無視して書いてみた。  
mapを使えばもっと簡単にかけそうな気がする。  
あと、再帰って関数の再帰呼び出し→やりたい処理の順で記述するとカウントアップになるのねー。（今初めて知った）


    (define (fib n)
            (cond ((= n 0) 0)
                  ((= n 1) 1)
                  (else (+ (fib (- n 1)) (fib (- n 2))))
            )
    )

    (define (print-fib n)
        (if (< n 0)
            0
            (begin (print-fib (- n 1))
                   (print (fib n)))
        )
    )

    (define (main args) 
        (define n (string->number (read-line)))
        (print-fib n)
        0)


つづく...