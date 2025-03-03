# System Craftowania

Craftowanie to sztuka, którą studiujemy w Gildii Tworzenia. Jest to gildia, która łączy ze sobą mistrzów:

- **Kowalstwo** (jeden NPC):
  - Kowal Broni
  - Kowal Pancerzy
  - Mistrz Obróbki Metalu
- **Szwactwo**:
  - Krawiec
  - Tkacz
  - Rzemieślnik Tkanin
  - Wyszywacz Zaklęć (dla magicznych szat)
- **Złotnictwo**:
  - Jubiler
  - Rzemieślnik Biżuterii
  - Mistrz Kamieni Szlachetnych
- **Ciesielstwo**:
  - Stolarz
  - Twórca Mebli
  - Konstruktor Broni Drewnianych (np. łuki, kusze)
- **Garncarstwo**:
  - Mistrz Ceramiki
  - Twórca Amfor
  - Specjalista Rytualnych Naczyń
- **Skórnictwo**:
  - Rymarz
  - Kuśnierz
  - Twórca Skórzanych Pancerzy
- **Magiczne Tworzenie**:
  - Zaklinacz
  - Twórca Artefaktów
  - Konstruktor Magicznych Run
- **Inżynieria**:
  - Mechanik
  - Konstruktor Pułapek
  - Mistrz Ruchomych Mechanizmów
- **Gotowanie**:
  - Szef Kuchni
  - Twórca Specjalnych Mikstur Żywieniowych
  - Pieczeniarz Królewski
- **Kamieniarstwo**:
  - Rzeźbiarz
  - Twórca Monumentów
  - Konstruktor Runicznych Kolumn
- **Zegarmistrzostwo**:
  - Twórca Mechanizmów Precyzyjnych
  - Konstruktor Magicznych Zegarków
- **Szklane Rzemiosło**:
  - Twórca Witraży
  - Konstruktor Fiolki i Ampułek
  - Rzemieślnik Ozdobnych Luster
- **Eksperymentalne Tworzenie**:
  - Eksperymentator Przedmiotów Nieznanych
  - Twórca Hybrydowych Mechanizmów

*Profesje związane z dekoracjami znajdą się w jendej kategorii.*

Istnieje 13 opcji warsztatowych do nauki. Każda opcja reprezentuje sztukę, którą terminuje się w Gildii. Poziom wtajemiczenia każdej z nich przedstawiany jest za pomocą paska postępu, którego maksymalny poziom wynosi **100**.

Osiągnięcie mistrzostwa danej sztuki pozwala tworzyć znacznie lepsze, rzadsze i bardziej wartościowe przedmioty w grze oraz wzmacnia postać gracza, wpływając na jej statystyki.

Sztuki mogą dzielić się na:

- **Sztuki domowe**
- **Sztuki płatnerskie**
- **Sztuki piękne**

Aby uzyskać dyplom ukończenia Gildii, należy zdać wszystkie przedmioty. Oznacza to ukończenie questów oraz podejście do testów i osiągnięcie wyniku przynajmniej 75% w każdym z nich. Każdy test końcowy będzie inny, a ukończenie testu na poziomie 75% lub wyższym dodatkowo zapewnia specjalne skille dla każdej profesji. Do testów końcowych można podchodzić nieskończenie wiele razy, jednak każde podejście kosztuje złoto.

## System obliczania poziomu każdej ze sztuk

Następująca formuła określa, ile punktów w danej sztuce musimy zdobyć, aby osiągnąć wyższy poziom wtajemniczenia.

```text
n - typ sztuki
Poziom typu sztuki = Poziom typu sztuki + 8*n + 1
```

## Mini-gry

Podczas praktykowania profesji, gracz bierze udział w mini-grach. Ich poziom trudności rośnie wraz z poziomem wtajemniczenia, np. poprzez wprowadzanie bardziej złożonych sekwencji działań lub etapów (w złotnictwie gracz będzie potrzebował osadzić więcej kamieni w określonym czasie).

Każda mini-gra posiada nieznaczne podpowiedzi w postaci błysków graficznych, które wskażą graczowi, jak wykonać dane czynności.

### Spis mini-gier

Lista mini-gier znajduje się w dokumencie [Spis Mini-gier Craftowania](../Spisy/SpisMiniGierCraftowania.md).

## Interfejs

Do przedstawienia graficznego tego modelu wykorzystuje się pasek postępu, który ładuje się od 0% do 100% z każdą wykonaną pracę w danej sztuce.

**Wzór**:

```text
Bar = 100%
Development = Poziom typu sztuki / Bar
```

Lub bardziej zrozumiale:

```text
Development = Poziom typu sztuki / 100%
```

## System dodatkowych statystyk

Wraz ze stawaniem się lepszym w danej sztuce, gracz otrzymuje dodatkowe statystyki. Statystyki otrzymywane są co 5 poziomów zdobytych w danym typie sztuki.

Przykład:

```text
n - indeks poziomu gwarantującego bonus
```

| Poziom wtajemniczenia | Indeks |
|-----------------------|--------|
| Poziom 5              | n = 1  |
| Poziom 10             | n + 1  |
| Poziom 15             | n + 2  |
| ... | |

### Bonusowe statystyki

Statystyki obliczane są następująco:

- **Attack speed bonus** = Attack speed bonus + 1 * n
- **Casting speed bonus** = Casting speed bonus + 1 * n
- **Charisma bonus** = Charisma bonus + 1 * n
- **Crafting bonus** = Crafting bonus + 1 * n
- **Dexterity bonus** = Dexterity bonus + 1 * n
- **Gold bonus** = Gold bonus + 1 * n
- **HP bonus** = HP bonus + 20 * n
- **Intelligence bonus** = Intelligence bonus + 1 * n
- **Kleptomancy bonus** = Kleptomancy bonus + 1 * n
- **Luck bonus** = Luck bonus + 1 * n
- **MP bonus** = MP bonus + 1 * n
- **Mentality bonus** = Mentality bonus + 1 * n
- **PvE Magical Damage bonus** = PvE Magical Damage bonus + 0.1 * n
- **PvE Physical Damage bonus** = PvE Physical Damage bonus + 0.1 * n
- **PvP Magical Damage bonus** = PvP Magical Damage bonus + 0.1 * n
- **PvP Physical Damage bonus** = PvP Physical Damage bonus + 0.1 * n
- **Strength bonus** = Strength bonus + 1 * n
- **Vitality bonus** = Vitality bonus + 1 * n

Dane sztuki wpływają na następujące statystyki:

#### Kowalstwo

- Strength bonus
- Vitality bonus
- HP bonus
- PvE Physical Damage bonus
- PvE Magical Damage bonus
- Crafting bonus

#### Szwactwo

- Dexterity bonus
- Vitality bonus
- Attack speed bonus
- Casting speed bonus
- PvE Physical Damage bonus
- PvE Magical Damage bonus
- Crafting bonus

#### Złotnictwo

- Intelligence bonus
- Mentality bonus
- Luck bonus
- Kleptomancy bonus
- PvE Physical Damage bonus
- PvE Magical Damage bonus
- Crafting bonus

#### Ciesielstwo

- Intelligence bonus
- Dexterity bonus
- Luck bonus
- Strength bonus
- PvE Physical Damage bonus
- PvE Magical Damage bonus
- Crafting bonus

#### Garncarstwo

- Attack speed bonus
- Casting speed bonus
- Luck bonus
- Kleptomancy bonus
- PvE Physical Damage bonus
- PvE Magical Damage bonus
- Crafting bonus

#### Skórnictwo

- PvP Physical Damage bonus
- PvP Magical Damage bonus
- Luck bonus
- Kleptomancy bonus
- PvE Physical Damage bonus
- PvE Magical Damage bonus
- Crafting bonus

#### Magiczne Tworzenie

- Intelligence bonus
- Mentality bonus
- Luck bonus
- MP bonus
- PvE Physical Damage bonus
- PvE Magical Damage bonus
- Crafting bonus

#### Inżynieria

- Intelligence bonus
- Dexterity bonus
- Luck bonus
- Kleptomancy bonus
- PvE Physical Damage bonus
- PvE Magical Damage bonus
- Crafting bonus

#### Gotowanie

- Attack speed bonus
- Casting speed bonus
- Luck bonus
- Gold bonus
- Charisma bonus
- PvE Physical Damage bonus
- PvE Magical Damage bonus
- Crafting bonus

#### Kamieniarstwo

- Strength bonus
- Vitality bonus
- Intelligence bonus
- PvE Physical Damage bonus
- PvE Magical Damage bonus
- Crafting bonus

#### Zegarmistrzostwo

- Dexterity bonus
- Intelligence bonus
- PvE Physical Damage bonus
- PvE Magical Damage bonus
- Crafting bonus

#### Szklane Rzemiosło

- Dexterity bonus
- Vitality bonus
- Attack speed bonus
- Casting speed bonus
- Intelligence bonus
- PvE Physical Damage bonus
- PvE Magical Damage bonus
- Crafting bonus

#### Eksperymentalne Tworzenie

- Strength bonus
- Dexterity bonus
- Vitality bonus
- Attack speed bonus
- Casting speed bonus
- HP bonus
- MP bonus
- Gold bonus
- Charisma bonus
- PvP Physical Damage bonus
- PvP Magical Damage bonus
- Crafting bonus

## Propozycja programu realizującego dany problem

```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
#include <conio.h>
#include <chrono>
#include <thread>
#include <string>
#include <vector>
#include <map>
#include <algorithm>
 
// Klasa bazowa dla wszystkich profesji
class Rzemieslnik {
protected:
    std::string nazwa_profesji;
    int poziom;
    int doswiadczenie;
    int doswiadczenie_do_nastepnego_poziomu;
    int n; // Indeks dla systemu piątek
 
    // Statystyki ogólne
    std::map<std::string, double> statystyki;
 
public:
    Rzemieslnik(std::string nazwa) : nazwa_profesji(nazwa), poziom(1), doswiadczenie(0), doswiadczenie_do_nastepnego_poziomu(0), n(0) {
        oblicz_doswiadczenie_do_nastepnego_poziomu();
        inicjalizuj_statystyki();
        srand(static_cast<unsigned int>(time(0)));
    }
 
    virtual void menu() = 0; // Metoda wirtualna dla menu profesji
 
    virtual void wykonaj_minigre() = 0; // Metoda wirtualna dla mini-gier
 
    void oblicz_doswiadczenie_do_nastepnego_poziomu() {
        int n_local = poziom;
        doswiadczenie_do_nastepnego_poziomu = doswiadczenie + 3 * n_local + (5 * n_local + 1);
    }
 
    void zdobywaj_doswiadczenie(int ilosc) {
        doswiadczenie += ilosc;
        std::cout << "Zdobyto " << ilosc << " punktów doświadczenia.\n";
        sprawdz_awans();
    }
 
    void sprawdz_awans() {
        while (doswiadczenie >= doswiadczenie_do_nastepnego_poziomu) {
            awansuj();
        }
    }
 
    void awansuj() {
        poziom++;
        std::cout << "Gratulacje! Awansowałeś na poziom " << poziom << " w profesji " << nazwa_profesji << ".\n";
        oblicz_doswiadczenie_do_nastepnego_poziomu();
 
        if (poziom % 5 == 0) {
            n++;
            aktualizuj_statystyki();
        }
    }
 
    virtual void aktualizuj_statystyki() = 0; // Metoda wirtualna dla aktualizacji statystyk
 
    void wypisz_statystyki() {
        std::cout << "Statystyki dla profesji " << nazwa_profesji << ":\n";
        for (const auto& [klucz, wartosc] : statystyki) {
            std::cout << klucz << ": " << wartosc << "\n";
        }
    }
 
    void wypisz_stan() {
        std::cout << "Poziom: " << poziom << "\n";
        std::cout << "Doświadczenie: " << doswiadczenie << "/" << doswiadczenie_do_nastepnego_poziomu << "\n";
    }
 
    void inicjalizuj_statystyki() {
        // Inicjalizacja statystyk na 0
        statystyki = {
            {"strength", 0},
            {"vitality", 0},
            {"hp", 0},
            {"intelligence", 0},
            {"mentality", 0},
            {"dexterity", 0},
            {"attack_speed", 0},
            {"casting_speed", 0},
            {"luck", 0},
            {"mp", 0},
            {"gold_bonus", 0},
            {"charisma", 0},
            {"pve_physical_dmg", 0},
            {"pve_magical_dmg", 0},
            {"pvp_physical_dmg", 0},
            {"pvp_magical_dmg", 0},
            {"crafting_bonus", 0},
            {"kleptomancy", 0}
        };
    }
};
 
// Implementacje poszczególnych profesji
 
// 1. Kowal
class Kowal : public Rzemieslnik {
public:
    Kowal() : Rzemieslnik("Kowal") {}
 
    void menu() override {
        char wybor;
        do {
            std::cout << "Profesja: " << nazwa_profesji << "\n";
            std::cout << "1. Tworzyć przedmiot\n";
            std::cout << "2. Sprawdzić statystyki\n";
            std::cout << "3. Wyjść\n";
            std::cin >> wybor;
 
            switch (wybor) {
                case '1':
                    wykonaj_minigre();
                    break;
                case '2':
                    wypisz_stan();
                    wypisz_statystyki();
                    break;
                case '3':
                    std::cout << "Powrót do głównego menu.\n";
                    break;
                default:
                    std::cout << "Nieznana opcja.\n";
                    break;
            }
            std::cout << "------------------------\n";
        } while (wybor != '3');
    }
 
void wykonaj_minigre() override {
    std::cout << "Rozpoczynasz tworzenie przedmiotu jako " << nazwa_profesji << ".\n";
 
    // Krok 1: Przygotowanie Młota
    std::cout << "Aby chwycić młot, wciśnij jednocześnie klawisze 'L' i 'P'. Masz 2 sekundy.\n";
    auto start = std::chrono::steady_clock::now();
    bool lewy_przycisk = false;
    bool prawy_przycisk = false;
 
    while (std::chrono::steady_clock::now() - start < std::chrono::seconds(2)) {
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'L' || ch == 'l') {
                lewy_przycisk = true;
            } else if (ch == 'P' || ch == 'p') {
                prawy_przycisk = true;
            }
            if (lewy_przycisk && prawy_przycisk) {
                break;
            }
        }
    }
 
    if (!(lewy_przycisk && prawy_przycisk)) {
        std::cout << "Nie udało Ci się chwycić młota.\n";
        return;
    }
 
    std::cout << "Chwyciłeś młot!\n";
 
    // Krok 2: Rozgrzewanie Metalu
    std::cout << "Utrzymuj temperaturę metalu w odpowiednim zakresie (70-100) przez 5 sekund.\n";
    int temperatura = 85; // Początkowa temperatura
    auto czas_konca = std::chrono::steady_clock::now() + std::chrono::seconds(5);
    while (std::chrono::steady_clock::now() < czas_konca) {
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'W' || ch == 'w') {
                temperatura += 5;
            } else if (ch == 'S' || ch == 's') {
                temperatura -= 5;
            }
        }
 
        // Symulacja zmiany temperatury
        temperatura += (rand() % 3 - 1); // Losowa zmiana temperatury
 
        // Wyświetlanie aktualnej temperatury
        std::cout << "Temperatura: " << temperatura << "   \r";
        std::cout.flush();
 
        // Sprawdzenie, czy temperatura jest w odpowiednim zakresie
        if (temperatura < 70 || temperatura > 100) {
            std::cout << "\nTemperatura poza zakresem! Proces nie powiódł się.\n";
            return;
        }
 
        std::this_thread::sleep_for(std::chrono::milliseconds(500));
    }
 
    std::cout << "\nTemperatura utrzymana w odpowiednim zakresie!\n";
 
    // Krok 3: Kucie Metalu
    std::cout << "Wykonaj sekwencję klawiszy: 'A', 'D', 'A', 'W'. Masz 5 sekund.\n";
    std::string sekwencja = "ADAW";
    std::string wprowadzona_sekwencja;
    start = std::chrono::steady_clock::now();
    while (wprowadzona_sekwencja.length() < sekwencja.length() && std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        if (_kbhit()) {
            char ch = _getch();
            wprowadzona_sekwencja += toupper(ch);
            std::cout << ch;
        }
    }
 
    if (wprowadzona_sekwencja != sekwencja) {
        std::cout << "\nNie udało Ci się wykonać poprawnej sekwencji.\n";
        return;
    }
 
    std::cout << "\nPoprawnie wykonałeś sekwencję!\n";
 
    // Krok 4: Hartowanie
    std::cout << "Wciśnij klawisz 'H' w momencie, gdy wskaźnik znajdzie się w zielonej strefie (4-6).\n";
    int wskaznik = 0;
    bool sukces = false;
    for (int i = 0; i < 20; ++i) {
        wskaznik = i % 10;
        std::cout << "Wskaźnik: " << wskaznik << "   \r";
        std::cout.flush();
 
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'H' || ch == 'h') {
                if (wskaznik >= 4 && wskaznik <= 6) {
                    sukces = true;
                    break;
                } else {
                    break;
                }
            }
        }
        std::this_thread::sleep_for(std::chrono::milliseconds(200));
    }
 
    if (!sukces) {
        std::cout << "\nNie udało Ci się zahartować przedmiotu w odpowiednim momencie.\n";
        return;
    }
 
    std::cout << "\nUdało Ci się stworzyć przedmiot!\n";
    zdobywaj_doswiadczenie(10);
}
    void aktualizuj_statystyki() override {
        statystyki["strength"] += 1 * n;
        statystyki["vitality"] += 1 * n;
        statystyki["hp"] += 20 * n;
        statystyki["pve_physical_dmg"] += 0.1 * n;
        statystyki["pve_magical_dmg"] += 0.1 * n;
        statystyki["crafting_bonus"] += 1 * n;
 
        std::cout << "Twoje statystyki zostały zaktualizowane!\n";
    }
};
 
// 2. Szwacz
class Szwacz : public Rzemieslnik {
public:
    Szwacz() : Rzemieslnik("Szwacz") {}
 
    void menu() override {
        char wybor;
        do {
            std::cout << "Profesja: " << nazwa_profesji << "\n";
            std::cout << "1. Szyć ubranie\n";
            std::cout << "2. Sprawdzić statystyki\n";
            std::cout << "3. Wyjść\n";
            std::cin >> wybor;
 
            switch (wybor) {
                case '1':
                    wykonaj_minigre();
                    break;
                case '2':
                    wypisz_stan();
                    wypisz_statystyki();
                    break;
                case '3':
                    std::cout << "Powrót do głównego menu.\n";
                    break;
                default:
                    std::cout << "Nieznana opcja.\n";
                    break;
            }
            std::cout << "------------------------\n";
        } while (wybor != '3');
    }
 
void wykonaj_minigre() override {
    std::cout << "Rozpoczynasz szycie ubrania jako " << nazwa_profesji << ".\n";
 
    // Krok 1: Przygotowanie Igły i Nici
    std::cout << "Aby chwycić nić, wciśnij jednocześnie klawisze 'L' i 'P'. Masz 2 sekundy.\n";
    auto start = std::chrono::steady_clock::now();
    bool lewy_przycisk = false;
    bool prawy_przycisk = false;
 
    while (std::chrono::steady_clock::now() - start < std::chrono::seconds(2)) {
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'L' || ch == 'l') {
                lewy_przycisk = true;
            } else if (ch == 'P' || ch == 'p') {
                prawy_przycisk = true;
            }
            if (lewy_przycisk && prawy_przycisk) {
                break;
            }
        }
    }
 
    if (!(lewy_przycisk && prawy_przycisk)) {
        std::cout << "Nie udało Ci się chwycić nici.\n";
        return;
    }
 
    std::cout << "Chwyciłeś nić!\n";
 
    // Krok 2: Przeciągnij nitkę przez oczko igły
    std::cout << "Przeciągnij nitkę przez oczko igły. Wciśnij klawisz 'I' w ciągu 3 sekund.\n";
    start = std::chrono::steady_clock::now();
    bool igla = false;
 
    while (std::chrono::steady_clock::now() - start < std::chrono::seconds(3)) {
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'I' || ch == 'i') {
                igla = true;
                break;
            }
        }
    }
 
    if (!igla) {
        std::cout << "Nie udało Ci się nawlec igły.\n";
        return;
    }
 
    std::cout << "Nawlekłeś igłę!\n";
 
    // Krok 3: Szycie Materiału
    std::cout << "Podążaj kursorem po wyświetlonej linii. Wciśnij sekwencję klawiszy 'A', 'S', 'D', 'W' w ciągu 5 sekund.\n";
    std::string sekwencja = "ASDW";
    std::string wprowadzona_sekwencja;
    start = std::chrono::steady_clock::now();
    while (wprowadzona_sekwencja.length() < sekwencja.length() && std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        if (_kbhit()) {
            char ch = _getch();
            wprowadzona_sekwencja += toupper(ch);
            std::cout << ch;
        }
    }
 
    if (wprowadzona_sekwencja != sekwencja) {
        std::cout << "\nNie udało Ci się zszyć materiału.\n";
        return;
    }
 
    std::cout << "\nZszyłeś materiał poprawnie!\n";
 
    // Krok 4: Dodawanie Ozdób
    std::cout << "Dodaj ozdoby do ubrania. Kliknij klawisz 'O' na migające punkty (masz 3 sekundy).\n";
    int ozdoby = 0;
    start = std::chrono::steady_clock::now();
    while (std::chrono::steady_clock::now() - start < std::chrono::seconds(3)) {
        std::cout << "Punkt ozdoby! Wciśnij 'O'!\n";
        std::this_thread::sleep_for(std::chrono::milliseconds(500));
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'O' || ch == 'o') {
                ozdoby++;
                std::cout << "Dodałeś ozdobę!\n";
            }
        }
    }
 
    if (ozdoby == 0) {
        std::cout << "Nie udało Ci się dodać żadnych ozdób.\n";
        return;
    }
 
    std::cout << "Udało Ci się stworzyć ubranie z " << ozdoby << " ozdobami!\n";
    zdobywaj_doswiadczenie(10);
}
    void aktualizuj_statystyki() override {
        statystyki["dexterity"] += 1 * n;
        statystyki["vitality"] += 1 * n;
        statystyki["attack_speed"] += 1 * n;
        statystyki["casting_speed"] += 1 * n;
        statystyki["pve_physical_dmg"] += 0.1 * n;
        statystyki["pve_magical_dmg"] += 0.1 * n;
        statystyki["crafting_bonus"] += 1 * n;
 
        std::cout << "Twoje statystyki zostały zaktualizowane!\n";
    }
};
 
// 3. Złotnik
class Zlotnik : public Rzemieslnik {
public:
    Zlotnik() : Rzemieslnik("Złotnik") {}
 
    void menu() override {
        char wybor;
        do {
            std::cout << "Profesja: " << nazwa_profesji << "\n";
            std::cout << "1. Tworzyć biżuterię\n";
            std::cout << "2. Sprawdzić statystyki\n";
            std::cout << "3. Wyjść\n";
            std::cin >> wybor;
 
            switch (wybor) {
                case '1':
                    wykonaj_minigre();
                    break;
                case '2':
                    wypisz_stan();
                    wypisz_statystyki();
                    break;
                case '3':
                    std::cout << "Powrót do głównego menu.\n";
                    break;
                default:
                    std::cout << "Nieznana opcja.\n";
                    break;
            }
            std::cout << "------------------------\n";
        } while (wybor != '3');
    }
 
void wykonaj_minigre() override {
    std::cout << "Rozpoczynasz tworzenie biżuterii jako " << nazwa_profesji << ".\n";
 
    // Krok 1: Przygotowanie Narzędzi
    std::cout << "Wybierz odpowiednie narzędzie. Wciśnij klawisz odpowiadający narzędziu:\n";
    std::cout << "1. Młotek (M)\n2. Pilnik (P)\n3. Pęseta (E)\n";
    char narzedzie;
    bool poprawne_narzedzie = false;
 
    for (int i = 0; i < 3; ++i) {
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'M' || ch == 'm') {
                narzedzie = 'M';
                poprawne_narzedzie = true;
                break;
            } else if (ch == 'P' || ch == 'p') {
                narzedzie = 'P';
                poprawne_narzedzie = true;
                break;
            } else if (ch == 'E' || ch == 'e') {
                narzedzie = 'E';
                poprawne_narzedzie = true;
                break;
            }
        }
        std::this_thread::sleep_for(std::chrono::milliseconds(500));
    }
 
    if (!poprawne_narzedzie) {
        std::cout << "Nie wybrałeś narzędzia na czas.\n";
        return;
    }
 
    std::cout << "Wybrałeś narzędzie: " << narzedzie << "\n";
 
    // Krok 2: Obróbka Metalu
    std::cout << "Kliknij na segmenty metalu we właściwej kolejności (1-3). Wciśnij klawisze '1', '2', '3'.\n";
    std::string poprawna_kolejnosc = "123";
    std::string wprowadzona_kolejnosc;
    auto start = std::chrono::steady_clock::now();
    while (wprowadzona_kolejnosc.length() < poprawna_kolejnosc.length() && std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        if (_kbhit()) {
            char ch = _getch();
            if (ch >= '1' && ch <= '3') {
                wprowadzona_kolejnosc += ch;
                std::cout << ch;
            }
        }
    }
 
    if (wprowadzona_kolejnosc != poprawna_kolejnosc) {
        std::cout << "\nNie udało Ci się obrobić metalu poprawnie.\n";
        return;
    }
 
    std::cout << "\nMetal został poprawnie obrobiony!\n";
 
    // Krok 3: Osadzanie Kamieni
    std::cout << "Przeciągnij kamienie na odpowiednie miejsca. Wciśnij 'K' dla każdego kamienia, unikając przeszkód.\n";
    int kamienie = 0;
    start = std::chrono::steady_clock::now();
    while (std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        std::cout << "Kamień do osadzenia! Wciśnij 'K'!\n";
        std::this_thread::sleep_for(std::chrono::milliseconds(500));
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'K' || ch == 'k') {
                kamienie++;
                std::cout << "Osadziłeś kamień!\n";
            }
        }
    }
 
    if (kamienie == 0) {
        std::cout << "Nie udało Ci się osadzić żadnych kamieni.\n";
        return;
    }
 
    std::cout << "Udało Ci się stworzyć biżuterię z " << kamienie << " kamieniami!\n";
    zdobywaj_doswiadczenie(10);
}
    void aktualizuj_statystyki() override {
        statystyki["intelligence"] += 1 * n;
        statystyki["mentality"] += 1 * n;
        statystyki["luck"] += 1 * n;
        statystyki["kleptomancy"] += 1 * n;
        statystyki["pve_physical_dmg"] += 0.1 * n;
        statystyki["pve_magical_dmg"] += 0.1 * n;
        statystyki["crafting_bonus"] += 1 * n;
 
        std::cout << "Twoje statystyki zostały zaktualizowane!\n";
    }
};
 
// 4. Cieśla
class Ciesla : public Rzemieslnik {
public:
    Ciesla() : Rzemieslnik("Cieśla") {}
 
    void menu() override {
        char wybor;
        do {
            std::cout << "Profesja: " << nazwa_profesji << "\n";
            std::cout << "1. Tworzyć drewniany przedmiot\n";
            std::cout << "2. Sprawdzić statystyki\n";
            std::cout << "3. Wyjść\n";
            std::cin >> wybor;
 
            switch (wybor) {
                case '1':
                    wykonaj_minigre();
                    break;
                case '2':
                    wypisz_stan();
                    wypisz_statystyki();
                    break;
                case '3':
                    std::cout << "Powrót do głównego menu.\n";
                    break;
                default:
                    std::cout << "Nieznana opcja.\n";
                    break;
            }
            std::cout << "------------------------\n";
        } while (wybor != '3');
    }
 
void wykonaj_minigre() override {
    std::cout << "Rozpoczynasz pracę jako " << nazwa_profesji << ".\n";
 
    // Krok 1: Wybór Drewna
    std::cout << "Wybierz rodzaj drewna. Naciśnij 'W' gdy wskaźnik będzie na właściwym drewnie.\n";
    std::vector<std::string> drewna = {"Dąb", "Sosna", "Brzoza"};
    int indeks = 0;
    auto start = std::chrono::steady_clock::now();
    bool wybrano = false;
    while (std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        indeks = (indeks + 1) % drewna.size();
        std::cout << "Aktualne drewno: " << drewna[indeks] << "   \r";
        std::cout.flush();
 
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'W' || ch == 'w') {
                wybrano = true;
                break;
            }
        }
        std::this_thread::sleep_for(std::chrono::milliseconds(500));
    }
 
    if (!wybrano) {
        std::cout << "\nNie wybrałeś drewna na czas.\n";
        return;
    }
 
    std::cout << "\nWybrałeś drewno: " << drewna[indeks] << "\n";
 
    // Krok 2: Cięcie Drewna
    std::cout << "Naciskaj na przemian klawisze 'A' i 'D' aby ciąć drewno. Masz 5 sekund.\n";
    char oczekiwany_klawisz = 'A';
    int ciecia = 0;
    start = std::chrono::steady_clock::now();
    while (ciecia < 5 && std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        if (_kbhit()) {
            char ch = toupper(_getch());
            if (ch == oczekiwany_klawisz) {
                ciecia++;
                oczekiwany_klawisz = (oczekiwany_klawisz == 'A') ? 'D' : 'A';
                std::cout << "Cięcie! (" << ciecia << ")\n";
            }
        }
    }
 
    if (ciecia < 5) {
        std::cout << "Nie udało Ci się przeciąć drewna.\n";
        return;
    }
 
    std::cout << "Przeciąłeś drewno!\n";
 
    // Krok 3: Składanie Konstrukcji
    std::cout << "Przeciągnij elementy na plan. Wciśnij 'S' gdy element jest na właściwym miejscu. Masz 5 sekund.\n";
    int elementy = 0;
    start = std::chrono::steady_clock::now();
    while (elementy < 3 && std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        std::cout << "Element do umieszczenia! Wciśnij 'S'!\n";
        std::this_thread::sleep_for(std::chrono::milliseconds(1000));
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'S' || ch == 's') {
                elementy++;
                std::cout << "Umieściłeś element! (" << elementy << "/3)\n";
            }
        }
    }
 
    if (elementy < 3) {
        std::cout << "Nie udało Ci się złożyć konstrukcji.\n";
        return;
    }
 
    std::cout << "Złożyłeś konstrukcję poprawnie!\n";
    zdobywaj_doswiadczenie(10);
}
    void aktualizuj_statystyki() override {
        statystyki["intelligence"] += 1 * n;
        statystyki["dexterity"] += 1 * n;
        statystyki["luck"] += 1 * n;
        statystyki["strength"] += 1 * n;
        statystyki["pve_physical_dmg"] += 0.1 * n;
        statystyki["pve_magical_dmg"] += 0.1 * n;
        statystyki["crafting_bonus"] += 1 * n;
 
        std::cout << "Twoje statystyki zostały zaktualizowane!\n";
    }
};
 
// 5. Garncarz
class Garncarz : public Rzemieslnik {
public:
    Garncarz() : Rzemieslnik("Garncarz") {}
 
    void menu() override {
        char wybor;
        do {
            std::cout << "Profesja: " << nazwa_profesji << "\n";
            std::cout << "1. Tworzyć naczynie\n";
            std::cout << "2. Sprawdzić statystyki\n";
            std::cout << "3. Wyjść\n";
            std::cin >> wybor;
 
            switch (wybor) {
                case '1':
                    wykonaj_minigre();
                    break;
                case '2':
                    wypisz_stan();
                    wypisz_statystyki();
                    break;
                case '3':
                    std::cout << "Powrót do głównego menu.\n";
                    break;
                default:
                    std::cout << "Nieznana opcja.\n";
                    break;
            }
            std::cout << "------------------------\n";
        } while (wybor != '3');
    }
 
void wykonaj_minigre() override {
    std::cout << "Rozpoczynasz formowanie gliny jako " << nazwa_profesji << ".\n";
 
    // Krok 1: Formowanie Gliny
    std::cout << "Obracaj koło garncarskie, kręcąc myszką (naciskaj szybko 'O'). Masz 3 sekundy.\n";
    int obroty = 0;
    auto start = std::chrono::steady_clock::now();
    while (std::chrono::steady_clock::now() - start < std::chrono::seconds(3)) {
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'O' || ch == 'o') {
                obroty++;
            }
        }
    }
 
    if (obroty < 10) {
        std::cout << "Nie udało Ci się wystarczająco obrócić koła.\n";
        return;
    }
 
    std::cout << "Koło garncarskie się kręci!\n";
 
    // Krok 2: Kształtowanie Naczynia
    std::cout << "Zmodyfikuj wysokość i szerokość naczynia. Wciśnij 'W' lub 'S' dla wysokości, 'A' lub 'D' dla szerokości.\n";
    int wysokosc = 5;
    int szerokosc = 5;
    start = std::chrono::steady_clock::now();
    while (std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'W' || ch == 'w') {
                wysokosc++;
            } else if (ch == 'S' || ch == 's') {
                wysokosc--;
            } else if (ch == 'A' || ch == 'a') {
                szerokosc--;
            } else if (ch == 'D' || ch == 'd') {
                szerokosc++;
            }
            std::cout << "Wysokość: " << wysokosc << ", Szerokość: " << szerokosc << "   \r";
            std::cout.flush();
        }
    }
 
    std::cout << "\nNadałeś naczyniu kształt!\n";
 
    // Krok 3: Dekorowanie
    std::cout << "Maluj wzory na naczyniu. Wciśnij 'M' gdy pojawi się wskazówka.\n";
    int wzory = 0;
    start = std::chrono::steady_clock::now();
    while (wzory < 3 && std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        std::cout << "Czas na wzór! Wciśnij 'M'!\n";
        std::this_thread::sleep_for(std::chrono::milliseconds(1000));
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'M' || ch == 'm') {
                wzory++;
                std::cout << "Dodałeś wzór! (" << wzory << "/3)\n";
            }
        }
    }
 
    if (wzory < 3) {
        std::cout << "Nie udało Ci się udekorować naczynia.\n";
        return;
    }
 
    std::cout << "Stworzyłeś piękne naczynie!\n";
    zdobywaj_doswiadczenie(10);
}
    void aktualizuj_statystyki() override {
        statystyki["attack_speed"] += 1 * n;
        statystyki["casting_speed"] += 1 * n;
        statystyki["luck"] += 1 * n;
        statystyki["kleptomancy"] += 1 * n;
        statystyki["pve_physical_dmg"] += 0.1 * n;
        statystyki["pve_magical_dmg"] += 0.1 * n;
        statystyki["crafting_bonus"] += 1 * n;
 
        std::cout << "Twoje statystyki zostały zaktualizowane!\n";
    }
};
 
// 6. Skórnik
class Skornik : public Rzemieslnik {
public:
    Skornik() : Rzemieslnik("Skórnik") {}
 
    void menu() override {
        char wybor;
        do {
            std::cout << "Profesja: " << nazwa_profesji << "\n";
            std::cout << "1. Tworzyć przedmiot ze skóry\n";
            std::cout << "2. Sprawdzić statystyki\n";
            std::cout << "3. Wyjść\n";
            std::cin >> wybor;
 
            switch (wybor) {
                case '1':
                    wykonaj_minigre();
                    break;
                case '2':
                    wypisz_stan();
                    wypisz_statystyki();
                    break;
                case '3':
                    std::cout << "Powrót do głównego menu.\n";
                    break;
                default:
                    std::cout << "Nieznana opcja.\n";
                    break;
            }
            std::cout << "------------------------\n";
        } while (wybor != '3');
    }
 
void wykonaj_minigre() override {
    std::cout << "Rozpoczynasz obróbkę skóry jako " << nazwa_profesji << ".\n";
 
    // Krok 1: Przygotowanie Skóry
    std::cout << "Klikaj na pojawiające się punkty na skórze, aby ją oczyścić. Wciśnij 'C' gdy pojawi się punkt.\n";
    int punkty = 0;
    auto start = std::chrono::steady_clock::now();
    while (punkty < 5 && std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        std::cout << "Punkt oczyszczania! Wciśnij 'C'!\n";
        std::this_thread::sleep_for(std::chrono::milliseconds(700));
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'C' || ch == 'c') {
                punkty++;
                std::cout << "Oczyściłeś punkt! (" << punkty << "/5)\n";
            }
        }
    }
 
    if (punkty < 5) {
        std::cout << "Nie udało Ci się oczyścić skóry.\n";
        return;
    }
 
    std::cout << "Skóra jest oczyszczona!\n";
 
    // Krok 2: Cięcie Skóry
    std::cout << "Podążaj kursorem po konturze. Wciśnij sekwencję klawiszy 'A', 'S', 'D', 'F' w ciągu 5 sekund.\n";
    std::string sekwencja = "ASDF";
    std::string wprowadzona_sekwencja;
    start = std::chrono::steady_clock::now();
    while (wprowadzona_sekwencja.length() < sekwencja.length() && std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        if (_kbhit()) {
            char ch = _getch();
            wprowadzona_sekwencja += toupper(ch);
            std::cout << ch;
        }
    }
 
    if (wprowadzona_sekwencja != sekwencja) {
        std::cout << "\nNie udało Ci się wyciąć kształtu.\n";
        return;
    }
 
    std::cout << "\nWyciąłeś kształt poprawnie!\n";
 
    // Krok 3: Łączenie Elementów
    std::cout << "Łącz elementy, klikając na pasujące krawędzie. Wciśnij 'L' gdy pojawi się wskazówka.\n";
    int laczenia = 0;
    start = std::chrono::steady_clock::now();
    while (laczenia < 3 && std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        std::cout << "Krawędź do połączenia! Wciśnij 'L'!\n";
        std::this_thread::sleep_for(std::chrono::milliseconds(1000));
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'L' || ch == 'l') {
                laczenia++;
                std::cout << "Połączyłeś krawędź! (" << laczenia << "/3)\n";
            }
        }
    }
 
    if (laczenia < 3) {
        std::cout << "Nie udało Ci się złożyć przedmiotu.\n";
        return;
    }
 
    std::cout << "Stworzyłeś przedmiot ze skóry!\n";
    zdobywaj_doswiadczenie(10);
}
    void aktualizuj_statystyki() override {
        statystyki["pvp_physical_dmg"] += 0.1 * n;
        statystyki["pvp_magical_dmg"] += 0.1 * n;
        statystyki["luck"] += 1 * n;
        statystyki["kleptomancy"] += 1 * n;
        statystyki["pve_physical_dmg"] += 0.1 * n;
        statystyki["pve_magical_dmg"] += 0.1 * n;
        statystyki["crafting_bonus"] += 1 * n;
 
        std::cout << "Twoje statystyki zostały zaktualizowane!\n";
    }
};
 
// 7. Magiczny Twórca
class MagicznyTworca : public Rzemieslnik {
public:
    MagicznyTworca() : Rzemieslnik("Magiczny Twórca") {}
 
    void menu() override {
        char wybor;
        do {
            std::cout << "Profesja: " << nazwa_profesji << "\n";
            std::cout << "1. Tworzyć magiczny przedmiot\n";
            std::cout << "2. Sprawdzić statystyki\n";
            std::cout << "3. Wyjść\n";
            std::cin >> wybor;
 
            switch (wybor) {
                case '1':
                    wykonaj_minigre();
                    break;
                case '2':
                    wypisz_stan();
                    wypisz_statystyki();
                    break;
                case '3':
                    std::cout << "Powrót do głównego menu.\n";
                    break;
            }
            std::cout << "------------------------\n";
        } while (wybor != '3');
    }
 
void wykonaj_minigre() override {
    std::cout << "Rozpoczynasz tworzenie magicznego przedmiotu jako " << nazwa_profesji << ".\n";
 
    // Krok 1: Dobór Składników
    std::cout << "Wybierz składniki spośród poruszających się ikon. Wciśnij 'S' gdy ikona jest nad składnikiem.\n";
    std::vector<std::string> skladniki = {"Kryształ", "Esencja", "Runy"};
    int indeks = 0;
    bool wybrano = false;
    auto start = std::chrono::steady_clock::now();
    while (!wybrano && std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        indeks = (indeks + 1) % skladniki.size();
        std::cout << "Aktualny składnik: " << skladniki[indeks] << "   \r";
        std::cout.flush();
 
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'S' || ch == 's') {
                wybrano = true;
                break;
            }
        }
        std::this_thread::sleep_for(std::chrono::milliseconds(500));
    }
 
    if (!wybrano) {
        std::cout << "\nNie wybrałeś składnika na czas.\n";
        return;
    }
 
    std::cout << "\nWybrałeś składnik: " << skladniki[indeks] << "\n";
 
    // Krok 2: Rytuał Tworzenia
    std::cout << "Odtwórz symbole runiczne. Wciśnij sekwencję klawiszy 'R', 'U', 'N' w ciągu 5 sekund.\n";
    std::string sekwencja = "RUN";
    std::string wprowadzona_sekwencja;
    start = std::chrono::steady_clock::now();
    while (wprowadzona_sekwencja.length() < sekwencja.length() && std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        if (_kbhit()) {
            char ch = toupper(_getch());
            wprowadzona_sekwencja += ch;
            std::cout << ch;
        }
    }
 
    if (wprowadzona_sekwencja != sekwencja) {
        std::cout << "\nRytuał nie powiódł się.\n";
        return;
    }
 
    std::cout << "\nRytuał zakończony sukcesem!\n";
 
    // Krok 3: Stabilizacja Energii
    std::cout << "Utrzymuj wskaźnik energii w zielonej strefie. Naciskaj 'A' i 'D' aby balansować.\n";
    int energia = 5;
    start = std::chrono::steady_clock::now();
    while (std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'A' || ch == 'a') {
                energia--;
            } else if (ch == 'D' || ch == 'd') {
                energia++;
            }
        }
 
        energia += (rand() % 3 - 1); // Losowa zmiana energii
        std::cout << "Energia: " << energia << "   \r";
        std::cout.flush();
 
        if (energia < 3 || energia > 7) {
            std::cout << "\nEnergia wymknęła się spod kontroli!\n";
            return;
        }
 
        std::this_thread::sleep_for(std::chrono::milliseconds(500));
    }
 
    std::cout << "\nUdało Ci się stworzyć magiczny przedmiot!\n";
    zdobywaj_doswiadczenie(10);
}
    void aktualizuj_statystyki() override {
        statystyki["intelligence"] += 1 * n;
        statystyki["mentality"] += 1 * n;
        statystyki["luck"] += 1 * n;
        statystyki["mp"] += 1 * n;
        statystyki["pve_physical_dmg"] += 0.1 * n;
        statystyki["pve_magical_dmg"] += 0.1 * n;
        statystyki["crafting_bonus"] += 1 * n;
 
        std::cout << "Twoje statystyki zostały zaktualizowane!\n";
    }
};
 
// 8. Inżynier
class Inzynier : public Rzemieslnik {
public:
    Inzynier() : Rzemieslnik("Inżynier") {}
 
    void menu() override {
        char wybor;
        do {
            std::cout << "Profesja: " << nazwa_profesji << "\n";
            std::cout << "1. Konstruować urządzenie\n";
            std::cout << "2. Sprawdzić statystyki\n";
            std::cout << "3. Wyjść\n";
            std::cin >> wybor;
 
            switch (wybor) {
                case '1':
                    wykonaj_minigre();
                    break;
                case '2':
                    wypisz_stan();
                    wypisz_statystyki();
                    break;
                case '3':
                    std::cout << "Powrót do głównego menu.\n";
                    break;
            }
            std::cout << "------------------------\n";
        } while (wybor != '3');
    }
 
    void wykonaj_minigre() override {
    std::cout << "Rozpoczynasz pracę jako " << nazwa_profesji << ".\n";
 
    // Krok 1: Wybór Projektu
    std::cout << "Wybierz projekt urządzenia. Naciśnij '1', '2' lub '3' gdy wskaźnik jest na wybranym projekcie.\n";
    std::vector<std::string> projekty = {"Pułapka", "Mechanizm", "Maszyna"};
    int indeks = 0;
    bool wybrano = false;
    auto start = std::chrono::steady_clock::now();
    while (!wybrano && std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        indeks = (indeks + 1) % projekty.size();
        std::cout << "Aktualny projekt: " << projekty[indeks] << "   \r";
        std::cout.flush();
 
        if (_kbhit()) {
            char ch = _getch();
            if (ch == '1' + indeks) {
                wybrano = true;
                break;
            }
        }
        std::this_thread::sleep_for(std::chrono::milliseconds(500));
    }
 
    if (!wybrano) {
        std::cout << "\nNie wybrałeś projektu na czas.\n";
        return;
    }
 
    std::cout << "\nWybrałeś projekt: " << projekty[indeks] << "\n";
 
    // Krok 2: Montaż Mechanizmu
    std::cout << "Przeciągnij elementy mechaniczne na schemat. Wciśnij 'M' dla każdego elementu.\n";
    int elementy = 0;
    start = std::chrono::steady_clock::now();
    while (elementy < 3 && std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        std::cout << "Element do zamontowania! Wciśnij 'M'!\n";
        std::this_thread::sleep_for(std::chrono::milliseconds(1000));
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'M' || ch == 'm') {
                elementy++;
                std::cout << "Zamontowałeś element! (" << elementy << "/3)\n";
            }
        }
    }
 
    if (elementy < 3) {
        std::cout << "Nie udało Ci się zmontować mechanizmu.\n";
        return;
    }
 
    std::cout << "Mechanizm zmontowany!\n";
 
    // Krok 3: Testowanie Urządzenia
    std::cout << "Szybko reaguj na sygnały. Wciśnij 'T' gdy zapali się lampka (3 razy).\n";
    int testy = 0;
    start = std::chrono::steady_clock::now();
    while (testy < 3 && std::chrono::steady_clock::now() - start < std::chrono::seconds(10)) {
        std::cout << "Lampka zapalona! Wciśnij 'T'!\n";
        std::this_thread::sleep_for(std::chrono::milliseconds(1500));
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'T' || ch == 't') {
                testy++;
                std::cout << "Reakcja! (" << testy << "/3)\n";
            }
        }
    }
 
    if (testy < 3) {
        std::cout << "Testowanie nie powiodło się.\n";
        return;
    }
 
    std::cout << "Urządzenie działa poprawnie!\n";
    zdobywaj_doswiadczenie(10);
}
 
    void aktualizuj_statystyki() override {
        statystyki["intelligence"] += 1 * n;
        statystyki["dexterity"] += 1 * n;
        statystyki["luck"] += 1 * n;
        statystyki["kleptomancy"] += 1 * n;
        statystyki["pve_physical_dmg"] += 0.1 * n;
        statystyki["pve_magical_dmg"] += 0.1 * n;
        statystyki["crafting_bonus"] += 1 * n;
 
        std::cout << "Twoje statystyki zostały zaktualizowane!\n";
    }
};
 
// 9. Kucharz
class Kucharz : public Rzemieslnik {
public:
    Kucharz() : Rzemieslnik("Kucharz") {}
 
    void menu() override {
        char wybor;
        do {
            std::cout << "Profesja: " << nazwa_profesji << "\n";
            std::cout << "1. Przygotować potrawę\n";
            std::cout << "2. Sprawdzić statystyki\n";
            std::cout << "3. Wyjść\n";
            std::cin >> wybor;
 
            switch (wybor) {
                case '1':
                    wykonaj_minigre();
                    break;
                case '2':
                    wypisz_stan();
                    wypisz_statystyki();
                    break;
                case '3':
                    std::cout << "Powrót do głównego menu.\n";
                    break;
            }
            std::cout << "------------------------\n";
        } while (wybor != '3');
    }
 
    void wykonaj_minigre() override {
    std::cout << "Rozpoczynasz gotowanie jako " << nazwa_profesji << ".\n";
 
    // Krok 1: Przygotowanie Składników
    std::cout << "Szybko klikaj na składniki pojawiające się na ekranie. Wciśnij 'S' gdy składnik się pojawi.\n";
    int skladniki = 0;
    auto start = std::chrono::steady_clock::now();
    while (skladniki < 5 && std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        std::cout << "Składnik! Wciśnij 'S'!\n";
        std::this_thread::sleep_for(std::chrono::milliseconds(700));
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'S' || ch == 's') {
                skladniki++;
                std::cout << "Zebrałeś składnik! (" << skladniki << "/5)\n";
            }
        }
    }
 
    if (skladniki < 5) {
        std::cout << "Nie udało Ci się zebrać składników.\n";
        return;
    }
 
    std::cout << "Składniki zebrane!\n";
 
    // Krok 2: Gotowanie
    std::cout << "Mieszaj w garnku (naciskaj 'M') i dodawaj składniki w odpowiedniej kolejności ('1', '2', '3').\n";
    int mieszanie = 0;
    std::string poprawna_sekwencja = "123";
    std::string wprowadzona_sekwencja;
    auto start_gotowania = std::chrono::steady_clock::now();
    while ((mieszanie < 5 || wprowadzona_sekwencja.length() < 3) && std::chrono::steady_clock::now() - start_gotowania < std::chrono::seconds(7)) {
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'M' || ch == 'm') {
                mieszanie++;
                std::cout << "Mieszasz... (" << mieszanie << ")\n";
            } else if (ch >= '1' && ch <= '3') {
                wprowadzona_sekwencja += ch;
                std::cout << "Dodałeś składnik " << ch << "!\n";
            }
        }
    }
 
    if (mieszanie < 5 || wprowadzona_sekwencja != poprawna_sekwencja) {
        std::cout << "Nie udało Ci się ugotować potrawy.\n";
        return;
    }
 
    std::cout << "Potrawa ugotowana!\n";
 
    // Krok 3: Serwowanie
    std::cout << "Dekoruj potrawę, przeciągając dodatki. Wciśnij 'D' gdy pojawi się wskazówka.\n";
    int dekoracje = 0;
    auto start_serwowania = std::chrono::steady_clock::now();
    while (dekoracje < 3 && std::chrono::steady_clock::now() - start_serwowania < std::chrono::seconds(5)) {
        std::cout << "Dodatek do dekoracji! Wciśnij 'D'!\n";
        std::this_thread::sleep_for(std::chrono::milliseconds(1000));
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'D' || ch == 'd') {
                dekoracje++;
                std::cout << "Dodałeś dekorację! (" << dekoracje << "/3)\n";
            }
        }
    }
 
    if (dekoracje < 3) {
        std::cout << "Nie udało Ci się udekorować potrawy.\n";
        return;
    }
 
    std::cout << "Potrawa gotowa do podania!\n";
    zdobywaj_doswiadczenie(10);
}
 
    void aktualizuj_statystyki() override {
        statystyki["attack_speed"] += 1 * n;
        statystyki["casting_speed"] += 1 * n;
        statystyki["luck"] += 1 * n;
        statystyki["gold_bonus"] += 1 * n;
        statystyki["charisma"] += 1 * n;
        statystyki["pve_physical_dmg"] += 0.1 * n;
        statystyki["pve_magical_dmg"] += 0.1 * n;
        statystyki["crafting_bonus"] += 1 * n;
 
        std::cout << "Twoje statystyki zostały zaktualizowane!\n";
    }
};
 
// 10. Kamieniarz
class Kamieniarz : public Rzemieslnik {
public:
    Kamieniarz() : Rzemieslnik("Kamieniarz") {}
 
    void menu() override {
        char wybor;
        do {
            std::cout << "Profesja: " << nazwa_profesji << "\n";
            std::cout << "1. Obrabiać kamień\n";
            std::cout << "2. Sprawdzić statystyki\n";
            std::cout << "3. Wyjść\n";
            std::cin >> wybor;
 
            switch (wybor) {
                case '1':
                    wykonaj_minigre();
                    break;
                case '2':
                    wypisz_stan();
                    wypisz_statystyki();
                    break;
                case '3':
                    std::cout << "Powrót do głównego menu.\n";
                    break;
            }
            std::cout << "------------------------\n";
        } while (wybor != '3');
    }
 
void wykonaj_minigre() override {
    std::cout << "Rozpoczynasz pracę z kamieniem jako " << nazwa_profesji << ".\n";
 
    // Krok 1: Wybór Bloku Kamienia
    std::cout << "Naciśnij 'Spacja' gdy wskaźnik jest na wybranym kamieniu.\n";
    std::vector<std::string> kamienie = {"Granit", "Marmur", "Bazalt"};
    int indeks = 0;
    bool wybrano = false;
    auto start = std::chrono::steady_clock::now();
    while (!wybrano && std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        indeks = (indeks + 1) % kamienie.size();
        std::cout << "Aktualny kamień: " << kamienie[indeks] << "   \r";
        std::cout.flush();
 
        if (_kbhit()) {
            char ch = _getch();
            if (ch == ' ') {
                wybrano = true;
                break;
            }
        }
        std::this_thread::sleep_for(std::chrono::milliseconds(500));
    }
 
    if (!wybrano) {
        std::cout << "\nNie wybrałeś kamienia na czas.\n";
        return;
    }
 
    std::cout << "\nWybrałeś kamień: " << kamienie[indeks] << "\n";
 
    // Krok 2: Cięcie Kamienia
    std::cout << "Naciskaj 'A' i 'D' w rytmie aby ciąć kamień. Masz 5 sekund.\n";
    char oczekiwany_klawisz = 'A';
    int ciecia = 0;
    start = std::chrono::steady_clock::now();
    while (ciecia < 5 && std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        if (_kbhit()) {
            char ch = toupper(_getch());
            if (ch == oczekiwany_klawisz) {
                ciecia++;
                oczekiwany_klawisz = (oczekiwany_klawisz == 'A') ? 'D' : 'A';
                std::cout << "Cięcie! (" << ciecia << ")\n";
            }
        }
    }
 
    if (ciecia < 5) {
        std::cout << "Nie udało Ci się przeciąć kamienia.\n";
        return;
    }
 
    std::cout << "Kamień przecięty!\n";
 
    // Krok 3: Rzeźbienie
    std::cout << "Klikaj na podświetlone obszary. Wciśnij 'R' gdy pojawi się wskazówka.\n";
    int rzezbienia = 0;
    start = std::chrono::steady_clock::now();
    while (rzezbienia < 3 && std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        std::cout << "Obszar do rzeźbienia! Wciśnij 'R'!\n";
        std::this_thread::sleep_for(std::chrono::milliseconds(1000));
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'R' || ch == 'r') {
                rzezbienia++;
                std::cout << "Rzeźbisz... (" << rzezbienia << "/3)\n";
            }
        }
    }
 
    if (rzezbienia < 3) {
        std::cout << "Nie udało Ci się wyrzeźbić dzieła.\n";
        return;
    }
 
    std::cout << "Stworzyłeś piękną rzeźbę!\n";
    zdobywaj_doswiadczenie(10);
}
    void aktualizuj_statystyki() override {
        statystyki["strength"] += 1 * n;
        statystyki["vitality"] += 1 * n;
        statystyki["intelligence"] += 1 * n;
        statystyki["pve_physical_dmg"] += 0.1 * n;
        statystyki["pve_magical_dmg"] += 0.1 * n;
        statystyki["crafting_bonus"] += 1 * n;
 
        std::cout << "Twoje statystyki zostały zaktualizowane!\n";
    }
};
 
// 11. Zegarmistrz
class Zegarmistrz : public Rzemieslnik {
public:
    Zegarmistrz() : Rzemieslnik("Zegarmistrz") {}
 
    void menu() override {
        char wybor;
        do {
            std::cout << "Profesja: " << nazwa_profesji << "\n";
            std::cout << "1. Tworzyć zegar\n";
            std::cout << "2. Sprawdzić statystyki\n";
            std::cout << "3. Wyjść\n";
            std::cin >> wybor;
 
            switch (wybor) {
                case '1':
                    wykonaj_minigre();
                    break;
                case '2':
                    wypisz_stan();
                    wypisz_statystyki();
                    break;
                case '3':
                    std::cout << "Powrót do głównego menu.\n";
                    break;
            }
            std::cout << "------------------------\n";
        } while (wybor != '3');
    }
 
void wykonaj_minigre() override {
    std::cout << "Rozpoczynasz tworzenie zegara jako " << nazwa_profesji << ".\n";
 
    // Krok 1: Składanie Mechanizmu
    std::cout << "Umieść trybiki i sprężyny na właściwych miejscach.\n";
    std::cout << "Naciśnij klawisz 'T' za każdym razem, gdy pojawi się komunikat 'Umieść trybik',\n";
    std::cout << "oraz 'S' gdy pojawi się 'Umieść sprężynę'. Masz 2 sekundy na każdą akcję.\n";
 
    int ilosc_elementow = 5;
    bool sukces = true;
    char oczekiwany_klawisz;
 
    for (int i = 0; i < ilosc_elementow; ++i) {
        std::this_thread::sleep_for(std::chrono::milliseconds(500));
 
        if (rand() % 2 == 0) {
            std::cout << "Umieść trybik teraz!\n";
            oczekiwany_klawisz = 'T';
        } else {
            std::cout << "Umieść sprężynę teraz!\n";
            oczekiwany_klawisz = 'S';
        }
 
        auto start = std::chrono::steady_clock::now();
        bool element_umieszczony = false;
 
        while (std::chrono::steady_clock::now() - start < std::chrono::seconds(2)) {
            if (_kbhit()) {
                char ch = toupper(_getch());
                if (ch == oczekiwany_klawisz) {
                    element_umieszczony = true;
                    break;
                }
            }
        }
 
        if (!element_umieszczony) {
            sukces = false;
            break;
        }
    }
 
    if (!sukces) {
        std::cout << "Nie udało Ci się złożyć mechanizmu.\n";
        return;
    }
 
    std::cout << "Mechanizm został poprawnie złożony!\n";
 
    // Krok 2: Regulacja Chodu
    std::cout << "Utrzymaj wskazówkę w zielonej strefie (wartości od 40 do 60).\n";
    std::cout << "Naciskaj 'W' aby zwiększyć pozycję wskazówki i 'S' aby ją zmniejszyć. Masz 5 sekund.\n";
 
    int pozycja_wskazowki = 50;
    auto start = std::chrono::steady_clock::now();
    bool stabilny = true;
 
    while (std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        if (_kbhit()) {
            char ch = toupper(_getch());
            if (ch == 'W') {
                pozycja_wskazowki += 2;
            } else if (ch == 'S') {
                pozycja_wskazowki -= 2;
            }
        }
 
        // Aktualizacja pozycji wskazówki
        if (pozycja_wskazowki < 0) pozycja_wskazowki = 0;
        if (pozycja_wskazowki > 100) pozycja_wskazowki = 100;
 
        // Wyświetlanie aktualnej pozycji
        std::cout << "Pozycja wskazówki: " << pozycja_wskazowki << "        \r";
        std::cout.flush();
 
        // Sprawdzenie, czy wskazówka jest w zielonej strefie
        if (pozycja_wskazowki < 40 || pozycja_wskazowki > 60) {
            stabilny = false;
            break;
        }
 
        std::this_thread::sleep_for(std::chrono::milliseconds(100));
    }
 
    if (!stabilny) {
        std::cout << "\nNie udało Ci się utrzymać wskazówki w zielonej strefie.\n";
        return;
    }
 
    std::cout << "\nWskazówka utrzymana w zielonej strefie!\n";
 
    // Krok 3: Testowanie
    std::cout << "Obserwuj działanie zegara przez 5 sekund.\n";
    std::cout << "Jeśli zauważysz problem (komunikat 'Problem!'), naciśnij 'P'.\n";
 
    bool problem_wystapil = rand() % 2 == 0;
    bool poprawna_reakcja = true;
 
    start = std::chrono::steady_clock::now();
    while (std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        std::this_thread::sleep_for(std::chrono::milliseconds(500));
 
        if (problem_wystapil && rand() % 5 == 0) {
            std::cout << "Problem!\n";
            auto problem_start = std::chrono::steady_clock::now();
            bool reakcja = false;
 
            while (std::chrono::steady_clock::now() - problem_start < std::chrono::seconds(2)) {
                if (_kbhit()) {
                    char ch = toupper(_getch());
                    if (ch == 'P') {
                        reakcja = true;
                        break;
                    }
                }
            }
 
            if (!reakcja) {
                poprawna_reakcja = false;
                break;
            } else {
                std::cout << "Problem naprawiony!\n";
                problem_wystapil = false; // Zakładamy, że problem został naprawiony
            }
        }
    }
 
    if (!poprawna_reakcja) {
        std::cout << "Nie zareagowałeś na problem z zegarem.\n";
        return;
    }
 
    std::cout << "Zegar działa prawidłowo! Udało Ci się go stworzyć.\n";
    zdobywaj_doswiadczenie(10);
}
    void aktualizuj_statystyki() override {
        statystyki["strength"] += 1 * n;
        statystyki["dexterity"] += 1 * n;
        statystyki["intelligence"] += 1 * n;
        statystyki["pve_physical_dmg"] += 0.1 * n;
        statystyki["pve_magical_dmg"] += 0.1 * n;
        statystyki["crafting_bonus"] += 1 * n;
 
        std::cout << "Twoje statystyki zostały zaktualizowane!\n";
    }
};
 
// 12. Szklarz
class Szklarz : public Rzemieslnik {
public:
    Szklarz() : Rzemieslnik("Szklarz") {}
 
    void menu() override {
        char wybor;
        do {
            std::cout << "Profesja: " << nazwa_profesji << "\n";
            std::cout << "1. Tworzyć przedmiot ze szkła\n";
            std::cout << "2. Sprawdzić statystyki\n";
            std::cout << "3. Wyjść\n";
            std::cin >> wybor;
 
            switch (wybor) {
                case '1':
                    wykonaj_minigre();
                    break;
                case '2':
                    wypisz_stan();
                    wypisz_statystyki();
                    break;
                case '3':
                    std::cout << "Powrót do głównego menu.\n";
                    break;
            }
            std::cout << "------------------------\n";
        } while (wybor != '3');
    }
 
void wykonaj_minigre() override {
    std::cout << "Rozpoczynasz pracę ze szkłem jako " << nazwa_profesji << ".\n";
 
    // Krok 1: Topienie Szkła
    std::cout << "Utrzymuj temperaturę pieca w zakresie 70-100 przez 5 sekund.\n";
    std::cout << "Naciskaj 'W' aby zwiększyć temperaturę i 'S' aby ją zmniejszyć.\n";
 
    int temperatura = 50; // Początkowa temperatura
    auto czas_konca = std::chrono::steady_clock::now() + std::chrono::seconds(5);
    bool sukces = true;
 
    while (std::chrono::steady_clock::now() < czas_konca) {
        if (_kbhit()) {
            char ch = toupper(_getch());
            if (ch == 'W') {
                temperatura += 5;
            } else if (ch == 'S') {
                temperatura -= 5;
            }
        }
 
        // Wyświetlanie aktualnej temperatury
        std::cout << "Temperatura: " << temperatura << "        \r";
        std::cout.flush();
 
        // Sprawdzenie, czy temperatura jest w odpowiednim zakresie
        if (temperatura < 70 || temperatura > 100) {
            sukces = false;
            break;
        }
 
        std::this_thread::sleep_for(std::chrono::milliseconds(100));
    }
 
    if (!sukces) {
        std::cout << "\nTemperatura poza zakresem! Proces nie powiódł się.\n";
        return;
    }
 
    std::cout << "\nMasa szklana jest gotowa!\n";
 
    // Krok 2: Dmuchanie Szkła
    std::cout << "Naciskaj szybko klawisz 'D' przez 5 sekund, aby nadać kształt szklance.\n";
 
    int liczba_nacisniec = 0;
    auto start = std::chrono::steady_clock::now();
 
    while (std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
        if (_kbhit()) {
            char ch = toupper(_getch());
            if (ch == 'D') {
                liczba_nacisniec++;
            }
        }
    }
 
    if (liczba_nacisniec < 30) {
        std::cout << "Nie udało Ci się nadać kształtu szklance.\n";
        return;
    }
 
    std::cout << "Szklanka uformowana!\n";
 
    // Krok 3: Chłodzenie i Wykańczanie
    std::cout << "Przeciągnij przedmiot do strefy chłodzenia. Naciśnij 'C' w ciągu 2 sekund.\n";
 
    sukces = false;
    start = std::chrono::steady_clock::now();
 
    while (std::chrono::steady_clock::now() - start < std::chrono::seconds(2)) {
        if (_kbhit()) {
            char ch = toupper(_getch());
            if (ch == 'C') {
                sukces = true;
                break;
            }
        }
    }
 
    if (!sukces) {
        std::cout << "Nie udało Ci się ochłodzić szklanki na czas.\n";
        return;
    }
 
    std::cout << "Szklanka została schłodzona.\n";
 
    // Wykańczanie
    std::cout << "Kliknij na miejsca wymagające wykończenia. Naciśnij 'W' gdy pojawi się komunikat 'Wykończ teraz'.\n";
    int ilosc_miejsc = 3;
    sukces = true;
 
    for (int i = 0; i < ilosc_miejsc; ++i) {
        std::this_thread::sleep_for(std::chrono::seconds(1));
        std::cout << "Wykończ teraz!\n";
 
        auto start = std::chrono::steady_clock::now();
        bool wykonczono = false;
 
        while (std::chrono::steady_clock::now() - start < std::chrono::seconds(2)) {
            if (_kbhit()) {
                char ch = toupper(_getch());
                if (ch == 'W') {
                    wykonczono = true;
                    break;
                }
            }
        }
 
        if (!wykonczono) {
            sukces = false;
            break;
        }
    }
 
    if (!sukces) {
        std::cout << "Nie udało Ci się wykończyć szklanki.\n";
        return;
    }
 
    std::cout << "Szklanka jest gotowa! Udało Ci się stworzyć piękny przedmiot.\n";
    zdobywaj_doswiadczenie(10);
}
    void aktualizuj_statystyki() override {
        statystyki["dexterity"] += 1 * n;
        statystyki["vitality"] += 1 * n;
        statystyki["attack_speed"] += 1 * n;
        statystyki["casting_speed"] += 1 * n;
        statystyki["intelligence"] += 1 * n;
        statystyki["pve_physical_dmg"] += 0.1 * n;
        statystyki["pve_magical_dmg"] += 0.1 * n;
        statystyki["crafting_bonus"] += 1 * n;
 
        std::cout << "Twoje statystyki zostały zaktualizowane!\n";
    }
};
 
// 13. Eksperymentator
class Eksperymentator : public Rzemieslnik {
public:
    Eksperymentator() : Rzemieslnik("Eksperymentator") {}
 
    void menu() override {
        char wybor;
        do {
            std::cout << "Profesja: " << nazwa_profesji << "\n";
            std::cout << "1. Przeprowadzić eksperyment\n";
            std::cout << "2. Sprawdzić statystyki\n";
            std::cout << "3. Wyjść\n";
            std::cin >> wybor;
 
            switch (wybor) {
                case '1':
                    wykonaj_minigre();
                    break;
                case '2':
                    wypisz_stan();
                    wypisz_statystyki();
                    break;
                case '3':
                    std::cout << "Powrót do głównego menu.\n";
                    break;
            }
            std::cout << "------------------------\n";
        } while (wybor != '3');
    }
 
void wykonaj_minigre() override {
    std::cout << "Rozpoczynasz eksperyment jako " << nazwa_profesji << ".\n";
 
    // Krok 1: Mieszanie Składników
    std::cout << "Przeciągnij składniki do kotła. Naciśnij klawisz 'S' trzy razy, aby dodać składniki.\n";
    int liczba_skladnikow = 0;
    auto start = std::chrono::steady_clock::now();
 
    while (liczba_skladnikow < 3 && std::chrono::steady_clock::now() - start < std::chrono::seconds(10)) {
        if (_kbhit()) {
            char ch = toupper(_getch());
            if (ch == 'S') {
                liczba_skladnikow++;
                std::cout << "Dodano składnik: " << liczba_skladnikow << "\n";
            }
        }
    }
 
    if (liczba_skladnikow < 3) {
        std::cout << "Nie udało Ci się dodać wszystkich składników.\n";
        return;
    }
 
    std::cout << "Składniki dodane do kotła.\n";
 
    // Krok 2: Obserwacja Reakcji
    std::cout << "Obserwuj reakcję w kotle. Jeśli pojawi się 'Podgrzej' naciśnij 'H', jeśli 'Schłodź' naciśnij 'C'.\n";
    bool sukces = true;
 
    for (int i = 0; i < 3; ++i) {
        std::this_thread::sleep_for(std::chrono::milliseconds(1000 + rand() % 1000));
        bool podgrzej = rand() % 2 == 0;
        std::cout << (podgrzej ? "Podgrzej teraz!\n" : "Schłodź teraz!\n");
        char oczekiwany_klawisz = podgrzej ? 'H' : 'C';
 
        auto start = std::chrono::steady_clock::now();
        bool reakcja_poprawna = false;
 
        while (std::chrono::steady_clock::now() - start < std::chrono::seconds(2)) {
            if (_kbhit()) {
                char ch = toupper(_getch());
                if (ch == oczekiwany_klawisz) {
                    reakcja_poprawna = true;
                    break;
                }
            }
        }
 
        if (!reakcja_poprawna) {
            sukces = false;
            break;
        }
    }
 
    if (!sukces) {
        std::cout << "Nie udało Ci się kontrolować reakcji.\n";
        return;
    }
 
    std::cout << "Reakcja przebiegła pomyślnie!\n";
 
    // Krok 3: Ocena Wyniku
    std::cout << "Otrzymujesz losowy przedmiot lub efekt.\n";
    std::vector<std::string> wyniki = {"Eliksir Mocy", "Bomba Dymna", "Niewypał", "Esencja Życia", "Nic"};
    std::string otrzymany_wynik = wyniki[rand() % wyniki.size()];
 
    std::cout << "Twój wynik eksperymentu: " << otrzymany_wynik << "\n";
 
    zdobywaj_doswiadczenie(10);
}
    void aktualizuj_statystyki() override {
        statystyki["strength"] += 1 * n;
        statystyki["dexterity"] += 1 * n;
        statystyki["intelligence"] += 1 * n;
        statystyki["vitality"] += 1 * n;
        statystyki["attack_speed"] += 1 * n;
        statystyki["casting_speed"] += 1 * n;
        statystyki["luck"] += 1 * n;
        statystyki["mp"] += 1 * n;
        statystyki["gold_bonus"] += 1 * n;
        statystyki["charisma"] += 1 * n;
        statystyki["mentality"] += 1 * n;
        statystyki["hp"] += 20 * n;
        statystyki["pve_physical_dmg"] += 0.1 * n;
        statystyki["pve_magical_dmg"] += 0.1 * n;
        statystyki["pvp_physical_dmg"] += 0.1 * n;
        statystyki["pvp_magical_dmg"] += 0.1 * n;
        statystyki["crafting_bonus"] += 1 * n;
 
        std::cout << "Twoje statystyki zostały zaktualizowane!\n";
    }
};
 
// Funkcja wyboru profesji
void wybierz_profesje() {
    std::vector<std::string> profesje = {
        "Kowal",
        "Szwacz",
        "Złotnik",
        "Cieśla",
        "Garncarz",
        "Skórnik",
        "Magiczny Twórca",
        "Inżynier",
        "Kucharz",
        "Kamieniarz",
        "Zegarmistrz",
        "Szklarz",
        "Eksperymentator"
    };
 
    std::cout << "Wybierz profesję:\n";
    for (size_t i = 0; i < profesje.size(); ++i) {
        std::cout << i + 1 << ". " << profesje[i] << "\n";
    }
 
    int wybor;
    std::cin >> wybor;
 
    Rzemieslnik* rzemieslnik = nullptr;
 
    switch (wybor) {
        case 1:
            rzemieslnik = new Kowal();
            break;
        case 2:
            rzemieslnik = new Szwacz();
            break;
        case 3:
            rzemieslnik = new Zlotnik();
            break;
        case 4:
            rzemieslnik = new Ciesla();
            break;
        case 5:
            rzemieslnik = new Garncarz();
            break;
        case 6:
            rzemieslnik = new Skornik();
            break;
        case 7:
            rzemieslnik = new MagicznyTworca();
            break;
        case 8:
            rzemieslnik = new Inzynier();
            break;
        case 9:
            rzemieslnik = new Kucharz();
            break;
        case 10:
            rzemieslnik = new Kamieniarz();
            break;
        case 11:
            rzemieslnik = new Zegarmistrz();
            break;
        case 12:
            rzemieslnik = new Szklarz();
            break;
        case 13:
            rzemieslnik = new Eksperymentator();
            break;
        default:
            std::cout << "Nieznana profesja.\n";
            return;
    }
 
    rzemieslnik->menu();
 
    delete rzemieslnik;
}
 
int main() {
    wybierz_profesje();
    return 0;
}
```
