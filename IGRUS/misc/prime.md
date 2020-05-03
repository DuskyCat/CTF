# prime
- - - -
rsa에 대한 문제라고 적혀있다.
문제 파일로 public.pem, flag.enc 가 주어 졌는데 rsa로 암호화 해서 flag.enc를 만든것이라 추측된다.
rsa방식은 큰 값의 서로다른 두 소수를 사용한 암호화 방식이며 매우 큰 수의 소인수분해가 어렵다는 점을 이용해 만들어 졌다. 문제에서는 공개키를 주고 flag의 값을 암호화한 결과를 flag.enc로 만든것이다.
문제를 풀기위해 openssl과 RsaCtrTool을 사용했다.

## payload
- - - -
![](prime/%E1%84%8F%E1%85%A2%E1%86%B8%E1%84%8E%E1%85%A5.PNG)
openssl로 public.pem에서 modulus를 추출한 후 이 값을 RsaCtrTool에 적용시켰다.

![](prime/%E1%84%8F%E1%85%A2%E1%86%B8%E1%84%8E%E1%85%A52.PNG)


## flag
- - - -
![](prime/%E1%84%8F%E1%85%A2%E1%86%B8%E1%84%8E%E1%85%A53.PNG)

#CTF/IGRUS/misc