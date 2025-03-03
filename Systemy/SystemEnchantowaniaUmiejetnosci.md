# System Enchantowania Umiejętności

System enchantowania umiejętności polega na korzystaniu ze specjalnych ksiąg mocy, które pozwalają "przelać" energię do umiejętności.

*Energia ta zostaje wywołana dodatkowo, gdy np. mag wykona określony system połączeń energetycznych prowadzących do aktywacji skilla lub gdy berserker napnie mięśnie. Proces ten działa autonomicznie, ale znacząco zwiększa moc umiejętności.*

**System jest prosty**: jedna księga wzmacnia jedną wybraną podstawową statystykę umiejętności.

Maksymalny poziom enchantowania umiejętności to +30.

*Po jego przekroczeniu wiązki energetyczne przepalają się, co uniemożliwia kontrolowanie energii, prowadząc do niekontrolowanych efektów, takich jak eksplozje lub trwałe uszkodzenia. W przypadku wzmocnienia sfery życiowej i mięśniowej może to skutkować pęknięciem wiązek mięśniowych i utratą zdolności do wykonywania umiejętności.*

*Badania nad tym zjawiskiem prowadzone były przez setki lat, a wiedza pochodzi z doświadczeń innych. W związku z tym wszystkie księgi mają ograniczenia, nie pozwalając na podbicie skilla powyżej +30. Dodatkowo każda istota od urodzenia posiada pieczęć Xis, która blokuje dalsze enchantowanie. Jeśli ktoś spróbuje przekroczyć ten limit, energia zostanie odrzucona i rozproszona w powietrzu.*

## Typy ksiąg

W świecie gry istnieje 5 różnych typów ksiąg, które dają różne rezultaty podczas enchantowania umiejętności:

1. **Księga Początkującego (Novice Enchantment Tome)**

    Podstawowa księga powszechnie dostępna od wczesnego etapu gry, oferująca niewielkie wzmocnienie skilla. Idealna dla początkujących graczy.

    Wzrost statystyki:

    `Base Value of Offering Stat = Base Value of Offering Stat + Base Value of Offering Stat * (n / 100)`

2. **Księga Adepta (Adept Enchantment Tome)**

    Zawiera bardziej zaawansowaną wiedzę o przepływach energetycznych. Rzadsza, wymaga większego doświadczenia.

    Wzrost statystyki:

    `Base Value of Offering Stat = Base Value of Offering Stat + Base Value of Offering Stat * (n / 95)`

    **Reset**: Umożliwia ponowne wykorzystanie tej lub wyższej księgi.

3. **Księga Mistrza (Master Enchantment Tome)**

    Przedmiot wysokiej jakości, używany przez mistrzów magii, sztuk walki i manipulacji energią. Znacząco zwiększa skuteczność skilli.

    Wzrost statystyki:

    `Base Value of Offering Stat = Base Value of Offering Stat + Base Value of Offering Stat * (n / 90)`,

    **Reset**: Umożliwia ponowne wykorzystanie tej lub wyższej księgi.

4. **Księga Arcymistrza (Archmage Enchantment Tome)**

    Artefakt rzadkiej klasy, dostępny tylko z trudnych questów lub jako nagroda za pokonywanie bossów. Zawiera tajemne formuły do perfekcyjnego zarządzania energią.

    Wzrost statystyki:

    `Base Value of Offering Stat = Base Value of Offering Stat + Base Value of Offering Stat * (n / 87)`

    **Reset**: Umożliwia ponowne wykorzystanie tej lub wyższej księgi.

5. **Księga Legendy (Legendary Enchantment Tome)**

   Najwyższy poziom księgi, prawdziwy rarytas. Można ją znaleźć jedynie w legendarnych ruinach lub zdobyć w epickich bitwach. Przekazuje energię w sposób niemal idealny.

    Wzrost statystyki:

    `Base Value of Offering Stat = Base Value of Offering Stat + Base Value of Offering Stat * (n / 84)`

    **Dodatkowa cecha**: Podwójny bonus – poziom enchantu wpływa na dwie statystyki jednocześnie (np. obrażenia i szybkość rzucania).

    **Reset**: Umożliwia ponowne wykorzystanie tej lub wyższej księgi.

## System resetowania enchantu

- **Koszt resetu:** Reset wymaga odpowiednich zasobów (np. złota, materiałów do rytuału lub specjalnego przedmiotu).
- **Reset zachowuje statystyki!**

## Propozycja programu realizującego dany problem

```cpp
#include <iostream>
#include <string>
#include <vector>

enum TomeType {
    NOVICE = 1,
    ADEPT,
    MASTER,
    ARCHMAGE,
    LEGENDARY
};

struct Skill {
    std::string name;
    double baseValue; // Bazowa wartość statystyki
    double enchantedValue; // Wartość po enchantowaniu
    int enchantLevel; // Aktualny poziom enchantu
};

double calculateEnchantment(Skill skill, int enchantLevel, TomeType tomeType) {
    double n = static_cast<double>(enchantLevel);
    double divisor;

    switch (tomeType) {
        case NOVICE:
            divisor = 100.0;
            break;
        case ADEPT:
            divisor = 95.0;
            break;
        case MASTER:
            divisor = 90.0;
            break;
        case ARCHMAGE:
            divisor = 87.0;
            break;
        case LEGENDARY:
            divisor = 84.0;
            break;
        default:
            divisor = 100.0;
            break;
    }

    double newValue = skill.baseValue + skill.baseValue * (n / divisor);
    return newValue;
}

void enchantSkill(Skill& skill, TomeType tomeType) {
    int enchantLevel;
    std::cout << "Podaj poziom enchantu (maksymalnie +30): ";
    std::cin >> enchantLevel;

    if (enchantLevel < 1 || enchantLevel > 30) {
        std::cout << "Poziom enchantu musi być w zakresie od 1 do 30.\n";
        return;
    }

    skill.enchantLevel = enchantLevel;
    skill.enchantedValue = calculateEnchantment(skill, enchantLevel, tomeType);

    std::cout << "\n=== Wynik Enchantowania ===\n";
    std::cout << "Skill: " << skill.name << "\n";
    std::cout << "Poziom enchantu: +" << enchantLevel << "\n";
    std::cout << "Nowa wartość statystyki: " << skill.enchantedValue << "\n";

    if (tomeType == LEGENDARY) {
        // Podwójny bonus dla Księgi Legendy
        Skill secondStat = skill;
        std::cout << "Podaj nazwę drugiej statystyki do enchantowania: ";
        std::cin >> secondStat.name;
        secondStat.enchantedValue = calculateEnchantment(secondStat, enchantLevel, tomeType);
        std::cout << "Nowa wartość drugiej statystyki: " << secondStat.enchantedValue << "\n";
    }
}

void resetEnchantment(Skill& skill) {
    char choice;
    std::cout << "Czy na pewno chcesz zresetować enchantowanie skilla " << skill.name << "? (t/n): ";
    std::cin >> choice;

    if (choice == 't' || choice == 'T') {
        skill.enchantLevel = 0;
        skill.enchantedValue = skill.baseValue;
        std::cout << "Enchantowanie skilla zostało zresetowane.\n";
        // Tutaj można dodać kod związany z kosztami resetu
    } else {
        std::cout << "Anulowano resetowanie.\n";
    }
}

int main() {
    Skill skill;
    std::cout << "Podaj nazwę skilla: ";
    std::cin >> skill.name;
    std::cout << "Podaj bazową wartość statystyki skilla: ";
    std::cin >> skill.baseValue;
    skill.enchantedValue = skill.baseValue;
    skill.enchantLevel = 0;

    int tomeChoice;
    std::cout << "\nWybierz księgę enchantowania:\n";
    std::cout << "1. Księga Początkującego\n";
    std::cout << "2. Księga Adepta\n";
    std::cout << "3. Księga Mistrza\n";
    std::cout << "4. Księga Arcymistrza\n";
    std::cout << "5. Księga Legendy\n";
    std::cout << "Twój wybór (1-5): ";
    std::cin >> tomeChoice;

    if (tomeChoice < 1 || tomeChoice > 5) {
        std::cout << "Nieprawidłowy wybór księgi.\n";
        return 1;
    }

    TomeType tomeType = static_cast<TomeType>(tomeChoice);

    enchantSkill(skill, tomeType);

    char resetChoice;
    std::cout << "\nCzy chcesz zresetować enchantowanie? (t/n): ";
    std::cin >> resetChoice;

    if (resetChoice == 't' || resetChoice == 'T') {
        resetEnchantment(skill);
        // Po resecie możemy ponownie enchantować
        enchantSkill(skill, tomeType);
    } else {
        std::cout << "Dziękujemy za skorzystanie z systemu enchantowania.\n";
    }

    return 0;
}
```
