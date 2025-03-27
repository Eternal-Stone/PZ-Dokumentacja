# System Nieoczekiwanych Sytuacji

## Dynamiczne Absurdalne Zdarzenia

Podstawowe założenia:

1. **Czym są nieoczekiwane sytuacje?**
    * To losowe, absurdalne wydarzenia, które pojawiają się w grze, aby wyrwać gracza z monotonii, stagnacji lub nudy.
    * Aktywują się, gdy gra monitoruje brak progresji, powtarzalność działań lub długotrwałą bezczynność.
2. **Dlaczego są istotne?**
    * Dodają humoru, świeżości i spontaniczności do rozgrywki.
    * Ukrywają w sobie wskazówki lub fragmenty mapy, które prowadzą gracza do **Legendarnego Miasta Diamentów**.
3. **Jak działają?**
    * **Dostosowanie do gracza:** System analizuje aktywność gracza, by dobrać odpowiednie wydarzenia.
    * **Rotacja wydarzeń:** Każde wydarzenie jest unikalne, a po jego ukończeniu gra wprowadza nowe sytuacje z innej puli.

Struktura systemu:

1. **Monitorowanie aktywności:**
    * Gra rozpoznaje stagnację na podstawie:
        * Braku eksploracji lub progresji.
        * Powtarzalnych czynności (np. farmienie).
        * Długotrwałej bezczynności (1-3 dni w grze).
2. **Wyzwalanie zdarzeń:**
    * System uruchamia odpowiednie wydarzenia w zależności od kontekstu:
        * Lekkie i zabawne w przypadku krótkiej stagnacji.
        * Złożone i bardziej nagradzające po dłuższej bezczynności.
3. **Wskazówki do Legendarnego Dungeona:**
    * Ukończenie wydarzeń może nagrodzić gracza:
        * Fragmentami mapy prowadzącej do dungeona.
        * Wskazówkami na temat ukrytych ścieżek i mechanik lochu.
        * Nietypowymi nagrodami, które pomagają w lochu.

Przykłady absurdalnych wydarzeń:

1. **Tańczący Goblin:**
    * NPC zaczyna spontanicznie tańczyć na środku wioski. Rozwiązaniem jest… taniec razem z nim!
    * Nagroda: Fragment mapy + komiczny dialog o dawnych bohaterach.
2. **Biegnący Kurier Kiełbasa:**
    * W lesie pojawia się kurier w przebraniu kiełbasy, którego trzeba dogonić.
    * Nagroda: Wskazówka o tajemnym wejściu w lochu.
3. **Ślimak w Neonowych Okularach:**
    * W polu spotykasz gadającego ślimaka, który oferuje wymianę twoich niepotrzebnych przedmiotów na wskazówkę o lochu.
4. **Spadająca Krowa:**
    * Nagle z nieba spada krowa w tutu, a gracze muszą pomóc jej dotrzeć do ukrytej doliny, gdzie czeka fragment mapy.

## Legendarne Miasto Diamentów: Epicki Dynamiczny Dungeon

Historia:

* **Legendarne Miasto Diamentów** to dawna siedziba potężnych bohaterów, którzy zginęli lub stracili zmysły w walce z Arcyczarnoksiężnikiem. Przejęte przez siły zła, stało się twierdzą, gdzie Arcyczarnoksiężnik planuje otworzyć portal do demonicznych mocy.
* Bohaterowie, którzy zostali wyrzuceni z lochu, są teraz rozsiani po świecie gry, postradali zmysły i w formie absurdalnych postaci dają graczowi wskazówki.

Struktura lochu:

1. **Dynamiczne generowanie:**
    * Każde podejście zmienia układ lochu, zagadki, pułapki i rozmieszczenie bossów.
    * Po ukończeniu lochu przenosi się on w inne miejsce na mapie.
2. **Poziomy trudności:**
    * **Normalny:** Standardowy loch z umiarkowaną trudnością.
    * **Heroiczny:** Więcej wrogów, bardziej złożone zagadki.
    * **Mityczny:** Ukryte bossy, dynamiczna zagadka finałowa i możliwość walki z Arcy Demonem.
3. **Bossowie:**
    * 6 głównych bossów reprezentujących dawne klasy bohaterów.
    * **Przykłady:**
        * **Kapłan Chaosu:** Przywołuje demoniczne bestie.
        * **Rycerz z Ostrzy:** Wirujące ostrza, które zamykają przestrzeń.
4. **Zagadkowa sala finałowa:**
    * Dynamiczna zagadka, która wymaga kreatywności:
        * Łączenie run.
        * Rozwiązywanie logicznych łamigłówek.
        * Znajdowanie ukrytych przełączników.
5. **Arcy Demon:**
    * Ostateczna walka w najwyższej sali.
    * W mitycznym trybie może pojawić się nawet dwóch lub trzech Arcy Demonów.
    * Pokonanie go zmienia historię lochu, powodując ucieczkę Arcyczarnoksiężnika.

Nagrody:

1. **Skarbiec Arcyczarnoksiężnika:**
    * Po pokonaniu Arcy Demona gracze zyskują dostęp do dynamicznie generowanego skarbca.
    * Ograniczony czas na zebranie łupów przed aktywacją strażników.
2. **Regrywalność:**
    * Loch przenosi się w inne miejsce, a jego układ i zawartość zmieniają się przy każdym podejściu.
3. **Medalion Mocy:**
    * Pozwala śledzić pozycję lochu na mapie, gdy pojawi się ponownie.

## Monitorowanie aktywności gracza

Podstawowe założenia monitorowania aktywności:

System monitoruje działania gracza w grze, by zrozumieć, czy znajduje się on w stanie stagnacji, braku motywacji lub monotonnego grania. Głównym celem jest **wyczucie momentu**, w którym gracz potrzebuje bodźca w postaci nieoczekiwanego zdarzenia.

Jak system rozpoznaje aktywność gracza?

1. **Czas bezczynności:**
    * Gra monitoruje, jak długo postać gracza nie wykonuje istotnych działań, takich jak:
        * Ruch w świecie gry.
        * Interakcja z NPC-ami.
        * Rozwiązywanie zagadek, walka lub eksploracja.
    * **Przykład działania:**
        * Jeśli gracz stoi w jednym miejscu przez ponad **3 godziny** (bez znaczących akcji), system zaczyna obniżać „aktywność gracza” w swoim algorytmie.
2. **Powtarzalność czynności:**
    * System rozpoznaje, jeśli gracz przez długi czas wykonuje te same, monotonne czynności, takie jak:
        * Grind (zabijanie tych samych przeciwników).
        * Zbieranie identycznych przedmiotów.
        * Powtarzalne odwiedzanie tej samej lokacji.
    * **Przykład działania:**
        * Gracz spędza kilka godzin w jednym miejscu, farmiąc wilki. System zaczyna zwiększać wskaźnik „stagnacji” i przygotowuje zdarzenie.
3. **Brak eksploracji nowych obszarów:**
    * Gra monitoruje, czy gracz odwiedza nowe miejsca na mapie lub angażuje się w odkrywanie świata.
    * **Przykład działania:**
        * Jeśli gracz spędza wiele godzin w jednej lokacji, ignorując inne obszary, system uruchamia mechanizm zwiększania wskaźnika stagnacji.
4. **Długoterminowa stagnacja (1-3 dni):**
    * System analizuje dane na przestrzeni kilku dni:
        * Brak postępu w fabule głównej lub zadaniach pobocznych.
        * Niewielka liczba zdobytych przedmiotów lub wykonanych zadań.
        * Stały brak interakcji z kluczowymi mechanikami gry.
    * **Przykład działania:**
        * Gracz przez 3 dni loguje się do gry, ale nie wykonuje żadnych znaczących akcji fabularnych. System traktuje to jako stagnację długoterminową i uruchamia zaawansowane zdarzenie.

Jak system reaguje na stagnację?

1. **Dostosowanie poziomu zdarzeń do aktywności:**
    * Im dłuższy czas stagnacji, tym bardziej złożone i zaawansowane wydarzenie:
        * **Średnioterminowa stagnacja (minimum 3 godziny):** Zdarzenie bardziej skomplikowane, wymagające interakcji lub rozwiązania zagadki.
        * **Długoterminowa stagnacja (kilka dni):** Zaawansowane wydarzenie fabularne, które silnie angażuje gracza i prowadzi do odkrycia fragmentu mapy.
2. **Czynniki wykluczające:**
    * Gra upewnia się, że gracz nie jest np. chwilowo nieobecny (poszedł do toalety, zrobił sobie przerwę).
        * **Mechanizm kontroli:** Zdarzenia nie aktywują się, jeśli w krótkim czasie od wykrycia stagnacji gracz wykonuje akcje, takie jak:
            * Wciśnięcie przycisków.
            * Minimalny ruch postaci.
        * **Przykład:** Jeśli gracz wraca do gry po 15 minutach przerwy, zdarzenie się nie uruchomi.

## Wyzwalanie zdarzeń

Podstawowe założenia:

Wyzwalanie zdarzeń opiera się na wcześniej zidentyfikowanych wzorcach zachowań gracza (np. stagnacja, monotonia). System dynamicznie dostosowuje zdarzenia do stopnia aktywności gracza oraz kontekstu, w jakim się znajduje (lokalizacja, aktualna fabuła, mechaniki w grze).

Rodzaje zdarzeń:

1. **Subtelne zdarzenia (minimum 3 godziny stagnacji):**
    * **Cel:** Delikatne przypomnienie o istnieniu ciekawych rzeczy w grze.
    * **Przykłady:**
        * NPC w pobliżu gracza zaczyna robić coś nietypowego (np. śpiewać, kręcić się w kółko).
        * W pobliżu postaci spada dziwny przedmiot (np. gadający kamień).
        * Nagle pojawia się zwierzę lub obiekt, który zwraca uwagę swoją nietypowością (np. kurczak w koronie).
    * **Interakcje:** Gracz może zignorować zdarzenie, ale angażowanie się w nie jest nagradzane małym humorem lub wskazówką fabularną.
2. **Interaktywne zdarzenia (kilka godzin monotonnego działania):**
    * **Cel:** Zmotywowanie gracza do eksploracji i interakcji z mechanikami gry.
    * **Przykłady:**
        * W lesie, gdzie gracz od dawna farmi wilki, nagle pojawia się gadająca beczka, która oferuje mini-quest.
        * W mieście handlarz zaczyna oferować „dziwnie znajomy” fragment mapy, ale wymaga rozwiązania zagadki lub dostarczenia nietypowego przedmiotu.
        * Nagle w świecie gry pojawia się portal, który prowadzi do zamkniętej lokacji wymagającej jednorazowego rozwiązania zagadki.
3. **Zaawansowane zdarzenia fabularne (1-3 dni stagnacji):**
    * **Cel:** Silne zaangażowanie gracza i wprowadzenie większego znaczenia do wydarzeń.
    * **Przykłady:**
        * Na środku miasta pojawia się parujący kocioł, z którego wyskakuje NPC, mówiąc: „Tajemniczy Duch Legendarnego Miasta mnie wysłał!”
        * Fragment mapy jest odnajdywany w trakcie spontanicznej eksploracji wnętrza nowo odkrytego jaskiniowego bossa.
        * W okolicach gracza pojawia się seria zagadek, które w logiczny sposób prowadzą do wskazówek o Legendarnym Mieście Diamentów.

Mechanizm dynamicznego dostosowywania zdarzeń:

1. **Dostosowanie do lokalizacji:**
    * Zdarzenia są generowane na podstawie miejsca, w którym gracz spędza czas.
        * **Przykład w lesie:** Pojawia się gadający wilk, który udaje przywódcę watahy i daje zadanie zebrania run.
        * **Przykład w mieście:** NPC sprzedający „dziwne, znajome” przedmioty, które są fragmentami mapy.
2. **Powiązanie z fabułą:**
    * Jeśli gracz zbliża się do kluczowych miejsc w fabule (np. regionu bliskiego Legendarnemu Miastu Diamentów), zdarzenia stają się bardziej związane z głównym wątkiem.
3. **Skalowanie trudności:**
    * Zdarzenia dostosowują się do poziomu gracza.
        * **Nowy gracz:** Proste zagadki lub humorystyczne sytuacje.
        * **Zaawansowany gracz:** Skrytki, portale i wskazówki wymagające kreatywnego myślenia.

Przykład zdarzenia:

**Kontekst:** Gracz od dawna farmi wilki w lesie.

* **Zdarzenie:** Pojawia się wilk gigant w garniturze, który mówi: „Czego tu szukasz? Otworzę ci drogę, ale najpierw zagrajmy w moje zasady.” Wilk wymaga rozwiązania logicznej zagadki (np. odnalezienia ukrytych symboli w lesie).
* **Efekt:** Po ukończeniu gracz otrzymuje fragment mapy lub wskazówkę dotyczącą Legendarnego Miasta Diamentów.

## Wskazówki do Legendarnego Dungeona: Fragmenty mapy i ich znaczenie

Podstawowe założenia:

* Każde absurdalne wydarzenie, które gracz napotyka w grze, może zawierać **wskazówkę lub fragment mapy** prowadzącej do Legendarnego Miasta Diamentów.
* **Fragmenty mapy** są nagrodą za kreatywność i rozwiązanie nietypowych zadań, a także kluczem do odblokowania dungeona.
* **Wskazówki** mogą przybierać różne formy, od bezpośrednich dialogów po zagadki, które gracz musi sam zinterpretować.

Jak działają wskazówki i fragmenty mapy?

1. **Fragmenty mapy:**
    * Każde absurdalne wydarzenie zawiera **część mapy**, która:
        * **Zawiera wizualne wskazówki:** Fragment mapy pokazuje kawałek terenu, symbol lub lokalizację.
        * **Nie zawsze jest kompletna:** Część fragmentów może być uszkodzona lub ukryta, co wymaga dodatkowego zaangażowania gracza.
        * **Łączy się z innymi fragmentami:** Gracz może składać kawałki mapy w całość, by zidentyfikować położenie dungeona.
    * **Przykład:** Po dogonieniu biegnącego kuriera kiełbasy gracz dostaje fragment mapy, na którym widnieje dziwny symbol góry z wyrzeźbioną twarzą.
2. **Wskazówki narracyjne:**
    * NPC lub wydarzenie może dostarczyć graczowi **zagmatwanych lub humorystycznych informacji**.
        * **Przykład:** Gadający kamień po ukończeniu minigry mówi: „Szukaj bramy tam, gdzie płyną srebrne łzy.”
        * Gracz musi zinterpretować to jako rzekę w okolicy, która prowadzi do kolejnego fragmentu.
3. **Zagadki powiązane z fragmentami:**
    * Niektóre fragmenty mapy są ukryte za zagadkami w świecie gry.
    * **Przykład:** W karczmie pojawia się NPC, który mówi: „Znalazłem coś, ale oddam ci to tylko, jeśli odkryjesz moje sekrety.” Aby zdobyć fragment mapy, gracz musi rozwiązać zagadkę logiczną, która ujawnia lokalizację ukrytego przedmiotu.

Dynamiczność systemu wskazówek:

1. **Różnorodne wydarzenia:**
    * Każde wydarzenie prowadzi do fragmentu mapy lub wskazówki, ale w unikalny sposób.
        * **Przykład:** W jednym przypadku gracz zdobywa fragment mapy przez interakcję z NPC-em, w innym — musi pokonać bossa, który go strzeże.
2. **Opcjonalność:**
    * Gracz może ignorować wydarzenia i nadal przechodzić główną fabułę gry, ale ścieżka do Legendarnego Miasta Diamentów pozostaje ukryta bez zaangażowania w te wydarzenia.
3. **Kreatywne wykorzystanie mechanik:**
    * Niektóre wskazówki mogą wymagać nietypowego użycia mechanik gry.
        * **Przykład:** Fragment mapy ukryty w beczce, którą można znaleźć, eksplorując za pomocą specjalnego zaklęcia.

Przykład zdarzenia prowadzącego do fragmentu mapy:

**Kontekst:** Gracz spędza długi czas w mieście, rozmawiając z NPC-ami.

* **Zdarzenie:** Na środku placu pojawia się gadający kurczak, który twierdzi, że zna tajemnicę skarbów Arcyczarnoksiężnika. Gracz musi znaleźć odpowiednie składniki (jajka, mleko i złotą monetę), by przekonać kurczaka do wyjawienia tajemnicy.
* **Rezultat:** Kurczak wypluwa fragment mapy i mówi: „Skarb jest tam, gdzie wielkie cienie tańczą pod gwiazdami.”

Wizualizacja fragmentów mapy:

* Fragmenty mapy są stylizowane i niosą wskazówki wizualne, takie jak:
  * Nietypowe symbole (np. góra, rzeka, drzewo o dziwnej koronie).
  * Strzałki i linie sugerujące drogę.
  * Ukryte znaki, które gracz może odkryć dopiero po zdobyciu specjalnych przedmiotów.

## Kompletny System Proceduralnego Generowania Dungeona

### Proceduralne generowanie mapy dungeona

Parametry startowe mapy

1. **Wielkość:**
    * Dungeon ma określone parametry definiujące maksymalną długość, szerokość, wysokość oraz liczbę pięter.
    * **Przykład:**
        * Na poziomie trudności **Normalnym**, dungeon może mieć 10-15 pomieszczeń.
        * Na poziomie **Mitycznym** rozmiar wzrasta do 20-30 pomieszczeń.
2. **System klas i obiektów:**
    * Każde pomieszczenie to obiekt z zestawem właściwości, takich jak:
        * Typ pomieszczenia: (zwykłe, zagadkowe, z bossem).
        * Połączenia: (wejście, wyjście, korytarze).
        * Elementy dodatkowe: (zagadki, pułapki, przeciwnicy, wystrój).

Algorytmy generowania

1. **Flood Fill Algorithm:**
    * Gwarantuje, że każde pomieszczenie jest połączone i zawsze istnieje droga między wejściem a wyjściem.
    * Działanie:
        * Wyznaczenie punktu startowego (wejścia).
        * Iteracyjne generowanie sąsiadujących pomieszczeń.
        * Wyznaczenie drogi do końca (wyjścia).
2. **Dynamiczne przypisywanie obiektów:**
    * **Ściany i wystrój:** Tworzone proceduralnie na podstawie kształtu i wymiarów pomieszczenia.
    * **Przeciwnicy:** Rozmieszczeni na podstawie typu pomieszczenia i poziomu trudności.
    * **Pułapki:** Losowo rozmieszczane, z uwzględnieniem logiki gry (np. nie mogą blokować jedynej ścieżki).

Rozwiązywanie problemów wizualnych i technicznych

1. **System boksów i monitorowanie:**
    * Każdy obiekt (np. przycisk, dźwignia) sprawdzany jest pod kątem:
        * Poprawnej lokalizacji w geometrii (np. przycisk na ścianie, a nie w powietrzu).
        * Dostępności dla gracza (np. czy nie koliduje ze ścianami).
2. **Przykład działania:**
    * Jeśli algorytm Flood Fill wygeneruje pustą przestrzeń, system automatycznie wypełnia ją domyślnym typem ściany i sprawdza, czy elementy w pokoju działają prawidłowo.

### Poziomy trudności

Normal i Heroic

1. **Cechy wspólne:**
    * Brak ukrytych bossów, super bossa i śmiertelnych pułapek.
    * Randomizacja obejmuje układ pomieszczeń, pułapki i przeciwników.
2. **Heroic:**
    * Mechanicznie trudniejszy (silniejsi przeciwnicy, więcej zagadek).
    * Większy rozmiar dungeona.

Mityczny

1. **Unikalne mechaniki:**
    * **Ukryci bossowie:** Proceduralne rozmieszczenie dodatkowych bossów, które można pokonać, by skrócić loch.
    * **Śmiertelne pułapki:** Pułapki, które mogą zakończyć dungeona, jeśli gracz popełni błąd.
    * **Super last boss:** Arcy Demon (lub kombinacja dwóch-trzech demonów), dostępny tylko na najwyższym piętrze.
2. **Randomizacja układu:**
    * Dynamiczne zmiany połączeń pomiędzy pomieszczeniami.
    * Proceduralne rozmieszczanie pułapek i elementów interaktywnych.

### Integracja mechanik bossów i pułapek

Bossowie

1. **Podział bossów:**
    * **Basic boss:** Stały zestaw przeciwników dostępny na każdym poziomie trudności.
    * **Hidden boss:** Opcjonalni bossowie dostępni na Mitycznym poziomie trudności.
    * **Super boss:** Arcy Demon, walka z nim jest dynamicznie generowana.
2. **System lokalizacji bossów:**
    * Algorytm umieszcza bossów w odpowiednich pomieszczeniach, sprawdzając:
        * Czy pomieszczenie ma odpowiedni rozmiar.
        * Czy dostęp do bossa jest logiczny w kontekście mapy.

Pułapki

1. **Typy pułapek:**
    * **Standardowe:** Minimalne obrażenia, proste wizualnie.
    * **Zaawansowane:** Mechaniczne zagadki, bardziej skomplikowane.
    * **Śmiertelne:** Tylko na Mitycznym poziomie, powodują natychmiastowe wyrzucenie gracza z lochu.
2. **Logika pułapek:**
    * System proceduralny losuje pułapki i sprawdza ich zgodność z otoczeniem:
        * Pułapki rozmieszczane są w pobliżu skrzyń, drzwi lub ścieżek prowadzących do ukrytych bossów.

### System proceduralnych boksów i prefabrykatów

Tworzenie klasy elementów

1. **Parametry klasy:**
    * Typ (ściana, korytarz, zagadka, przeciwnik).
    * Połączenia (z czym może się łączyć).
    * Funkcjonalność (np. dźwignia otwiera drzwi, przeciwnik patroluje teren).

Proceduralne losowanie i korekcja

1. **Algorytm losowania pułapek:**
    * Każdy boks zawiera zestaw obiektów, które są losowo wybierane:
        * Trzy szanse na dopasowanie pułapki do otoczenia.
        * Jeśli nie pasuje, wybierany jest obiekt z największym prawdopodobieństwem dopasowania.
2. **Algorytm przeciwników:**
    * Najpierw sprawdza, czy przeciwnik może istnieć w danej pozycji.
    * Jeśli nie, wyznacza najbliższą poprawną pozycję na podstawie lokalnego fragmentu mapy.

### Zakończenie dungeona

Standardowe zakończenie

* **Skarbiec:** Po pokonaniu Arcyczarnoksiężnika gracz zostaje odepchnięty do skarbca z nagrodami.
* **Medalion mocy:** Pozwala śledzić nową lokalizację lochu.

Super Boss i unikalne zakończenie

* **Super Boss:** Ostateczna walka z Arcy Demonem na najwyższym poziomie trudności.
* **Przeniesienie dungeona:** Po walce dungeon znika i pojawia się w nowej, losowej lokalizacji.

## Roziwzywanie problemów

### Parametry startowe mapy

**Problem: Jak zdefiniować elastyczne i precyzyjne parametry dla mapy dungeona?**

**Rozwiązanie:**

1. **Struktura mapy:**
    * **Dynamiczna siatka 3D:** Użycie dynamicznej siatki (grid-based procedural generation), która pozwala na zdefiniowanie:
        * **Długości, szerokości i wysokości** dungeona.
        * **Podziału na piętra:** Piętra są generowane w ramach tego samego systemu, z zachowaniem możliwości generowania korytarzy łączących poziomy.
2. **Użycie klas i obiektów:**
    * Każde pomieszczenie i korytarz traktowane jako obiekt klasy o następujących właściwościach:
        * **Właściwości geometryczne:** Rozmiar, typ połączeń, wysokość sufitu.
        * **Funkcja:** (np. zwykłe, zagadkowe, z bossem).
        * **Dynamiczne modyfikacje:** Klasa umożliwia modyfikowanie obiektów w trakcie generacji (np. wstawianie większych przeciwników do pomieszczenia).
3. **Ustalanie parametrów rozmiaru:**
    * Na początku generacji algorytm ustala maksymalną liczbę pomieszczeń, pięter i ich wzajemne relacje:
        * **Normalny poziom trudności:** Mała liczba pomieszczeń (10–15), proste połączenia.
        * **Heroiczny poziom trudności:** Więcej pomieszczeń (15–20), bardziej złożona struktura.
        * **Mityczny poziom trudności:** Rozbudowana struktura (20–30 pomieszczeń), w tym ukryte piętra i tajne przejścia.

### Algorytmy generowania

**Problem: Jak zapewnić poprawne generowanie mapy i połączeń między pomieszczeniami?**

**Rozwiązanie:**

1. **Flood Fill Algorithm:**
    * **Opis:** Flood Fill gwarantuje, że wszystkie pomieszczenia są połączone, a każda mapa ma co najmniej jedno wejście i wyjście.
    * **Działanie:**
        1. Algorytm zaczyna od punktu wejścia (start room).
        2. Iteracyjnie wypełnia sąsiadujące przestrzenie (pomieszczenia i korytarze), łącząc je w logiczny sposób.
        3. Wyznacza ścieżkę do punktu końcowego (exit room).
2. **Korygowanie mapy:**
    * **Backtracking:** Jeśli Flood Fill nie może wygenerować ścieżki do wyjścia, algorytm cofa się i generuje nowe połączenia.
    * **Random Walk Algorithm:** Można go użyć jako uzupełnienie Flood Fill, aby dodawać losowe odnogi i ślepe zaułki, co zwiększa różnorodność mapy.
3. **Dynamiczne przypisywanie obiektów:**
    * Każde pomieszczenie po wygenerowaniu struktury jest „uzupełniane” o zawartość:
        1. **Ściany i wystrój:** Generowane zgodnie z parametrami rozmiaru.
        2. **Przeciwnicy i pułapki:** Umieszczane na podstawie ich przypisanych klas (więcej w sekcji o systemie boksów).

### Rozwiązywanie problemów wizualnych i technicznych

**Problem: Jak uniknąć błędów wizualnych, takich jak unoszące się przedmioty lub źle umieszczone obiekty?**

**Rozwiązanie:**

1. **System boksów:**
    * Każdy obiekt proceduralny (np. pułapka, przycisk, przeciwnik) jest częścią „boksu,” który zawiera zestaw predefiniowanych właściwości:
        * **Lokalizacja:** Obiekt musi być przypisany do konkretnej przestrzeni w pomieszczeniu (np. pułapki muszą być na podłodze lub suficie).
        * **Zasady kompatybilności:** System sprawdza, czy obiekt pasuje do kontekstu (np. przycisk na ścianie).
2. **Algorytmy kontroli jakości:**
    * **Collision Check:** System sprawdza kolizję każdego obiektu przed jego umieszczeniem.
    * **Logic Check:** Każdy element musi być umieszczony zgodnie z logiką gry (np. dźwignie nie mogą być ukryte w niedostępnych miejscach).
3. **Automatyczna korekcja:**
    * Jeśli obiekt jest niepoprawnie umieszczony (np. zapadnia w powietrzu), algorytm automatycznie przemieszcza go do najbliższego poprawnego miejsca

**Poziomy trudności**:

#### Normal i Heroic

**Problem: Jak zdefiniować różnice w poziomach trudności między Normal i Heroic?**

**Rozwiązanie:**

1. **Charakterystyka poziomu trudności Normal:**
    * **Liczba pomieszczeń:** Ograniczona liczba, np. 10–15 pomieszczeń.
    * **Typy przeciwników:** Podstawowi wrogowie z minimalnymi umiejętnościami specjalnymi.
    * **Pułapki:** Standardowe, służące głównie jako element dekoracyjny, z minimalnym ryzykiem (np. powolne kolce, które łatwo ominąć).
    * **Zagadki:** Proste, z wyraźnymi wskazówkami (np. „Wciśnij ten przycisk, aby otworzyć drzwi”).
    * **Boss:** Jeden Basic Boss na końcu lochu.
2. **Charakterystyka poziomu trudności Heroic:**
    * **Liczba pomieszczeń:** Zwiększona (15–20), co wydłuża eksplorację.
    * **Typy przeciwników:** Silniejsze wersje wrogów z bardziej złożonymi mechanikami (np. wrogowie strzelający pociskami, teleportujący się).
    * **Pułapki:** Bardziej zaawansowane, z większą różnorodnością (np. wirujące ostrza, które poruszają się w określonym rytmie).
    * **Zagadki:** Wymagają większej spostrzegawczości, z ukrytymi mechanizmami (np. „Znajdź trzy ukryte przełączniki, aby otworzyć drzwi”).
    * **Boss:** Jeden Basic Boss z dodatkowymi mechanikami (np. faza nieśmiertelności, podczas której gracz musi rozwiązać zagadkę, aby kontynuować walkę).
3. **Mechaniczne różnice między poziomami:**
    * **Heroiczny poziom trudności:** Wprowadza zmienne takie jak:
        * Zwiększona liczba wrogów na pomieszczenie.
        * Mechanizmy, które wymagają bardziej dynamicznej reakcji gracza (np. unikanie stref obrażeń, przeciwnicy wymagający użycia określonych umiejętności).

#### Mityczny

**Problem: Jak zaprojektować poziom trudności, który jest unikalny, dynamiczny i regrywalny, jednocześnie wprowadzając nowe mechaniki?**

**Rozwiązanie:**

1. **Charakterystyka poziomu trudności Mityczny:**
    * **Liczba pomieszczeń:** 20–30 pomieszczeń, w tym dodatkowe piętra i tajne przejścia.
    * **Typy przeciwników:**
        * Wrogowie z unikalnymi zdolnościami (np. wrogowie leczący innych, osłaniający bossów, tworzący kopie siebie).
        * Proceduralne kombinacje przeciwników (np. grupy składające się z różnych typów wrogów współpracujących ze sobą).
    * **Pułapki:**
        * **Śmiertelne pułapki:** Mogą natychmiast zakończyć loch w przypadku błędu gracza.
        * **Dynamiczne pułapki:** Proceduralnie zmieniające się w trakcie gry (np. wirujące ostrza zmieniające prędkość, zapadnie pojawiające się w nowych miejscach).
    * **Zagadki:**
        * Wielowarstwowe zagadki, które wymagają interakcji w kilku pomieszczeniach.
        * Mechaniki czasowe (np. rozwiązanie zagadki w określonym czasie, zanim pomieszczenie wypełni się toksyną).
    * **Bossowie:**
        * **Hidden Boss:** Opcjonalni bossowie, którzy pojawiają się w ukrytych pomieszczeniach i pozwalają skrócić loch po ich pokonaniu.
        * **Super Last Boss:** Walka z jednym, dwoma lub trzema Arcy Demonami, gdzie mechanika jest dynamicznie generowana (np. losowe efekty obszarowe, fazy bossów zmieniające się w czasie rzeczywistym).
2. **Specjalne mechaniki Mitycznego poziomu trudności:**

    **a) Dynamiczne zmiany połączeń:**

    * Proceduralnie zmieniające się korytarze i połączenia między pomieszczeniami podczas rozgrywki.
        * **Przykład:** Po ukończeniu jednej zagadki otwiera się nowa ścieżka, a poprzednia staje się niedostępna.

    **b) Proceduralne rozmieszczenie ukrytych bossów i pułapek:**

    * Hidden Bossowie pojawiają się losowo na podstawie algorytmu sprawdzającego ich zgodność z typem pomieszczenia.
    * Pułapki umieszczane są z użyciem systemu boksów (opisany w sekcji 4).

    **c) Dynamiczne wydarzenia:**

    * Mityczny poziom trudności może wprowadzać losowe wydarzenia w trakcie rozgrywki:
        * Pojawienie się nowych wrogów w korytarzu, który wcześniej był pusty.
        * Zmiana warunków w pomieszczeniu (np. pojawienie się toksycznej mgły, która zmusza gracza do szybszego działania).

3. Integracja mechanik bossów i pułapek

### Bossowie

**Problem: Jak zaprojektować system proceduralnego umieszczania bossów i ich mechanik, aby były spójne z resztą mapy i poziomem trudności?**

**Rozwiązanie:**

1. **Podział bossów:**
    * **Basic Boss:** Stały zestaw bossów, pojawiający się na końcu dungeona we wszystkich poziomach trudności.
    * **Hidden Boss:** Opcjonalni bossowie, rozmieszczeni losowo w ukrytych pomieszczeniach na poziomie Mitycznym.
    * **Super Boss (Arcy Demon):** Ostateczny boss, generowany wyłącznie na najwyższym piętrze dungeona na poziomie Mitycznym.
2. **Mechanika proceduralnego rozmieszczania bossów:**
    * Każdy boss jest przypisany do swojej klasy z właściwościami, takimi jak:
        * Typ pomieszczenia, w którym może być umieszczony (np. duże sale, areny).
        * Minimalna i maksymalna liczba wrogów towarzyszących (np. Basic Boss na Normalnym poziomie ma 1–2 wrogów pomocniczych).
        * Wymagania przestrzenne (np. boss latający potrzebuje większego sufitu).
3. **Algorytm rozmieszczania bossów:**
    * **Kroki:**
        * Algorytm wybiera odpowiednie pomieszczenie na mapie, sprawdzając:
            * Czy ma wystarczająco miejsca na walkę z bossem i jego mechaniki.
            * Czy znajduje się w logicznym miejscu w strukturze dungeona (np. blisko końca mapy).
        * Jeśli pomieszczenie nie spełnia warunków, algorytm przeszukuje pobliskie segmenty mapy, aby znaleźć lepsze dopasowanie.
        * Boss jest rozmieszczany, a dodatkowe elementy (np. pułapki lub wrogowie pomocniczy) są generowane proceduralnie wokół niego.
4. **Mechaniki walk bossów:**
    * **Basic Boss:**
        * Mechaniki na poziomie Normalnym:
            * Stałe ataki, łatwe do przewidzenia.
            * Proste fazy (np. zwiększona prędkość ataku po utracie połowy zdrowia).
        * Mechaniki na poziomie Heroicznym:
            * Ataki specjalne (np. obrażenia obszarowe).
            * Przerwy w walce, podczas których gracz musi rozwiązać mini-zagadkę (np. wciśnięcie dźwigni, aby przerwać fazę nieśmiertelności).
    * **Hidden Boss:**
        * Wyjątkowe umiejętności, takie jak:
            * Przywoływanie innych przeciwników.
            * Mechaniki wymagające współpracy w grze wieloosobowej (np. gracz musi odwrócić uwagę bossa, aby inni mogli zadać obrażenia).
    * **Super Boss (Arcy Demon):**
        * Fazy dynamicznie zmieniające się w zależności od poziomu trudności:
            * Na Mitycznym poziomie może losowo zmieniać swoje typy ataków (np. ogień, lód, trucizna).
            * Zmiany w środowisku podczas walki (np. wypełnienie pomieszczenia lawą, wymuszające szybsze poruszanie się).

### Pułapki

**Problem: Jak wprowadzić dynamiczne i logiczne rozmieszczanie pułapek, które nie tylko utrudniają rozgrywkę, ale również są zintegrowane z mechaniką dungeona?**

**Rozwiązanie:**

1. **Podział pułapek:**
    * **Standardowe:** Dekoracyjne i proste mechanizmy (np. kolce wysuwające się z podłogi, łatwe do uniknięcia).
    * **Zaawansowane:** Mechaniczne zagadki wymagające interakcji (np. wirujące ostrza, które trzeba zatrzymać, włączając odpowiedni przełącznik).
    * **Śmiertelne:** Na poziomie Mitycznym, natychmiast kończące rozgrywkę w lochu (np. zapadnie prowadzące do piekielnej przepaści).
2. **Algorytm rozmieszczania pułapek:**
    * **Kroki:**
        1. Każde pomieszczenie posiada przypisany **boks pułapek**, który zawiera 20 różnych typów pułapek.
        2. Procedura losowania pułapek (z trzykrotną próbą dopasowania):
            * Pierwsze losowanie: Sprawdzenie, czy wybrana pułapka pasuje do pomieszczenia.
            * Drugie losowanie: Jeśli pierwsza próba się nie uda, pułapka trafia na listę oczekujących, a system wybiera kolejną.
            * Trzecie losowanie: Jeśli nadal brak dopasowania, system przypisuje pułapkę o największym prawdopodobieństwie pasowania.
        3. Jeśli żadna pułapka nie pasuje, pomieszczenie pozostaje bez pułapek.
3. **Logika działania pułapek:**
    * **Zależność od typu pomieszczenia:**
        1. Zapadnie umieszczane w długich korytarzach.
        2. Wirujące ostrza w większych przestrzeniach, gdzie gracz ma szansę ich unikać.
    * **Złożoność pułapek:**
        3. Na Normalnym poziomie: Jednostajne działanie (np. powolne wysuwanie kolców).
        4. Na Mitycznym poziomie: Dynamiczne zmiany zachowania (np. ostrza zmieniające prędkość, zapadnie pojawiające się w losowych miejscach).
4. **Procedura korekcji pozycji:**
    * Jeśli pułapka zostanie umieszczona w nieodpowiednim miejscu (np. kolce w ścianie):
        5. Algorytm przeszukuje najbliższe dostępne pozycje, aby poprawić jej umieszczenie.
        6. Jeśli korekcja jest niemożliwa, pułapka zostaje usunięta.

**System proceduralnych boksów i prefabrykatów**:

#### Tworzenie klasy elementów

**Problem: Jak zbudować uniwersalny system klas i prefabrykatów, który pozwoli dynamicznie generować elementy dungeona bez błędów?**

**Rozwiązanie:**

1. **Klasa elementu proceduralnego:**
    * Każdy element w dungeonach jest traktowany jako obiekt klasy z następującymi właściwościami:
        * **Typ elementu:**
            * Pomieszczenie (zwykłe, zagadkowe, arena bossa).
            * Pułapka (kolce, ostrza, zapadnie).
            * Przedmiot interaktywny (przycisk, dźwignia, portal).
            * Przeciwnik (standardowy mob, boss).
        * **Lokalizacja:**
            * Koordynaty XYZ w przestrzeni dungeona.
        * **Zależności przestrzenne:**
            * Określenie, czy element wymaga podłogi, ściany, sufitu lub swobodnej przestrzeni.
        * **Logika działania:**
            * Definicja funkcji elementu (np. aktywacja dźwigni otwiera drzwi, przeciwnik patroluje obszar).
2. **Hierarchia klas:**
    * **Bazowa klasa elementu (ElementBase):**
        * Właściwości wspólne dla wszystkich elementów (np. pozycja, typ, stan aktywacji).
    * **Klasy dziedziczące:**
        * Każdy typ elementu (pułapka, przeciwnik, pomieszczenie) dziedziczy po bazowej klasie i dodaje unikalne właściwości.
            * **Przykład dla pułapki:**
                * Typ działania (np. wysuwanie kolców).
                * Promień aktywacji (czy uruchamia się, gdy gracz znajdzie się w pobliżu).
            * **Przykład dla przeciwnika:**
                * Ścieżka patrolu.
                * Typ ataku.
3. **Prefabrykaty jako podstawowe jednostki:**
    * **Prefabrykat (Prefab):** Gotowy zestaw elementów, który może być użyty w dowolnym miejscu mapy:
        * **Przykład prefabrykatu:** Pomieszczenie z dźwignią, która aktywuje zapadnię.
    * **Dynamiczne dostosowanie prefabrykatów:**
        * Prefabrykaty adaptują się do rozmiaru pomieszczenia i kontekstu mapy (np. rozszerzenie lub zmniejszenie obszaru pułapek w zależności od dostępnej przestrzeni).

#### Proceduralne losowanie i korekcja

**Problem: Jak efektywnie losować elementy i poprawiać ich pozycję, aby zapobiec błędom graficznym i mechanicznym?**

**Rozwiązanie:**

1. **System boksów:**
    * **Czym jest boks:** Każdy boks to kontener (plecak) zawierający elementy do losowania w określonym typie pomieszczenia.
        * **Przykład boksu dla pułapek:** Zawiera 20 różnych pułapek (np. zapadnie, wirujące ostrza).
        * **Przykład boksu dla przeciwników:** Zawiera wrogów dostosowanych do poziomu trudności (np. bossów dla Mitycznego poziomu).
    * **Losowanie elementów:**
        * Procedura losowania składa się z trzech prób:
            1. **Pierwsze losowanie:** Algorytm wybiera losowy element z boksu i sprawdza jego dopasowanie do mapy.
            2. **Drugie losowanie:** Jeśli pierwszy element nie pasuje (np. kolce umieszczone w powietrzu), zostaje tymczasowo usunięty, a system wybiera kolejny.
            3. **Trzecie losowanie:** Jeśli drugi element również nie pasuje, system wybiera element z największym prawdopodobieństwem dopasowania.
        * Jeśli po trzech próbach element nie pasuje, pomieszczenie pozostaje bez tego typu obiektu.
2. **Korekcja pozycji:**
    * Jeśli element jest umieszczony niepoprawnie (np. przeciwnik poza granicami mapy):
        * Algorytm przeszukuje lokalny fragment mapy, aby znaleźć najbliższe miejsce zgodne z logiką gry.
        * **Przykład:** Zapadnia zostaje przeniesiona na najbliższą dostępną podłogę.
3. **Zabezpieczenie przed błędami:**
    * **Collision Check:** Każdy element jest sprawdzany pod kątem kolizji z innymi obiektami.
    * **Logic Check:** Sprawdzane są zależności przestrzenne (np. przycisk musi być na ścianie, a nie w powietrzu).
    * **Fallback Mechanism:** Jeśli element nadal nie pasuje, zostaje zastąpiony neutralnym prefabrykatem (np. pusta ściana).

#### Integracja z mapą

**Problem: Jak połączyć system boksów z generowaniem mapy, aby wszystkie elementy działały spójnie?**

**Rozwiązanie:**

1. **Przypisanie boksów do pomieszczeń:**
    * Każde pomieszczenie podczas generacji otrzymuje zestaw boksów zgodnych z jego typem.
        * **Przykład:** Arena bossa otrzymuje boks bossów, a korytarz — boks pułapek.
    * Algorytmy losowania i korekcji są wywoływane osobno dla każdego typu elementu.
2. **Dynamiczna adaptacja prefabrykatów:**
    * Prefabrykaty są skalowane i dostosowywane w trakcie generacji mapy:
        * Jeśli pomieszczenie jest większe niż prefabrykat, system dodaje dodatkowe elementy (np. więcej pułapek).
        * Jeśli pomieszczenie jest mniejsze, prefabrykat zostaje uproszczony.
3. **Iteracyjna kontrola mapy:**
    * Po zakończeniu generacji mapy system przeprowadza iterację przez wszystkie pomieszczenia:
        * Sprawdza zgodność elementów z mapą.
        * Poprawia lub usuwa elementy, które nie pasują.

**Zakończenie dungeona**:

#### Standardowe zakończenie: Skarbiec

**Problem: Jak zaprojektować zakończenie dungeona w sposób, który zawsze zapewni logiczną i satysfakcjonującą konkluzję bez zaburzania ciągłości rozgrywki?**

**Rozwiązanie:**

1. **Mechanika zakończenia dungeona:**
    * Po pokonaniu głównego bossa (Basic Boss lub Super Boss) gracz nie kończy dungeona od razu.
    * Zamiast tego:
        * Boss wykonuje ostatni ruch fabularny, np. odepchnięcie gracza do **skarbcowej sali**, pozostawiając za sobą klucz lub artefakt.
        * Arcyczarnoksiężnik zawsze **ucieka**, zachowując możliwość regrywalności dungeona w nowej lokalizacji.
2. **Skarbiec:**
    * **Charakterystyka:**
        * To ostatnia sala dungeona, zawierająca dynamicznie generowane skarby.
        * Gracz ma ograniczony czas na zebranie nagród przed uruchomieniem mechanizmów ochronnych (np. aktywacja pułapek lub strażników).
    * **Dynamiczna zawartość:**
        * Proceduralny system losuje zawartość skarbca w momencie wejścia gracza.
        * Mechanika „szczęścia” zwiększa prawdopodobieństwo otrzymania rzadkich przedmiotów przy większym wysiłku (np. na Mitycznym poziomie trudności).
3. **Wyjście z dungeona:**
    * Po opuszczeniu skarbca gracz musi znaleźć wyjście:
        * Wyjście jest zawsze dostępne i prowadzi do **początkowego punktu mapy**.
        * Na poziomie Mitycznym mogą pojawić się nowe wyzwania w trakcie ucieczki (np. odrodzeni przeciwnicy, aktywowane pułapki).

#### Unikalne zakończenie na poziomie Mitycznym

**Problem: Jak stworzyć epickie zakończenie na najwyższym poziomie trudności, które wyróżni się fabularnie i mechanicznie?**

**Rozwiązanie:**

1. **Super Boss i najwyższa sala:**
    * **Super Last Boss (Arcy Demon):**
        * Ostateczna walka odbywa się w dynamicznie generowanej sali finałowej.
        * **Mechaniki walki:**
            * Losowe zmiany w środowisku (np. sala wypełniająca się lawą, zmniejszająca przestrzeń walki).
            * Dynamiczne fazy bossa:
                * Na początku walka z jednym Arcy Demonem.
                * W późniejszych fazach mogą pojawić się dodatkowe demony (np. dwóch lub trzech naraz).
        * Gracz musi pokonać Super Bossa, aby „rozbić” dungeona i zmusić Arcyczarnoksiężnika do przeniesienia swojej twierdzy.
2. **Przeniesienie dungeona:**
    * Po pokonaniu Arcy Demona dungeon zostaje **przeniesiony do nowej lokalizacji** na mapie świata.
    * **Mechanika przenoszenia:**
        * Gracz otrzymuje **Medalion Mocy**, który pozwala śledzić, gdzie dungeon się pojawi.
        * Każda nowa lokalizacja wprowadza zmienione elementy, np. nowe wrogów, unikalne zagadki, modyfikacje mapy.
3. **Dynamiczna regrywalność:**
    * Po ukończeniu Mitycznego poziomu trudności dungeon pozostaje dostępny, ale:
        * Zmienia swoje wyzwania, aby zachować świeżość (np. inny układ pomieszczeń, nowe bossy, dodatkowe pułapki).
        * Nagrody są wciąż losowe, ale ich rzadkość wzrasta przy kolejnych podejściach.

#### Mechanizmy zabezpieczające i optymalizujące zakończenie

**Problem: Jak uniknąć błędów w zakończeniu, takich jak brak wyjścia, źle rozmieszczone elementy czy niespójności w fabule?**

**Rozwiązanie:**

1. **Spójność fabularna:**
    * Mechanika ucieczki Arcyczarnoksiężnika jest zawsze aktywna — fabularnie nigdy nie ginie.
    * Każde zakończenie prowadzi do skarbca, co zapewnia graczowi nagrodę bez względu na poziom trudności.
2. **Automatyczna kontrola mapy:**
    * Przed udostępnieniem wyjścia system przeprowadza finalny „test jakości”:
        * Czy wszystkie ścieżki prowadzą do skarbca i wyjścia?
        * Czy w skarbcu znajdują się odpowiednie nagrody?
        * Czy nie ma błędów kolizji lub brakujących elementów mapy.
3. **Fail-Safe Mechanisms (zabezpieczenia awaryjne):**
    * Jeśli z jakiegoś powodu gracz nie może znaleźć wyjścia:
        * System generuje awaryjny teleport w skarbcu, prowadzący gracza do bezpiecznej lokalizacji.
    * Jeśli boss nie został poprawnie wygenerowany:
        * System automatycznie tworzy kopię zapasową areny z alternatywnym bossem.

---

Po pokonaniu dungeona niezależnie od jakiego poziomu trudności dostajemy cooldown na wejście na jeden tydzień (po pokonaniu to znaczy że możemy do niego wchodzić ile razy chcemy i go resetować aż go nie pokonamy ) cooldown jest nakładany na dany poziom trudności oczywiście jeżeli pokonamy wpierw mityczny poziom trudności to będziemy musieli znaleźć nową lokację dungeonu  i dopiero wtedy będziemy mogli podjąć inne poziomy trudności. Najlepsza strategia wpierw pokonać dwa pierwsze poziomy trudności a dopiero ostatni aby zwiększyć zysk do maksimum.

**Przedmioty fabularne**:

Medalion mocy -> pozwala śledzić gdzie znajduję się legendarny dungeon ale aby go użyć wpierw trzeba go naładować mocą.

**Bryłka dwojakiej legendarności**:

Przedmiot który może wypaść (Bardzo duża szansa ale nie pewnik)

Jężeli będziemy walczyć na najwyższym poziomie trudności i akurat wylosuje nam 3 arcydemonów (strategia jak najszybciej zdobyć bryłkę otóż wystarczy że będziemy resstować dungeon aż w końcu wylosuje nam do pokonania 3 arcydemonów i wtedy je pokonamy iaczenj po pokonaniu legendarnego dungeona będziemy musieli czekać  na następne wejście aż tydzień)

Alternatywą dostania się do legendarnego dungeona będą mini gry w karczmach, gospodach ,tawernach w których możemy zagrać z odpowiednim npc gdy dużo czasu spędzamy tam trafić może nam się npc od właśnie takich wydarzeń co może nam pomóc w uzyskaniu passu do legendarnego dungeonu.
