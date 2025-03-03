# System Peta

Ten system opiera się na zwierzaku, który jest kompanem gracza i wzmacnia go swoją aurą i obecnością. Pet jest astralnym zbiorem energii, który wspomaga postać w różnych aspektach gry.

- Wzmacnia siły fizyczne, magiczne i inne zdolności postaci.
- Może rozwijać swój poziom, stając się coraz silniejszym.

## Umiejętności peta

Pet posiada zestaw unikalnych umiejętności, które wpływają na postać. Dzięki nim gracz może uzyskać dodatkowe wzmocnienia, takie jak:

- Zwiększona regeneracja many lub zdrowia.
- Podwyższenie statystyk bojowych.
- Dodatkowe efekty wspomagające podczas walki.

## Przedmioty Astralne dla peta

Pet posiada zdolność do noszenia specjalnych przedmiotów astralnych, które wzmacniają jego sieć energetyczną. Efektem tego jest zwiększenie jego potencjału bojowego, co również przekłada się na wzmocnienia postaci. Przedmioty te mogą zwiększać:

- Wytrzymałość peta.
- Siłę jego umiejętności.
- Możliwości obronne oraz regeneracyjne.

## Runy Astralne

Nawet astralne postacie mogą być wzmacniane przez runy astralne. Te specjalne inskrypcje pozwalają na dalsze ulepszanie Peta, zwiększając jego efektywność w walce oraz wspomagającą rolę dla naszej postaci. Runy mogą poprawiać:

- Poziom mocy umiejętności.
- Efektywność aury wspierającej.
- Odpowiedź na nasze własne ataki oraz obronę.

## Smocze Księgi Astralne

Smocza rasa odkryła specjalne związki energetyczne zapisane w księgach, które wzmacniają sieć astralną Peta. Księgi te określają strukturę mocy w sposób łańcuchowy, co oznacza, że im więcej ich posiadamy, tym silniejszy staje się nasz Pet. Efekty ksiąg mogą obejmować:

- Zwiększenie synergii między nami a Petem.
- Nowe, unikalne umiejętności.
- Wzmocnienie podstawowych statystyk Peta.

### Poziomowanie peta

Maksymalny poziom Peta wynosi **200**. Każde **5 poziomów** oferuje dodatkowe wzmocnienia, co pozwala na progresję i personalizację zwierzaka.

```text
n = indeks poziomu

P.ATK bonus = P.ATK bonus + 5 * n
M.ATK bonus = M.ATK bonus + 7 * n
Status bonus = Status bonus + 1 * n
Determinacja bonus = Determinacja bonus + 1 * n
Dominacja bonus = Dominacja bonus + 1 * n
HP/MP bonus = HP/MP bonus + 30 * n
```

## Propozycja programu realizującego dany problem

```cpp
#include <iostream>

class Pet {
public:
    int level;
    const int maxLevel;
    int pAtkBonus;
    int mAtkBonus;
    int statusBonus;
    int determinationBonus;
    int dominationBonus;
    int hpMpBonus;

    Pet() : level(1), maxLevel(200), pAtkBonus(0), mAtkBonus(0), statusBonus(0),
            determinationBonus(0), dominationBonus(0), hpMpBonus(0) {}

    void levelUp(int levels) {
        level += levels;
        if (level > maxLevel) {
            level = maxLevel;
        }
        calculateBonuses();
    }

    void calculateBonuses() {
        // Resetujemy bonusy
        pAtkBonus = 0;
        mAtkBonus = 0;
        statusBonus = 0;
        determinationBonus = 0;
        dominationBonus = 0;
        hpMpBonus = 0;

        int n_max = level / 5; // Obliczamy ile razy pet osiągnął wielokrotność 5 poziomów

        // Obliczamy sumy arytmetyczne dla bonusów
        pAtkBonus = 5 * n_max * (n_max + 1) / 2;
        mAtkBonus = 7 * n_max * (n_max + 1) / 2;
        statusBonus = n_max * (n_max + 1) / 2;
        determinationBonus = n_max * (n_max + 1) / 2;
        dominationBonus = n_max * (n_max + 1) / 2;
        hpMpBonus = 30 * n_max * (n_max + 1) / 2;
    }

    void displayBonuses() {
        std::cout << "=== Statystyki Peta ===\n";
        std::cout << "Poziom Peta: " << level << "\n";
        std::cout << "P ATK Bonus: " << pAtkBonus << "\n";
        std::cout << "M ATK Bonus: " << mAtkBonus << "\n";
        std::cout << "Status Bonus: " << statusBonus << "\n";
        std::cout << "Determinacja Bonus: " << determinationBonus << "\n";
        std::cout << "Dominacja Bonus: " << dominationBonus << "\n";
        std::cout << "HP/MP Bonus: " << hpMpBonus << "\n";
    }
};

int main() {
    Pet pet;

    int levelsToAdd;
    std::cout << "Podaj liczbę poziomów do dodania dla Peta: ";
    std::cin >> levelsToAdd;

    pet.levelUp(levelsToAdd);
    pet.displayBonuses();

    return 0;
}
```
