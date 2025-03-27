# System Personalizacji Statystyk

System personalizacji pozwala na wybranie dodatkowych statystyk (maksymalnie 5) po ewolucji przedmiotu (przejście na wyższy grade).

## Świadomość Przedmiotu

W zależności od grade'u przedmiotów świadomość przedmiotu narasta:

Przedmioty dzielą się na:

```text
D -> C -> B -> A -> S -> Blessed S -> X -> X Lvl 1 -> X Lvl 2 -> X Lvl 3 -> X Dark Mode -> X Supreme Mode -> Legendary Set
```

Świadomość przedmiotu to wskaźnik określający liczbę dodatkowych statystyk, jakie przedmiot może posiadać:

- **Na poziomie X** przedmiot otrzymuje pierwszy dar świadomości, pozwalający wybrać jedną statystykę.
- **Na poziomie X Dark Mode** możliwe jest wybranie dwóch statystyk.
- **Na poziomie Supreme Mode** możliwe jest wybranie czterech statystyk.
- **Na poziomie Legendarnym** możliwe jest wybranie aż pięciu statystyk.

Można wybierać te same statystyki wielokrotnie. Wszystkie statystyki się ze sobą sumują, zarówno w obrębie jednego przedmiotu, jak i pomiędzy różnymi przedmiotami.

## Statystyki

### Statystyki Ofensywne

Bonus personalizacyjny = current stat + current stat * **3%**

- **Increased Damage to Rulers** – Zwiększa obrażenia przeciwko Władcom.
  
  `Total Damage = Base Damage + (Base Damage × Increased Damage to Emperors %)`

- **Increased Damage to Statues** – Zwiększa obrażenia przeciwko Posągom.
  
  `Total Damage = Base Damage + (Base Damage × Increased Damage to Statues %)`

- **Increased Damage in Specific Areas** – Zwiększa obrażenia w określonych lokacjach.
  
  `Total Damage = Base Damage + (Base Damage × Increased Damage in Specific Areas %)`

- **Increased Damage to Humans** – Zwiększa obrażenia przeciwko Ludziom.
  
  `Total Damage = Base Damage + (Base Damage × Increased Damage to Humans%)`

- **Precision** – Zwiększa obrażenia krytyczne.
  
  `Critical Damage = Base Critical Damage + (Base Critical Damage × Precision %)`

- **Destruction** – Redukuje wartość pancerza przeciwnika.
  
  `Effective Enemy Armor = Enemy Armor × (1 - Destruction %)`

- **Aggression** – Zadaje dodatkowe obrażenia zależne od HP przeciwnika.
  
  ```text
  Additional Damage = Enemy Current HP × Aggression %
  Total Damage = Base Damage + Additional Damage
  ```

- **Domination** – Wzmacnia obrażenia i efekty zaklęć przeciwko Władcom.
  
  `Total Damage = Base Damage + (Base Damage × Domination%)`

- **Auto Attack Damage Bonus** – Dodaje stały bonus do obrażeń ataków podstawowych.
  
  `Total Damage = Base Damage + Auto Attack Damage Bonus`

- **AOE Damage** – Zwiększa obrażenia obszarowe.
  
  `AOE Damage = Base AOE Damage + (Base AOE Damage × AOE Damage %)`

- **Physical Attack (P.Atk)** – Podstawowa wartość fizycznych obrażeń.
  
  `Physical Damage = P.Atk + Modifiers`

- **Magical Attack (M.Atk)** – Podstawowa wartość magicznych obrażeń.
  
  `Magical Damage = M.Atk + Modifiers`

### Statystyki Defensywne

Bonus personalizacyjny = current stat + current stat * **2%**

- **Resistance to Humans** – Redukuje obrażenia otrzymane od Ludzi.
  
  `Damage Received = Base Damage - (Base Damage × Resistance to Humans %)`

- **Resistance to Critical Damage** – Redukuje dodatkowe obrażenia od trafień krytycznych.
  
  `Critical Damage Received = Additional Critical Damage - (Additional Critical Damage × Resistance to Critical Damage %)`

- **Physical Resistance** – Redukuje obrażenia fizyczne.
  
  `Physical Damage Received = Physical Damage - (Physical Damage × Physical Resistance %)`

- **Tenacity** – Zmniejsza efekt agresji.
  
  `Aggression Damage Received = Aggression Damage - (Aggression Damage × Tenacity %)`

- **Maximum HP %** – Zwiększa maksymalne HP.
  
  `Max HP = Base HP + (Base HP × Maximum HP %)`

### Statystyki Związane z Zasobami

Bonus personalizacyjny = current stat + current stat * **3.5%**

- **Gold Bonus** – Szansa na potrojenie zdobytego złota od Władców.

  - Szansa na potrojenie: `Chance = Gold Bonus %`
  - Formuła: `Gold Amount = Base Gold + (Base Gold × 200%)`

- **Kleptomancy** – Zwiększa szansę na zdobycie przedmiotów od przeciwników.
  
  `Total Drop Chance = Base Drop Chance + (Base Drop Chance × Kleptomancy %)`

- **Mining Power** – Zwiększa obrażenia zadawane złożom rud.
  
  `Total Damage to Ore = Base Damage + Mining Power`

- **Harvest** – Szansa na potrojenie zasobów z roślin.

  - Szansa na potrojenie: `Chance = Harvest %`
  - Formuła: `Resource Amount = Base Amount + (Base Amount × 200%)`

### Atak i Odporność Atrybutowa

Bonus personalizacyjny = current stat + current stat * **1.75%**

- **Attribute Attack** – Dodaje obrażenia żywiołowe (Ogień, Woda, Ziemia, Wiatr, Świętość, Ciemność).
  
  `Total Damage = Base Damage + Attribute Attack`

- **Attribute Resistance** – Redukuje obrażenia od ataków żywiołowych.
  
  `Damage Received = Damage - (Damage × Attribute Resistance %)`

### Statystyki Walki

Bonus personalizacyjny = current stat + current stat * **3.75%**

- **Physical Attack (P.Atk)** – Podstawowa wartość obrażeń fizycznych.
  
  `Physical Damage = P.Atk + Modifiers`

- **Magical Attack (M.Atk)** – Podstawowa wartość obrażeń magicznych.
  
  `Magical Damage = M.Atk + Modifiers`

- **Physical Defense (P.Def)** – Redukuje obrażenia fizyczne.
  
  `Damage Received = Incoming Damage - (P.Def × Reduction Coefficient)`

- **Magical Defense (M.Def)** – Redukuje obrażenia magiczne.
  
  `Damage Received = Incoming Magic Damage - (M.Def × Reduction Coefficient)`

- **Physical Accuracy** – Określa precyzję ataków fizycznych.
  
  `Hit Chance = Base Chance + (P. Accuracy × Percentage Increase)`

- **Physical Evasion** – Zwiększa szansę na uniknięcie ataku fizycznego.
  
  `Evade Chance = Base Chance + (P. Evasion × Percentage Increase)`

### Statystyki PvP i PvE

Bonus personalizacyjny = current stat + current stat * **2.25%**

- **PvP Physical Damage** – Redukuje fizyczne obrażenia otrzymane od graczy.
  
  `PvP Physical Damage Received = Damage - (Damage × PvP P. Dmg %)`

- **PvP Magical Damage** – Redukuje magiczne obrażenia otrzymane od graczy.
  
  `PvP Magical Damage Received = Damage - (Damage × PvP M. Dmg %)`

- **PvE Physical Damage** – Redukuje fizyczne obrażenia otrzymane od potworów.
  
  `PvE Physical Damage Received = Damage - (Damage × PvE P. Dmg %)`

- **PvE Magical Damage** – Redukuje magiczne obrażenia otrzymane od potworów.
  
  `PvE Magical Damage Received = Damage - (Damage × PvE M. Dmg %)`

## Propozycja programu realizującego dany problem

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <map>


// Enum dla klas przedmiotów
enum class ItemGrade {
    D,
    C,
    B,
    A,
    S,
    BlessedS,
    X,
    XLv1,
    XLv2,
    XLv3,
    XDarkMode,
    XSupremeMode,
    LegendarySet
};


// Mapowanie ItemGrade na nazwy
std::map<ItemGrade, std::string> itemGradeNames = {
    {ItemGrade::D, "D"},
    {ItemGrade::C, "C"},
    {ItemGrade::B, "B"},
    {ItemGrade::A, "A"},
    {ItemGrade::S, "S"},
    {ItemGrade::BlessedS, "Blessed S"},
    {ItemGrade::X, "X"},
    {ItemGrade::XLv1, "X Lvl 1"},
    {ItemGrade::XLv2, "X Lvl 2"},
    {ItemGrade::XLv3, "X Lvl 3"},
    {ItemGrade::XDarkMode, "X Dark Mode"},
    {ItemGrade::XSupremeMode, "X Supreme Mode"},
    {ItemGrade::LegendarySet, "Legendary Set"}
};


// Enum dla kategorii statystyk
enum class StatCategory {
    Offensive,
    Defensive,
    Other,
    Attribute,
    Combat,
    PvP_PvE
};


// Enum dla typów statystyk
enum class StatType {
    // Statystyki Ofensywne
    IncreasedDamageToRulers,
    IncreasedDamageToStatues,
    IncreasedDamageInSpecificAreas,
    IncreasedDamageToHumans,
    Precision,
    Destruction,
    Aggression,
    Domination,
    AutoAttackDamageBonus,
    AOEDamage,
    PhysicalAttack,
    MagicalAttack,


    // Statystyki Defensywne
    ResistanceToHumans,
    ResistanceToCriticalDamage,
    PhysicalResistance,
    Tenacity,
    MaximumHPPercent,


    // Inne Statystyki
    GoldBonus,
    Kleptomancy,
    MiningPower,
    Harvest,


    // Atak i Odporność Atrybutowa
    AttributeAttack,
    AttributeResistance,


    // Statystyki Walki
    PhysicalDefense,
    MagicalDefense,
    PhysicalAccuracy,
    PhysicalEvasion,


    // Statystyki PvP i PvE
    PvPPhysicalDamage,
    PvPMagicalDamage,
    PvEPhysicalDamage,
    PvEMagicalDamage
};


// Mapowanie StatType na nazwy
std::map<StatType, std::string> statTypeNames = {
    // Statystyki Ofensywne
    {StatType::IncreasedDamageToRulers, "Increased Damage to Rulers"},
    {StatType::IncreasedDamageToStatues, "Increased Damage to Statues"},
    {StatType::IncreasedDamageInSpecificAreas, "Increased Damage in Specific Areas"},
    {StatType::IncreasedDamageToHumans, "Increased Damage to Humans"},
    {StatType::Precision, "Precision"},
    {StatType::Destruction, "Destruction"},
    {StatType::Aggression, "Aggression"},
    {StatType::Domination, "Domination"},
    {StatType::AutoAttackDamageBonus, "Auto Attack Damage Bonus"},
    {StatType::AOEDamage, "AOE Damage"},
    {StatType::PhysicalAttack, "Physical Attack"},
    {StatType::MagicalAttack, "Magical Attack"},


    // Statystyki Defensywne
    {StatType::ResistanceToHumans, "Resistance to Humans"},
    {StatType::ResistanceToCriticalDamage, "Resistance to Critical Damage"},
    {StatType::PhysicalResistance, "Physical Resistance"},
    {StatType::Tenacity, "Tenacity"},
    {StatType::MaximumHPPercent, "Maximum HP %"},


    // Inne Statystyki
    {StatType::GoldBonus, "Gold Bonus"},
    {StatType::Kleptomancy, "Kleptomancy"},
    {StatType::MiningPower, "Mining Power"},
    {StatType::Harvest, "Harvest"},


    // Atak i Odporność Atrybutowa
    {StatType::AttributeAttack, "Attribute Attack"},
    {StatType::AttributeResistance, "Attribute Resistance"},


    // Statystyki Walki
    {StatType::PhysicalDefense, "Physical Defense"},
    {StatType::MagicalDefense, "Magical Defense"},
    {StatType::PhysicalAccuracy, "Physical Accuracy"},
    {StatType::PhysicalEvasion, "Physical Evasion"},


    // Statystyki PvP i PvE
    {StatType::PvPPhysicalDamage, "PvP Physical Damage"},
    {StatType::PvPMagicalDamage, "PvP Magical Damage"},
    {StatType::PvEPhysicalDamage, "PvE Physical Damage"},
    {StatType::PvEMagicalDamage, "PvE Magical Damage"}
};


// Struktura dla statystyki
struct Stat {
    StatType type;
    double value;


    Stat(StatType type, double value) : type(type), value(value) {}
};


// Klasa dla przedmiotu
class Item {
private:
    std::string name;
    ItemGrade grade;
    std::vector<Stat> baseStats;
    std::vector<Stat> personalizedStats;


public:
    Item(const std::string& name, ItemGrade grade) : name(name), grade(grade) {}


    std::string getName() const { return name; }
    ItemGrade getGrade() const { return grade; }


    // Funkcja dodająca bazową statystykę
    void addBaseStat(StatType type, double value) {
        baseStats.emplace_back(type, value);
    }


    // Funkcja zwracająca liczbę dostępnych slotów personalizacji
    int getPersonalizationSlots() const {
        switch (grade) {
            case ItemGrade::X:
            case ItemGrade::XLv1:
            case ItemGrade::XLv2:
            case ItemGrade::XLv3:
                return 1;
            case ItemGrade::XDarkMode:
                return 2;
            case ItemGrade::XSupremeMode:
                return 4;
            case ItemGrade::LegendarySet:
                return 5;
            default:
                return 0;
        }
    }


    // Funkcja personalizująca przedmiot
    void personalizeStats(const std::vector<StatType>& chosenStats) {
        int slots = getPersonalizationSlots();
        if (slots == 0) {
            std::cout << "Ten przedmiot nie może być personalizowany.\n";
            return;
        }
        if (chosenStats.size() > slots) {
            std::cout << "Wybrano zbyt wiele statystyk do personalizacji.\n";
            return;
        }


        // Czyścimy poprzednie personalizacje
        personalizedStats.clear();


        // Mapowanie statystyk bazowych dla łatwego dostępu
        std::map<StatType, double> baseStatMap;
        for (const auto& stat : baseStats) {
            baseStatMap[stat.type] = stat.value;
        }


        // Personalizacja statystyk
        for (const auto& statType : chosenStats) {
            double baseValue = baseStatMap[statType];
            double bonusValue = calculateBonus(statType, baseValue);
            double newValue = baseValue + bonusValue;


            // Dodajemy lub aktualizujemy statystykę
            personalizedStats.emplace_back(statType, newValue);
        }
    }


    // Funkcja obliczająca bonus personalizacyjny
    double calculateBonus(StatType type, double baseValue) {
        double bonusPercent = 0.0;


        // Ustalanie procentowego bonusu w zależności od kategorii statystyki
        switch (type) {
            // Statystyki Ofensywne
            case StatType::IncreasedDamageToRulers:
            case StatType::IncreasedDamageToStatues:
            case StatType::IncreasedDamageInSpecificAreas:
            case StatType::IncreasedDamageToHumans:
            case StatType::Precision:
            case StatType::Destruction:
            case StatType::Aggression:
            case StatType::Domination:
            case StatType::AutoAttackDamageBonus:
            case StatType::AOEDamage:
            case StatType::PhysicalAttack:
            case StatType::MagicalAttack:
                bonusPercent = 0.03; // 3%
                break;


            // Statystyki Defensywne
            case StatType::ResistanceToHumans:
            case StatType::ResistanceToCriticalDamage:
            case StatType::PhysicalResistance:
            case StatType::Tenacity:
            case StatType::MaximumHPPercent:
                bonusPercent = 0.02; // 2%
                break;


            // Inne Statystyki
            case StatType::GoldBonus:
            case StatType::Kleptomancy:
            case StatType::MiningPower:
            case StatType::Harvest:
                bonusPercent = 0.035; // 3.5%
                break;


            // Atak i Odporność Atrybutowa
            case StatType::AttributeAttack:
            case StatType::AttributeResistance:
                bonusPercent = 0.0175; // 1.75%
                break;


            // Statystyki Walki
            case StatType::PhysicalDefense:
            case StatType::MagicalDefense:
            case StatType::PhysicalAccuracy:
            case StatType::PhysicalEvasion:
                bonusPercent = 0.0375; // 3.75%
                break;


            // Statystyki PvP i PvE
            case StatType::PvPPhysicalDamage:
            case StatType::PvPMagicalDamage:
            case StatType::PvEPhysicalDamage:
            case StatType::PvEMagicalDamage:
                bonusPercent = 0.0225; // 2.25%
                break;


            default:
                bonusPercent = 0.0;
                break;
        }


        return baseValue * bonusPercent;
    }


    // Funkcja wyświetlająca statystyki przedmiotu
    void displayStats() const {
        std::cout << "Przedmiot: " << name << " (Klasa: " << itemGradeNames[grade] << ")\n";
        std::cout << "Statystyki bazowe:\n";
        for (const auto& stat : baseStats) {
            std::cout << "  - " << statTypeNames[stat.type] << ": " << stat.value << "\n";
        }
        if (!personalizedStats.empty()) {
            std::cout << "Statystyki spersonalizowane:\n";
            for (const auto& stat : personalizedStats) {
                std::cout << "  - " << statTypeNames[stat.type] << ": " << stat.value << "\n";
            }
        }
        std::cout << "\n";
    }
};


int main() {
    // Tworzenie przedmiotu o klasie X
    Item sword("Miecz Świadomości", ItemGrade::X);


    // Dodawanie bazowych statystyk
    sword.addBaseStat(StatType::PhysicalAttack, 100);
    sword.addBaseStat(StatType::Precision, 50);


    // Personalizacja statystyk - możemy wybrać jedną statystykę
    std::vector<StatType> chosenStats = { StatType::PhysicalAttack }; // Wybieramy statystykę do personalizacji
    sword.personalizeStats(chosenStats);


    // Wyświetlanie statystyk przedmiotu
    sword.displayStats();


    // Tworzenie przedmiotu o klasie X Supreme Mode
    Item armor("Zbroja Ostateczności", ItemGrade::XSupremeMode);


    // Dodawanie bazowych statystyk
    armor.addBaseStat(StatType::PhysicalDefense, 200);
    armor.addBaseStat(StatType::MagicalDefense, 150);
    armor.addBaseStat(StatType::MaximumHPPercent, 10);


    // Personalizacja statystyk - możemy wybrać cztery statystyki
    std::vector<StatType> chosenStatsArmor = {
        StatType::PhysicalDefense,
        StatType::PhysicalDefense,
        StatType::MaximumHPPercent,
        StatType::PhysicalResistance
    };
    armor.personalizeStats(chosenStatsArmor);


    // Wyświetlanie statystyk przedmiotu
    armor.displayStats();


    // Tworzenie przedmiotu o klasie Legendary Set
    Item ring("Pierścień Legendy", ItemGrade::LegendarySet);


    // Dodawanie bazowych statystyk
    ring.addBaseStat(StatType::Kleptomancy, 20);
    ring.addBaseStat(StatType::GoldBonus, 15);


    // Personalizacja statystyk - możemy wybrać pięć statystyk
    std::vector<StatType> chosenStatsRing = {
        StatType::Kleptomancy,
        StatType::GoldBonus,
        StatType::Kleptomancy,
        StatType::GoldBonus,
        StatType::Kleptomancy
    };
    ring.personalizeStats(chosenStatsRing);


    // Wyświetlanie statystyk przedmiotu
    ring.displayStats();


    return 0;
}
```
