# System Żywiołów

Lista żywiołów:

- Ogień
- Woda
- Ziemia
- Wiatr
- Światło
- Mrok

Z ksiąg druidzkich wynika, że istnieje 10 typów (rzadkości) run:

1. Postrzępiona runa kiepskiej jakości  
2. Zwykła Runa matowego odbicia  
3. Lśniąca Runa Pradawnych Żywiołów  
4. Runa Mistycznego Żaru  
5. Runa Kryształowego Przebudzenia  
6. Runa Duchowej Harmonii  
7. Runa Żywiołowej Energii  
8. Runa Astralnego Blasku  
9. Runa Wieczystej Harmonii  
10. Runa Boskiego Żywiołu  

Żywioły są ściśle powiązane z [Systemem Run](SystemRun.md). Im rzadszą runę gracz znajdzie, tym potężniejszy jest jej żywioł (więcej statystyk, grupa elementów się nie zmienia). Runy można nałożyć na każdy przedmiot, wzmacniając siłę w danym żywiole.

## System obliczenia run

```text
n - stopień rzadkości runy
```

**Dla broni:** `Base element = Base element + 20*n`

**Dla pancerza:** `Base element resistance = Base element resistance + 2*n`

**Dla pozostałych przedmiotów:**

- `Base element = Base element + 3*n`
- `Base element resistance = Base element resistance + 1*n`

## Zasady używania run

Przy umieszczaniu run szansa powodzenia wynosi 100%. Runy można wymieniać, co ma miejsce poprzez zdjęcie poprzedniej i nałożenie nowej runy.

### Umieszczanie run

1. W broni można umieścić tylko jedną runę.
2. W każdej części pancerza można umieścić do 3 run z różnymi żywiołami.
3. W pozostałych przedmiotach można umieścić tylko jedną runę.

## Propozycja programu realizującego dany problem

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <map>
#include <algorithm>


// Enum dla typów elementów
enum class ElementType {
    Fire,
    Water,
    Earth,
    Wind,
    Holy,
    Dark,
    // Możesz dodać inne elementy według potrzeb
};


// Mapowanie ElementType na nazwy
std::map<ElementType, std::string> elementNames = {
    {ElementType::Fire, "Ogień"},
    {ElementType::Water, "Woda"},
    {ElementType::Earth, "Ziemia"},
    {ElementType::Wind, "Wiatr"},
    {ElementType::Holy, "Świętość"},
    {ElementType::Dark, "Ciemność"},
};


// Enum dla typów przedmiotów
enum class ItemType {
    Weapon,
    Armor,
    Other,
};


// Mapowanie ItemType na nazwy
std::map<ItemType, std::string> itemTypeNames = {
    {ItemType::Weapon, "Broń"},
    {ItemType::Armor, "Pancerz"},
    {ItemType::Other, "Inne"},
};


// Struktura dla runy
struct Rune {
    std::string name;
    int degree; // Stopień runy (1-10)
    ElementType element;


    Rune(const std::string& name, int degree, ElementType element)
        : name(name), degree(degree), element(element) {}
};


// Klasa dla przedmiotu
class Item {
private:
    std::string name;
    ItemType type;
    int baseElementValue;
    int baseElementResistance;
    std::vector<Rune> runes;


public:
    Item(const std::string& name, ItemType type)
        : name(name), type(type), baseElementValue(0), baseElementResistance(0) {}


    std::string getName() const { return name; }
    ItemType getType() const { return type; }


    // Funkcja dodająca runę do przedmiotu
    bool addRune(const Rune& rune) {
        // Sprawdzenie ograniczeń liczby run i elementów
        if (type == ItemType::Weapon) {
            if (!runes.empty()) {
                std::cout << "Broń może mieć tylko jedną runę.\n";
                return false;
            }
            runes.push_back(rune);
            calculateElementalValues();
            return true;
        }
        else if (type == ItemType::Armor) {
            if (runes.size() >= 3) {
                std::cout << "Pancerz może mieć maksymalnie trzy runy.\n";
                return false;
            }
            // Sprawdzenie czy runa o tym elemencie już istnieje
            for (const auto& r : runes) {
                if (r.element == rune.element) {
                    std::cout << "Nie można dodać run o tym samym elemencie do pancerza.\n";
                    return false;
                }
            }
            runes.push_back(rune);
            calculateElementalValues();
            return true;
        }
        else { // Inne przedmioty
            if (!runes.empty()) {
                std::cout << "Ten przedmiot może mieć tylko jedną runę.\n";
                return false;
            }
            runes.push_back(rune);
            calculateElementalValues();
            return true;
        }
    }


    // Funkcja usuwająca runę z przedmiotu
    bool removeRune(ElementType element) {
        auto it = std::find_if(runes.begin(), runes.end(), [&](const Rune& r) {
            return r.element == element;
        });
        if (it != runes.end()) {
            runes.erase(it);
            calculateElementalValues();
            return true;
        }
        else {
            std::cout << "Brak runy z tym elementem w przedmiocie.\n";
            return false;
        }
    }


    // Funkcja obliczająca nowe wartości elementarne
    void calculateElementalValues() {
        baseElementValue = 0;
        baseElementResistance = 0;
        for (const auto& rune : runes) {
            int n = rune.degree;
            if (type == ItemType::Weapon) {
                baseElementValue += 20 * n;
            }
            else if (type == ItemType::Armor) {
                baseElementResistance += 2 * n;
            }
            else { // Inne przedmioty
                baseElementResistance += 1 * n;
                baseElementValue += 3 * n;
            }
        }
    }


    // Funkcja wyświetlająca informacje o przedmiocie
    void displayInfo() const {
        std::cout << "Przedmiot: " << name << " (" << itemTypeNames[type] << ")\n";
        std::cout << "Runy:\n";
        for (const auto& rune : runes) {
            std::cout << "  - " << rune.name << " (Stopień: " << rune.degree
                      << ", Element: " << elementNames[rune.element] << ")\n";
        }
        std::cout << "Wartość Elementu: " << baseElementValue << "\n";
        std::cout << "Odporność Elementarna: " << baseElementResistance << "\n\n";
    }
};


int main() {
    // Tworzenie run o różnych stopniach i elementach
    Rune rune1("Runa Mistycznego Żaru", 4, ElementType::Fire);
    Rune rune2("Runa Kryształowego Przebudzenia", 5, ElementType::Water);
    Rune rune3("Runa Żywiołowej Energii", 6, ElementType::Earth);
    Rune rune4("Runa Astralnego Blasku", 7, ElementType::Wind);
    Rune rune5("Runa Duchowej Harmonii", 3, ElementType::Holy);
    Rune rune6("Runa Cienia", 2, ElementType::Dark);


    // Tworzenie przedmiotów
    Item sword("Miecz Ognia", ItemType::Weapon);
    Item armor("Zbroja Wody", ItemType::Armor);
    Item ring("Pierścień Ziemi", ItemType::Other);


    // Dodawanie run do broni
    sword.addRune(rune1); // Powinno się udać
    sword.displayInfo();


    // Próba dodania drugiej runy do broni
    sword.addRune(rune2); // Powinno się nie udać


    // Dodawanie run do pancerza
    armor.addRune(rune2);
    armor.addRune(rune3);
    armor.addRune(rune4); // Trzy różne runy elementów
    armor.displayInfo();


    // Próba dodania czwartej runy do pancerza
    armor.addRune(rune5); // Powinno się nie udać


    // Próba dodania runy o tym samym elemencie
    armor.addRune(rune2); // Powinno się nie udać


    // Dodawanie runy do przedmiotu innego typu
    ring.addRune(rune5);
    ring.displayInfo();


    // Wymiana runy w pierścieniu
    ring.removeRune(ElementType::Holy);
    ring.addRune(rune6);
    ring.displayInfo();


    return 0;
}
```
