# Horror Feeds

## Steps

1. We create a account and login (nothing in here).
2. We try to create a account with username = `admin` => `User exists already!`
   
**Ideal**: login `admin` account to get the flag.

3. After checking source, basic `/api/register ` action : check input and the existence of username -> hash passwd  `if` an except error happen, the server return error with message `else` insert data.

**Ideal**: create an exception error 

![image](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/77b525a8-95b6-4be9-91b9-3a63800d9d6c)


4. We have the hashed passwd from error and
`    query_db(f'INSERT INTO users (username, password) VALUES ("{username}", "{hashed}")')
`

**Ideal**: change admin's passwd.

5. I try `UPDATE SET` to change passwd but:

![image](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/75915ece-a6de-4bff-a817-5d391545725e)


6. Then i search ` update combine with insert in mysql ` i find the ideal use `INSERT ... ON DUPLICATE KEY UPDATE`
7. Let's try it: 

![image](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/57cb599d-b204-419f-9236-fe544b96c2e3)


8. The passwd changed, let's login and get flag !!!

![image](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/b2ce90fd-4a18-47c6-965c-2efeab596018)




