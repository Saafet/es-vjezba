## Zadatak 1

kad je status green sve primarne i replikacijske sharde su aktivne i sto znaci da klaster radi ispravno i bez problema
kad je status yellow sve primarne sharde su aktivne i podaci su dostupni ali neke replikacijske sharde nisu dodijeljene 
kad je status red jedna ili više primarnih shardi nije aktivna dio podataka je nedostupan i klaster ne funkcionira ispravno

## Zadatak 2

1 pitanje:
Naslov je tipa tekst zato što treba on i treba biti da bi full text search ispravno radio.

2 pitanje:
Keyword verzija čuva originalnu vrijednost što omogućuje točno sortiranje i agregiranje po naslovu. Text polje se ne moze koristiti za sortiranje jer je razlomljeno na tokene.

3 pitanje:
Jer ih uvijek pretražujemo po točnoj vrijednosti (npr. točan autor "Ivo Andrić"), a ne full-text pretragom. Koriste se i za agregacije tj. samo grupiranje knjiga po autoru ili žanru.

4 pitanje:
Opis se ne bi trebao spremati kao keyword zato sto se radi o dugackom tekstu gdje s druge strane nema smisla da bude keyword, jer pogodan je za full text search

