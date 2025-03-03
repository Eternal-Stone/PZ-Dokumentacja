# System Ewolucji Umiejętności

System ewolucji skilli opiera się na częstym korzystaniu z umiejętności – im częściej używany jest dany skill, tym potężniejszy się staje. Poprzez regularne używanie zdolności, postać doprowadza ją do perfekcji. Dodatkowo, energia użytkownika stopniowo adaptuje się do tej umiejętności, co zwiększa jej efektywność.

## Podstawowe założenia systemu

- Początkowy poziom umiejętności: **1**
- Maksymalny poziom umiejętności: **100**
- Każde użycie skilla zwiększa jego efektywność oraz wpływa na rozwój statystyk powiązanych z daną zdolnością.

## Sposób obliczania wzmacniania umiejętności

Dla każdej umiejętności obowiązują następujące wzory:

```text
n - poziom skilla
```

1. **Wartość bazowa statusu:**  
   `Base Value Status = Base Casting Speed Spell + Base Casting Speed Spell * log(n+11) * log(n+12) * log(n+13)`

2. **Redukcja czasu odnowienia (CDR):**  
   `Base CDR = Base Casting Speed Spell - Base Casting Speed Spell * log(n)`

3. **Rozmiar efektu:**  
   `Base Size = Base Casting Speed Spell + Base Casting Speed Spell * log(n)`

4. **Prędkość rzucania zaklęcia:**  
   `Base Casting Speed Spell = Base Casting Speed Spell + Base Casting Speed Spell * log(n)`

## System naliczania paska doświadczenia umiejętności

Aby osiągnąć kolejny poziom umiejętności, wymagane jest wypełnienie paska doświadczenia:

```text
n - poziom umiejętności
Bar Ilość Użycia Skilla = log(n) * ln / (n + (n + 1)) * 20
```

## Propozycja programu realizującego dany problem

```cpp
#include <iostream>
#include <cmath>

int main() {
    // Deklaracja zmiennych
    int N; // Poziom skilla
    double baseCastingSpeedSpell; // Bazowa szybkość rzucania zaklęcia

    // Pobranie danych od użytkownika
    std::cout << "Podaj poziom swojego skilla (N): ";
    std::cin >> N;

    // Sprawdzenie, czy N jest większe od 0
    if (N <= 0) {
        std::cout << "Poziom skilla musi być większy od 0." << std::endl;
        return 1;
    }

    std::cout << "Podaj bazową szybkość rzucania zaklęcia: ";
    std::cin >> baseCastingSpeedSpell;

    // Obliczenia
    // Używamy logarytmu naturalnego (ln), funkcja log() w C++ to ln
    double baseValueStatus = baseCastingSpeedSpell + baseCastingSpeedSpell * log(N + 11) * log(N + 12) * log(N + 13);

    double baseCdr = baseCastingSpeedSpell - baseCastingSpeedSpell * log(N);

    double baseSize = baseCastingSpeedSpell + baseCastingSpeedSpell * log(N);

    double updatedBaseCastingSpeedSpell = baseCastingSpeedSpell + baseCastingSpeedSpell * log(N);

    // Obliczanie baru napełnienia się aby uzyskać kolejny poziom skilla
    double lnN = log(N);
    double barUsage = (lnN * lnN) / (2 * N + 1) * 20;

    // Wyświetlenie wyników
    std::cout << "\n=== Wyniki ===" << std::endl;
    std::cout << "Base Value Status: " << baseValueStatus << std::endl;
    std::cout << "Base CDR: " << baseCdr << std::endl;
    std::cout << "Base Size: " << baseSize << std::endl;
    std::cout << "Updated Base Casting Speed Spell: " << updatedBaseCastingSpeedSpell << std::endl;
    std::cout << "Bar ilość użycia skilla: " << barUsage << std::endl;

    return 0;
}
```
