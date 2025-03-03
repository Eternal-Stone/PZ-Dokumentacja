# System Pisarza

Aby zostać pisarzem, należy najpierw zostać czeladnikiem u mistrza pisarzy, który krok po kroku nauczy gracza tworzenia dzieł pisarskich.

Dzięki pisarstwu gracz tworzyć pergaminy (materiały), scrolle enchantów, księgi enchantów, tłumaczyć receptury dla alchemików i kowali, a także wiele innych przydatnych przedmiotów potrzebnych do craftowania. Sugeruje się podział wytwarzania różnych dzieł: domyślnie tworząc receptury i "zwyczajne" przedmioty, a w ramach specjalizacji oraz w wyjątkowych miejscach można byłoby tworzyć scrolle i enchanty.

Dodatkowo, umiejętność pisarska wpływa na ogólne statystyki postaci – im postać lepsza jest w pisarstwie, tym staje się mocniejsza.

Maksymalny poziom pisarstwa: **100**

Poziom wpływa na możliwości tworzenia rzadszych receptur, rzadkich enchantów i innych unikalnych przedmiotów.

## Sposób działania systemu

System pisarski podzielony jest na dwie mini-gry:

### Tworzenie pergaminów

Gracz podchodzi do stołu pisarskiego, klika przycisk i wybiera opcję "Tworzenie".

- Otwiera się interfejs wyboru przedmiotu oraz liczby sztuk do stworzenia.
- Po potwierdzeniu gracz przechodzi do mini-gry.
- Kliknięcie lewym i prawym przyciskiem myszy powoduje, że postać bierze do ręki włóczkę i zaczyna tworzyć pergamin.
- Gracz musi wykonać określoną liczbę obrotów myszką, a następnie poruszać nią w lewo i prawo, powtarzając operację aż do zakończenia procesu.

### Tworzenie pisarskie

Gracz podchodzi do stołu pisarskiego, klika przycisk i wybiera opcję "Pisanie".

- Otwiera się interfejs wyboru przedmiotu oraz liczby sztuk do stworzenia.
- Po potwierdzeniu gracz przechodzi do mini-gry.
- Kliknięcie lewym i prawym przyciskiem myszy powoduje, że postać bierze do ręki pióro.
- Gracz musi śledzić linię, która jest rysowana.
- W trudniejszych przypadkach może być konieczne śledzenie kilku linii.

W zależności od precyzji wykonania mini-gry jakość materiałów oraz szansa na powodzenie tworzenia przedmiotu mogą się zmieniać.

Minigry różnią się w zależności od rodzaju tworzonego przedmiotu. Na przykład:

- **Dla ksiąg**: Pisanie liter.
- **Dla zwojów enchantów**: Układanie sekwencji symboli.
- **Dla pergaminów**: Mieszanie kolorów lub kształtów.

## System obliczania poziomu pisarstwa

Poziom pisarza obliczamy według wzoru:

```text
n - aktualny poziom pisarza
Poziom pisarza = Poziom pisarza + 10n + 1
```

### Interfejs

Graficzne przedstawienie progresji może być realizowane poprzez pasek postępu od 0% do 100%, który ładuje się za każdą wykonaną pracę pisarską.

```text
Bar = 100%
Development = poziom pisarza / Bar
```

Alternatywnie:

```text
Development = poziom pisarza / 100%
```

### Dodatkowe statystyki

Postać otrzymuje bonusy co 5 poziomów pisarstwa.

Przykład:

```text
n - indeks poziomu gwarantującego bonus
```

| Poziom pisarza | Indeks |
|----------------|--------|
| Poziom 5       | n = 1  |
| Poziom 10      | n + 1  |
| Poziom 15      | n + 2  |
| ... | |

**Statystyki:**

- **Luck bonus** = Luck bonus + 1*n
- **Charisma bonus** = Charisma bonus + 0.1*n
- **Writer bonus** = Writer bonus + 1*n
- **PVE Physical Damage Bonus** = PVE Physical Damage Bonus + 0.1*n
- **PVE Magical Damage Bonus** = PVE Magical Damage Bonus + 0.1*n

## Propozycja programu realizującego dany problem

```cpp
#include <iostream>
#include <cstdlib>     // dla rand() i srand()
#include <ctime>       // dla time()
#include <chrono>      // dla std::chrono
#include <thread>      // dla std::this_thread::sleep_for
#include <conio.h>     // dla _kbhit() i _getch()
#include <vector>


class Pisarz {
private:
    int poziom;
    int doswiadczenie;
    int doswiadczenie_do_nastepnego_poziomu;
    int n; // indeks dla systemu piątek


    // Statystyki
    int luc_bonus;
    double charisma_bonus;
    int writer_bonus;
    double pve_physical_dmg_bonus;
    double pve_magical_dmg_bonus;


    // Receptury (dla uproszczenia)
    struct Receptura {
        std::string nazwa;
        int trudnosc; // 1 - łatwa, 2 - średnia, 3 - trudna
        int wymagane_materialy;
    };
    std::vector<Receptura> receptury_pergaminy;
    std::vector<Receptura> receptury_pisanie;


    // Ekwipunek (dla uproszczenia)
    int materialy;


public:
    Pisarz() : poziom(1), doswiadczenie(0), doswiadczenie_do_nastepnego_poziomu(0),
               n(0), luc_bonus(0), charisma_bonus(0.0), writer_bonus(0),
               pve_physical_dmg_bonus(0.0), pve_magical_dmg_bonus(0.0),
               materialy(100) { // Załóżmy, że zaczynamy ze 100 materiałami
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
        // Receptury pergaminów
        receptury_pergaminy.push_back({"Zwykły Pergamin", 1, 2});
        receptury_pergaminy.push_back({"Pergamin Enchantu", 2, 5});
        receptury_pergaminy.push_back({"Rzadki Pergamin", 3, 10});


        // Receptury pisania
        receptury_pisanie.push_back({"Księga Zaklęć", 1, 3});
        receptury_pisanie.push_back({"Scroll Enchantu", 2, 6});
        receptury_pisanie.push_back({"Rzadki Przepis", 3, 12});
    }


    void menu() {
        char wybor;
        do {
            std::cout << "Co chcesz zrobić?\n";
            std::cout << "1. Tworzyć pergaminy\n";
            std::cout << "2. Tworzyć dzieła pisarskie\n";
            std::cout << "3. Sprawdzić statystyki\n";
            std::cout << "4. Wyjść\n";
            std::cin >> wybor;


            switch (wybor) {
                case '1':
                    tworzenie_pergaminu();
                    break;
                case '2':
                    tworzenie_dziela_pisarskiego();
                    break;
                case '3':
                    wypisz_stan();
                    wypisz_statystyki();
                    break;
                case '4':
                    std::cout << "Do zobaczenia!\n";
                    break;
                default:
                    std::cout << "Nieznana opcja.\n";
                    break;
            }
            std::cout << "------------------------\n";
        } while (wybor != '4');
    }


    void tworzenie_pergaminu() {
        std::cout << "Wybierz pergamin do stworzenia:\n";
        for (size_t i = 0; i < receptury_pergaminy.size(); ++i) {
            std::cout << i + 1 << ". " << receptury_pergaminy[i].nazwa << " (Trudność: " << receptury_pergaminy[i].trudnosc
                      << ", Wymagane materiały: " << receptury_pergaminy[i].wymagane_materialy << ")\n";
        }


        int wybor_receptury;
        std::cin >> wybor_receptury;
        if (wybor_receptury < 1 || wybor_receptury > static_cast<int>(receptury_pergaminy.size())) {
            std::cout << "Nieprawidłowy wybór.\n";
            return;
        }


        Receptura wybrana_receptura = receptury_pergaminy[wybor_receptury - 1];


        std::cout << "Ile pergaminów chcesz stworzyć?\n";
        int ilosc;
        std::cin >> ilosc;


        int calkowity_koszt = wybrana_receptura.wymagane_materialy * ilosc;
        if (materialy < calkowity_koszt) {
            std::cout << "Nie masz wystarczającej ilości materiałów.\n";
            return;
        }


        materialy -= calkowity_koszt;


        // Mini-gra
        std::cout << "Rozpoczynasz tworzenie " << ilosc << " pergaminu(ów) " << wybrana_receptura.nazwa << ".\n";


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
            std::cout << "Nie udało Ci się rozpocząć tworzenia pergaminu.\n";
            return;
        }


        // Krok 2: Obrót i ruchy myszką
        int wymagane_powtorzenia = 0;
        switch (wybrana_receptura.trudnosc) {
            case 1:
                wymagane_powtorzenia = 3;
                break;
            case 2:
                wymagane_powtorzenia = 5;
                break;
            case 3:
                wymagane_powtorzenia = 7;
                break;
            default:
                wymagane_powtorzenia = 5;
                break;
        }


        for (int i = 0; i < wymagane_powtorzenia; ++i) {
            std::cout << "Wykonaj obrót myszką ('O') i ruch lewo-prawo ('R'). Masz 5 sekund.\n";
            bool obrot = false;
            bool ruch = false;
            start = std::chrono::steady_clock::now();
            while (std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
                if (_kbhit()) {
                    char ch = _getch();
                    if (ch == 'O' || ch == 'o') {
                        obrot = true;
                        std::cout << "Obrót wykonany.\n";
                    } else if (ch == 'R' || ch == 'r') {
                        ruch = true;
                        std::cout << "Ruch lewo-prawo wykonany.\n";
                    }
                    if (obrot && ruch) {
                        break;
                    }
                }
            }


            if (!(obrot && ruch)) {
                std::cout << "Nie udało Ci się poprawnie wykonać ruchów.\n";
                return;
            }
        }


        std::cout << "Udało Ci się stworzyć " << ilosc << " pergaminu(ów)!\n";
        zdobywaj_doswiadczenie(ilosc); // 1 pergamin = 1 exp
    }


    void tworzenie_dziela_pisarskiego() {
        std::cout << "Wybierz dzieło do stworzenia:\n";
        for (size_t i = 0; i < receptury_pisanie.size(); ++i) {
            std::cout << i + 1 << ". " << receptury_pisanie[i].nazwa << " (Trudność: " << receptury_pisanie[i].trudnosc
                      << ", Wymagane materiały: " << receptury_pisanie[i].wymagane_materialy << ")\n";
        }


        int wybor_receptury;
        std::cin >> wybor_receptury;
        if (wybor_receptury < 1 || wybor_receptury > static_cast<int>(receptury_pisanie.size())) {
            std::cout << "Nieprawidłowy wybór.\n";
            return;
        }


        Receptura wybrana_receptura = receptury_pisanie[wybor_receptury - 1];


        std::cout << "Ile dzieł chcesz stworzyć?\n";
        int ilosc;
        std::cin >> ilosc;


        int calkowity_koszt = wybrana_receptura.wymagane_materialy * ilosc;
        if (materialy < calkowity_koszt) {
            std::cout << "Nie masz wystarczającej ilości materiałów.\n";
            return;
        }


        materialy -= calkowity_koszt;


        // Mini-gra
        std::cout << "Rozpoczynasz tworzenie " << ilosc << " dzieła(ł) " << wybrana_receptura.nazwa << ".\n";


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
            std::cout << "Nie udało Ci się rozpocząć pisania.\n";
            return;
        }


        // Krok 2: Śledzenie linii
        int liczba_linii = 0;
        switch (wybrana_receptura.trudnosc) {
            case 1:
                liczba_linii = 1;
                break;
            case 2:
                liczba_linii = 2;
                break;
            case 3:
                liczba_linii = 3;
                break;
            default:
                liczba_linii = 2;
                break;
        }


        for (int i = 0; i < liczba_linii; ++i) {
            std::cout << "Śledź linię " << i + 1 << "! Wciśnij sekwencję klawiszy: 'A' -> 'S' -> 'D'. Masz 5 sekund.\n";
            bool a_wcisniete = false;
            bool s_wcisniete = false;
            bool d_wcisniete = false;
            start = std::chrono::steady_clock::now();


            while (std::chrono::steady_clock::now() - start < std::chrono::seconds(5)) {
                if (_kbhit()) {
                    char ch = _getch();
                    if (ch == 'A' || ch == 'a') {
                        a_wcisniete = true;
                        std::cout << "Klawisz 'A' wciśnięty.\n";
                    } else if ((ch == 'S' || ch == 's') && a_wcisniete && !s_wcisniete) {
                        s_wcisniete = true;
                        std::cout << "Klawisz 'S' wciśnięty.\n";
                    } else if ((ch == 'D' || ch == 'd') && s_wcisniete && !d_wcisniete) {
                        d_wcisniete = true;
                        std::cout << "Klawisz 'D' wciśnięty.\n";
                    }
                    if (a_wcisniete && s_wcisniete && d_wcisniete) {
                        break;
                    }
                }
            }


            if (!(a_wcisniete && s_wcisniete && d_wcisniete)) {
                std::cout << "Nie udało Ci się poprawnie śledzić linii.\n";
                return;
            }
        }


        std::cout << "Udało Ci się stworzyć " << ilosc << " dzieła(ł)!\n";
        zdobywaj_doswiadczenie(ilosc); // 1 dzieło = 1 exp
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
        luc_bonus += 1 * n;
        charisma_bonus += 0.1 * n;
        writer_bonus += 1 * n;
        pve_physical_dmg_bonus += 0.1 * n;
        pve_magical_dmg_bonus += 0.1 * n;


        std::cout << "Twoje statystyki zostały zaktualizowane!\n";
        wypisz_statystyki();
    }


    void wypisz_statystyki() {
        std::cout << "Statystyki:\n";
        std::cout << "Luc bonus: " << luc_bonus << "\n";
        std::cout << "Charisma bonus: " << charisma_bonus << "\n";
        std::cout << "Writer bonus: " << writer_bonus << "\n";
        std::cout << "PvE Physical Damage Bonus: " << pve_physical_dmg_bonus << "\n";
        std::cout << "PvE Magical Damage Bonus: " << pve_magical_dmg_bonus << "\n";
    }


    void wypisz_stan() {
        std::cout << "Poziom: " << poziom << "\n";
        std::cout << "Doświadczenie: " << doswiadczenie << "/" << doswiadczenie_do_nastepnego_poziomu << "\n";
        std::cout << "Posiadane materiały: " << materialy << "\n";
    }
};


int main() {
    Pisarz pisarz;
    pisarz.menu();
    return 0;
}
```
