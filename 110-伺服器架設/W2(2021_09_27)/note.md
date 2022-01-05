# 雜記

* yum --> help you compiler the source code install the compiled software into your system
    1. centos(維護週期10年)
    2. fedora
    3. redhat

* ubuntu(維護週期10年)

* rpm 需要按照順序安裝library才能安裝軟體
* yum 則不用，因為yum已經整理好了

---

## 指令
* `uname -a` : 知道現在所使用的是甚麼系統
* `rpm -qa | grep http` : 查詢http是否安裝
* `wget + link` : 下載網路上的檔案
* `rpm -ivh` : 
    1. i: install
    2. v: 想得到更detail的資料
    3. h: 進度條
* `rpm -U` : 升級rpm

---
## test
* Q:要怎麼知道是否安裝httpd
    * A: `rpm -qa | grep httpd`

* Q:查詢安裝了那些檔案到你的系統
    * A:`rpm -ql httpd`

* Q:查詢系統特定檔案的來源封包
    * A: `rpm -qf /usr/share/httpd/icons/a.gif`

* Q:不限定任何平台，通用各類平台的RPM套件軟體
    * A: noarch


