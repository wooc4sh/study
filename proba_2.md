Struktury danych w języku C
===
## Wstęp
Witaj,
w ramach treningu i poszerzenia wiedzy, postanowiłem aby napisać ten skrypt. Jest to skrypt o algorytmach i strukturach danych, napisany na podstawie książki Adama Drozdka i Donalda L. Simona "struktury danych w języku C". Jest to mój pierwszy takowy dokument, tak jak wspominałem, traktuję to jako naukę. Bedę tu głównie publikował moje notatki do każdego podrozdziału oraz moje rozwiązania poszczególnych zadań. Kimkolwiek jesteś, życzę Ci dobrze. 

## Rozdział 1. Projektowanie programu w języku C.

### 1.1 Projektowanie zstępujące
Struktura danych- narzędzie do reprezentowania informacji, która ma być przetwarzana przez program. **Projektowanie zstępujące** (ang. top-down design) rozpoczyna się od zdefiniowania problemu, który należy rozwiązać. Problem dzieli się na główne kroki- **podproblemy**. Podproblemy są z kolei dzielone na drobniejsze kroki tak długo, aż rozwiązanie drobnych problemów staje sie łatwe do zapisania albo można wykorzystać bądź zaadoptować znane rozwiązanie. 
Proces dzielenia kroków na mniejsze fragmenty nazywa się **stopniowym uszczegółowianiem**. W idealnym przypadku podproblemy powinny być rozwiązywane niezależnie, a ich rozwiązania powinny być łączone w celu uzyskania rozwiązania głównego problemu. W prawdziwym świecie współzależność między poszczególbymi krokami jest zazwyczaj skomplikowana. Celem projektowania zstępującego jest zminimalizowanie tej współzależności. 
Niektóre zalety projektowania zstępującego:
 - jest to systematyczna metoda rozwiązywania problemów,
 - otrzymane rozwiązanie jest **modularne**,
 - otrzymane rozwiązanie poprzez swą modularność, jest łatwiejsze do zrozumienia,
 - dobrze zaprojektowane fragmenty, mogą być użyte do rozwiązywania innych problemów,
 - dzięki rozpoczęciu projektownia "od góry", można rozpoznać wspólne podproblemy na samym początku i zaoszczędzić sobie pracy.
 
Jako przykład rozważmy problem porządkowania kart. Wydzielimy tu następujące kroki:
1. Podziel talię na kolory.
2. W ramach każdego koloru, ułóż karty według wartości.
3. Połącz uporządkowane kolory.
![](https://hackmd.io/_uploads/rJH3-DxJa.png)


Kroki pierwszy i trzeci są proste. Natomiast krok drugi, jest ciutke bardziej skomplikowany. Możemy go podzielić tak:
- Rozłóż karty w wachlarz.
- Dla każdej karty w wachlarzu, zaczynając od drugiej karty z lewej strony, a kończąc na ostatniej z prawej strony, umieść kartę we właściwym miejscu między kartami leżącymi na lewo od niej(Kartę, którą się właśnie zajmujemy, nazywamy **kartą bieżącą**).

W kropce drugiej użyliśmy pętli(dla każdej karty...). Zostało jeszcze rozpracować operację "umieść kartę(bieżącą) we właściwym miejscu":

- Zaczynając od karty znajdującej się bezpośrednio na od karty bieżącej i przemiesczając się w lewo, przekładaj karty o wartości większej niż wartość kart bieżącej o jedne miejsce w prawo. Zatrzymaj się, jeśli kolejna karta ma wartość mniejszą niż wartość karty bieżącej lub też jeśli nie ma więcej kart do przełożenia.
- Wstaw kartę bieżącą w to miejsce.

Częścią tego zadania jest ustalenie typu danych do reprezentowania wartości kart(u nas to karta) i struktury przechowującej karty(u nas to dłoń ręki).

### 1.2 Projektowanie wstępujące: maszyny wirtualne
Projektowanie zstępujące nie jest jedyną metodą budowania programów. Inne podejście polega na wyjściu od samego języka i wzbogacaniu go nowymi operacjami, dopóki nie będzie można rozwiązać problemu w rozszerzonym języku. Podejście to nazywa się **projektowaniem wstępującym**(ang. bottom-up desgin).
Każde oprogramowanie działające na maszynie cyfrowej rozszerza jej możliwości o nowe funkcje. W efekcie uruchomienie programu na komputerze tworzy nową maszynę, która nie wykonuje swoich operacji bezpośrednio, ale zamienia je na prostsze, wykonywalne przez sprzęt. Tę nową maszynę nazywamy **maszyną wirtualną**, ponieważ istnieje w świecie abstrakcyjnym, a nie fizycznym. To samo dotyczy sytuacji, gdy dodajemy nową operację do języka programowania, pisząc funkcję. Zwiększa ona jego funkcjonalność, tworząc nowy, silniejszy język. O zbiorze nowych funkcji można myśleć jak o wirtualnej maszynie zbudowanej na bazie starego języka.
Przy projektowaniu wstępującym nie dzieli się problemu na kroki, które za pomocą tego języka można zrealizować. Zamiast tego rozbudowuje się język, dodając nowe, coraz silniejsze konstrukcje, tak długo, aż problem da się w języku rozwiązać bezpośrednio. 
Jako przykład rozważmy napisanie programu, który wczytuje, oblicza i wypisuje wyrażenia zbudowane z ułamków. Jeżeli np. na wejściu mamy wyrażenie
:::info
(3/28 + 2/7) * 4/3 -1
:::
to program powinien wypisać wynik
:::success
61/84
:::
Język C nie jest wyposażony w możliwość bezpośredniego reprezentowania i manipulowania ułamkami. Dlatego należałoby zacząć od rozszerzenia języka C przez dodanie funkcji implementujących działania +, -, * i / na ułamkach oraz wczytywania i wypisywania ułamków. Taki pakieto do obliczeń na ułamkach może się przydać w wielu innych programach, nie tylko w tym jednym.

**Podsumowanie**
Zwykle programy projektuje się łącząc obie metody: zstępującą oraz wstępującą. Programista zaczyna od podzielenia problemu na pod problemy i ustala jaki pakiet funkcji byłby mu potrzebny. Następnym krokiem jest ustalenie jakie funkcje wejdą w skład pakietu i użycie ich do rozszerzenia języka. Podproblemy można dalej dzielić na prostsze, a język wzbogacać dopóty, dopóki rozwiązania wszystkich problemów składowych nie dadzą się zapisać bezpośrednio w rozszerzonym języku. Wtedy problem będzie rozwiązany a program- ukończony.
Jednym z celów przy pisaniu programu metodą systematyczną jest to, aby kod programu odzwierciedlał rozbicie na podproblemy. Każdy krok projektu zstępującego mógłby być na przykład zaimplementowany jako wywołanie funkcji. Czyniąc każdy krok funkcją, możemy przypisywać znaczące nazwy spójnym fragmentom kodu, a funkcja może być wywoływana równieżw innych programach. Kod staje się czytelniejszy i łatwiejszy do uruchomienia i ulepszania. Jednym słowem elegancja.


### 1.3. Projektowanie do wielokrotnego użytku: oddzielna kompilacja
W języku C pakiet zawiera się w dwóch plikach: nagłówkowym i źródłowym. Dzięki temu jego funkcje mogą być z łatwością użyte w dowolnym programie. Taką parę plików nazywamy się **modułem**(ang. unit). 
Plik **nagłówkowy**(ang. header, z rozszerzeniem .h) zawiera deklaracje funkcji pakietu. Może też zawierać dyrektywy włączenia innych innych plików oraz makrodefinicje.
Plik **źródłowy**(ang. source, z rozszerzeniem .c) zawiera definicje funkcji. Może także zawierać pomocnicze funkcje i zmienne do wewnętrznego użytku.
Na rysunku 1.1 widać plik nagłówkowy dla pakietu operacji na ułamkach. Plik nagłówkowy włącza plik stdio.h, potrzebny w funkcji writeRat(). Test #ifndef ma na celu zapewnienie, że deklaracje zawarte w tym pliku będą przetwarzane tylko raz, chociaż plik może być włączony do programu wielokrotnie, np gdy program główny włącza ten nagłówek, a inny plik także używa ułamków. 
Plik źródłowy rational.c zawiera kod implementujący te funkcje. Dodatkowo trzeba będzie zdefiniować funkcję obliczającą nwd oraz skracającą ułamek.
Aby można było wywołać funkcje z modułu, plik nagłówkowy musi być włączony do programu. Plik źródłowy modułu także musi włączać swój plik nagłówkowy, ponieważ ten zawiera wymagane dla funkcji deklaracje.
Oba pliki mogą być teraz kompilowane niezależnie, a otrzymane pliki pośrednie- połączone, co tworzy gotowy program. Proces ten nazywa się **oddzielną kompilacją**. Oto jej zalety:
- jeśli jest potrzebna zmiana, to tylko pliki, których ona dotyczy, musza być powtórnie kompilowane. Po ponownej kompilacji wszystkie pliki muszą być znowu łączone, ale zajmuje to zwykle mniej czasu niż kompilacja całości,
- moduł może być stosowany w różnych programach, bez żadnych zmian w jego kodzie,
- plik nagłówkowy zawiera całość informacji potrzebnej do wykorzystania pakietu.

**Rys. 1.1.** Plik rational.h
```=c
#ifndef RATIONALS
#define RATIONALS

#include <stdio.>

typedef struct {
    int num, denom;
} Rational;

int readRat(Rational *);
int writeRat(Rational);
Rational addRat(Rational, Rational);
Rational subRat(Rational, Rational);
Rational multRat(Rational, Rational);
Rational divRat(Rational, Rational);

#endif RATIONALS
```
Użytkownik musi jedynie wiedzieć, jak wywoływać funkcje, a nie jak są zaimplementowane. Wystarczy przejrzeć plik nagłówkowy, aby dowiedzieć się, jak używać pakietu.
Często operacje z pakietu nie zależą od konkretnego typu danych, którym posługuje się program główny. 
Typ danych, dla którego operacje nie zależą od jego szczególnych własności, nazywamy **abstrakcyjnym typem danych (ATD)**.


### 1.4. Abstrakcyjne typy danych(ATD)

### 1.5. Ćwiczenia

## Rozdział 2.

### 2.1. Algorytmy zachłanne
### 2.2. Algorytmy oparte na strategii "dziel i rządź"
### 2.3. Algorytmy oparte na programowaniu dynamicznym
### 2.4. Algorytmy z powrotami(backtracking)
### 2.5. Ćwiczenia
