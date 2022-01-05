## 刪除特定數字、大小寫字母、特殊字元等

* 去除數字
    ```
    //法一:
    [user@localhost ~]$ echo "abcdABCD1234" | tr -d [1-9]
    abcdABCD

    //法二:
    [user@localhost ~]$ echo "abcd#AB?CD.1234" | tr -d "[:digit:]"
    abcd#AB?CD.
    ```
* 去除數字、大小寫字母
    ```
    //法一:
    [user@localhost ~]$ echo "abcdABCD1234" | tr -d [1-9A-Za-z]

    //法二:
    [user@localhost ~]$ echo "abcd#AB?CD.1234" | tr -d "[:alnum:]"
    #?.

    ```
* 去除特殊字元
    ```
    [user@localhost ~]$ echo "abcd#AB?CD1234" | tr -d [#?]
    abcdABCD1234
    ```
* 去除大小寫字母
    ```
    //法一:
    [user@localhost ~]$ echo "abcd#AB?CD.1234" | tr -d "[:alpha:]"
    #?.1234

    //法二:
    [user@localhost ~]$ echo "abcd#AB?CD.1234" | tr -d "[a-zA-Z]"
    #?.1234
    ```

* 將大寫轉成小寫
```
[user@localhost ~]$ echo "ABCD" | tr [:upper:] [:lower:]
abcd
```

* 將指定符號轉換為"*"
```
[user@localhost ~]$ echo "ABCDabcd1234" | tr -c "0-9" "*"
********1234*
```

* 簡單製作加解密的動作
```
[user@localhost ~]$ echo "hello" | tr 'abcdefghijklmnopqrstuvwxyz' 'cdefghijklmnopqrstuvwxyzab'
jgnnq
[user@localhost ~]$ echo "jgnnq" | tr 'cdefghijklmnopqrstuvwxyzab' 'abcdefghijklmnopqrstuvwxyz' 
hello

```

## 遠端登陸

- 1. 使用putty
![]()

- 2. 


```
smallko, [04.10.21 15:08]
scp c.txt root@192.168.56.108:/tmp  (upload the file)

smallko, [04.10.21 15:08]
scp root@192.168.56.108:/tmp c.txt (download the file)
```

## 產生序列seq
* 從5到12每次間格2
```
$seq 5 2 12
5
7
9
11
```
* 從10到1每次間格-1
```
seq 10 -1 1
10
9
8
7
6
5
4
3
2
1
```

* 生成1~5的檔案
```
$touch seq 1 5
```

* 刪除1~5的檔案
```
$rm -f seq 1 5
```

* 將前面都補齊
```
$seq -w 1 2 11
01
03
05
07
09
11
```

* 
```
$seq -s `+` 1 10
1+2+3+4+5+6+7+8+9+10
```

* 類似計算機的功能
```
$seq -s `+` 1 10 | bc
55
```

* 
```
$echo `1.1+2.3+2` | bc
5.7
```

*
```
$seq -s `+` 1 5 |bc
120
```
