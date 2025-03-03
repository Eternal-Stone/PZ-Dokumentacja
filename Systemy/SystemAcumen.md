# System Acumen Crystals

## Opis systemu

System Acumen Crystals polega na wprowadzaniu do przedmiotów życiodajnych kryształów przenikliwości (Acumen Crystals), które oferują różne bonusy w zależności od podtypu przedmiotu. Jest to system identyfikacji przedmiotu, który pozwala odkryć jego prawdziwą naturę i ukazać jego ukrytą moc.

## Rozwój kryształów

- Kryształy przenikliwości dzielą się na poziomy (stage) od 1 do 15.
- Można je ulepszać poprzez wlewanie do nich życiodajnej mocy rzadkich minerałów.
- Im więcej minerałów zostanie przetopionych, tym potężniejszy staje się kryształ i oferuje lepsze efekty.

## Zasady stosowania kryształów

- Kryształy mogą być stosowane w dowolnych przedmiotach.
- Można je przenosić między przedmiotami za opłatą u NPC-a.
- Przy ulepszaniu wybierana jest jedna statystyka do wzmocnienia.
- Jeden kryształ może wzmacniać tylko jedną statystykę.
- Limit 3 kryształów na przedmiot (wstępne założenia).
- Aktywacja jednego bonusu w danej grupie blokuje aktywację innych bonusów z tej grupy
  - np. aktywacja "P. ATK bonus" uniemożliwia aktywację "M. ATK bonus".
- Szansa na sukces wynosi 100%.

***Do sprawdzenia**: czy każda statystyka z bonusem została opisana.*

## System bonusów i obliczanie ich wartości

Każdy bonus jest obliczany na podstawie poziomu kryształu według następujących wzorów:

```text
g - aktualny poziom kryształu przenikliwości
```

### Broń

- **P. ATK bonus** = `10 * log(g+10) * log(g+11) * log(g+12)`
- **M. ATK bonus** = `10 * log(g+10) * log(g+11) * log(g+12)`
- **Ogólny ATK bonus** = `5 * log(g+10) * log(g+11) * log(g+12)`
- **P. Skill Power bonus** = `3 * log(g+10) * log(g+11) * log(g+12)`
- **M. Skill Power bonus** = `3 * log(g+10) * log(g+11) * log(g+12)`
- **Strong against Statuses bonus** = `1 * log(g+10) * log(g+11) * log(g+12)`
- **Strong against Emperors bonus** = `1 * log(g+10) * log(g+11) * log(g+12)`
- **Strong against Monsters bonus** = `1 * log(g+10) * log(g+11) * log(g+12)`
- **PVM bonus** = `1 * log(g+10) * log(g+11) * log(g+12)`
- **PVP bonus** = `1 * log(g+10) * log(g+11) * log(g+12)`
- **PVE bonus** = `1 * log(g+10) * log(g+11) * log(g+12)`

### Pancerz

- **P. DEF bonus** = `4 * log(g+10) * log(g+11) * log(g+12)`
- **P. ATK bonus** = `5 * log(g+10) * log(g+11) * log(g+12)`
- **M. ATK bonus** = `5 * log(g+10) * log(g+11) * log(g+12)`
- **P. Skill Power bonus** = `1 * log(g+10) * log(g+11) * log(g+12)`
- **M. Skill Power bonus** = `1 * log(g+10) * log(g+11) * log(g+12)`
- **Strong against Statuses bonus** = `0.5 * log(g+10) * log(g+11) * log(g+12)`
- **Strong against Emperors bonus** = `0.5 * log(g+10) * log(g+11) * log(g+12)`
- **Strong against Monsters bonus** = `0.5 * log(g+10) * log(g+11) * log(g+12)`
- **PVM bonus** = `0.5 * log(g+10) * log(g+11) * log(g+12)`
- **PVP bonus** = `0.5 * log(g+10) * log(g+11) * log(g+12)`
- **PVE bonus** = `0.5 * log(g+10) * log(g+11) * log(g+12)`

### Biżuteria

- **M. DEF bonus** = `4 * log(g+10) * log(g+11) * log(g+12)`
- **P. ATK bonus** = `5 * log(g+10) * log(g+11) * log(g+12)`
- **M. ATK bonus** = `5 * log(g+10) * log(g+11) * log(g+12)`
- **P. Skill Power bonus** = `1 * log(g+10) * log(g+11) * log(g+12)`
- **M. Skill Power bonus** = `1 * log(g+10) * log(g+11) * log(g+12)`
- **Strong against Statuses bonus** = `0.5 * log(g+10) * log(g+11) * log(g+12)`
- **Strong against Emperors bonus** = `0.5 * log(g+10) * log(g+11) * log(g+12)`
- **Strong against Monsters bonus** = `0.5 * log(g+10) * log(g+11) * log(g+12)`
- **PVM bonus** = `0.5 * log(g+10) * log(g+11) * log(g+12)`
- **PVP bonus** = `0.5 * log(g+10) * log(g+11) * log(g+12)`
- **PVE bonus** = `0.5 * log(g+10) * log(g+11) * log(g+12)`

### Inne przedmioty

- **P. DEF bonus** = `4 * log(g+10) * log(g+11) * log(g+12)`
- **M. DEF bonus** = `4 * log(g+10) * log(g+11) * log(g+12)`
- **P. ATK bonus** = `5 * log(g+10) * log(g+11) * log(g+12)`
- **M. ATK bonus** = `5 * log(g+10) * log(g+11) * log(g+12)`
- **P. Skill Power bonus** = `1 * log(g+10) * log(g+11) * log(g+12)`
- **M. Skill Power bonus** = `1 * log(g+10) * log(g+11) * log(g+12)`
- **Strong against Statuses bonus** = `0.5 * log(g+10) * log(g+11) * log(g+12)`
- **Strong against Emperors bonus** = `0.5 * log(g+10) * log(g+11) * log(g+12)`
- **Strong against Monsters bonus** = `0.5 * log(g+10) * log(g+11) * log(g+12)`
- **PVM bonus** = `0.5 * log(g+10) * log(g+11) * log(g+12)`
- **PVP bonus** = `0.5 * log(g+10) * log(g+11) * log(g+12)`

## Propozycja programu realizującego dany problem

```cpp
#include <iostream>
#include <cmath>
#include <string>
#include <iomanip>

enum ItemType {
    WEAPON,
    ARMOR,
    JEWELRY,
    OTHER
};

struct Item {
    ItemType type;
    int acumenLevel; // g: Level of the Acumen crystal (1-15)
    // Base stats
    double basePAtk;
    double baseMAtk;
    double basePDef;
    double baseMDef;
    double basePSkillPower;
    double baseMSkillPower;
    double baseStrongAgainstStatues;
    double baseStrongAgainstEmperors;
    double baseStrongAgainstMonsters;
    double basePVM;
    double basePVP;
    double basePVE;
    // Current stats after Acumen bonuses
    double currentPAtk;
    double currentMAtk;
    double currentPDef;
    double currentMDef;
    double currentPSkillPower;
    double currentMSkillPower;
    double currentStrongAgainstStatues;
    double currentStrongAgainstEmperors;
    double currentStrongAgainstMonsters;
    double currentPVM;
    double currentPVP;
    double currentPVE;


    // Constructor to initialize base stats
    Item(ItemType itemType)
        : type(itemType), acumenLevel(0),
          basePAtk(0), baseMAtk(0), basePDef(0), baseMDef(0),
          basePSkillPower(0), baseMSkillPower(0),
          baseStrongAgainstStatues(0), baseStrongAgainstEmperors(0),
          baseStrongAgainstMonsters(0), basePVM(0), basePVP(0), basePVE(0),
          currentPAtk(0), currentMAtk(0), currentPDef(0), currentMDef(0),
          currentPSkillPower(0), currentMSkillPower(0),
          currentStrongAgainstStatues(0), currentStrongAgainstEmperors(0),
          currentStrongAgainstMonsters(0), currentPVM(0), currentPVP(0), currentPVE(0)
    {}
};


// Function to calculate bonuses based on item type and Acumen level
void applyAcumenBonus(Item& item) {
    int g = item.acumenLevel;
    if (g < 1 || g > 15) {
        std::cerr << "Acumen level must be between 1 and 15.\n";
        return;
    }


    // Calculate log values once to avoid redundancy
    double log1 = log(g + 10);
    double log2 = log(g + 11);
    double log3 = log(g + 12);


    // Total multiplier
    double multiplier = log1 * log2 * log3;


    // Assuming natural logarithm (base e)
    // If base 10 logarithm is required, use log10() instead


    switch (item.type) {
        case WEAPON:
            item.currentPAtk = item.basePAtk + 10 * multiplier;
            item.currentMAtk = item.baseMAtk + 10 * multiplier;
            item.currentPSkillPower = item.basePSkillPower + 3 * multiplier;
            item.currentMSkillPower = item.baseMSkillPower + 3 * multiplier;
            item.currentStrongAgainstStatues = item.baseStrongAgainstStatues + 1 * multiplier;
            item.currentStrongAgainstEmperors = item.baseStrongAgainstEmperors + 1 * multiplier;
            item.currentStrongAgainstMonsters = item.baseStrongAgainstMonsters + 1 * multiplier;
            item.currentPVM = item.basePVM + 1 * multiplier;
            item.currentPVP = item.basePVP + 1 * multiplier;
            item.currentPVE = item.basePVE + 1 * multiplier;
            break;
        case ARMOR:
        case JEWELRY:
            item.currentPDef = item.basePDef + 4 * multiplier;
            item.currentMDef = item.baseMDef + 4 * multiplier; // For Jewelry
            item.currentPAtk = item.basePAtk + 5 * multiplier;
            item.currentMAtk = item.baseMAtk + 5 * multiplier;
            item.currentPSkillPower = item.basePSkillPower + 1 * multiplier;
            item.currentMSkillPower = item.baseMSkillPower + 1 * multiplier;
            item.currentStrongAgainstStatues = item.baseStrongAgainstStatues + 0.5 * multiplier;
            item.currentStrongAgainstEmperors = item.baseStrongAgainstEmperors + 0.5 * multiplier;
            item.currentStrongAgainstMonsters = item.baseStrongAgainstMonsters + 0.5 * multiplier;
            item.currentPVM = item.basePVM + 0.5 * multiplier;
            item.currentPVP = item.basePVP + 0.5 * multiplier;
            item.currentPVE = item.basePVE + 0.5 * multiplier;
            break;
        case OTHER:
            item.currentPDef = item.basePDef + 4 * multiplier;
            item.currentMDef = item.baseMDef + 4 * multiplier;
            item.currentPAtk = item.basePAtk + 5 * multiplier;
            item.currentMAtk = item.baseMAtk + 5 * multiplier;
            item.currentPSkillPower = item.basePSkillPower + 1 * multiplier;
            item.currentMSkillPower = item.baseMSkillPower + 1 * multiplier;
            item.currentStrongAgainstStatues = item.baseStrongAgainstStatues + 0.5 * multiplier;
            item.currentStrongAgainstEmperors = item.baseStrongAgainstEmperors + 0.5 * multiplier;
            item.currentStrongAgainstMonsters = item.baseStrongAgainstMonsters + 0.5 * multiplier;
            item.currentPVM = item.basePVM + 0.5 * multiplier;
            item.currentPVP = item.basePVP + 0.5 * multiplier;
            item.currentPVE = item.basePVE + 0.5 * multiplier;
            break;
        default:
            std::cerr << "Unknown item type.\n";
            break;
    }
}


// Function to display item stats
void displayItemStats(const Item& item) {
    std::cout << std::fixed << std::setprecision(2);
    std::string itemType;
    switch (item.type) {
        case WEAPON: itemType = "Weapon"; break;
        case ARMOR: itemType = "Armor"; break;
        case JEWELRY: itemType = "Jewelry"; break;
        case OTHER: itemType = "Other"; break;
        default: itemType = "Unknown"; break;
    }
    std::cout << "Item Type: " << itemType << "\n";
    std::cout << "Acumen Level: " << item.acumenLevel << "\n";
    std::cout << "Current Stats after Acumen bonuses:\n";
    if (item.currentPAtk > 0)
        std::cout << "  Physical Attack (P.Atk): " << item.currentPAtk << "\n";
    if (item.currentMAtk > 0)
        std::cout << "  Magical Attack (M.Atk): " << item.currentMAtk << "\n";
    if (item.currentPDef > 0)
        std::cout << "  Physical Defense (P.Def): " << item.currentPDef << "\n";
    if (item.currentMDef > 0)
        std::cout << "  Magical Defense (M.Def): " << item.currentMDef << "\n";
    if (item.currentPSkillPower > 0)
        std::cout << "  Physical Skill Power: " << item.currentPSkillPower << "\n";
    if (item.currentMSkillPower > 0)
        std::cout << "  Magical Skill Power: " << item.currentMSkillPower << "\n";
    if (item.currentStrongAgainstStatues > 0)
        std::cout << "  Strong against Statues: " << item.currentStrongAgainstStatues << "\n";
    if (item.currentStrongAgainstEmperors > 0)
        std::cout << "  Strong against Emperors: " << item.currentStrongAgainstEmperors << "\n";
    if (item.currentStrongAgainstMonsters > 0)
        std::cout << "  Strong against Monsters: " << item.currentStrongAgainstMonsters << "\n";
    if (item.currentPVM > 0)
        std::cout << "  PVM Bonus: " << item.currentPVM << "\n";
    if (item.currentPVP > 0)
        std::cout << "  PVP Bonus: " << item.currentPVP << "\n";
    if (item.currentPVE > 0)
        std::cout << "  PVE Bonus: " << item.currentPVE << "\n";
    std::cout << "\n";
}


int main() {
    // Example usage
    Item myWeapon(WEAPON);
    myWeapon.acumenLevel = 5; // Set Acumen level (1-15)
    myWeapon.basePAtk = 100.0;
    myWeapon.baseMAtk = 50.0;
    myWeapon.basePSkillPower = 20.0;
    myWeapon.baseMSkillPower = 15.0;


    applyAcumenBonus(myWeapon);
    displayItemStats(myWeapon);


    Item myArmor(ARMOR);
    myArmor.acumenLevel = 10;
    myArmor.basePDef = 80.0;
    myArmor.basePAtk = 30.0;
    myArmor.baseMAtk = 25.0;


    applyAcumenBonus(myArmor);
    displayItemStats(myArmor);


    Item myJewelry(JEWELRY);
    myJewelry.acumenLevel = 7;
    myJewelry.baseMDef = 60.0;
    myJewelry.basePAtk = 20.0;
    myJewelry.baseMAtk = 35.0;


    applyAcumenBonus(myJewelry);
    displayItemStats(myJewelry);


    Item myOther(OTHER);
    myOther.acumenLevel = 12;
    myOther.basePDef = 40.0;
    myOther.baseMDef = 45.0;
    myOther.basePAtk = 15.0;
    myOther.baseMAtk = 20.0;


    applyAcumenBonus(myOther);
    displayItemStats(myOther);


    return 0;
}
```
