# 🔐 Hash Cracking Lab

![Hashcat](https://img.shields.io/badge/Tool-Hashcat-red)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)
![License](https://img.shields.io/badge/License-MIT-blue)

> Password strength & cracking time analysis using Hashcat — showing why length beats complexity.

---

## 🎯 Goal

This project investigates how password length and complexity affect
cracking time, using Hashcat on self-generated test passwords and hashes.

**Goal:** demonstrate why length matters more than apparent complexity when
choosing a strong password.

## 🛠️ Tools Used

- **Hashcat** (v6.2.6)
- **rockyou.txt** — well-known leaked password list, used as dictionary
- **MD5, SHA256, and bcrypt** hashing

## 🔬 Method

1. 🧪 Test passwords created (ranging from weak to strong)
2. 🔑 Hashes generated for each password using MD5, SHA256, and bcrypt
3. 📖 Dictionary attack performed using rockyou.txt
4. 💪 Brute-force (mask attack) tested with increasing length
5. ⚡ Cracking speed compared across hash algorithms

## 📊 Results

| Password      | Length | Attack Type | Result      | Time                |
| ------------- | :----: | ----------- | ----------- | -------------------- |
| `123456`      |   6    | Dictionary  | ✅ Cracked   | < 1 second           |
| `Password1`   |   12   | Dictionary  | ✅ Cracked   | < 1 second           |
| 6-char random |   6    | Brute-force | ✅ Exhausted | 1 min 40 sec          |
| 7-char random |   7    | Brute-force | ✅ Exhausted | 4h 33 min             |
| `K7#mP9$vL2`  |   10   | Brute-force | ❌ Not cracked | Infeasible (>years) |

## 💡 Conclusion

This experiment shows that **password length has a far greater impact on
cracking time than complexity alone**. In brute-force attacks, cracking time
grows exponentially: from 1 minute 40 seconds at 6 characters to 4 hours
33 minutes at 7 characters — each additional character multiplies the
number of possible combinations.

It also shows that passwords that *look* "complex," such as `Password1`
(capital letter + number), are still cracked within seconds via a
dictionary attack, because they follow a predictable pattern already
present in leaked password lists.

> **Takeaway:** a long passphrase (e.g. 4+ random words) is both
> stronger *and* easier to remember than a short, "complex" password.

## ⚙️ Algorithm Comparison

| Hash     | Speed         | Relative to MD5   |
| -------- | ------------- | ------------------ |
| 🟢 MD5    | 10,839.5 kH/s | 1x (baseline)      |
| 🟡 SHA256 | 1,080.6 MH/s  | ~100x slower       |
| 🔴 bcrypt | 190 H/s       | ~57,000x slower    |

Beyond password length, the **choice of hashing algorithm** matters enormously
for storage security. MD5 and SHA256 are designed to be fast — great for
file integrity checks, terrible for password storage. bcrypt is deliberately
slow, making large-scale cracking attempts against a leaked database far
less practical: a full rockyou.txt run against MD5 finishes in seconds,
while the same run against bcrypt is estimated at **3 days, 11 hours**.

This is why modern systems use **bcrypt, scrypt, or Argon2** for password
storage instead of MD5/SHA256.

## 🔁 Reproduction

**Requirements:** Hashcat, a wordlist (e.g. rockyou.txt)

1. Generate hashes of your own test passwords (MD5, SHA256, and/or bcrypt),
   one hash per line in a `.txt` file
2. Download a wordlist:

https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt

3. Run a dictionary attack (`-m` sets hash type: `0`=MD5, `1400`=SHA256, `3200`=bcrypt):
```bash
   hashcat.exe -m 0 -a 0 hashes.txt rockyou.txt
```
4. Run a brute-force test (increasing length):
```bash
   hashcat.exe -m 0 -a 3 hashes.txt --increment --increment-min 1 --increment-max 10 ?a?a?a?a?a?a?a?a?a?a
```
5. View results:
```bash
   hashcat.exe -m 0 --show hashes.txt
```

---

📫 **Connect:** [LinkedIn](https://www.linkedin.com/in/sebastiaanvasseur/) &nbsp;|&nbsp; 🐙 [GitHub](https://github.com/cbahvas)
