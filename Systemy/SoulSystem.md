# Soul System

Soul System to system, w którym po pokonaniu **Cesarza Ciemności** zdobędziemy **Amulet Ciemności**. Jest to potężny artefakt o zdolności pochłaniania cząstek energii dusz z pokonanych przeciwników.

Cząstki dusz możemy również wyodrębnić (wyciągnąć) w Amulecie Cesarza. Cały proces korzystania z tego legendarnego przedmiotu poznajemy w Zapomnianych Komnatach.

Z cząstek energii jesteśmy w stanie stworzyć przedmiot Soul Orb. W książce znajdują się opisy różnych typów tych orbów oraz sposób ich ewolucji.

Drugim sposobem użycia cząstek energii jest nasycanie przedmiotów. Proces ten polega na przelaniu energii na dany przedmiot.

Niestety, nie można jednorazowo wlać zbyt dużej ilości energii, ponieważ przedmiot ulegnie zniszczeniu. Sam przedmiot i energia dusz muszą się do siebie dostosować. Nasycanie na silniejszy poziom odbywa się w cyklach i w odpowiednich odstępach czasu.

Nasycenie przedmiotu odblokowuje unikatowe zdolności oraz animacje dla klasy.

## Przykłady specjalnych właściwości

### Zdolności i gameplay

1. **Shadow Rebirth** – Po śmierci gracz odradza się jako eteryczny cień na 5 sekund, mogąc uciec lub zadać ostatni cios.

2. **Soul Surge** – Każde trafienie podstawowym atakiem ładuje energię, a przy pełnym pasku postać wykonuje potężny atak obszarowy.

3. **Echo Strike** – Po uderzeniu przeciwnika, duchowa kopia gracza powtarza ten sam cios z opóźnieniem.

4. **Phantom Dash** – Unik, który zostawia za sobą cienisty ślad – dotknięcie go przez wroga spowalnia go na 2 sekundy.

5. **Abyssal Chains** – Uderzenie bronią tworzy łańcuchy energii, które na krótko unieruchamiają przeciwnika.

6. **Soul Infusion** – Broń zmienia swój żywioł w zależności od pochłoniętych dusz, np. ogień, lód, błyskawice.

7. **Ethereal Strike** – Cios ignorujący 30% obrony przeciwnika, jeśli postać jest w cieniu.

8. **Void Step** – Pozwala teleportować się na krótką odległość, zostawiając po sobie iluzoryczny klon.

9. **Spirit Guardian** – Przywołuje eterycznego strażnika, który odbija 10% obrażeń wroga.

10. **Doom Mark** – Trafienie wroga nakłada klątwę, która po kilku sekundach eksploduje, zadając dodatkowe obrażenia.

### Animacje i efekty wizualne

1. **Aura Duszy** – Po aktywowaniu zdolności wokół postaci pojawia się migocząca, mistyczna poświata.

2. **Znikające Kroki** – Podczas ruchu gracz zostawia za sobą subtelne, błękitne ślady dusz.

3. **Widmowy Cień** – Po wykonaniu uniku przez chwilę widoczny jest półprzezroczysty sobowtór postaci.

4. **Efekt Pęknięcia Duszy** – Ataki krytyczne sprawiają, że przeciwnik na chwilę pęka jak szklana rzeźba i rozpada się w powietrzu.

5. **Duchowy Wybuch** – Przy zabiciu przeciwnika jego ciało znika w wirze energetycznych cząsteczek.

6. **Rozbłysk Ostatecznego Ciosu** – Ostatnie uderzenie wroga powoduje nagły rozbłysk czarnej lub złotej energii.

7. **Iluzoryczne Ostrze** – Broń zostawia smugi energii, które wyglądają jak dodatkowe klingi.

8. **Eteryczna Przemiana** – W momencie aktywacji zdolności gracz na chwilę staje się półprzezroczysty.

9. **Zawieszenie w Powietrzu** – Podczas channelowania magii gracz unosi się delikatnie nad ziemią.

10. **Eksplozja Dusz** – Przy aktywacji najwyższego poziomu nasycenia, postać na chwilę otacza krąg pulsujących dusz.

## Propozycja programu realizującego dany problem

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <map>
#include <iomanip>


// Enum for Item Types
enum ItemType {
    WEAPON,
    ARMOR,
    OTHER
};


// Struct for Item Bonuses
struct BonusStats {
    double pAtk;      // Physical Attack Bonus
    double mAtk;      // Magical Attack Bonus
    double pDef;      // Physical Defense Bonus
    double mDef;      // Magical Defense Bonus
    double hp;        // Health Points Bonus
    double mp;        // Mana Points Bonus
    // ... Add other bonuses as needed


    // Constructor to initialize bonuses
    BonusStats()
        : pAtk(0), mAtk(0), pDef(0), mDef(0), hp(0), mp(0) {}
};


// Struct for Item
struct Item {
    std::string name;
    ItemType type;
    BonusStats baseBonuses;    // Original bonuses
    BonusStats currentBonuses; // Bonuses after enhancements
    int saturationLevel;       // n: Saturation level
    int maxSaturationLevel;    // Max saturation level based on item type


    // Constructor
    Item(const std::string& itemName, ItemType itemType)
        : name(itemName), type(itemType), saturationLevel(0) {
        // Set max saturation level based on item type
        switch (type) {
            case WEAPON: maxSaturationLevel = 50; break;
            case ARMOR:  maxSaturationLevel = 30; break;
            case OTHER:  maxSaturationLevel = 20; break;
            default:     maxSaturationLevel = 0;  break;
        }
        // Initialize current bonuses to base bonuses
        currentBonuses = baseBonuses;
    }


    // Function to display item stats
    void displayStats() const {
        std::cout << "Item: " << name << "\n";
        std::cout << "Type: " << getItemTypeName() << "\n";
        std::cout << "Saturation Level: " << saturationLevel << "/" << maxSaturationLevel << "\n";
        std::cout << "Bonuses:\n";
        displayBonus("Physical Attack", baseBonuses.pAtk, currentBonuses.pAtk);
        displayBonus("Magical Attack", baseBonuses.mAtk, currentBonuses.mAtk);
        displayBonus("Physical Defense", baseBonuses.pDef, currentBonuses.pDef);
        displayBonus("Magical Defense", baseBonuses.mDef, currentBonuses.mDef);
        displayBonus("Health Points", baseBonuses.hp, currentBonuses.hp);
        displayBonus("Mana Points", baseBonuses.mp, currentBonuses.mp);
        // ... Display other bonuses as needed
        std::cout << "\n";
    }


private:
    std::string getItemTypeName() const {
        switch (type) {
            case WEAPON: return "Weapon";
            case ARMOR:  return "Armor";
            case OTHER:  return "Other";
            default:     return "Unknown";
        }
    }


    void displayBonus(const std::string& name, double baseValue, double currentValue) const {
        if (baseValue != 0 || currentValue != 0) {
            std::cout << "  " << name << ": Base = " << baseValue
                      << ", Current = " << std::fixed << std::setprecision(2) << currentValue << "\n";
        }
    }
};


// Function to perform saturation on an item
void saturateItem(Item& item, int levelsToSaturate) {
    if (levelsToSaturate <= 0) {
        std::cout << "Invalid saturation levels.\n";
        return;
    }


    int newSaturationLevel = item.saturationLevel + levelsToSaturate;


    if (newSaturationLevel > item.maxSaturationLevel) {
        std::cout << "Cannot saturate beyond maximum level (" << item.maxSaturationLevel << ").\n";
        levelsToSaturate = item.maxSaturationLevel - item.saturationLevel;
        newSaturationLevel = item.maxSaturationLevel;
    }


    // Update saturation level
    item.saturationLevel = newSaturationLevel;


    // Calculate total percentage increase
    double n = static_cast<double>(item.saturationLevel);
    double percentageIncrease = n / 100.0;


    // Additional bonus for every +5 saturation
    int bonusIncrements = item.saturationLevel / 5;
    double additionalBonus = bonusIncrements * 0.02; // Each +5 grants an extra 2%


    // Total multiplier
    double totalMultiplier = 1.0 + percentageIncrease + additionalBonus;


    // Update current bonuses
    item.currentBonuses.pAtk = item.baseBonuses.pAtk * totalMultiplier;
    item.currentBonuses.mAtk = item.baseBonuses.mAtk * totalMultiplier;
    item.currentBonuses.pDef = item.baseBonuses.pDef * totalMultiplier;
    item.currentBonuses.mDef = item.baseBonuses.mDef * totalMultiplier;
    item.currentBonuses.hp   = item.baseBonuses.hp   * totalMultiplier;
    item.currentBonuses.mp   = item.baseBonuses.mp   * totalMultiplier;
    // ... Update other bonuses as needed


    std::cout << "Item saturated by " << levelsToSaturate << " levels.\n";
}


// Example usage
int main() {
    // Create an example weapon
    Item myWeapon("Sword of Legends", WEAPON);
    myWeapon.baseBonuses.pAtk = 100.0;
    myWeapon.baseBonuses.mAtk = 50.0;
    myWeapon.baseBonuses.hp = 200.0;


    // Display initial stats
    std::cout << "Before Saturation:\n";
    myWeapon.displayStats();


    // Perform saturation
    saturateItem(myWeapon, 10);


    // Display stats after saturation
    std::cout << "After Saturation:\n";
    myWeapon.displayStats();


    // Further saturation
    saturateItem(myWeapon, 15);


    // Display stats after further saturation
    std::cout << "After Further Saturation:\n";
    myWeapon.displayStats();


    // Attempt to over-saturate
    saturateItem(myWeapon, 30);


    // Display final stats
    std::cout << "Final Stats:\n";
    myWeapon.displayStats();


    return 0;
}
```
