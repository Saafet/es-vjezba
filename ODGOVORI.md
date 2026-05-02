## Zadatak 1

1. kad je status green sve primarne i replikacijske sharde su aktivne i sto znaci da klaster radi ispravno i bez problema

2. kad je status yellow sve primarne sharde su aktivne i podaci su dostupni ali neke replikacijske sharde nisu dodijeljene 

3. kad je status red jedna ili više primarnih shardi nije aktivna dio podataka je nedostupan i klaster ne funkcionira ispravno

## Zadatak 2

1. pitanje:
Naslov je tipa tekst zato što treba on i treba biti da bi full text search ispravno radio.

2. pitanje:
Keyword verzija čuva originalnu vrijednost što omogućuje točno sortiranje i agregiranje po naslovu. Text polje se ne moze koristiti za sortiranje jer je razlomljeno na tokene.

3. pitanje:
Jer ih uvijek pretražujemo po točnoj vrijednosti (npr. točan autor "Ivo Andrić"), a ne full-text pretragom. Koriste se i za agregacije tj. samo grupiranje knjiga po autoru ili žanru.

4. pitanje:
Opis se ne bi trebao spremati kao keyword zato sto se radi o dugackom tekstu gdje s druge strane nema smisla da bude keyword, jer pogodan je za full text search

## Zadatak 3

1. pitanje:
Jer indeks koristi hrvatski_analyzer s asciifolding filterom koji pretvara dijakritike u ASCII ekvivalente. Kad se dokument indeksira gdjes e "ćuprija" sprema kao token "cuprija". Kad pretražujemo "cuprija" query prolazi kroz isti analyzer i traži token cuprija koji se podudara.

2. pitanje:
_score je mjera relevantnosti dokumenta za zadani upit, izračunata BM25 algoritmom. Uzima u obzir koliko često se pojam pojavljuje u dokumentu i koliko je rijedak u cijelom indeksu. Dokumenti koji sadrže traženi pojam vise puta ili u kracem tekstu dobivaju visi score.

## Zadatak 5

1. tokeni na drini cuprija
{
  "tokens": [
    {
      "token": "na",
      "start_offset": 0,
      "end_offset": 2,
      "type": "<ALPHANUM>",
      "position": 0
    },
    {
      "token": "drini",
      "start_offset": 3,
      "end_offset": 8,
      "type": "<ALPHANUM>",
      "position": 1
    },
    {
      "token": "cuprija",
      "start_offset": 9,
      "end_offset": 16,
      "type": "<ALPHANUM>",
      "position": 2
    }
  ]
}

2. pitanje;
Pretvara sva slova u mala — Drini postaje drini. Bez ovoga bi pretraga drini ne ih pronašla Drini. Razlika od asciifolding: lowercase se bavi velikim/malim slovima, a asciifolding se bavi specijalnim znakovima.

3. pitanje
Bez analyzera Elasticsearch bi uspoređivao doslovne vrijednostinp "Ćuprija" i "cuprija" bili bi potpuno različiti stringovi i pretraga ne bi radila. Analyzer normalizira i tekst dokumenta i tekst upita na isti način, pa pretraga funkcionira neovisno o dijakritikama, velikim slovima ili interpunkciji.

## Završni zadatak

Elasticsearch je puno bolji od SQL LIKE '%tekst%' iz vise razloga. SQL LIKE mora proci kroz svaki red u tablici i uspoređivati string po string sto postaje jako sporo kad imas puno podataka. Elasticsearch s druge strane koristi invertirani indeks sto znaci da za svaku rijec vec zna tocno gdje se nalazi pa je pretraga brza cak i na milijunima dokumenata.

Osim same brzine, Elasticsearch razumije tekst na drugaciji nacin. Kroz analyzere moze normalizirati dijakritike i velika/mala slova pa npr. pretraga cuprija pronalazi ćuprija što SQL LIKE jednostavno ne moze. Također rezultati nisu samo pronađeno/nije pronađeno nego su rangirani po relevantnosti kroz _score tako da uvijek dobijemo najbitnije rezultate prvo.

Na kraju Elasticsearch je dizajniran da radi na više nodova i lako se skalira dok relacijske baze nisu bas stvorene za takav tip pretrage.