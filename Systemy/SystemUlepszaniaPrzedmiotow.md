# System Ulepszania Przedmiotów

Ulepszanie przedmitów polega na wykorzystywaniu specjalnych kamieni, w których zawarta jest wspaniała energia życiowa.

Kamienie dzielą się na następujące podtypy:

```text
D -> C -> B -> A -> S -> Blessed S -> X -> X Lvl 1 -> X Lvl 2 -> X Lvl 3 -> X Dark Mode -> X Supreme Mode -> Legendary Set.
```

Każdy z kamieni ma unikalną moc, która zwiększa właściwości przedmiotu. Ulepszenie jest resetowany, gdy przedmiot przechodzi ewolucję.

Maksymalny poziom ulepszenia przedmiotów:

- Broń: +30
- Pancerz: +30
- Biżuteria: +30
- Inne: max +10 enchant

Szansa na sukces ulepszenia wynosi:

```text
n - aktualny poziom ulepszenia
100% - n*2%
```

Przykład:

- Na +0 szansa na upgrade to 100%
- Na +1 szansa na upgrade to 98%

## Kamienie

W grze możemy uzyskać poprzez craftowanie następujące przedmioty:

- **Niebiański kamień**
- **Kamienie doskonałe**

### Specjalne kamienie

**Blessed Stone**: zwiększa szansę enchantowania o 5% i w razie porażki obniża enchant o -1, zamiast niszczyć przedmiot.

**Goddess Stone**: zwiększa szansę enchantowania o 8% i w razie porażki nie obniża poziomu enchantu.

## System obliczania statystyk

```text
n – indeks enchantu
g – grade scrolla (wartość przypisana do danego poziomu enchantu)
```

### Dla broni

- Bonus p. atk = Bonus p. atk +1 \* (n) \* g / (g-1) \* (n+1)
- Bonus m. atk = Bonus m. atk +1 \* (n) \* g / (g-1) \* (n+1)

Co pięć enchantów:

- Bonus P. skill power = Bonus P. skill power +1 \* (n) \* g / (g-1) \* (n+1)
- Bonus M. skill power = Bonus M. skill power +1 \* (n) \* g / (g-1) \* (n+1) \* 100%

### Dla zbroi

- Bonus p. def = Bonus p. def +1 \* (n) \* g / (g-1) \* (2n+1)

Co pięć enchantów:

- Bonus P. skill critical dmg = Bonus P. skill critical dmg +1 \* (n) \* g / (g-1) \* (n+1)
- Bonus M. skill critical dmg = Bonus M. skill critical dmg +1 \* (n) \* g / (g-1) \* (n+1) \* 100%

### Dla biżuterii

- Bonus m. def = Bonus m. def +1 \* (n) \* g / (g-1) \* (2n+1)

Co pięć enchantów:

- Bonus P. skill critical dmg = Bonus P. skill critical dmg +1 \* (n) \* g / (g-1) \* (n+1)
- Bonus M. skill critical dmg = Bonus M. skill critical dmg +1 \* (n) \* g / (g-1) \* (n+1)

### Dla innych przedmiotów

Maksymalny poziom enchantu: +10

- Bonus P. skill critical dmg = Bonus P. skill critical dmg +1 \* (n) \* g / (g-1) \* (n+1)
- Bonus M. skill critical dmg = Bonus M. skill critical dmg +1 \* (n) \* g / (g-1) \* (n+1)
- Bonus P. skill power = Bonus P. skill power +1 \* (n) \* g / (g-1) \* (n+1)
- Bonus M. skill power = Bonus M. skill power +1 \* (n) \* g / (g-1) \* (n+1)

Jeśli wartość wynosi 0.5 lub więcej, to wynik jest zaokrąglany do wartości naturalnej, czyli **1**.

## Propozycja programu realizującego dany problem

```cpp
#include <iostream>
#include <cmath>
#include <cstdlib> // dla funkcji rand()
#include <ctime>   // dla funkcji time()


enum ItemType {
    WEAPON,
    ARMOR,
    JEWELRY,
    OTHER
};


enum StoneType {
    NORMAL,
    CELESTIAL,
    PERFECT
};


struct Item {
    ItemType type;
    int enchantLevel; // n
    int maxEnchantLevel;
    int scrollGrade;  // g
    StoneType stoneType;


    // Bazowe statystyki
    double basePAtk;
    double baseMAtk;
    double basePDef;
    double baseMDef;
    double basePSkillPower;
    double baseMSkillPower;
    double basePSkillCritDmg;
    double baseMSkillCritDmg;
    double baseMinusPSkillCritDmg;
    double baseMinusMSkillCritDmg;
    double baseMinusPSkillPower;
    double baseMinusMSkillPower;


    // Aktualne statystyki po enchantach
    double currentPAtk;
    double currentMAtk;
    double currentPDef;
    double currentMDef;
    double currentPSkillPower;
    double currentMSkillPower;
    double currentPSkillCritDmg;
    double currentMSkillCritDmg;
    double currentMinusPSkillCritDmg;
    double currentMinusMSkillCritDmg;
    double currentMinusPSkillPower;
    double currentMinusMSkillPower;


    // Konstruktor domyślny
    Item() : enchantLevel(0), maxEnchantLevel(30), scrollGrade(1), stoneType(NORMAL),
             basePAtk(0), baseMAtk(0), basePDef(0), baseMDef(0),
             basePSkillPower(0), baseMSkillPower(0),
             basePSkillCritDmg(0), baseMSkillCritDmg(0),
             baseMinusPSkillCritDmg(0), baseMinusMSkillCritDmg(0),
             baseMinusPSkillPower(0), baseMinusMSkillPower(0),
             currentPAtk(0), currentMAtk(0), currentPDef(0), currentMDef(0),
             currentPSkillPower(0), currentMSkillPower(0),
             currentPSkillCritDmg(0), currentMSkillCritDmg(0),
             currentMinusPSkillCritDmg(0), currentMinusMSkillCritDmg(0),
             currentMinusPSkillPower(0), currentMinusMSkillPower(0)
    {}
};


// Funkcja do obliczania bonusu w zależności od formuły
double CalculateBonus(int n, int g, double multiplier) {
    if (g <= 1) {
        return 0;
    }
    double value = multiplier * n * g / (g - 1) * (n + 1);


    // Jeśli wartość jest 0.5 lub wyższa, zaokrąglamy do 1
    if (value - static_cast<int>(value) >= 0.5) {
        value = std::ceil(value);
    } else {
        value = std::floor(value);
    }
    return value;
}


// Funkcja aktualizująca statystyki przedmiotu
void UpdateItemStats(Item& item) {
    int n = item.enchantLevel;
    int g = item.scrollGrade;


    // Resetowanie aktualnych statystyk do bazowych
    item.currentPAtk = item.basePAtk;
    item.currentMAtk = item.baseMAtk;
    item.currentPDef = item.basePDef;
    item.currentMDef = item.baseMDef;
    item.currentPSkillPower = item.basePSkillPower;
    item.currentMSkillPower = item.baseMSkillPower;
    item.currentPSkillCritDmg = item.basePSkillCritDmg;
    item.currentMSkillCritDmg = item.baseMSkillCritDmg;
    item.currentMinusPSkillCritDmg = item.baseMinusPSkillCritDmg;
    item.currentMinusMSkillCritDmg = item.baseMinusMSkillCritDmg;
    item.currentMinusPSkillPower = item.baseMinusPSkillPower;
    item.currentMinusMSkillPower = item.baseMinusMSkillPower;


    if (n == 0) {
        return; // Brak dodatkowych bonusów dla enchantu 0
    }


    switch (item.type) {
    case WEAPON: {
        double bonus = CalculateBonus(n, g, 1.0);
        item.currentPAtk += bonus;
        item.currentMAtk += bonus;


        if (n % 5 == 0) {
            item.currentPSkillPower += bonus;
            item.currentMSkillPower += bonus * 1.0; // *100%
        }
        break;
    }
    case ARMOR: {
        double bonus = CalculateBonus(n, g, 1.0);
        item.currentPDef += bonus;


        if (n % 5 == 0) {
            item.currentMinusPSkillCritDmg += bonus;
            item.currentMinusMSkillCritDmg += bonus * 1.0; // *100%
        }
        break;
    }
    case JEWELRY: {
        double bonus = CalculateBonus(n, g, 1.0);
        item.currentMDef += bonus;


        if (n % 5 == 0) {
            item.currentPSkillCritDmg += bonus;
            item.currentMSkillCritDmg += bonus;
        }
        break;
    }
    case OTHER: {
        if (n > 10) {
            n = 10; // Maksymalny enchant dla Others to +10
        }
        double bonus = CalculateBonus(n, g, 1.0);
        item.currentPSkillCritDmg += bonus;
        item.currentMSkillCritDmg += bonus;
        item.currentMinusPSkillCritDmg += bonus;
        item.currentMinusMSkillCritDmg += bonus;
        item.currentPSkillPower += bonus;
        item.currentMSkillPower += bonus;
        item.currentMinusPSkillPower += bonus;
        item.currentMinusMSkillPower += bonus;
        break;
    }
    default:
        break;
    }
}


// Funkcja do ulepszania przedmiotu
bool UpgradeItem(Item& item) {
    int n = item.enchantLevel;
    double successChance = 100.0 - n * 2.0;


    // Modyfikacja szansy na sukces w zależności od rodzaju kamienia
    switch (item.stoneType) {
    case CELESTIAL:
        successChance += 5.0;
        break;
    case PERFECT:
        successChance += 8.0;
        break;
    default:
        break;
    }


    if (successChance > 100.0) {
        successChance = 100.0;
    }


    // Generowanie losowej wartości dla symulacji sukcesu
    double randomValue = static_cast<double>(rand() % 10000) / 100.0; // 0.00 - 99.99
    bool success = randomValue < successChance;


    if (success) {
        // Ulepszenie się powiodło
        item.enchantLevel += 1;
        if (item.enchantLevel > item.maxEnchantLevel) {
            item.enchantLevel = item.maxEnchantLevel;
        }
    } else {
        // Ulepszenie nie powiodło się
        switch (item.stoneType) {
        case CELESTIAL:
            // Przedmiot nie zostaje zniszczony, poziom enchantu spada o 1
            item.enchantLevel -= 1;
            if (item.enchantLevel < 0) {
                item.enchantLevel = 0;
            }
            break;
        case PERFECT:
            // Przedmiot nie zostaje zniszczony, poziom enchantu nie zmienia się
            break;
        default:
            // Zwykły kamień: przedmiot zostaje zniszczony (w tej implementacji resetujemy enchant)
            item.enchantLevel = 0;
            break;
        }
    }


    // Aktualizacja statystyk przedmiotu po zmianie enchantu
    UpdateItemStats(item);


    return success;
}


int main() {
    srand(static_cast<unsigned int>(time(0))); // Inicjalizacja generatora liczb losowych


    // Przykładowy przedmiot
    Item myWeapon;
    myWeapon.type = WEAPON;
    myWeapon.enchantLevel = 0;
    myWeapon.maxEnchantLevel = 30;
    myWeapon.scrollGrade = 2; // Przykładowy grade scrolla (g)
    myWeapon.stoneType = NORMAL;


    // Bazowe statystyki
    myWeapon.basePAtk = 100.0;
    myWeapon.baseMAtk = 50.0;


    // Aktualizacja statystyk przed pierwszym ulepszeniem
    UpdateItemStats(myWeapon);


    std::cout << "Przedmiot przed ulepszeniem:\n";
    std::cout << "Poziom enchantu: " << myWeapon.enchantLevel << "\n";
    std::cout << "P.Atk: " << myWeapon.currentPAtk << "\n";
    std::cout << "M.Atk: " << myWeapon.currentMAtk << "\n\n";


    // Próbujemy ulepszyć przedmiot
    bool result = UpgradeItem(myWeapon);


    std::cout << "Ulepszanie zakończone: " << (result ? "Sukces" : "Porażka") << "\n";
    std::cout << "Poziom enchantu po ulepszeniu: " << myWeapon.enchantLevel << "\n";
    std::cout << "P.Atk: " << myWeapon.currentPAtk << "\n";
    std::cout << "M.Atk: " << myWeapon.currentMAtk << "\n";


    return 0;
}
```
