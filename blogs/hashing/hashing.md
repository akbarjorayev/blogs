---
title="Hashing"
published="May 3, 2025"
wallpaper="https://raw.githubusercontent.com/akbarjorayev/blogs/refs/heads/main/blogs/hashing/assets/blog-wallpaper.light.webp"
---

Hashing — generating a hashed string from a given key or string so that it cannot be reversed back to its original form. The function that does this is called a *hash function*.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/akbarjorayev/blogs/main/blogs/hashing/assets/plaintext-to-hash.dark.webp">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/akbarjorayev/blogs/main/blogs/hashing/assets/plaintext-to-hash.light.webp">
  <img src="https://raw.githubusercontent.com/akbarjorayev/blogs/main/blogs/hashing/assets/plaintext-to-hash.light.webp" alt="Plaintext to hash" width="500" height="333">
</picture>

## Why is hashing important?

You should never store a password in a database as plaintext. If hackers gain access to our database, they could steal our users' passwords. Instead, store the **hashed password**.

Imagine generating a hashed password as a one-way process. We can generate the hashed password, but we cannot reverse it; we cannot get the original plaintext from the hashed version. So how do we check whether the given plaintext is correct if we cannot reverse the hashed password? Simple: we generate the hashed password from the given plaintext and then compare it with the stored one.

Tip:

> Use special characters and more than 8 characters. Different services, different passwords. Skip personal info. Just use a strong, suggested password 😉

## Strong passwords matter & Salting

For example, take the hashing algorithm SHA-256. No matter how many times you hash the string `"Hello"`, it always returns the exact result: `185f8db32271fe25f561a6fc938b2e264306ec304eda518007d1764826381969`. If we store them in a database, with the hashed password as the key and the actual password as the value, we can easily look up the actual password if we have the hashed one. Guess what... hackers have already done that for [most used passwords](https://en.wikipedia.org/wiki/Wikipedia:10,000_most_common_passwords). If you use one of them or another simple password, even though they have the hashed version of our weak password, they can easily find our password by its hashed version (they've already collected them). This type of attack is called a rainbow table attack 🌈. So, always use strong passwords.

If we salt our plaintext, we can avoid such an attack. If a user enters a simple password, such as 12345678, and we add a random salt like s@1TValUe to generate our virtual password and then hash it, we can avoid a rainbow table attack. We store both the hashed password and the salt. To check the password, we add the stored salt to the entered plaintext, hash it, and check the hashed value against our stored hash.

> plaintext + salt = salted password

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/akbarjorayev/blogs/main/blogs/hashing/assets/password-salting.dark.webp">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/akbarjorayev/blogs/main/blogs/hashing/assets/password-salting.light.webp">
  <img src="https://raw.githubusercontent.com/akbarjorayev/blogs/main/blogs/hashing/assets/password-salting.light.webp" alt="Salting a password" width="500" height="500">
</picture>

Here's how you'd implement salting:

```javascript
const crypto = require('crypto');

function hashPassword(password, salt) {
  return crypto.createHmac('sha256', salt).update(password).digest('hex');
}

function verifyPassword(inputPassword, salt, storedHash) {
  return hashPassword(inputPassword, salt) === storedHash;
}

function getSalt() {
  return crypto.randomBytes(16).toString('hex');
}

const simplePassword = '12345678';
const salt = getSalt();
const hashedPassword = hashPassword(simplePassword, salt);

const inputPassword = '12345678';
const isValid = verifyPassword(inputPassword, salt, hashedPassword);

console.log(isValid);
```

## Hashing ≠ Encryption

Encryption — securing data using a key, transforming it into unreadable text that can only be reversed (decrypted) with that key.

Imagine a scenario where you need to store a user ID in cookies. If you store it as a simple number (e.g., 1, 2, 3...), users can easily modify it and send requests to server as another user. This method is insecure. However, if you encrypt the ID and store the encrypted version, only you can decrypt it and retrieve the actual user ID. **Don't share this key**.
| Feature            | Hashing                          | Encryption                         |
|--------------------|----------------------------------|------------------------------------|
| Purpose            | Data integrity                   | Data confidentiality               |
| Reversibility      | **One-way** (irreversible)       | **Two-way** (reversible)           |
| Output             | Fixed length                     | Variable length (based on input)   |
| Key usage          | No key needed                    | Requires key                       |

## Timing attacks

To understand timing attacks, we first need to know how == or === comparisons work under the hood. Let’s say we have:

```javascript
const user_input = "hello";
const actual_password = "he1lo";
```

The comparison goes character by character: 'h' == 'h', 'e' == 'e', 'l' == '1' — boom, mismatch. It exits immediately. This "early exit" can leak information that part of the password is correct. Over multiple attempts, hackers could reconstruct the actual password.

To avoid this problem, we should ensure that every attempt takes roughly the same amount of time.

```javascript
function constantTimeCompare(a, b) {
  if (a.length !== b.length) return false;

  let result = 0;
  for (let i = 0; i < a.length; i++) {
    result |= a.charCodeAt(i) ^ b.charCodeAt(i);
  }
  return result === 0;
}
```

## Hashing in dev

In almost every programming language, there are *set* and *map* collections. The time complexity for CRUD (Create, Read, Update, Delete) operations in sets and maps is O(1), which means they happen instantly. They also use a `hash function` to create a **hash code** and store the data at that hash code. More on hashing in dev: [W3Schools Hash Tables](https://www.w3schools.com/dsa/dsa_theory_hashtables.php)

<img src="https://raw.githubusercontent.com/akbarjorayev/blogs/refs/heads/main/blogs/hashing/assets/gatsby-toast.gif" alt="Gatsby Toast" width="478" height="200">

This is all I have so far. Don't forget to protect against brute force attacks with **rate limits**.
