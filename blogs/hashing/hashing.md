META_DATA_START
title="Hashing"
published="Apr 25, 2025"
META_DATA_END

BLOG_START
Hashing — generate hashed string from a given key or string so that it could not be reversed back to original form. The function which does that is called *hash function*

In this blog, we will talk about **password hashing** and will see some examples.

### Why is hashing important?
You should never ever store a password in a database as plain text. Because if your database is taken by hackers they could access your users' password. You store **hashed password**.

Imagine generating hashed password as it is a one-way process, we can generate hashed password but we cannot reverse it, we cannot get password from hashed password. So how do we check whether given password is correct if we cannot reverse hashed password? Simple, we generate hashed password from given password then compare it with stored one.

![Plaintext to hash](https://raw.githubusercontent.com/akbarjorayev/blogs/hashing/blogs/hashing/photos/plaintext_to_hash.webp)(500x333)

### Strong passwords matter
For example, take the hashing algorithm `SHA-256` no matter how many times you hash the string `"Hello"` it always returns exact result: `185f8db32271fe25f561a6fc938b2e264306ec304eda518007d1764826381969`. If we store them in database, hashed password as key and actual password as value, we can easily look up for actual password if we have hashed one, guess what... hackers have already done that for [most used passwords](https://en.wikipedia.org/wiki/Wikipedia:10,000_most_common_passwords). If you use one of them or another simple password, even though they have hashed version of your weak password, they can easily find your password by hashed version (they already collected them). So always use **strong passwords**.

Tips:
> Use special characters and over 8 characters. Different services, different passwords. Skip personal info. Just use a strong, suggested password 😉

### Salting
### SHA-256
### Argon2
BLOG_END
