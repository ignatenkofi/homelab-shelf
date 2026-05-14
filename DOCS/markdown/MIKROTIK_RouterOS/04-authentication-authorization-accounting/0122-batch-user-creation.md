## Batch user creation 

It is possible to create multiple new users with randomly generated usernames and passwords. For example, the following command will generate 3 new users with 6 lowercase symbols as the username and 6 lowercase, uppercase, and numbers as the password. 

```
/user-manager user
```

```
add-batch-users number-of-users=3 password-characters=lowercase,numbers,uppercase password-length=6 username-
characters=lowercase username-length=6
```

The command generated users can be seen by printing the user's table: 

```
/user-manager user print
```
