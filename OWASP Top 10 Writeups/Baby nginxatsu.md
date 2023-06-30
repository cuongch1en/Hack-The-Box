# Baby nginxatsu
## Steps

1. Create a account and login.
2. Then we access `/storage/` ( `/` in the end is an error config in nginx ).

![image](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/523f5262-7374-42ca-bf7d-e62ba5473aff)

3. We' download `v1_db_backup_1604123342.tar.gz`.
4. Unzip it.

![image](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/48e76f40-a74c-4fb5-b763-9cef5ff16068)

- We get 3 account.

![image](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/83abe3b8-c7ce-403c-b6fe-b5d125619b27)

5. Decode the passwd, we get account `nginxatsu-adm-01@makelarid.es` with passwd `adminadmin1`.
6. Login and get flag.

![image](https://github.com/0jamaKig86/Hack-The-Box.ojmk/assets/95555712/a83bd321-0d5a-4076-a7fe-99d52e2fe481)

