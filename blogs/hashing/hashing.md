META_DATA_START
title="Hashing"
published="Apr 25, 2025"
META_DATA_END

BLOG_START
Hashing — generating a hashed string from a given key or string so that it cannot be reversed back to its original form. The function that does this is called a *hash function*.

![Plaintext to hash](https://raw.githubusercontent.com/akbarjorayev/blogs/hashing/blogs/hashing/photos/plaintext_to_hash.webp)(500x333)

### Why is hashing important?
You should never store a password in a database as plaintext. If hackers gain access to our database, they could steal our users' passwords. Instead, store the **hashed password**.

Imagine generating a hashed password as a one-way process. We can generate the hashed password, but we cannot reverse it; we cannot get the original plaintext from the hashed version. So how do we check whether the given plaintext is correct if we cannot reverse the hashed password? Simple: we generate the hashed password from the given plaintext and then compare it with the stored one.

Tips:
> Use special characters and more than 8 characters. Different services, different passwords. Skip personal info. Just use a strong, suggested password 😉

### Strong passwords matter & Salting
For example, take the hashing algorithm `SHA-256`. No matter how many times you hash the string `"Hello"`, it always returns the exact result: `185f8db32271fe25f561a6fc938b2e264306ec304eda518007d1764826381969`. If we store them in a database, with the hashed password as the key and the actual password as the value, we can easily look up the actual password if we have the hashed one. Guess what... hackers have already done that for [most used passwords](https://en.wikipedia.org/wiki/Wikipedia:10,000_most_common_passwords). If you use one of them or another simple password, even though they have the hashed version of our weak password, they can easily find our password by its hashed version (they've already collected them). This type of attack is called a **rainbow table attack 🌈**. So, always use **strong passwords**.

If we `salt` our plaintext, we can avoid such an attack. If a user enters a simple password, such as `12345678`, and we add a random salt like `s@1TValUe` to generate our virtual password and then hash it, we can avoid a rainbow table attack. We store both the hashed password and the salt. To check the password, we add the stored salt to the entered plaintext, hash it, and check the hashed value against our stored hash.

> plaintext + salt = virtual password

```
const crypto = require('crypto');

function hashPassword(password, salt) {
  return crypto.createHmac('sha256', salt).update(password).digest('hex');
}

function getSalt() {
  return crypto.randomBytes(16).toString('hex');
}

const simplePassword = '12345678';
const salt = getSalt();
const hashedPassword = hashPassword(simplePassword, salt);

const inputPassword = '12345678';
const isValid = hashPassword(inputPassword, salt) === hashedPassword;

console.log(isValid);
```
BLOG_END
