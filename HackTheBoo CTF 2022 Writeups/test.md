# Horror Feeds

## Steps

1. We create a account and login (nothing in here).
2. We try to create a account with username = `admin` => `User exists already!`
   
**Ideal**: login `admin` account to get the flag.

3. After checking source, basic `/api/register ` action : check input and the existence of username -> hash passwd  `if` an except error happen, the server return error with message `else` insert data.

**Ideal**: create an exception error 

![Alt text](image-1.png)

4. We have the hashed passwd from error and
`    query_db(f'INSERT INTO users (username, password) VALUES ("{username}", "{hashed}")')
`

**Ideal**: change admin's passwd.

5. I try `UPDATE SET` to change passwd but:

![Alt text](image-2.png)

6. Then i search ` update combine with insert in mysql ` i find the ideal use `INSERT ... ON DUPLICATE KEY UPDATE`
7. Let's try it: 

![Alt text](image-3.png)

8. The passwd changed, let's login and get flag !!!

![Alt text](Screenshot_2023-06-22_06-16-25.png)



