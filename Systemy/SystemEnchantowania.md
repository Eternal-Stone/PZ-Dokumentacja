# System Enchantowania

Enchantowanie polega na czarowaniu danego przedmiotu poprzez wykorzystanie specjalnych Scrolli i energii zawartej w tych scrollach.

Scrolle dzielą się na podtypy:

```text
D -> C -> B -> A -> S -> Blessed S -> X -> X Lvl 1 -> X Lvl 2 -> X Lvl 3 -> X Dark Mode -> X Supreme Mode -> Legendary Set
```

Każdy ze scrolli ma w sobie zawartą inną moc, która zwiększa moce naszego przedmiotu. Bonus pozostaje po zmianie grade'u.

***Do ustalenia**: koszt enchantowania.*

Nasz enchant jest resetowany, kiedy nasz przedmiot przechodzi ewolucję.

Maksymalny enchant naszego przedmiotu to +30:

- Broń: +30
- Zbroja: +30
- Biżuteria: +30
- Inne: +10

## Jak obliczać szansę

```text
n - indeks stopnia enchantu
```

Szansa na sukces enchantu wynosi: `100% - n * 2%`

Dla przykładu:

- Na +0 szansa na enchant to 100%
- Na +1 szansa na enchant to 98%
- Na +2 szansa na enchant to 96%

W grze możemy uzyskać poprzez crafting **Blessed Scroll Enchant** oraz **Goddess Scroll Enchant**.

- **Blessed Scroll Enchant** daje większą szansę enchantowania o 5% i nie niszczy przedmiotu. W razie porażki przedmiot traci -1 enchant.
- **Goddess Scroll Enchant** daje większą szansę enchantowania o 8% i nie niszczy przedmiotu. W razie porażki przedmiot nie traci poziomu enchantu.

## System obliczania statystyk

```text
n - poziom enchantu (np. +1 = lvl 1, +30 = lvl 30)
g - poziom scrolla (D grade = 1, C grade = 2 itd.)
```

### Dla broni

- **Bonus P. Atk** = `Old Bonus P. Atk + Base P. Atk * (n) * g / (g-1) * (n+1) * 100%`
- **Bonus M. Atk** = `Old Bonus M. Atk + Base M. Atk * (n) * g / (g-1) * (n+1) * 100%`
- Co pięć enchantów:
  - **Bonus P. Skill Power** = `Old Bonus P. Skill Power + Base P. Skill Power * (n) * g / (g-1) * (n+1) * 100%`
  - **Bonus M. Skill Power** = `Old Bonus M. Skill Power + Base M. Skill Power * (n) * g / (g-1) * (n+1) * 100%`

### Dla zbroi

- **Bonus P. Def** = `Old Bonus P. Def + Base P. Def * (n) * g / (g-1) * (2n+1) * 100%`
- Co pięć enchantów:
  - **Bonus P. Skill Critical Dmg** = `Old Bonus P. Skill Critical Dmg + Base P. Skill Critical Dmg * (n) * g / (g-1) * (n+1) * 100%`
  - **Bonus M. Skill Critical Dmg** = `Old Bonus M. Skill Critical Dmg + Base M. Skill Critical Dmg * (n) * g / (g-1) * (n+1) * 100%`

### Dla biżuterii

- **Bonus M. Def** = `Old Bonus M. Def + Base M. Def * (n) * g / (g-1) * (2n+1) * 100%`
- Co pięć enchantów:
  - **Bonus P. Skill Critical Dmg** = `Old Bonus P. Skill Critical Dmg + Base P. Skill Critical Dmg * (n) * g / (g-1) * (n+1) * 100%`
  - **Bonus M. Skill Critical Dmg** = `Old Bonus M. Skill Critical Dmg + Base M. Skill Critical Dmg * (n) * g / (g-1) * (n+1) * 100%`

### Dla innych przedmiotów

- **Bonus P. Skill Critical Dmg** = `Old Bonus P. Skill Critical Dmg + Base P. Skill Critical Dmg * (n) * g / (g-1) * (n+1) * 100%`
- **Bonus M. Skill Critical Dmg** = `Old Bonus M. Skill Critical Dmg + Base M. Skill Critical Dmg * (n) * g / (g-1) * (n+1) * 100%`
- **Bonus P. Skill Power** = `Old Bonus P. Skill Power + Base P. Skill Power * (n) * g / (g-1) * (n+1) * 100%`
- **Bonus M. Skill Power** = `Old Bonus M. Skill Power + Base M. Skill Power * (n) * g / (g-1) * (n+1) * 100%`

Jeśli wartość wynosi **0.5 lub więcej**, to zaokrąglamy ją do **1**.

## Propozycja programu realizującego dany problem

```cpp
#include <iostream>
#include <string>
#include <cstdlib>  // For rand() and srand()
#include <ctime>    // For time()


// Enum for item types
enum class ItemType {
    Weapon,
    Armor,
    Jewelry,
    Others
};


// Enum for scroll types
enum class ScrollType {
    Normal,
    Blessed,
    Goddess
};


// Struct to represent an item
struct Item {
    ItemType type;
    int grade;            // Grade lvl 'g', e.g., D=1, C=2, ..., Legendary=12
    int enchantLevel;     // Current enchant level 'n'
    double basePAtk;      // Base Physical Attack
    double baseMAtk;      // Base Magical Attack
    double basePDef;      // Base Physical Defense
    double baseMDef;      // Base Magical Defense
    double bonusPAtk;     // Current bonus Physical Attack
    double bonusMAtk;     // Current bonus Magical Attack
    double bonusPDef;     // Current bonus Physical Defense
    double bonusMDef;     // Current bonus Magical Defense
    // Add other base stats and bonus stats as needed
};


// Function to perform enchantment
bool EnchantItem(Item& item, ScrollType scrollType) {
    // Calculate success chance
    int n = item.enchantLevel;
    double successChance = 100.0 - n * 2.0;


    // Adjust success chance based on scroll type
    if (scrollType == ScrollType::Blessed) {
        successChance += 5.0;
    } else if (scrollType == ScrollType::Goddess) {
        successChance += 8.0;
    }


    // Ensure success chance is not over 100% or below 0%
    if (successChance > 100.0) successChance = 100.0;
    if (successChance < 0.0) successChance = 0.0;


    // Generate a random number to determine success or failure
    srand(static_cast<unsigned int>(time(0)));  // Seed the random number generator
    double roll = static_cast<double>(rand() % 100) + 1.0;


    bool success = roll <= successChance;


    if (success) {
        // Enchantment succeeded
        item.enchantLevel += 1;


        int g = item.grade;  // Grade lvl
        double gFactor = static_cast<double>(g) / (g - 1);
        double enchantMultiplier = n * gFactor * (n + 1) / 100.0;


        // Update stats based on item type
        if (item.type == ItemType::Weapon) {
            // Update Physical Attack
            item.bonusPAtk += item.basePAtk * enchantMultiplier;


            // Update Magical Attack
            item.bonusMAtk += item.baseMAtk * enchantMultiplier;


            // Every five enchants, update skill power
            if (item.enchantLevel % 5 == 0) {
                // Assuming we have base skill power stats
                // item.bonusPSkillPower += item.basePSkillPower * enchantMultiplier;
                // item.bonusMSkillPower += item.baseMSkillPower * enchantMultiplier;
            }
        } else if (item.type == ItemType::Armor) {
            // Update Physical Defense
            double defMultiplier = n * gFactor * (2 * n + 1) / 100.0;
            item.bonusPDef += item.basePDef * defMultiplier;


            // Every five enchants, update critical damage resistance
            if (item.enchantLevel % 5 == 0) {
                // item.bonusNegatePSkillCritDmg += item.baseNegatePSkillCritDmg * enchantMultiplier;
                // item.bonusNegateMSkillCritDmg += item.baseNegateMSkillCritDmg * enchantMultiplier;
            }
        } else if (item.type == ItemType::Jewelry) {
            // Update Magical Defense
            double defMultiplier = n * gFactor * (2 * n + 1) / 100.0;
            item.bonusMDef += item.baseMDef * defMultiplier;


            // Every five enchants, update critical damage
            if (item.enchantLevel % 5 == 0) {
                // item.bonusPSkillCritDmg += item.basePSkillCritDmg * enchantMultiplier;
                // item.bonusMSkillCritDmg += item.baseMSkillCritDmg * enchantMultiplier;
            }
        } else if (item.type == ItemType::Others) {
            // Max enchant level is +10
            if (item.enchantLevel > 10) item.enchantLevel = 10;


            // Update various stats
            // item.bonusPSkillCritDmg += item.basePSkillCritDmg * enchantMultiplier;
            // item.bonusMSkillCritDmg += item.baseMSkillCritDmg * enchantMultiplier;
            // Update other bonuses as per your formula
        }


        std::cout << "Enchantment succeeded! New enchant level: +" << item.enchantLevel << std::endl;
        return true;
    } else {
        // Enchantment failed
        if (scrollType == ScrollType::Normal) {
            // Item is destroyed or enchant level resets
            std::cout << "Enchantment failed. Item destroyed or enchant level reset." << std::endl;
            // Handle item destruction or reset as per game rules
            // For this example, we'll reset enchant level to 0
            item.enchantLevel = 0;
            item.bonusPAtk = 0;
            item.bonusMAtk = 0;
            item.bonusPDef = 0;
            item.bonusMDef = 0;
        } else if (scrollType == ScrollType::Blessed) {
            // Enchant level decreases by 1
            if (item.enchantLevel > 0) item.enchantLevel -= 1;
            std::cout << "Enchantment failed. Enchant level decreased by 1." << std::endl;
        } else if (scrollType == ScrollType::Goddess) {
            // Enchant level remains the same
            std::cout << "Enchantment failed. Enchant level remains the same." << std::endl;
        }
        return false;
    }
}


// Example usage
int main() {
    // Create an example weapon item
    Item sword;
    sword.type = ItemType::Weapon;
    sword.grade = 2;  // Example grade lvl for C-grade
    sword.enchantLevel = 0;
    sword.basePAtk = 100.0;
    sword.baseMAtk = 50.0;
    sword.bonusPAtk = 0.0;
    sword.bonusMAtk = 0.0;


    // Perform enchantment using a normal scroll
    EnchantItem(sword, ScrollType::Normal);


    // Output the updated stats
    std::cout << "Weapon Stats after Enchantment:" << std::endl;
    std::cout << "Enchant Level: +" << sword.enchantLevel << std::endl;
    std::cout << "Bonus P.Atk: " << sword.bonusPAtk << std::endl;
    std::cout << "Bonus M.Atk: " << sword.bonusMAtk << std::endl;


    return 0;
}
```
