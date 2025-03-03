# System Ewolucji Przedmiotów

System ewolucji przedmiotów to mechanizm podnoszenia kwalifikacji przedmiotu, zwiększania jego wartości statystyk oraz podnoszenia samoświadomości (sprawdź plik Samoświadomość - ***plik nie istnieje***).

Ewolucja następuje w wyniku aktywnego użycia danego przedmiotu. Jest to proces zmiany gradu na wyższy, co skutkuje wzrostem wartości statystyk oraz samoświadomości (sprawdź plik Samoświadomość - ***plik nie istnieje***).

## Klasyfikacja przedmiotów według Krasnoludów

Dzięki wiekowym praktykom krasnoludy podzieliły przedmioty na klasy (grade):

`D -> C -> B -> A -> S -> Blessed S -> X -> X Lvl 1 -> X Lvl 2 -> X Lvl 3 -> X Dark Mode -> X Supreme Mode -> Legendary Set`

Dodatkowo, w każdej klasie istnieją podtypy jakości:

1. **Kiepska jakość**  
2. **Zwykła jakość**  
3. **Wspaniała jakość**  
4. **Doskonała jakość**  

Aby uzyskać wyższy grade, należy kolejno przejść przez wszystkie podtypy jakości. Przykładowo:

- Startujemy od **D grade kiepskiej jakości** → **D grade zwykłej jakości** → **D grade wspaniałej jakości** → **D grade doskonałej jakości**.
- Po osiągnięciu poziomu doskonałego możliwa jest ewolucja do **C grade kiepskiej jakości**, a proces rozpoczyna się ponownie.

## Mechanika podnoszenia jakości

Aby podbijać jakość przedmiotu, wymagane są odpowiednie materiały, które pozwalają na przetopienie przedmiotu na wyższą jakość.

**Uwaga!**  

- **Enchant resetuje się po podniesieniu gradu przedmiotu!** Statystyki, które były przed resetem, zapisują się do bonusu, podobnie jak przy upgradowaniu.
- **Pozostałe ulepszenia pozostają i nie wpływają na podnoszenie gradu przedmiotu!**

**Wskazówka:** Aby osiągnąć szczyt możliwości przedmiotu, **najbardziej opłacalne jest enchantowanie na poziomie doskonałej jakości**. Upgradowanie natomiast jest statystyką flatową, więc można je wykonywać niezależnie od jakości przedmiotu.

## Obliczanie ewolucji przedmiotu

Indeks ewolucji (n) zwiększa się o 1 na każdym etapie przejścia, wliczając zarówno podtypy jakości, jak i ewolucję do wyższego gradu.

Przykładowo, **D grade doskonałej jakości** będzie miało indeks 4, a **C grade kiepskiej jakości** indeks 5.

| Typ Przedmiotu | Wzór na Bazową Statystykę po Ewolucji                                 |
|----------------|-----------------------------------------------------------------------|
| **Broń**       | `Base stat item = base stat item + (base stat item * n * 80) / 100`   |
| **Pancerz**    | `Base stat item = base stat item + (base stat item * n * 15) / 100`   |
| **Biżuteria**  | `Base stat item = base stat item + (base stat item * n * 15) / 100`   |
| **Inne**       | `Base stat item = base stat item + (base stat item * n * 12.5) / 100` |

## Propozycja programu realizującego dany problem

```cpp
#include <iostream>
#include <string>
#include <map>
#include <vector>
#include <iomanip>


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


// Mapowanie nazw klas przedmiotów
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


// Enum dla podtypów jakości
enum class ItemSubGrade {
    PoorQuality,        // Kiepska jakość
    CommonQuality,      // Zwykła jakość
    ExcellentQuality,   // Wspaniała jakość
    PerfectQuality      // Doskonała jakość
};


// Mapowanie nazw podtypów jakości
std::map<ItemSubGrade, std::string> itemSubGradeNames = {
    {ItemSubGrade::PoorQuality, "Kiepska jakość"},
    {ItemSubGrade::CommonQuality, "Zwykła jakość"},
    {ItemSubGrade::ExcellentQuality, "Wspaniała jakość"},
    {ItemSubGrade::PerfectQuality, "Doskonała jakość"}
};


// Enum dla typów przedmiotów
enum class ItemType {
    Weapon,
    Armor,
    Jewelry,
    Other
};


// Mapowanie nazw typów przedmiotów
std::map<ItemType, std::string> itemTypeNames = {
    {ItemType::Weapon, "Broń"},
    {ItemType::Armor, "Pancerz"},
    {ItemType::Jewelry, "Biżuteria"},
    {ItemType::Other, "Inne"}
};


// Klasa reprezentująca przedmiot
class Item {
private:
    std::string name;
    ItemType type;
    ItemGrade grade;
    ItemSubGrade subGrade;
    int gradeIndex; // Indeks n
    double initialBaseStat; // Początkowa bazowa statystyka przedmiotu
    double baseStat; // Bazowa statystyka przedmiotu
    double enchantBonus; // Bonus z enchantów (zapisany przy ewolucji)
    double upgradeBonus; // Bonus z upgradów (nie resetuje się)
    double otherEnhancements; // Inne ulepszenia (nie wpływają na ewolucję)


public:
    // Konstruktor
    Item(const std::string& name, ItemType type, double baseStat)
        : name(name), type(type), grade(ItemGrade::D), subGrade(ItemSubGrade::PoorQuality),
          gradeIndex(1), initialBaseStat(baseStat), baseStat(baseStat),
          enchantBonus(0), upgradeBonus(0), otherEnhancements(0) {}


    // Funkcja wyświetlająca informacje o przedmiocie
    void displayInfo() const {
        std::cout << "Przedmiot: " << name << "\n";
        std::cout << "Typ: " << itemTypeNames.at(type) << "\n";
        std::cout << "Klasa: " << itemGradeNames.at(grade) << " " << itemSubGradeNames.at(subGrade) << "\n";
        std::cout << "Indeks ewolucji (n): " << gradeIndex << "\n";
        std::cout << std::fixed << std::setprecision(2);
        std::cout << "Bazowa statystyka: " << baseStat << "\n";
        std::cout << "Bonus z enchantów: " << enchantBonus << "\n";
        std::cout << "Bonus z upgradów: " << upgradeBonus << "\n";
        std::cout << "Inne ulepszenia: " << otherEnhancements << "\n";
        std::cout << "----------------------------------------\n";
    }


    // Funkcja do enchantowania przedmiotu
    void enchant(double value) {
        enchantBonus += value;
        std::cout << "Przedmiot został enchantowany. Dodano " << value << " do enchantu.\n";
    }


    // Funkcja do upgradów przedmiotu
    void upgrade(double value) {
        upgradeBonus += value;
        std::cout << "Przedmiot został upgradowny. Dodano " << value << " do upgradu.\n";
    }


    // Funkcja do ewolucji przedmiotu
    void evolve() {
        // Sprawdzamy, czy przedmiot jest na poziomie Doskonałej jakości
        if (subGrade == ItemSubGrade::PerfectQuality) {
            // Resetujemy enchant, ale dodajemy jego wartość do bazowej statystyki jako bonus
            baseStat += enchantBonus;
            enchantBonus = 0;


            // Przechodzimy do następnej klasy przedmiotu
            grade = nextGrade(grade);
            subGrade = ItemSubGrade::PoorQuality;
            std::cout << "Przedmiot awansował do klasy " << itemGradeNames.at(grade) << " Kiepska jakość.\n";
        } else {
            // Przechodzimy do następnego podtypu jakości
            subGrade = nextSubGrade(subGrade);
            std::cout << "Przedmiot awansował do jakości " << itemSubGradeNames.at(subGrade) << ".\n";
        }


        // Zwiększamy indeks ewolucji
        gradeIndex++;


        // Obliczamy nową bazową statystykę
        double multiplierPercentage = 0.0;
        switch (type) {
            case ItemType::Weapon:
                multiplierPercentage = 80.0;
                break;
            case ItemType::Armor:
            case ItemType::Jewelry:
                multiplierPercentage = 15.0;
                break;
            case ItemType::Other:
                multiplierPercentage = 12.5;
                break;
        }
        double increase = initialBaseStat * ((gradeIndex * multiplierPercentage) / 100.0);
        baseStat = initialBaseStat + increase;


        std::cout << "Nowa bazowa statystyka po ewolucji: " << baseStat << "\n";
    }


    // Funkcja pomocnicza do uzyskania następnego podtypu jakości
    ItemSubGrade nextSubGrade(ItemSubGrade current) {
        switch (current) {
            case ItemSubGrade::PoorQuality:
                return ItemSubGrade::CommonQuality;
            case ItemSubGrade::CommonQuality:
                return ItemSubGrade::ExcellentQuality;
            case ItemSubGrade::ExcellentQuality:
                return ItemSubGrade::PerfectQuality;
            case ItemSubGrade::PerfectQuality:
                return ItemSubGrade::PerfectQuality; // Już na najwyższym poziomie
            default:
                return current;
        }
    }


    // Funkcja pomocnicza do uzyskania następnej klasy przedmiotu
    ItemGrade nextGrade(ItemGrade current) {
        switch (current) {
            case ItemGrade::D:
                return ItemGrade::C;
            case ItemGrade::C:
                return ItemGrade::B;
            case ItemGrade::B:
                return ItemGrade::A;
            case ItemGrade::A:
                return ItemGrade::S;
            case ItemGrade::S:
                return ItemGrade::BlessedS;
            case ItemGrade::BlessedS:
                return ItemGrade::X;
            case ItemGrade::X:
                return ItemGrade::XLv1;
            case ItemGrade::XLv1:
                return ItemGrade::XLv2;
            case ItemGrade::XLv2:
                return ItemGrade::XLv3;
            case ItemGrade::XLv3:
                return ItemGrade::XDarkMode;
            case ItemGrade::XDarkMode:
                return ItemGrade::XSupremeMode;
            case ItemGrade::XSupremeMode:
                return ItemGrade::LegendarySet;
            case ItemGrade::LegendarySet:
                return ItemGrade::LegendarySet; // Już na najwyższym poziomie
            default:
                return current;
        }
    }


    // Funkcja dodająca inne ulepszenia
    void addOtherEnhancement(double value) {
        otherEnhancements += value;
        std::cout << "Dodano inne ulepszenie o wartości " << value << ".\n";
    }
};


int main() {
    // Tworzenie przedmiotu
    Item sword("Miecz Bohatera", ItemType::Weapon, 100);


    // Wyświetlanie początkowych informacji
    sword.displayInfo();


    // Enchantowanie przedmiotu
    sword.enchant(20);


    // Upgradowanie przedmiotu
    sword.upgrade(10);


    // Dodanie innego ulepszenia
    sword.addOtherEnhancement(5);


    // Wyświetlanie informacji po ulepszeniach
    sword.displayInfo();


    // Ewolucja przez podtypy jakości
    sword.evolve(); // Z Kiepskiej na Zwykłą jakość
    sword.evolve(); // Z Zwykłej na Wspaniałą jakość
    sword.evolve(); // Z Wspaniałej na Doskonałą jakość


    // Enchantowanie na poziomie Doskonałej jakości
    sword.enchant(30);


    // Wyświetlanie informacji
    sword.displayInfo();


    // Ewolucja do wyższej klasy (z resetem enchantu)
    sword.evolve(); // Przejście do klasy C Kiepska jakość


    // Wyświetlanie informacji po ewolucji
    sword.displayInfo();


    // Kontynuacja ewolucji
    sword.evolve(); // Z Kiepskiej na Zwykłą jakość
    sword.evolve(); // Z Zwykłej na Wspaniałą jakość
    sword.evolve(); // Z Wspaniałej na Doskonałą jakość


    // Upgradowanie przedmiotu (upgrady nie resetują się)
    sword.upgrade(15);


    // Wyświetlanie końcowych informacji
    sword.displayInfo();


    return 0;
}
```
