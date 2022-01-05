# 雜記
* `\cp a.txt b.txt` : 拷貝時不做任何詢問


* `export PATH=$PATH:/home/user/bin`  //在做設定時前面不用加上$，且這樣`a.sh`就可以直接執行了

*  `./a.sh` =  `/home/user/bin/a.sh`

* `alias ll='ls-l`   //之後ll指令就會等於ls -l

* 假設輸入`alias`如果沒出現`alias re='rm -i`，那麼將其增加上去，這是做double check的動作

* `alias ll='ls-l`這個動作只會出現在做那個指令的termial中，如果每次都能使用自己設定的指令，用`gedit .bashrc`，將這段指令(alias ll='ls-l)加上去，每次打開termial都可以使用`ll`這個指令

* 假設想要`echo ""`盡量加上雙引號

* `ping -c 1 -w 1 8.8.8.8` : -c 代表ping幾次，-w 設定timeout

* `curl` : 文字版的瀏覽器，可將網頁抓回來


## 變數

* 我們使用`$IFS`時沒出現任何東西，因為預設是空白，也就是輸入指令之間的空白

* 使用`$UID`如是0表示是0那麼是超級使用者，如果不是那就是一般使用者

* `echo $Random | md5sum` : 可以產生更長的亂數

* `echo $Random | md5sum | cut -c | -10` : 產生可控長度的亂數

* `echo $?` : 確認上個指令是否執行成功，如果出現0表示成功，如果出現其他數字表示不成功

## 腳本範例




