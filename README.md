# Hash Cracking Lab

Password strength & cracking time analysis using Hashcat

## Goal

This project investigates how password length and complexity affect
cracking time, using Hashcat on self-generated test passwords and hashes.
Goal: demonstrate why length matters more than apparent complexity when
choosing a strong password.

## Tools used

- Hashcat (v6.2.6)
- rockyou.txt (well-known leaked password list, used as dictionary)
- MD5 hashing

## Method

1. Test passwords created (ranging from weak to strong)
2. MD5 hashes generated for each password
3. Dictionary attack performed using rockyou.txt
4. Brute-force (mask attack) tested with increasing length

## Results

| Password         | Length | Attack type | Result       | Time                |
|------------------|--------|-------------|--------------|----------------------|
| 123456           | 6      | Dictionary  | Cracked      | < 1 second          |
| Password1        | 12     | Dictionary  | Cracked      | < 1 second          |
| (6 chars, ?a)    | 6      | Brute-force | Exhausted    | 1 min 40 sec         |
| (7 chars, ?a)    | 7      | Brute-force | Exhausted    | 4h 33 min            |
| K7#mP9$vL2       | 10     | Brute-force | Not cracked  | Infeasible (>years) |

## Conclusion

This experiment shows that password length has a far greater impact on
cracking time than complexity alone. In brute-force attacks, cracking time
grows exponentially: from 1 minute 40 seconds at 6 characters to 4 hours
33 minutes at 7 characters — each additional character multiplies the
number of possible combinations.

It also shows that passwords that look "complex," such as Password1
(capital letter + number), are still cracked within seconds via a
dictionary attack, because they follow a predictable pattern already
present in leaked password lists. Randomness and length matter far more
than simply adding a capital letter or number.

Practical takeaway: a long passphrase (e.g. 4+ random words) is both
stronger and easier to remember than a short, "complex" password.

## Reproduction

Requirements: Hashcat, a wordlist (e.g. rockyou.txt)

1. Generate MD5 hashes of your own test passwords (e.g. via md5hashgenerator.com),
   one hash per line in `hashes.txt`
2. Download a wordlist, e.g.:
   https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt
3. Dictionary attack: 
  hashcat.exe -m 0 -a 0 hashes.txt rockyou.txt
4. Brute-force test (increasing length):  
  hashcat.exe -m 0 -a 3 hashes.txt --increment --increment-min 1 --increment-max 10 ?a?a?a?a?a?a?a?a?a?a
5. View results:
  hashcat.exe -m 0 --show hashes.txt
