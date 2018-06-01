## Pythonでバブルソート

バブルソートのアルゴリズムは非常に単純で配列内の隣り合った要素を比較して交換していくだけ。  
終了条件はとなりどうしを比較して交換が発生しなくなったら終わり。

flagを利用するとfor forみたいなコードにならないのでシンプルで覚えやすいと思った。  
flagは交換が発生したらもう一度ループするよという意味になっている。  

    # 標準入力が "10 30 20 100"みたいに与えられたときにリストに格納する便利な方法 
    data = [int(x) for x in input().split()]
    
    flag = True
    while flag:
        flag = False
        for i in range(1, len(data)):
            if data[i-1] > data[i]:
                data[i-1], data[i] = data[i], data[i-1] # こう書くとPythonではtempがいらないので便利
                flag = True
    
    print(data)


上記をさらに効率化したコードが書籍には載っている...  
つづく...