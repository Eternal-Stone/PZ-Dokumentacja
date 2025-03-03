# System Złodzieja

Aby zostać złodziejem, gracz musi najpierw zostać czeladnikiem u mistrza złodziejstwa, a on krok po kroku nauczy go fachu złodzieja.

Dzięki fachowi złodziejstwa gracz jest w stanie otwierać zamki do drzwi i skrzyń, rozbrajać pułapki, okradać ludzi z ich pieniędzy, a także zdobywać przydatne umiejętności interpersonalne, które mogą przynosić korzyści w rozmowach z NPC.

Dodatkowo, sama umiejętność złodziejstwa wpływa na ogólne statystyki postaci. Im postać jest lepsza w fachu złodzieja, tym staje się mocniejsza.

Maksymalny poziom umiejętności złodziejstwa to **100**.

Poziom wpływa na otwieranie trudniejszych zamków, podejmowanie bardziej wymagających rozmów, okradanie trudniejszych przeciwników itp. Można podjąć się każdej minigry niezależnie od poziomu, lecz będą one trudniejsze.

## Sposób działania

System złodziejstwa dzieli się na **cztery mini-gry**:

### 1. Otwieranie zamków

- Gracz podchodzi do drzwi, skrzyni lub innego obiektu z zamkiem.
- Gracz klika przycisk, otwierając okienko minigry.
- Gra polega na znalezieniu odpowiedniej formuły (hasła) poprzez klikanie strzałek (lewo, prawo, góra, dół).
- Im trudniejszy zamek, tym bardziej skomplikowany system, który musimy rozbroić (podobnie jak w serii *Gothic*).
- Szansa na złamanie wytrychu zależna jest od poziomu umiejętności złodziejstwa.
- Im dłużej siedzimy nad zamkiem, tym większa szansa na złamanie wytrychu. Jeśli nam się nie uda, musimy odczekać przed kolejną próbą.

### 2. Rozbrajanie pułapek

- Gracz podchodzi do pułapki (ale nie za blisko, by jej nie aktywować).
- Gracz klika przycisk, otwierając okienko minigry.
- Gra polega na rozpracowaniu kodu w zależności od rodzaju pułapki (można dodać trybów rozbrajania).

### 3. Okradanie przeciwnika

- Podchodzimy od tyłu do przeciwnika (NPC).
- Jeśli jesteśmy wystarczająco blisko, pojawia się graficzny sygnał umożliwiający kradzież.
- Klikamy przycisk, otwierając minigrę:
  - Klikamy lewy i prawy przycisk myszy, by chwycić sztylet.
  - Wykonujemy ruch pół obrotu myszą, aby przeciąć mieszek.
  - Im trudniejszy NPC, tym szybciej musimy wykonać operację. Jeśli się nie uda, zostajemy wykryci i musimy uciekać.
- Element losowy w okradaniu – NPC może mieć w mieszku pieniądze, klucze, mikstury itp.

### Dodatkowe mechaniki

- Wysoki poziom "sławy złodzieja" (np. po wielu udanych kradzieżach) może sprawić, że strażnicy będą bardziej podejrzliwi.
- Nieudane kradzieże mogą prowadzić do aresztowania, konieczności zapłaty grzywny lub questów naprawczych.

## Unikalne zdolności złodzieja

Na wyższych poziomach gracz może odblokować specjalne zdolności, np.:

- **Złodziejski dotyk** – zwiększona szansa na niepostrzeżoną kradzież.
- **Zmysł złodzieja** – umiejętność wykrywania ukrytych przejść i skrytek.

## System obliczania poziomu złodziejstwa

System określa, ile razy należy wykonać czynności związane ze złodziejstwem, aby zdobyć kolejny poziom:

```text
n - poziom złodziejstwa
Poziom złodziejstwa = Poziom złodziejstwa + 8n + 1
```

## Interfejs

Graficznie poziom można przedstawić jako pasek postępu:

```text
Bar = 100%
Development = poziom złodziejstwa / Bar
```

Alternatywnie:

```text
Development = poziom złodziejstwa / 100%
```

## System obliczania dodatkowych statystyk

Statystyki zwiększają się co 5 poziomów zdobytych jako złodziej.

### Przykład

```text
n - indeks poziomu gwarantującego bonus
```

| Poziom złodziejstwa | Indeks |
|---------------------|--------|
| Poziom 5            | n = 1  |
| Poziom 10           | n + 1  |
| Poziom 15           | n + 2  |
| ... | |

### Statystyki

- **Dexterity bonus** = Dexterity bonus + 1\*n
- **Intelligence bonus** = Intelligence bonus + 1\*n
- **Luck bonus** = Luck bonus + 1\*n
- **Charisma bonus** = Charisma bonus + 0.1\*n
- **Thief bonus** = Thief bonus + 1\*n
- **PvP Physical Damage Bonus** = PvE Physical Damage Bonus + 0.1\*n
- **PvP Magical Damage Bonus** = PvE Magical Damage Bonus + 0.1\*n

## Propozycja programu realizującego dany problem

```cpp
#include <iostream>
#include <cstdlib>     // dla rand() i srand()
#include <ctime>       // dla time()
#include <chrono>      // dla std::chrono
#include <thread>      // dla std::this_thread::sleep_for
#include <conio.h>     // dla _kbhit() i _getch()
#include <string>
#include <vector>


class Zlodziej {
private:
    int poziom;
    int doswiadczenie;
    int doswiadczenie_do_nastepnego_poziomu;
    int n; // indeks dla systemu piątek


    // Statystyki
    int strength_bonus;
    int dexterity_bonus;
    int intelligence_bonus;
    int luck_bonus;
    double charisma_bonus;
    int thief_bonus;
    double pvp_physical_dmg_bonus;
    double pvp_magical_dmg_bonus;


    // Inne
    int slawa_zlodzieja; // Wpływa na podejrzliwość NPC
    bool zlodziejski_dotyk; // Unikalna zdolność


public:
    Zlodziej() : poziom(1), doswiadczenie(0), doswiadczenie_do_nastepnego_poziomu(0),
                 n(0), strength_bonus(0), dexterity_bonus(0), intelligence_bonus(0),
                 luck_bonus(0), charisma_bonus(0.0), thief_bonus(0),
                 pvp_physical_dmg_bonus(0.0), pvp_magical_dmg_bonus(0.0),
                 slawa_zlodzieja(0), zlodziejski_dotyk(false) {
        oblicz_doswiadczenie_do_nastepnego_poziomu();
        // Inicjalizacja generatora liczb losowych
        srand(static_cast<unsigned int>(time(0)));
    }


    void oblicz_doswiadczenie_do_nastepnego_poziomu() {
        int n = poziom;
        doswiadczenie_do_nastepnego_poziomu = doswiadczenie + 3 * n + (5 * n + 1);
    }


    void menu() {
        char wybor;
        do {
            std::cout << "Co chcesz zrobić?\n";
            std::cout << "1. Otwierać zamki\n";
            std::cout << "2. Rozbrajać pułapki\n";
            std::cout << "3. Okradać przeciwników\n";
            std::cout << "4. Rozmawiać w trybie złodzieja\n";
            std::cout << "5. Sprawdzić statystyki\n";
            std::cout << "6. Wyjść\n";
            std::cin >> wybor;


            switch (wybor) {
                case '1':
                    otwieranie_zamku();
                    break;
                case '2':
                    rozbrajanie_pulapki();
                    break;
                case '3':
                    okradanie_przeciwnika();
                    break;
                case '4':
                    rozmowa_zlodziejska();
                    break;
                case '5':
                    wypisz_stan();
                    wypisz_statystyki();
                    break;
                case '6':
                    std::cout << "Do zobaczenia!\n";
                    break;
                default:
                    std::cout << "Nieznana opcja.\n";
                    break;
            }
            std::cout << "------------------------\n";
        } while (wybor != '6');
    }


    void otwieranie_zamku() {
        std::cout << "Podchodzisz do zamka. Przygotuj się do otwierania...\n";
        int trudnosc_zamka = poziom; // Im wyższy poziom, tym trudniejsze zamki możesz otwierać
        int proba = 0;
        std::string haslo = generuj_haslo(trudnosc_zamka);
        std::string proba_uzytkownika;


        std::cout << "Zamek wymaga wpisania odpowiedniej sekwencji strzałek (np. 'w s a d').\n";


        while (proba < 3) {
            std::cout << "Wpisz sekwencję (użyj 'w', 's', 'a', 'd' oddzielonych spacją):\n";
            std::cin.ignore();
            std::getline(std::cin, proba_uzytkownika);


            if (proba_uzytkownika == haslo) {
                std::cout << "Udało Ci się otworzyć zamek!\n";
                zdobywaj_doswiadczenie(10);
                return;
            } else {
                std::cout << "Niepoprawna sekwencja.\n";
                proba++;
            }
        }


        std::cout << "Nie udało Ci się otworzyć zamka.\n";
    }


    std::string generuj_haslo(int trudnosc) {
        std::vector<std::string> kierunki = {"w", "s", "a", "d"};
        std::string haslo;
        for (int i = 0; i < trudnosc; ++i) {
            haslo += kierunki[rand() % 4];
            if (i != trudnosc - 1) haslo += " ";
        }
        return haslo;
    }


    void rozbrajanie_pulapki() {
        std::cout << "Podchodzisz do pułapki. Przygotuj się do rozbrajania...\n";
        int trudnosc_pulapki = poziom;
        int proba = 0;
        int kod = rand() % (10 * trudnosc_pulapki) + 1;
        int odpowiedz;


        std::cout << "Musisz odgadnąć kod pułapki (liczba od 1 do " << (10 * trudnosc_pulapki) << "). Masz 3 próby.\n";


        while (proba < 3) {
            std::cout << "Podaj liczbę:\n";
            std::cin >> odpowiedz;


            if (odpowiedz == kod) {
                std::cout << "Udało Ci się rozbroić pułapkę!\n";
                zdobywaj_doswiadczenie(15);
                return;
            } else if (odpowiedz < kod) {
                std::cout << "Kod jest większy.\n";
            } else {
                std::cout << "Kod jest mniejszy.\n";
            }
            proba++;
        }


        std::cout << "Nie udało Ci się rozbroić pułapki.\n";
    }


    void okradanie_przeciwnika() {
        std::cout << "Podchodzisz do przeciwnika od tyłu. Przygotuj się do kradzieży...\n";


        // Krok 1: Wciśnięcie lewego i prawego przycisku myszy jednocześnie
        std::cout << "Aby rozpocząć, wciśnij jednocześnie klawisze 'L' i 'P'. Masz 2 sekundy.\n";
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
            std::cout << "Nie udało Ci się rozpocząć kradzieży.\n";
            return;
        }


        // Krok 2: Wykonanie pół obrotu myszą ('O')
        std::cout << "Wykonaj szybki pół obrót myszką ('O'). Masz 1 sekundę.\n";
        start = std::chrono::steady_clock::now();
        bool obrot = false;


        while (std::chrono::steady_clock::now() - start < std::chrono::seconds(1)) {
            if (_kbhit()) {
                char ch = _getch();
                if (ch == 'O' || ch == 'o') {
                    obrot = true;
                    break;
                }
            }
        }


        if (!obrot) {
            std::cout << "Nie udało Ci się wykonać obrotu na czas. Zostałeś wykryty!\n";
            slawa_zlodzieja += 5;
            return;
        }


        // Sukces kradzieży
        std::cout << "Udało Ci się okraść przeciwnika!\n";
        zdobywaj_doswiadczenie(20);


        // Losowy przedmiot
        std::vector<std::string> przedmioty = {"Pieniądze", "Klucz", "Mikstura"};
        std::string zdobyty_przedmiot = przedmioty[rand() % przedmioty.size()];
        std::cout << "Zdobyłeś: " << zdobyty_przedmiot << "\n";
    }


    void rozmowa_zlodziejska() {
        std::cout << "Rozpoczynasz rozmowę w trybie złodzieja...\n";
        int trudnosc_rozmowy = poziom;
        int wybor;


        std::cout << "NPC: Czego chcesz?\n";
        std::cout << "Wybierz odpowiedź:\n";
        std::cout << "1. Pochlebstwo\n";
        std::cout << "2. Groźba\n";
        std::cout << "3. Łapówka\n";
        std::cin >> wybor;


        int szansa = charisma_bonus * 10 + luck_bonus * 5 + thief_bonus * 2;
        int wynik = rand() % 100 + 1;


        if (wybor == 1) {
            szansa += 20;
            std::cout << "Wybrałeś pochlebstwo.\n";
        } else if (wybor == 2) {
            szansa += 10;
            std::cout << "Wybrałeś groźbę.\n";
        } else if (wybor == 3) {
            szansa += 30;
            std::cout << "Wybrałeś łapówkę.\n";
        } else {
            std::cout << "Niepoprawny wybór.\n";
            return;
        }


        if (wynik <= szansa) {
            std::cout << "NPC pozytywnie zareagował na Twoje słowa.\n";
            zdobywaj_doswiadczenie(10);
        } else {
            std::cout << "NPC nie dał się przekonać.\n";
            slawa_zlodzieja += 2;
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


        // Unikalne zdolności
        if (poziom == 10 && !zlodziejski_dotyk) {
            zlodziejski_dotyk = true;
            std::cout << "Zdobyłeś unikalną zdolność: Złodziejski dotyk!\n";
        }
    }


    void aktualizuj_statystyki() {
        strength_bonus += 1 * n;
        dexterity_bonus += 1 * n;
        intelligence_bonus += 1 * n;
        luck_bonus += 1 * n;
        charisma_bonus += 0.1 * n;
        thief_bonus += 1 * n;
        pvp_physical_dmg_bonus += 0.1 * n;
        pvp_magical_dmg_bonus += 0.1 * n;


        std::cout << "Twoje statystyki zostały zaktualizowane!\n";
        wypisz_statystyki();
    }


    void wypisz_statystyki() {
        std::cout << "Statystyki:\n";
        std::cout << "Strength bonus: " << strength_bonus << "\n";
        std::cout << "Dexterity bonus: " << dexterity_bonus << "\n";
        std::cout << "Intelligence bonus: " << intelligence_bonus << "\n";
        std::cout << "Luck bonus: " << luck_bonus << "\n";
        std::cout << "Charisma bonus: " << charisma_bonus << "\n";
        std::cout << "Thief bonus: " << thief_bonus << "\n";
        std::cout << "PvP Physical Damage Bonus: " << pvp_physical_dmg_bonus << "\n";
        std::cout << "PvP Magical Damage Bonus: " << pvp_magical_dmg_bonus << "\n";
        std::cout << "Sława złodzieja: " << slawa_zlodzieja << "\n";
        if (zlodziejski_dotyk) {
            std::cout << "Posiadasz zdolność: Złodziejski dotyk\n";
        }
    }


    void wypisz_stan() {
        std::cout << "Poziom: " << poziom << "\n";
        std::cout << "Doświadczenie: " << doswiadczenie << "/" << doswiadczenie_do_nastepnego_poziomu << "\n";
    }
};


int main() {
    Zlodziej zlodziej;
    zlodziej.menu();
    return 0;
}
```
