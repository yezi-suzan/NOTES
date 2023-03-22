WSL: 输入xclock,报错Warning: Missing charsets in String to FontSet conversion
============================================================================
问题
----
```bash
suw@ubuntu2204:~$ xclock
Warning: Missing charsets in String to FontSet conversion
```

-----------------------------------------------------------------------
解决方案
--------
```bash
suw@ubuntu2204:~$ export LANG=C
```

------------------------------------------------------------------------
原理
----
    待补充。。。

------------------------------------------------------------------------
参考
----
https://blog.csdn.net/qq_43845426/article/details/106273557