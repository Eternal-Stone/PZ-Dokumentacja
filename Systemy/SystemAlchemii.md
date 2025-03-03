# System Alchemii

Aby zostać Alchemikiem, musimy wpierw zostać czeladnikiem u mistrza Alchemii, a on krok po kroku nauczy nas, jak tworzyć mikstury.

Dzięki Alchemii jesteśmy w stanie tworzyć mikstury, maści, specjalne oliwy i inne przedmioty wspomagające lub potrzebne do ulepszania przedmiotów oraz do innych form craftingu.

Dodatkowo sama umiejętność Alchemii wpływa na ogólne statystyki naszej postaci. Im lepsi jesteśmy w tworzeniu mikstur, tym nasza postać także staje się mocniejsza.

Maksymalny poziom, jaki możemy osiągnąć w Alchemii, to 100.

Poziom wpływa na możliwość tworzenia rzadkich mikstur, maści, specjalnych oliw lub potrzebnych wywarów, które dają specjalne efekty lub są wymagane do wytwarzania rzadkich przedmiotów.

## Jak ma działać system Alchemii

Podchodzimy do stołu alchemicznego, a po naciśnięciu odpowiedniego przycisku otwiera się interfejs, który pokazuje nam różne podtypy Alchemii, np. tworzenie mikstur, maści itp.

Po wybraniu odpowiedniego podtypu możemy wskazać daną recepturę. Zostaną wtedy wyświetlone wymagania do stworzenia mikstury. Możemy również określić liczbę wytwarzanych mikstur, przesuwając inteligentny suwak, który pozwala na maksymalne wykorzystanie zasobów dostępnych w ekwipunku.

Następnie naciskamy „OK” i rozpoczyna się minigra, w której:

- Musimy jednocześnie kliknąć lewy i prawy przycisk myszy.
- Potem kręcimy myszką, aby napełnić pasek mieszania składników.
- Po napełnieniu paska przechodzimy do procesu podgrzewania, w którym przesuwamy myszkę w górę i w dół, aby utrzymać odpowiednią temperaturę mikstury.

Cały proces trwa od kilku do kilkunastu sekund, w zależności od rodzaju mikstury. Po zakończeniu tego etapu nasza mikstura jest gotowa.

Liczba tworzonych mikstur nie wpływa na minigrę, ale wpływa na poziom umiejętności. Za każdą wytworzoną miksturę otrzymujemy 1 punkt doświadczenia (np. jeśli tworzymy 15 mikstur, zdobywamy 15 punktów doświadczenia).

## Poziomy trudności receptur

System uwzględnia różne poziomy trudności receptur:

- **Łatwe** – dla początkujących alchemików.
- **Trudniejsze** – wymagające więcej zasobów i bardziej skomplikowanej minigry (np. konieczność szybszego lub wolniejszego kręcenia myszką itp.).

## System obliczania poziomu Alchemii

System określa, ile doświadczenia musimy zdobyć, aby osiągnąć wyższy poziom:

```text
n - aktualny poziom alchemii

Poziom alchemii = Poziom alchemii + 5n + (5n + 1)
```

## Problem interfejsu

Graficzne przedstawienie modelu można zrealizować poprzez pasek postępu od 0% do 1100%, który ładuje się za każdą ukończoną miksturę.

Formuła obliczania postępu:

```text
Bar = 100%

Development = Poziom alchemii / Bar
```

lub bardziej zrozumiale:

```text
Development = Poziom alchemii / 100%
```

### System obliczania dodatkowych statystyk

Co 5 poziomów Alchemii otrzymujemy dodatkowe statystyki:

Przykład:

```text
5 poziom = n
10 poziom = n + 1
15 poziom = n + 2
```

(n reprezentuje indeks systemu co 5 poziomów)

### Bonusy za poziomy

```text
Intelligence Bonus = Intelligence Bonus + 1 * n
Physical Resistance Bonus = Physical Resistance Bonus + 0.1 * n
Alchemy Bonus = Alchemy Bonus + 1 * n
Tenacity Bonus = Tenacity Bonus + 0.1 * n
```

## Propozycja programu realizującego dany problem

```cpp
#include <iostream>
#include <cstdlib>     // dla rand() i srand()
#include <ctime>       // dla time()
#include <chrono>      // dla std::chrono
#include <thread>      // dla std::this_thread::sleep_for
#include <conio.h>     // dla _kbhit() i _getch()
#include <vector>

class Alchemik {
private:
    int poziom;
    int doswiadczenie;
    int doswiadczenie_do_nastepnego_poziomu;
    int n; // indeks dla systemu piątek

    // Statystyki
    int inteligencja_bonus;
    double fizyczna_odpornosc_bonus;
    int alchemia_bonus;
    double wytrzymalosc_bonus;

    // Receptury (dla uproszczenia)
    struct Receptura {
        std::string nazwa;
        int trudnosc; // 1 - łatwa, 2 - średnia, 3 - trudna
        int wymagane_skladniki;
    };
    std::vector<Receptura> receptury;

    // Ekwipunek (dla uproszczenia)
    int skladniki;

public:
    Alchemik() : poziom(1), doswiadczenie(0), doswiadczenie_do_nastepnego_poziomu(0),
                 n(0), inteligencja_bonus(0), fizyczna_odpornosc_bonus(0.0), alchemia_bonus(0), wytrzymalosc_bonus(0.0),
                 skladniki(100) { // Załóżmy, że zaczynamy ze 100 składnikami
        oblicz_doswiadczenie_do_nastepnego_poziomu();
        inicjalizuj_receptury();
        // Inicjalizacja generatora liczb losowych
        srand(static_cast<unsigned int>(time(0)));
    }

    void oblicz_doswiadczenie_do_nastepnego_poziomu() {
        int n = poziom;
        doswiadczenie_do_nastepnego_poziomu = doswiadczenie + 5 * n + (5 * n + 1);
    }

    void inicjalizuj_receptury() {
        receptury.push_back({"Mikstura Leczenia", 1, 2});
        receptury.push_back({"Eliksir Siły", 2, 5});
        receptury.push_back({"Napój Niewidzialności", 3, 10});
    }

    void tworzenie_mikstur() {
        std::cout << "Wybierz recepturę do stworzenia:\n";
        for (size_t i = 0; i < receptury.size(); ++i) {
            std::cout << i + 1 << ". " << receptury[i].nazwa << " (Trudność: " << receptury[i].trudnosc
                      << ", Wymagane składniki: " << receptury[i].wymagane_skladniki << ")\n";
        }

        int wybor_receptury;
        std::cin >> wybor_receptury;
        if (wybor_receptury < 1 || wybor_receptury > static_cast<int>(receptury.size())) {
            std::cout << "Nieprawidłowy wybór.\n";
            return;
        }

        Receptura wybrana_receptura = receptury[wybor_receptury - 1];

        std::cout << "Ile mikstur chcesz stworzyć?\n";
        int ilosc;
        std::cin >> ilosc;

        int calkowity_koszt = wybrana_receptura.wymagane_skladniki * ilosc;
        if (skladniki < calkowity_koszt) {
            std::cout << "Nie masz wystarczającej ilości składników.\n";
            return;
        }

        skladniki -= calkowity_koszt;

        // Mini-gra
        std::cout << "Rozpoczynasz tworzenie " << ilosc << " mikstur(y) " << wybrana_receptura.nazwa << ".\n";

        // Krok 1: Kliknięcie lewego i prawego przycisku myszy jednocześnie
        std::cout << "Aby rozpocząć, wciśnij jednocześnie klawisze 'L' i 'P'. Masz 3 sekundy.\n";
        auto start = std::chrono::steady_clock::now();
        bool lewy_przycisk = false;
        bool prawy_przycisk = false;

        while (std::chrono::steady_clock::now() - start < std::chrono::seconds(3)) {
            if (_kbhit()) {
                char ch = _getch();
                if (ch == 'L' || ch == 'l') {
                    lewy_przycisk = true;
                    std::cout << "Lewy przycisk wciśnięty.\n";
                } else if (ch == 'P' || ch == 'p') {
                    prawy_przycisk = true;
                    std::cout << "Prawy przycisk wciśnięty.\n";
                }
                if (lewy_przycisk && prawy_przycisk) {
                    break;
                }
            }
        }

        if (!(lewy_przycisk && prawy_przycisk)) {
            std::cout << "Nie udało Ci się rozpocząć tworzenia mikstury.\n";
            return;
        }

        // Krok 2: Mieszanie składników
        std::cout << "Teraz mieszaj składniki! Kręć myszką (wciśnij szybko klawisze 'A' i 'D') aby napełnić pasek.\n";
        int wymagane_mieszanie = 0;
        switch (wybrana_receptura.trudnosc) {
            case 1:
                wymagane_mieszanie = 5;
                break;
            case 2:
                wymagane_mieszanie = 10;
                break;
            case 3:
                wymagane_mieszanie = 15;
                break;
            default:
                wymagane_mieszanie = 10;
                break;
        }

        int liczba_mieszania = 0;
        start = std::chrono::steady_clock::now();
        while (liczba_mieszania < wymagane_mieszanie) {
            if (_kbhit()) {
                char ch = _getch();
                if (ch == 'A' || ch == 'a' || ch == 'D' || ch == 'd') {
                    liczba_mieszania++;
                    std::cout << "Mieszanie: " << liczba_mieszania << "/" << wymagane_mieszanie << "\n";
                }
            }
        }

        // Krok 3: Podgrzewanie
        std::cout << "Utrzymuj odpowiednią temperaturę! Przesuwaj myszą w górę ('W') i w dół ('S').\n";
        int czas_podgrzewania = 0;
        switch (wybrana_receptura.trudnosc) {
            case 1:
                czas_podgrzewania = 5;
                break;
            case 2:
                czas_podgrzewania = 8;
                break;
            case 3:
                czas_podgrzewania = 12;
                break;
            default:
                czas_podgrzewania = 8;
                break;
        }

        int utrzymana_temperatura = 0;
        start = std::chrono::steady_clock::now();
        auto koniec = start + std::chrono::seconds(czas_podgrzewania);
        while (std::chrono::steady_clock::now() < koniec) {
            if (_kbhit()) {
                char ch = _getch();
                if (ch == 'W' || ch == 'w' || ch == 'S' || ch == 's') {
                    utrzymana_temperatura++;
                    std::cout << "Temperatura utrzymana przez: " << utrzymana_temperatura << " sekund.\n";
                }
            }
            std::this_thread::sleep_for(std::chrono::seconds(1));
        }

        if (utrzymana_temperatura >= czas_podgrzewania) {
            std::cout << "Udało Ci się stworzyć " << ilosc << " mikstur(y)!\n";
            zdobywaj_doswiadczenie(ilosc); // 1 mikstura = 1 exp
        } else {
            std::cout << "Proces tworzenia mikstur nie powiódł się.\n";
        }
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
        std::cout << "Gratulacje! Awansowałeś na poziom " << poziom << ".\n";
        oblicz_doswiadczenie_do_nastepnego_poziomu();

        if (poziom % 5 == 0) {
            n++;
            aktualizuj_statystyki();
        }
    }

    void aktualizuj_statystyki() {
        inteligencja_bonus += 1 * n;
        fizyczna_odpornosc_bonus += 0.1 * n;
        alchemia_bonus += 1 * n;
        wytrzymalosc_bonus += 0.1 * n;

        std::cout << "Twoje statystyki zostały zaktualizowane!\n";
        wypisz_statystyki();
    }

    void wypisz_statystyki() {
        std::cout << "Statystyki:\n";
        std::cout << "Inteligencja bonus: " << inteligencja_bonus << "\n";
        std::cout << "Fizyczna odporność bonus: " << fizyczna_odpornosc_bonus << "\n";
        std::cout << "Alchemia bonus: " << alchemia_bonus << "\n";
        std::cout << "Wytrzymałość bonus: " << wytrzymalosc_bonus << "\n";
    }

    void wypisz_stan() {
        std::cout << "Poziom: " << poziom << "\n";
        std::cout << "Doświadczenie: " << doswiadczenie << "/" << doswiadczenie_do_nastepnego_poziomu << "\n";
        std::cout << "Posiadane składniki: " << skladniki << "\n";
    }
};

int main() {
    Alchemik alchemik;

    char wybor;
    do {
        std::cout << "Co chcesz zrobić?\n";
        std::cout << "1. Tworzyć mikstury\n";
        std::cout << "2. Sprawdzić statystyki\n";
        std::cout << "3. Wyjść\n";
        std::cin >> wybor;

        switch (wybor) {
            case '1':
                alchemik.tworzenie_mikstur();
                break;
            case '2':
                alchemik.wypisz_stan();
                alchemik.wypisz_statystyki();
                break;
            case '3':
                std::cout << "Do zobaczenia!\n";
                break;
            default:
                std::cout << "Nieznana opcja.\n";
                break;
        }
        std::cout << "------------------------\n";
    } while (wybor != '3');

    return 0;
}
```
