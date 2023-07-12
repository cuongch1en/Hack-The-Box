# Wafwaf
## Steps

1. We have the source code.

![image](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/f0905cd9-bf08-4a9e-a9d7-051cea7896f6)


2. We can see that the server filters many things.

![image](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/310e8b5d-14be-45e1-b530-acd623def997)


**Ideal**: it maybe is SQLi.

3. We see `json_decode()` , it is vulnerable.

**Ideal**: encode the payload to bypass filter.

4. Let's try the encoded `' or sleep(10) #` payload and nothing responses.

![image](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/a2db934b-7b78-4d33-93e1-c253e984d67e)


==> SQLi Blind

5. Use SQlmap to inject to `user` para.

`sqlmap -r request.txt -tamper charunicodeescape -v 3 --batch --level=5 --risk=3 --threads=10 --technique=T --dbs --dbms=mysql`

- We get the `db_m8452` database.
- Then we use SQlmap to colect table name and datas
- Finally, we have `HTB{w4f_w4fing_my_w4y_0utt4_h3r3}` flag in `definitely_not_a_flag` table.
