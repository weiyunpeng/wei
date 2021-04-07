# linux 下python2.7 pip升级报错


解决办法；
```sh
yum remove python-pip
cd /usr/local/src
wget https://bootstrap.pypa.io/pip/2.7/get-pip.py
python get-pip.py
```