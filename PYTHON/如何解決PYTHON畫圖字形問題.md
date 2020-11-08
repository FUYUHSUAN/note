## 如果在PYTHON模組設定中不知道有甚麼文字可以使用以下程式碼去尋找

```
import matplotlib.font_manager
 
a = sorted([f.name for f in matplotlib.font_manager.fontManager.ttflist])
 
for i in a:
    print(i)
    
```
* 就會列出所有在這台機器上能使用的文字
* 中文字的部分目前我有找到的
>* DFKai-SB
>* YouYuan
>* FZShuTi
>* STZhongsong
>* STXingkai



