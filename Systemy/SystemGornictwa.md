# System górnictwa

*Górnik to bardzo ciężka praca. Wymaga posiadania odpowiednich umiejętności, aby ją wykonywać.*

Aby zostać górnikiem, należy najpierw znaleźć odpowiedniego mistrza, u którego będzie się terminować. Aby zostać czeladnikiem, najpierw trzeba wykonać serię questów sprawdzających, czy postać nadaje się do tej pracy. Jest to seria prostych questów wprowadzających do systemu górnictwa.

Praca górnika przynosi szereg korzyści dla gracza. Oprócz możliwości zarobku na wykopanych materiałach, można je wykorzystać do craftingu, ulepszania, enchantowania oraz wielu innych systemów. Dodatkowo sama praca górnika wyrabia tężyznę i siłę w ciele każdego pracownika.

Maksymalny poziom górnictwa, jaki można osiągnąć to **100**.

Poziom górnictwa wpływa na możliwość rozłupywania znacznie trudniejszych minerałów, które są bardziej wartościowe. Wyższy poziom pozwala również na rozłupywanie specjalnych ścian, co daje dostęp do sekretnych przejść i ukrytych łupów - głównie w dungeonach.

## Jak działa system górnictwa

Gdy gracz podchodzi do złoża, kopca, skały macierzystej lub bloku skalnego, może wejść w tryb mini-gry.

**Tryb mini-gry**:

1. Gracz klika lewy i prawy przycisk myszy, aby chwycić kilof.
2. Następnie musi przesunąć mysz do tyłu, aby podnieść kilof do góry.
3. W celu uderzenia skały musi wykonywać szybkie ruchy myszką do przodu i do tyłu.
4. Po rozłupaniu skały gracz otrzymuje minerały.

Czym wyższy poziom górnictwa, tym większa szansa na dodatkowe uzyskanie rzadkich minerałów.

## System poziomowania górnictwa

**Obliczanie poziomu górnictwa:**

```text
n - aktualny poziom górnictwa
Nowy poziom górnictwa = 6n + 1
```

## Interfejs

Postęp poziomu górnictwa jest przedstawiony w formie paska postępu (0-100%).

```text
Bar = 100%
Development = poziom górnictwa / Bar
```

Alternatywnie:

```text
Development = poziom górnictwa / 100%
```

## System dodatkowych statystyk

Za każde 5 poziomów górnictwa gracz otrzymuje bonusy do statystyk:

Przykład:

```text
n - indeks poziomu gwarantującego bonus
```

| Poziom górnictwa | Indeks |
|------------------|--------|
| Poziom 5         | n = 1  |
| Poziom 10        | n + 1  |
| Poziom 15        | n + 2  |
| ... | |

**Obliczanie bonusów:**

- Strength bonus = Strength bonus + 1 * n
- Aggression bonus = Aggression bonus + 1 * n
- Domination bonus = Precision bonus + 1 * n
- Mining power = Mining power + 1 * n

## Propozycja programu realizującego dany problem

```cpp
#include <iostream>
#include <cstdlib>     // dla rand() i srand()
#include <ctime>       // dla time()
#include <chrono>      // dla std::chrono
#include <thread>      // dla std::this_thread::sleep_for
#include <conio.h>     // dla _kbhit() i _getch()


class Gornik {
private:
    int poziom;
    int doswiadczenie;
    int doswiadczenie_do_nastepnego_poziomu;
    int n; // indeks dla systemu piątek


    // Statystyki
    int sila_bonus;
    int agresja_bonus;
    int dominacja_bonus;


public:
    Gornik() : poziom(1), doswiadczenie(0), doswiadczenie_do_nastepnego_poziomu(0),
               n(0), sila_bonus(0), agresja_bonus(0), dominacja_bonus(0) {
        oblicz_doswiadczenie_do_nastepnego_poziomu();
        // Inicjalizacja generatora liczb losowych
        srand(static_cast<unsigned int>(time(0)));
    }


    void oblicz_doswiadczenie_do_nastepnego_poziomu() {
        int n = poziom;
        doswiadczenie_do_nastepnego_poziomu = doswiadczenie + 3 * n + (2 * n + 1);
    }


    void kopanie_skaly() {
        // Symulacja kopania skały
        std::cout << "Podchodzisz do złoża. Przygotuj się do kopania...\n";


        // Krok 1: Złapanie kilofa
        std::cout << "Aby złapać kilof, wciśnij jednocześnie klawisze 'L' i 'P'. Masz 3 sekundy.\n";
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
            std::cout << "Nie zdążyłeś złapać kilofa.\n";
            return;
        }


        // Krok 2: Podniesienie kilofa
        std::cout << "Aby podnieść kilof, wciśnij klawisz 'F'. Masz 2 sekundy.\n";
        start = std::chrono::steady_clock::now();
        bool kilof_podniesiony = false;


        while (std::chrono::steady_clock::now() - start < std::chrono::seconds(2)) {
            if (_kbhit()) {
                char ch = _getch();
                if (ch == 'F' || ch == 'f') {
                    kilof_podniesiony = true;
                    std::cout << "Kilof podniesiony.\n";
                    break;
                }
            }
        }


        if (!kilof_podniesiony) {
            std::cout << "Nie zdążyłeś podnieść kilofa.\n";
            return;
        }


        // Krok 3: Uderzanie w skałę
        std::cout << "Teraz uderzaj w skałę! Wciskaj szybko klawisz 'H' przez 5 sekund.\n";
        start = std::chrono::steady_clock::now();
        int liczba_uderzen = 0;


        while (std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
            if (_kbhit()) {
                char ch = _getch();
                if (ch == 'H' || ch == 'h') {
                    liczba_uderzen++;
                    std::cout << "Uderzenie #" << liczba_uderzen << "\n";
                }
            }
        }


        // Sprawdzenie, czy udało się rozłupać skałę
        int wymagane_uderzenia = 10; // Możesz dostosować tę wartość
        if (liczba_uderzen >= wymagane_uderzenia) {
            std::cout << "Udało Ci się rozłupać skałę i wydobyć minerały!\n";
            zdobywaj_doswiadczenie(15); // Przyjmijmy, że za każdą skałę dostajemy 15 punktów doświadczenia


            // Szansa na bonusowe minerały
            int szansa_na_bonus = poziom; // Im wyższy poziom, tym większa szansa
            int losowa_wartosc = rand() % 100 + 1; // Losowa liczba od 1 do 100


            if (losowa_wartosc <= szansa_na_bonus) {
                std::cout << "Znalazłeś rzadki minerał!\n";
                // Możesz tutaj dodać kod dodający minerał do ekwipunku gracza
            }
        } else {
            std::cout << "Nie udało Ci się rozłupać skały.\n";
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
        sila_bonus += 1 * n;
        agresja_bonus += 1 * n;
        dominacja_bonus += 1 * n;


        std::cout << "Twoje statystyki zostały zaktualizowane!\n";
        wypisz_statystyki();
    }


    void wypisz_statystyki() {
        std::cout << "Statystyki:\n";
        std::cout << "Siła bonus: " << sila_bonus << "\n";
        std::cout << "Agresja bonus: " << agresja_bonus << "\n";
        std::cout << "Dominacja bonus: " << dominacja_bonus << "\n";
    }


    void wypisz_stan() {
        std::cout << "Poziom: " << poziom << "\n";
        std::cout << "Doświadczenie: " << doswiadczenie << "/" << doswiadczenie_do_nastepnego_poziomu << "\n";
    }
};


int main() {
    Gornik gornik;


    char wybor;
    do {
        std::cout << "Co chcesz zrobić?\n";
        std::cout << "1. Kopać skały\n";
        std::cout << "2. Sprawdzić statystyki\n";
        std::cout << "3. Wyjść\n";
        std::cin >> wybor;


        switch (wybor) {
            case '1':
                gornik.kopanie_skaly();
                break;
            case '2':
                gornik.wypisz_stan();
                gornik.wypisz_statystyki();
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
