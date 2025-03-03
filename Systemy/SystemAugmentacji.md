# System Augmentacji

Augmentacja ma różne właściwości i może dawać różne efekty niezależnie od przedmiotu.

Kamienie można łączyć w różne kombinacje. Istnieją sekretne kombinacje o wyjątkowo korzystnych bonusach. Gracz może odkryć je poprzez szczęśliwy traf lub znaleźć wskazówki w świecie gry (dialogi NPC-ów, zwoje z notatkami itp.).

Ponowne losowanie kombinacji kosztuje pewną ilość waluty/surowców. Z każdym losowaniem koszt trochę rośnie, aż do osiągnięcia pewnego górnego limitu. Ma to na celu umożliwienie graczowi osiągnięcia pożądanych efektów metodą brute force.

Efektem zmieszania kilku kamieni jest jeden silniejszy kamień. Jak bardzo zależy od tego, jak dobrej kombinacji użyliśmy. Do jednego przedmiotu można wsadzić jednocześnie tylko jeden kamień.

Przenoszenie kamieni pomiędzy przedmiotami jest możliwe, jednak nie można zrobić tego w dowolnym momencie. Trzeba udać się do odpowiedniego NPC-a i zapłacić pieniędzmi lub/i surowcami.

Oprócz losowości trzeba wprowadzić system gwarantujący różnorodność wyników, tak żebyśmy w kółko nie dostawali tego samego. To uczyni ten system bardziej przyjaznym i mniej frustrującym dla graczy. Pomysł na implementację: system losowości bez zwracania.

Czym potężniejsza hybryda, tym potężniejsze wzmocnienie dla naszego przedmiotu otrzymamy:

## Podział kamieni Augmentacji

Kamienie Augmentacji dzielą się na: matowy, błyszczący, rzadki, starożytny, antyczny, cudowny, nieskończoności.
Każdy z tych kamieni także ma swój stage (lvl) od 1-5, licząc rosnąco:

- Matowy 1
- Matowy 2
- Matowy 3
- Matowy 4
- Matowy 5
- Błyszczący 1
- Błyszczący 2 ...

Powodem takiego sposobu podziału było zauważenie przez krasnoludów, że nawet matowe kamienie różnią się między sobą właściwościami, a tak naprawdę siłą, z jaką oddziałują.

## System wzmacniania przedmiotów

Co możemy uzyskać, wzmacniając nasz przedmiot:

- Możemy otrzymać do 5 bonusów, które są wybierane na zasadzie losowania z puli.
- Możemy nasze wzmocnienia oczywiście resetować i próbować dalej, aż uda nam się trafić te pożądane.
- Parametry wybierane podczas augmentacji nie mogą się ze sobą nakładać (stackować). Losowanie odbywa się na zasadzie bez zwracania do puli parametru.
- Kiedy resetujemy wzmocnienie, resetuje się także pula parametrów, które możemy wylosować.

### Obliczanie bonusów

```text
A - indeks, który jest naliczany od naszego kamienia
```

| Kamień Augmentacji | A |
|--------------------|---|
| Matowy 1           | 1 |
| Matowy 2           | 2 |
| Błyszczący 1       | 6 |
| ... | |

(indeks rośnie o 1 co stage)

| Bonus                         | Wzór                                      |
|-------------------------------|-------------------------------------------|
| Status bonus                  | `1 * log(A+10) * log(A+11) * log(A+12)`   |
| P. DEF bonus                  | `8 * log(A+10) * log(A+11) * log(A+12)`   |
| M. DEF bonus                  | `8 * log(A+10) * log(A+11) * log(A+12)`   |
| P. ATK bonus                  | `10 * log(A+10) * log(A+11) * log(A+12)`  |
| M. ATK bonus                  | `10 * log(A+10) * log(A+11) * log(A+12)`  |
| P. Skill Power bonus          | `2 * log(A+10) * log(A+11) * log(A+12)`   |
| M. Skill Power bonus          | `2 * log(A+10) * log(A+11) * log(A+12)`   |
| Strong against Statues bonus  | `1 * log(A+10) * log(A+11) * log(A+12)`   |
| Strong against Emperors bonus | `1 * log(A+10) * log(A+11) * log(A+12)`   |
| Strong against monsters bonus | `1 * log(A+10) * log(A+11) * log(A+12)`   |
| PVM bonus                     | `1 * log(A+10) * log(A+11) * log(A+12)`   |
| PVP bonus                     | `1 * log(A+10) * log(A+11) * log(A+12)`   |
| PVE bonus                     | `1 * log(A+10) * log(A+11) * log(A+12)`   |
| P. Skill Critical Damage      | `2 * log(A+10) * log(A+11) * log(A+12)`   |
| M. Skill Critical Damage      | `2 * log(A+10) * log(A+11) * log(A+12)`   |
| Bonus EXP                     | `5 * log(A+10) * log(A+11) * log(A+12)`   |
| Bonus Gold                    | `5 * log(A+10) * log(A+11) * log(A+12)`   |
| Kleptomancy bonus             | `5 * log(A+10) * log(A+11) * log(A+12)`   |
| Chance to enchant bonus       | `0.5 * log(A+10) * log(A+11) * log(A+12)` |
| Chance to upgrade bonus       | `0.5 * log(A+10) * log(A+11) * log(A+12)` |
| Fire resistance bonus         | `2 * log(A+10) * log(A+11) * log(A+12)`   |
| Water resistance bonus        | `2 * log(A+10) * log(A+11) * log(A+12)`   |
| Earth resistance bonus        | `2 * log(A+10) * log(A+11) * log(A+12)`   |
| Wind resistance bonus         | `2 * log(A+10) * log(A+11) * log(A+12)`   |
| Holy resistance bonus         | `2 * log(A+10) * log(A+11) * log(A+12)`   |
| Dark resistance bonus         | `2 * log(A+10) * log(A+11) * log(A+12)`   |
| Elemental resistance bonus    | `2 * log(A+10) * log(A+11) * log(A+12)`   |
| HP bonus                      | `20 * log(A+10) * log(A+11) * log(A+12)`  |
| MP bonus                      | `20 * log(A+10) * log(A+11) * log(A+12)`  |
| MP/HP bonus                   | `25 * log(A+10) * log(A+11) * log(A+12)`  |
| Aggression                    | `8 * log(A+10) * log(A+11) * log(A+12)`   |

Każdy bonus ma taką samą szansę zdarzenia. Życzymy szczęścia w trafieniu 5 wymarzonych bonusów!

## Propozycja programu realizującego dany problem

```cpp
#include <iostream>
#include <cmath>
#include <string>
#include <vector>
#include <map>
#include <algorithm>
#include <random>
#include <iomanip>
#include <chrono>


// Function to calculate factorial (used for probability calculation)
unsigned long long factorial(int n) {
    unsigned long long result = 1;
    for(int i = 2; i <= n; ++i)
        result *= i;
    return result;
}


// Enum for Augmentation Stone Types
enum StoneType {
    MATOWY,
    BLYSZCZACY,
    RZADKI,
    STAROZYTNY,
    ANTYCZNY,
    CUDOWNY,
    NIESKONCZONOSCI
};


// Struct for Augmentation Stone
struct AugmentationStone {
    StoneType type;
    int stage; // Stage from 1 to 5
    int index; // A: Calculated based on type and stage


    AugmentationStone(StoneType t, int s) : type(t), stage(s) {
        // Calculate index A based on the type and stage
        index = calculateIndex(t, s);
    }


    // Function to calculate index A
    static int calculateIndex(StoneType type, int stage) {
        int baseIndex = 0;
        switch (type) {
            case MATOWY: baseIndex = 1; break;
            case BLYSZCZACY: baseIndex = 6; break;
            case RZADKI: baseIndex = 11; break;
            case STAROZYTNY: baseIndex = 16; break;
            case ANTYCZNY: baseIndex = 21; break;
            case CUDOWNY: baseIndex = 26; break;
            case NIESKONCZONOSCI: baseIndex = 31; break;
            default: baseIndex = 1; break;
        }
        return baseIndex + (stage - 1);
    }
};


// Struct for Item
struct Item {
    std::string name;
    std::map<std::string, double> bonuses;


    // Function to display item bonuses
    void displayBonuses() const {
        std::cout << "Item: " << name << "\n";
        std::cout << "Bonuses:\n";
        for (const auto& bonus : bonuses) {
            std::cout << "  " << bonus.first << ": " << std::fixed << std::setprecision(2) << bonus.second << "\n";
        }
        std::cout << "\n";
    }
};


// Function to calculate bonus value based on formula
double calculateBonusValue(int A, double multiplier) {
    double log1 = std::log(A + 10);
    double log2 = std::log(A + 11);
    double log3 = std::log(A + 12);
    double value = multiplier * log1 * log2 * log3;
    return value;
}


// Function to perform augmentation on an item
void augmentItem(Item& item, const AugmentationStone& stone) {
    // List of all 35 possible bonuses
    std::vector<std::string> bonusPool = {
        "P.def bonus",
        "M.def bonus",
        "P. ATK bonus",
        "M ATK bonus",
        "P. Skill Power bonus",
        "M. Skill Power bonus",
        "Strong against Statues bonus",
        "Strong against Emperors bonus",
        "Strong against Monsters bonus",
        "PVM bonus",
        "PVP bonus",
        "PVE bonus",
        "Status bonus",
        "P skill critical dmg",
        "M skill critical dmg",
        "Bonus exp bonus",
        "Bonus gold bonus",
        "Kleptomancy bonus",
        "Chance to enchant bonus",
        "Chance to upgrade bonus",
        "Fire resistance bonus",
        "Water resistance bonus",
        "Earth resistance bonus",
        "Wind resistance bonus",
        "Holy resistance bonus",
        "Dark resistance bonus",
        "Elemental resistance bonus",
        "Hp bonus",
        "Mp bonus",
        "Mp/hp bonus",
        "- P. Skill Power bonus",
        "- M. Skill Power bonus",
        "- P skill critical dmg",
        "- M skill critical dmg",
        "Aggression"
    };


    // Seed with a real random value, if available
    std::random_device rd;


    // Random number generator
    std::mt19937 rng(rd());


    // Shuffle the bonus pool
    std::shuffle(bonusPool.begin(), bonusPool.end(), rng);


    // Select exactly 5 bonuses without replacement
    int numberOfBonuses = 5;
    std::vector<std::string> selectedBonuses(bonusPool.begin(), bonusPool.begin() + numberOfBonuses);


    // Clear existing bonuses
    item.bonuses.clear();


    // Calculate bonuses and apply to item
    int A = stone.index;
    for (const auto& bonusName : selectedBonuses) {
        double multiplier = 0.0;
        if (bonusName == "P.def bonus" || bonusName == "M.def bonus" || bonusName == "Hp bonus" || bonusName == "Mp bonus" || bonusName == "Mp/hp bonus") {
            if (bonusName == "Hp bonus" || bonusName == "Mp bonus")
                multiplier = 20.0;
            else if (bonusName == "Mp/hp bonus")
                multiplier = 25.0;
            else
                multiplier = 8.0;
        }
        else if (bonusName == "P. ATK bonus" || bonusName == "M ATK bonus") {
            multiplier = 10.0;
        }
        else if (bonusName == "P. Skill Power bonus" || bonusName == "M. Skill Power bonus") {
            multiplier = 2.0;
        }
        else if (bonusName == "Strong against Statues bonus" || bonusName == "Strong against Emperors bonus" || bonusName == "Strong against Monsters bonus" ||
                 bonusName == "PVM bonus" || bonusName == "PVP bonus" || bonusName == "PVE bonus" || bonusName == "Status bonus") {
            multiplier = 1.0;
        }
        else if (bonusName == "P skill critical dmg" || bonusName == "M skill critical dmg" || bonusName == "Fire resistance bonus" ||
                 bonusName == "Water resistance bonus" || bonusName == "Earth resistance bonus" || bonusName == "Wind resistance bonus" ||
                 bonusName == "Holy resistance bonus" || bonusName == "Dark resistance bonus" || bonusName == "Elemental resistance bonus") {
            multiplier = 2.0;
        }
        else if (bonusName == "Bonus exp bonus" || bonusName == "Bonus gold bonus" || bonusName == "Kleptomancy bonus") {
            multiplier = 5.0;
        }
        else if (bonusName == "Chance to enchant bonus" || bonusName == "Chance to upgrade bonus") {
            multiplier = 0.5;
        }
        else if (bonusName == "- P. Skill Power bonus" || bonusName == "- M. Skill Power bonus" ||
                 bonusName == "- P skill critical dmg" || bonusName == "- M skill critical dmg") {
            multiplier = 1.5;
        }
        else if (bonusName == "Aggression") {
            multiplier = 8.0;
        }
        else {
            multiplier = 1.0; // Default multiplier
        }


        double bonusValue = calculateBonusValue(A, multiplier);
        item.bonuses[bonusName] = bonusValue;
    }


    // Calculate and display the probability of obtaining this specific combination
    unsigned long long totalCombinations = factorial(35) / (factorial(5) * factorial(35 - 5));
    double probability = 1.0 / totalCombinations * 100.0;
    std::cout << "Probability of obtaining this combination: " << std::fixed << std::setprecision(6) << probability << "%\n\n";
}


int main() {
    // Create an item
    Item myItem;
    myItem.name = "Legendary Sword";


    // Choose an augmentation stone
    StoneType stoneType = CUDOWNY; // For example, "Cudowny"
    int stage = 4; // Stage from 1 to 5
    AugmentationStone myStone(stoneType, stage);


    // Perform augmentation
    augmentItem(myItem, myStone);


    // Display item bonuses
    myItem.displayBonuses();


    // Optionally, reset augmentation and try again
    // augmentItem(myItem, myStone);
    // myItem.displayBonuses();


    return 0;
}
```
