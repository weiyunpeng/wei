### 问题


1. 升级pip（pip install --upgrade pip）后报错
```
Traceback (most recent call last):
  File "/usr/bin/pip", line 9, in <module>
    from pip import main
ImportError: cannot import name main

```
解决办法：
```
sudo vim /usr/bin/pip
正确代码如下：

import sys

# Run the main entry point, similarly to how setuptools does it, but because
# we didn't install the actual entry point from setup.py, don't use the
# pkg_resources API.
from pip._internal import main
if __name__ == '__main__':
    sys.exit(main())
```