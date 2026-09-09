# password-audit-lab

Password strength \& cracking time analysis using Hashcat




\## Doel

Dit project onderzoekt hoe wachtwoordlengte en -complexiteit de kraaktijd 

beïnvloeden, met behulp van Hashcat op zelf gegenereerde testwachtwoorden 

en hashes. Doel: aantonen waarom lengte belangrijker is dan schijnbare 

complexiteit bij het kiezen van een sterk wachtwoord.



\## Gebruikte tools

\- Hashcat (v6.2.6)

\- rockyou.txt (bekende gelekte wachtwoordenlijst, gebruikt als dictionary)

\- MD5 hashing



\## Methode

1\. Testwachtwoorden verzonnen (van zwak naar sterk)

2\. MD5-hashes gegenereerd van elk wachtwoord

3\. Dictionary-attack uitgevoerd met rockyou.txt

4\. Brute-force (mask attack) getest met oplopende lengte


## Resultaten



| Wachtwoord      | Lengte | Aanvalstype     | Resultaat    | Tijd        |

|------------------|--------|-----------------|--------------|-------------|

| 123456           | 6      | Dictionary      | Gekraakt     | < 1 seconde |

| Wachtwoord1      | 12     | Dictionary      | Gekraakt     | < 1 seconde |

| (6 tekens, ?a)   | 6      | Brute-force     | Volledig     | 1 min 40 sec|

| (7 tekens, ?a)   | 7      | Brute-force     | Volledig     | 4u 33 min   |

| K7#mP9$vL2       | 10     | Brute-force     | Niet gekraakt| Onhaalbaar (>jaren) |

