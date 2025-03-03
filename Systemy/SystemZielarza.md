# System Zielarza

Aby zostać zielarzem, należy najpierw zostać czeladnikiem u mistrza zbieractwa, który krok po kroku nauczy gracza, jak pozyskiwać rośliny.

Dzięki zbieractwu gracz jest w stanie zdobywać bardzo ważne przedmioty, które są potrzebne do tworzenia różnych mikstur, ubrań, ksiąg umiejętności i pergaminów.

Dodatkowo, same umiejętności zielarskie wpływają na ogólne statystyki naszej postaci. Im postać jest lepsza w zbieractwie roślin, tym staje się mocniejsza.

## Poziomy i rozwój

Maksymalny poziom zielarstwa, jaki postać może osiągnąć, to **100**.

Poziom wpływa na możliwość zbierania trudniejszych roślin, które są wyjątkowe. Ich wartość jest znacznie atrakcyjniejsza, a ich unikalność pozwala wytwarzać naprawdę rzadkie przedmioty. Jeśli mamy zbyt niski poziom, roślina niszczy się podczas zbierania.

## Mechanika działania

W momencie podejścia do rośliny naciskamy przycisk, co uruchamia mini-grę.

- Gracz musi nacisnąć lewy i prawy przycisk myszy jednocześnie, aby postać chwyciła sierp.
- Następnie należy szybko przesuwać mysz w lewo, a potem w prawo, aby postać wykonała delikatny zamach i jednym ruchem ścięła roślinę, którą chce zdobyć.

## System obliczania poziomu zielarza

System określa, ile roślin musimy zdobyć, aby osiągnąć wyższy poziom:

```text
n - poziom zielarza 
Poziom zielarza = Poziom zielarza + 6n + 1
```

## Interfejs

Postęp poziomu zielarza jest przedstawiony w formie paska postępu (0-100%).

```text
Bar = 100%
Development = poziom zielarza / Bar
```

Alternatywnie:

```text
Development = poziom zielarza / 100%
```

## System dodatkowych statystyk

Za każde 5 poziomów zielarza gracz otrzymuje bonusy do statystyk:

Przykład:

```text
n - indeks poziomu gwarantującego bonus
```

| Poziom zielarza | Indeks |
|-----------------|--------|
| Poziom 5        | n = 1  |
| Poziom 10       | n + 1  |
| Poziom 15       | n + 2  |
| ... | |

### Bonusy statystyk

- **Mentality bonus** = Mentality bonus + 1 * n
- **Kleptomancy bonus** = Kleptomancy bonus + 1 * n
- **Harvest bonus** = Harvest bonus + 1 * n
- **MP Bonus** = MP Bonus + 22 * n

## Propozycja programu realizującego dany problem

```cpp
#include <iostream>
#include <cstdlib>     // dla rand() i srand()
#include <ctime>       // dla time()
#include <chrono>      // dla std::chrono
#include <thread>      // dla std::this_thread::sleep_for
#include <conio.h>     // dla _kbhit() i _getch()


class Zielarz {
private:
    int poziom;
    int doswiadczenie;
    int doswiadczenie_do_nastepnego_poziomu;
    int n; // indeks dla systemu piątek


    // Statystyki
    int mentality_bonus;
    int kleptomancy_bonus;
    int harvest_bonus;
    int mp_bonus;


public:
    Zielarz() : poziom(1), doswiadczenie(0), doswiadczenie_do_nastepnego_poziomu(0),
                n(0), mentality_bonus(0), kleptomancy_bonus(0), harvest_bonus(0), mp_bonus(0) {
        oblicz_doswiadczenie_do_nastepnego_poziomu();
        // Inicjalizacja generatora liczb losowych
        srand(static_cast<unsigned int>(time(0)));
    }


    void oblicz_doswiadczenie_do_nastepnego_poziomu() {
        int n = poziom;
        doswiadczenie_do_nastepnego_poziomu = doswiadczenie + 3 * n + (3 * n + 1);
    }


    void zbieranie_rosliny() {
        // Symulacja zbierania rośliny
        std::cout << "Podchodzisz do rośliny. Przygotuj się do zbierania...\n";


        // Krok 1: Chwytanie sierpa
        std::cout << "Aby chwycić sierp, wciśnij jednocześnie klawisze 'L' i 'P'. Masz 3 sekundy.\n";
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
            std::cout << "Nie zdążyłeś chwycić sierpa.\n";
            return;
        }


        // Krok 2: Zamach sierpem
        std::cout << "Aby zamachnąć się sierpem, przesuń mysz w lewo ('A') i w prawo ('D') w ciągu 2 sekund.\n";
        start = std::chrono::steady_clock::now();
        bool ruch_w_lewo = false;
        bool ruch_w_prawo = false;


        while (std::chrono::steady_clock::now() - start < std::chrono::seconds(2)) {
            if (_kbhit()) {
                char ch = _getch();
                if (ch == 'A' || ch == 'a') {
                    ruch_w_lewo = true;
                    std::cout << "Ruch w lewo wykonany.\n";
                } else if (ch == 'D' || ch == 'd') {
                    ruch_w_prawo = true;
                    std::cout << "Ruch w prawo wykonany.\n";
                }
                if (ruch_w_lewo && ruch_w_prawo) {
                    break;
                }
            }
        }


        if (!(ruch_w_lewo && ruch_w_prawo)) {
            std::cout << "Nie zdążyłeś wykonać zamachu.\n";
            return;
        }


        std::cout << "Udało Ci się zebrać roślinę!\n";
        zdobywaj_doswiadczenie(12); // Przyjmijmy, że za każdą roślinę dostajemy 12 punktów doświadczenia


        // Szansa na bonusowe rośliny
        int szansa_na_bonus = poziom; // Im wyższy poziom, tym większa szansa
        int losowa_wartosc = rand() % 100 + 1; // Losowa liczba od 1 do 100


        if (losowa_wartosc <= szansa_na_bonus) {
            std::cout << "Znalazłeś rzadką roślinę!\n";
            // Możesz tutaj dodać kod dodający roślinę do ekwipunku gracza
        }
    }


    void zdobywaj_doswiadczenie(int ilosc) {
        doswiadczenie += ilosc;
        std::cout << "Zdobyto " << ilosc << " punktów doświadczenia.\n";
        sprawdz_awans();
    }


    void sprawdz_awans() {
        if (doswiadczenie >= doswiadczenie_do_nastepnego_poziomu) {
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
        mentality_bonus += 1 * n;
        kleptomancy_bonus += 1 * n;
        harvest_bonus += 1 * n;
        mp_bonus += 22 * n;


        std::cout << "Twoje statystyki zostały zaktualizowane!\n";
        wypisz_statystyki();
    }


    void wypisz_statystyki() {
        std::cout << "Statystyki:\n";
        std::cout << "Mentality bonus: " << mentality_bonus << "\n";
        std::cout << "Kleptomancy bonus: " << kleptomancy_bonus << "\n";
        std::cout << "Harvest bonus: " << harvest_bonus << "\n";
        std::cout << "MP bonus: " << mp_bonus << "\n";
    }


    void wypisz_stan() {
        std::cout << "Poziom: " << poziom << "\n";
        std::cout << "Doświadczenie: " << doswiadczenie << "/" << doswiadczenie_do_nastepnego_poziomu << "\n";
    }
};


int main() {
    Zielarz zielarz;


    char wybor;
    do {
        std::cout << "Co chcesz zrobić?\n";
        std::cout << "1. Zbierać rośliny\n";
        std::cout << "2. Sprawdzić statystyki\n";
        std::cout << "3. Wyjść\n";
        std::cin >> wybor;


        switch (wybor) {
            case '1':
                zielarz.zbieranie_rosliny();
                break;
            case '2':
                zielarz.wypisz_stan();
                zielarz.wypisz_statystyki();
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
