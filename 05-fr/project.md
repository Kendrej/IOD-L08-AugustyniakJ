# System aukcyjny

## Wprowadzenie

Specyfikacja wymagań funkcjonalnych w ramach informatyzacji procesu sprzedaży produktów w oparciu o mechanizm aukcyjny. 

## Procesy biznesowe

---
<a id="bc1"></a>
### BC1: Sprzedaż aukcyjna 

**Aktorzy:** [Sprzedający](#ac1), [Kupujący](#ac2)

**Opis:** Proces biznesowy opisujący sprzedaż za pomocą mechanizmu aukcyjnego. |

**Scenariusz główny:**
1. [Sprzedający](#ac1) wystawia produkt na aukcję. ([UC1](#uc1))
2. [Kupujący](#ac2) oferuje kwotę za produkt wyższą od aktualnie najwyższej oferty. ([BR1](#br1)) ([UC2](#uc2))
3. [Kupujący](#ac2) wygrywa aukcję ([BR2](#br2))
4. [Kupujący](#ac2) przekazuje należność Sprzedającemu. ([UC3](#uc3))
5. [Sprzedający](#ac1) przekazuje produkt Kupującemu.

**Scenariusze alternatywne:** 

2.A. Oferta Kupującego została przebita, a [Kupujący](#ac2) pragnie przebić aktualnie najwyższą ofertę.
* 2.A.1. Przejdź do kroku 2.

3.A. Czas aukcji upłynął i [Kupujący](#ac2) przegrał aukcję. ([BR2](#br2))
* 3.A.1. Koniec przypadku użycia.

---

## Aktorzy

<a id="ac1"></a>
### AC1: Sprzedający

Osoba oferująca towar na aukcji.

<a id="ac2"></a>
### AC2: Kupujący

Osoba chcąca zakupić produkt na aukcji.


## Przypadki użycia poziomu użytkownika

### Aktorzy i ich cele

[Sprzedający](#ac1):
* [UC1](#uc1): Wystawienie produktu na aukcję

[Kupujący](#ac2):
* [UC2](#uc2): Złożenie oferty
* [UC3](#uc3): Przekazanie należności za wygraną aukcję

---
<a id="uc1"></a>
### UC1: Wystawienie produktu na aukcję

**Aktorzy:** [Sprzedający](#ac1)

**Scenariusz główny:**
1. [Sprzedający](#ac1) zgłasza do systemu chęć wystawienia produktu na aukcję.
2. System prosi o podanie danych produktu i ceny wywoławczej.
3. [Sprzedający](#ac1) podaje dane produktu oraz cenę wywoławczą.
4. System weryfikuje poprawność danych.
5. System informuje o pomyślnym wystawieniu produktu na aukcję.

**Scenariusze alternatywne:** 

4.A. Podano niepoprawne lub niekompletne dane produktu.
* 4.A.1. System informuje o błędnie podanych danych.
* 4.A.2. Przejdź do kroku 2.

---

<a id="uc2"></a>
### UC2: Złożenie oferty

**Aktorzy:** [Kupujący](#ac2)

**Scenariusz główny:**
1. [Kupujący](#ac2) zgłasza do systemu chęć złożenia [oferty](#bo3) w wybranej [aukcji](#bo1).
2. System prezentuje aktualnie najwyższą ofertę i prosi o podanie kwoty.
3. [Kupujący](#ac2) podaje kwotę oferty.
4. System weryfikuje, czy kwota spełnia warunek złożenia oferty. ([BR1](#br1))
5. System rejestruje ofertę jako aktualnie najwyższą w aukcji.
6. System informuje o pomyślnym złożeniu oferty.

**Scenariusze alternatywne:** 

1.A. Aukcja została już zakończona. ([BR2](#br2))
* 1.A.1. System informuje, że w zakończonej aukcji nie można składać ofert.
* 1.A.2. Koniec przypadku użycia.

4.A. Podana kwota nie spełnia warunku złożenia oferty. ([BR1](#br1))
* 4.A.1. System informuje o zbyt niskiej kwocie i podaje minimalną kwotę oferty.
* 4.A.2. Przejdź do kroku 3.

---

<a id="uc3"></a>
### UC3: Przekazanie należności za wygraną aukcję

**Aktorzy:** [Kupujący](#ac2), [Sprzedający](#ac1)

**Scenariusz główny:**
1. [Kupujący](#ac2) zgłasza do systemu chęć opłacenia wygranej [aukcji](#bo1).
2. System prezentuje kwotę należności równą zwycięskiej [ofercie](#bo3) ([BR2](#br2)) i prosi o wybór sposobu płatności.
3. [Kupujący](#ac2) wybiera sposób płatności i potwierdza [płatność](#bo4).
4. System realizuje płatność na rzecz [Sprzedającego](#ac1).
5. System informuje [Kupującego](#ac2) i [Sprzedającego](#ac1) o opłaceniu aukcji.

**Scenariusze alternatywne:** 

1.A. Upłynął termin płatności za aukcję. ([BR3](#br3))
* 1.A.1. System informuje, że aukcja nie może już zostać opłacona.
* 1.A.2. Koniec przypadku użycia.

4.A. Płatność nie powiodła się.
* 4.A.1. System informuje o niepowodzeniu płatności.
* 4.A.2. Przejdź do kroku 2.

---

## Obiewkty biznesowe (inaczje obiekty dziedzinowe lub informatycjne)

<a id="bo1"></a>
### BO1: Aukcja

Aukcja jest formą zawierania transakcji kupna-sprzedaży, w której Sprzedający określa cenę wywoławczą produktu, natomiast Kupujący mogą oferować własną ofertę zakupu każdorazowo proponując kwotę wyższą od aktualnie oferowanej kwoty. Aukcja kończy się po upływie określonego czasu. Jeśli złożona została co najmniej jedna oferta zakupy produkt nabywa ten Kupujący, który zaproponował najwyższą kwotę. 

<a id="bo2"></a>
### BO2: Produkt

Fizyczny lub cyfrowy obiekt, który ma zostać sprzedany w ramach aukcji.

<a id="bo3"></a>
### BO3: Oferta

Kwota zaproponowana przez [Kupującego](#ac2) za produkt w ramach aukcji. Najwyższa oferta w momencie zakończenia aukcji jest ofertą zwycięską.

<a id="bo4"></a>
### BO4: Płatność

Przekazanie [Sprzedającemu](#ac1) należności za produkt przez [Kupującego](#ac2), który wygrał aukcję.

## Reguły biznesowe

<a id="br1"></a>
### BR1: Złożenie oferty

Złożenie oferty wymaga zaproponowania kwoty wyższej niż aktualnie oferowana o minimum 1,00 PLN.


<a id="br2"></a>
### BR2: Rozstrzygnięcie aukcji

Aukcję wygrywa ten z [Kupujący](#ac2)ch, który w momencie jej zakończenia (upłynięcia czasu) złożył najwyższą ofertę.

<a id="br3"></a>
### BR3: Termin płatności

[Kupujący](#ac2), który wygrał aukcję, musi przekazać należność w ciągu 7 dni od jej zakończenia.

## Macierz CRUDL


| Przypadek użycia                                  | Aukcja | Produkt | Oferta | Płatność |
| ------------------------------------------------- | ------ | ------- | ------ | -------- |
| UC1: Wystawienie produktu na aukcję               |    C   |    C    |        |          |
| UC2: Złożenie oferty                              |    R   |    R    |   CR   |          |
| UC3: Przekazanie należności za wygraną aukcję     |    R   |         |    R   |    C     |

### Analiza kompletności

| Obiekt biznesowy | Pokryte operacje | Brakujące operacje | Wniosek |
| ---------------- | ---------------- | ------------------ | ------- |
| Aukcja           | C, R             | U, D, L            | Brak możliwości przeglądania listy aukcji (L) - Kupujący nie ma jak znaleźć aukcji, w której chce złożyć ofertę. Brak edycji (U) i anulowania (D) aukcji przez Sprzedającego. |
| Produkt          | C, R             | U, L               | Sprzedający nie może poprawić danych wystawionego produktu (U). Lista produktów (L) jest realizowana razem z listą aukcji. Usunięcie produktu (D) następuje razem z anulowaniem aukcji. |
| Oferta           | C, R             | L                  | Brak podglądu historii ofert w aukcji (L). Edycja (U) i wycofanie (D) oferty są celowo niedostępne - złożona oferta jest wiążąca. |
| Płatność         | C                | R, L               | Sprzedający nie może sprawdzić, czy aukcja została opłacona (R), a Kupujący nie ma wglądu w historię swoich płatności (L). Edycja (U) i usunięcie (D) płatności nie mają sensu biznesowego. |


