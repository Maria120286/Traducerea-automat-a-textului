Instalarea pachetului
Cel mai bun lucru despre acest API este că este extrem de ușor de configurat și de utilizat. Pur și simplu deschide terminalul ("cmd.exe" în Windows) 
și folosește comanda pip pentru a instala API-ul, 
la fel cum ai face pentru oricare altă bibliotecă Python:

![image](https://github.com/Maria120286/Traducerea-automat-a-textului/assets/157504181/a6a71e45-9771-4b9b-a5f1-e8aefa7dd7f8)
pip install googletrans==4.0.0-rc1

Avem nevoie de această versiune (4.0.0-rc1) pentru a preveni unele bug-uri mai vechi. Așteptăm câteva momente și dacă totul a funcționat corect, modulul a fost instalat cu succes:

![image](https://github.com/Maria120286/Traducerea-automat-a-textului/assets/157504181/26a5d529-fb93-4993-87c6-e547a37b191b)

Info. Citește mai multe detalii [despre PIP].

Documentația oficială a modului Google Translate pentru Python o poți găsi [aici].

Ce limbi sunt disponibile?
Păi cam aceasta ar putea fi prima interacțiune cu acest modul în Python. Priviți codul de mai jos:

import googletrans
print(googletrans.LANGUAGES)

Programul meu este salvat într-un fișier cu extensia py, numit "google.py":
![image](https://github.com/Maria120286/Traducerea-automat-a-textului/assets/157504181/5fc63879-9b61-4599-b305-ff508524ec7d)

Am executat programul și a fost afișată o listă a tuturor limbilor care pot fi utilizate de modul, alături de codul lor corespunzător. Spre exemplu, pentru limba română este "ro", pentru engleză este "en", limba franceză, "fr", limba germană, "de", ș.a.m.d.

Un prim exemplu de traducere
Analizați codul de mai jos, precum și rezultatul în consolă:

from googletrans import Translator
translator = Translator()
rezultat = translator.translate('Salutare, ma bucur sa te intalnesc!')
print(rezultat.text)
![image](https://github.com/Maria120286/Traducerea-automat-a-textului/assets/157504181/1f73e7e9-b7dd-4470-9a44-0900abb6c033)
Mai întâi, am importat clasa Translator din modulul googletrans. Variabila translator reține o instanțiere (un obiect) a clasei Translator. Variabila rezultat va conține o clasă de tip googletrans.models.Translated, care la rândul ei are unele atribute utile pentru noi. Spre exemplu, textul tradus este reținut de atributul text, apelat prin rezultat.text.

Metoda translate a obiectului translator a primit ca unic parametru un text sub forma unui string (clasa str), iar traducerea a fost efectuată automat în limba care este implicită - engleza. Interesant este faptul că funcția a detectat automat limba sursă - româna.

Putem afișa spre exemplu și alte atribute ale rezultatului, exemplul fiind evident:

...
print("Limba initiala:",rezultat.src) #text sursa
print("Limba rezultatului:",rezultat.dest) #text procesat
![image](https://github.com/Maria120286/Traducerea-automat-a-textului/assets/157504181/207ef66f-1562-45cf-a6e8-17415464afb5)
De asemenea, mai există și atributele origin (textul inițial), precum și pronunciation (modul de pronunțare a textului rezultat), iar acestea pot fi utile în cadrul programelor noastre.

Limba rezultatului traducerii
Putem impune limba rezultatului cu ajutorul parametrului dest al metodei translate:

from googletrans import Translator
translator = Translator()
rezultat = translator.translate('Python este foarte fain!', dest='fr')
print(rezultat.text)
![image](https://github.com/Maria120286/Traducerea-automat-a-textului/assets/157504181/5292cb05-426f-4e9f-9516-8a21d5f19d20)
De data aceasta am ales limba franceză cu ajutorul codului "fr". Dacă este necesar, se poate impune și limba textului sursă, folosind parametrul suplimentar src:

rezultat = translator.translate('Python este foarte fain!', src='ro', dest='fr')

Traducerea componentelor unei liste
Să presupunem că avem o listă care conține mai multe elemente de tip string (șir de caractere, clasa str) și ne dorim să le traducem folosind modulul Google Translate, rezultatele fiind salvate într-o altă listă.

Nimic mai simplu, analizați programul de mai jos:

from googletrans import Translator
t = Translator()
culori = ['rosu','verde','albastru','alb','negru','galben']
culori_fr = []
for i in culori:
    culori_fr.append(t.translate(i, dest='fr').text)
print(culori)
print(culori_fr)
![image](https://github.com/Maria120286/Traducerea-automat-a-textului/assets/157504181/55dba650-9070-4584-9677-16e8543ed167)
Metoda translate acceptă textul doar în format string, așadar a trebuit să iterăm printre toate elementele listei noastre. Am tradus textul reținut de fiecare element al listei, adăugându-l la fiecare pas în interiorul noii liste numită culori_fr. Am scris totul pe o singură linie, trimițând ca parametru pentru metoda append rezultatul metodei translate. Puteam scrie și așa, pentru o mai bună înțelegere a codului, folosind o variabilă auxiliară:

...
for i in culori:
    i_tradus = t.translate(i, dest='fr').text
    culori_fr.append(i_tradus)
...










