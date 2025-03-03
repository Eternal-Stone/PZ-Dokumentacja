# System Run Peta

Nawet na astralnej postaci jesteśmy w stanie wykonywać runy astralne, które wzmacniają naszego peta.

**Odblokowanie:**
Dostępny od poziomu 140 peta.

**Runy:**

- 8 run, każda z maksymalnym poziomem 25.
- Runy wzmacniają procentowo 8 umiejętności peta.

**Tworzenie Run:**

- Wymaga alchemii i mieszania materiałów.
- Proces mieszania determinuje poziom i efektywność runy.

Efektywność zwiększana jest przez podbijanie alchemiczne run, innymi słowy, polewamy astralnego przyjaciela odpowiednio sporządzaną miksturą, która przelewa energię astralną i wzmacnia jego umiejętności.

Proces jest stopniowy i trzeba odczekać odpowiedni okres, zanim znowu będzie można polewać peta miksturą.

Maksymalny poziom run: **25**.

## Umiejętności peta

- **Agresja**
- **Obrońca**
- **Złotnik**
- **Łowca**
- **Kolos**
- **Oprawca**
- **Mądrość**
- **Zwinność**

## Sposób obliczania efektów

1. **Runiczny Zew Gniewu**

    ```text
    P.Atk bonus skill = P.Atk bonus skill + (P.Atk bonus skill * n) / 100
    M.Atk bonus skill = M.Atk bonus skill + (M.Atk bonus skill * n) / 100
    ```

2. **Tarcza Strażnika**

    ```text
    P.Def bonus skill = P.Def bonus skill + (P.Def bonus skill * n) / 100
    M.Def bonus skill = M.Def bonus skill + (M.Def bonus skill * n) / 100
    ```

3. **Astralna Moneta**

    ```text
    Bonus gold skill = Bonus gold skill + (Bonus gold skill * n) / 100
    ```

4. **Pazur Łowcy**

    ```text
    Siła na potwory bonus skill = Siła na potwory bonus skill + (Siła na potwory bonus skill * n) / 100
    ```

5. **Runiczny Filar**

    ```text
    Hp bonus skill = Hp bonus skill + (Hp bonus skill * n) / 100
    Mp Bonus skill = Mp Bonus skill + (Mp Bonus skill * n) / 100
    ```

6. **Piętno Oprawcy**

    ```text
    Pvp dmg bonus skill = Pvp dmg bonus skill + (Pvp dmg bonus skill * n) / 100
    Pvp dmg bonus skill = - Pvp dmg bonus skill + (- Pvp dmg bonus skill * n) / 100
    ```

7. **Kryształ Wiedzy**

    ```text
    Kleptomancja bonus skill = Kleptomancja bonus skill + (Kleptomancja bonus skill * n)
    ```

8. **Cień Zwinności**

    ```text
    Szybkość ruchu bonus skill = Szybkość ruchu bonus skill + (Szybkość ruchu bonus skill * n) / 100
    P critical dmg bonus skill = P critical dmg bonus skill + (P critical dmg bonus skill * n) / 100
    M critical dmg bonus skill = M critical dmg bonus skill + (M critical dmg bonus skill * n) / 100
    ```

## Spis Run Peta

Lista przedmiotów znajduje się w dokumencie [Spis Run Peta](../Spisy/SpisRunPeta.md).

## Propozycja programu realizującego dany problem

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <unordered_map>
#include <cmath>

class PetSkill {
public:
    std::string name;
    double pAtkBonusSkill;
    double mAtkBonusSkill;
    double pDefBonusSkill;
    double mDefBonusSkill;
    double bonusGoldSkill;
    double monsterDamageBonusSkill;
    double hpBonusSkill;
    double mpBonusSkill;
    double pvpDamageBonusSkill;
    double pvpDamageReductionSkill;
    double kleptomaniaBonusSkill;
    double movementSpeedBonusSkill;
    double pCriticalDamageBonusSkill;
    double mCriticalDamageBonusSkill;

    PetSkill(const std::string& name)
        : name(name), pAtkBonusSkill(0), mAtkBonusSkill(0),
          pDefBonusSkill(0), mDefBonusSkill(0), bonusGoldSkill(0),
          monsterDamageBonusSkill(0), hpBonusSkill(0), mpBonusSkill(0),
          pvpDamageBonusSkill(0), pvpDamageReductionSkill(0),
          kleptomaniaBonusSkill(0), movementSpeedBonusSkill(0),
          pCriticalDamageBonusSkill(0), mCriticalDamageBonusSkill(0) {}
};

class PetRune {
public:
    std::string name;
    std::string associatedSkill;
    int level;
    const int maxLevel = 25;

    PetRune(const std::string& name, const std::string& associatedSkill)
        : name(name), associatedSkill(associatedSkill), level(0) {}

    void levelUp(int levels) {
        if (level + levels > maxLevel) {
            levels = maxLevel - level;
        }
        level += levels;
    }

    void applyEffect(PetSkill& skill) {
        int n = level;
        if (n <= 0) return;

        if (name == "Runiczny Zew Gniewu") {
            skill.pAtkBonusSkill += (skill.pAtkBonusSkill * n) / 100.0;
            skill.mAtkBonusSkill += (skill.mAtkBonusSkill * n) / 100.0;
        }
        else if (name == "Tarcza Strażnika") {
            skill.pDefBonusSkill += (skill.pDefBonusSkill * n) / 100.0;
            skill.mDefBonusSkill += (skill.mDefBonusSkill * n) / 100.0;
        }
        else if (name == "Astralna Moneta") {
            skill.bonusGoldSkill += (skill.bonusGoldSkill * n) / 100.0;
        }
        else if (name == "Pazur Łowcy") {
            skill.monsterDamageBonusSkill += (skill.monsterDamageBonusSkill * n) / 100.0;
        }
        else if (name == "Runiczny Filar") {
            skill.hpBonusSkill += (skill.hpBonusSkill * n) / 100.0;
            skill.mpBonusSkill += (skill.mpBonusSkill * n) / 100.0;
        }
        else if (name == "Piętno Oprawcy") {
            skill.pvpDamageBonusSkill += (skill.pvpDamageBonusSkill * n) / 100.0;
            skill.pvpDamageReductionSkill += (skill.pvpDamageReductionSkill * n) / 100.0;
        }
        else if (name == "Kryształ Wiedzy") {
            skill.kleptomaniaBonusSkill += skill.kleptomaniaBonusSkill * n;
        }
        else if (name == "Cień Zwinności") {
            skill.movementSpeedBonusSkill += (skill.movementSpeedBonusSkill * n) / 100.0;
            skill.pCriticalDamageBonusSkill += (skill.pCriticalDamageBonusSkill * n) / 100.0;
            skill.mCriticalDamageBonusSkill += (skill.mCriticalDamageBonusSkill * n) / 100.0;
        }
    }

    void displayRuneInfo() {
        std::cout << "\n=== Informacje o Runie ===\n";
        std::cout << "Nazwa Runy: " << name << "\n";
        std::cout << "Powiązana Umiejętność: " << associatedSkill << "\n";
        std::cout << "Poziom Runy: " << level << "\n";
    }
};

class Pet {
public:
    int level;
    const int maxLevel = 200;
    std::unordered_map<std::string, PetSkill> skills;
    std::unordered_map<std::string, PetRune> runes;

    Pet(int level = 1) : level(level) {
        // Inicjalizacja umiejętności
        skills["Agresja"] = PetSkill("Agresja");
        skills["Obrońca"] = PetSkill("Obrońca");
        skills["Złotnik"] = PetSkill("Złotnik");
        skills["Łowca"] = PetSkill("Łowca");
        skills["Kolos"] = PetSkill("Kolos");
        skills["Oprawca"] = PetSkill("Oprawca");
        skills["Mądrość"] = PetSkill("Mądrość");
        skills["Zwinność"] = PetSkill("Zwinność");

        calculateSkillBonuses();
    }

    void levelUp(int levels) {
        level += levels;
        if (level > maxLevel) {
            level = maxLevel;
        }
        calculateSkillBonuses();
    }

    void calculateSkillBonuses() {
        // Obliczenia bonusów umiejętności na podstawie poziomu Peta
        // Możesz tutaj wykorzystać wcześniejsze wzory z poprzedniego problemu
    }

    void unlockRunes() {
        if (level >= 140 && runes.empty()) {
            // Tworzymy runy dla Peta
            runes["Runiczny Zew Gniewu"] = PetRune("Runiczny Zew Gniewu", "Agresja");
            runes["Tarcza Strażnika"] = PetRune("Tarcza Strażnika", "Obrońca");
            runes["Astralna Moneta"] = PetRune("Astralna Moneta", "Złotnik");
            runes["Pazur Łowcy"] = PetRune("Pazur Łowcy", "Łowca");
            runes["Runiczny Filar"] = PetRune("Runiczny Filar", "Kolos");
            runes["Piętno Oprawcy"] = PetRune("Piętno Oprawcy", "Oprawca");
            runes["Kryształ Wiedzy"] = PetRune("Kryształ Wiedzy", "Mądrość");
            runes["Cień Zwinności"] = PetRune("Cień Zwinności", "Zwinność");

            std::cout << "Runy zostały odblokowane!\n";
        } else if (level < 140) {
            std::cout << "Musisz osiągnąć poziom 140, aby odblokować runy.\n";
        } else {
            std::cout << "Runy są już odblokowane.\n";
        }
    }

    void levelUpRune(const std::string& runeName, int levels) {
        if (runes.find(runeName) != runes.end()) {
            runes[runeName].levelUp(levels);
            runes[runeName].applyEffect(skills[runes[runeName].associatedSkill]);
            std::cout << "Runa " << runeName << " została ulepszona do poziomu " << runes[runeName].level << ".\n";
        } else {
            std::cout << "Nie posiadasz takiej runy.\n";
        }
    }

    void displayPetInfo() {
        std::cout << "\n=== Informacje o Peta ===\n";
        std::cout << "Poziom Peta: " << level << "\n";

        for (const auto& skillPair : skills) {
            const PetSkill& skill = skillPair.second;
            std::cout << "\nUmiejętność: " << skill.name << "\n";
            displaySkillBonuses(skill);
        }
    }

    void displaySkillBonuses(const PetSkill& skill) {
        if (skill.name == "Agresja") {
            std::cout << "P.Atk Bonus Skill: " << skill.pAtkBonusSkill << "\n";
            std::cout << "M.Atk Bonus Skill: " << skill.mAtkBonusSkill << "\n";
        }
        else if (skill.name == "Obrońca") {
            std::cout << "P.Def Bonus Skill: " << skill.pDefBonusSkill << "\n";
            std::cout << "M.Def Bonus Skill: " << skill.mDefBonusSkill << "\n";
        }
        else if (skill.name == "Złotnik") {
            std::cout << "Bonus Gold Skill: " << skill.bonusGoldSkill << "%\n";
        }
        else if (skill.name == "Łowca") {
            std::cout << "Siła na Potwory Bonus Skill: " << skill.monsterDamageBonusSkill << "%\n";
        }
        else if (skill.name == "Kolos") {
            std::cout << "HP Bonus Skill: " << skill.hpBonusSkill << "\n";
            std::cout << "MP Bonus Skill: " << skill.mpBonusSkill << "\n";
        }
        else if (skill.name == "Oprawca") {
            std::cout << "PvP Damage Bonus Skill: " << skill.pvpDamageBonusSkill << "%\n";
            std::cout << "PvP Damage Reduction Skill: " << skill.pvpDamageReductionSkill << "%\n";
        }
        else if (skill.name == "Mądrość") {
            std::cout << "Kleptomania Bonus Skill: " << skill.kleptomaniaBonusSkill << "%\n";
        }
        else if (skill.name == "Zwinność") {
            std::cout << "Szybkość Ruchu Bonus Skill: " << skill.movementSpeedBonusSkill << "%\n";
            std::cout << "P Critical Damage Bonus Skill: " << skill.pCriticalDamageBonusSkill << "%\n";
            std::cout << "M Critical Damage Bonus Skill: " << skill.mCriticalDamageBonusSkill << "%\n";
        }
    }
};

int main() {
    Pet pet;

    int levelsToAdd;
    std::cout << "Podaj liczbę poziomów do dodania dla Peta: ";
    std::cin >> levelsToAdd;

    pet.levelUp(levelsToAdd);

    // Odblokowanie run, jeśli poziom Peta >= 140
    pet.unlockRunes();

    // Jeśli runy są odblokowane, możemy ulepszać runy
    if (!pet.runes.empty()) {
        std::cout << "\nDostępne runy:\n";
        int index = 1;
        for (const auto& runePair : pet.runes) {
            std::cout << index++ << ". " << runePair.first << "\n";
        }

        int runeChoice;
        std::cout << "Wybierz runę do ulepszenia (podaj numer): ";
        std::cin >> runeChoice;

        if (runeChoice >= 1 && runeChoice <= (int)pet.runes.size()) {
            auto it = pet.runes.begin();
            std::advance(it, runeChoice - 1);
            std::string selectedRuneName = it->first;

            int runeLevelsToAdd;
            std::cout << "Podaj liczbę poziomów do dodania dla runy " << selectedRuneName << ": ";
            std::cin >> runeLevelsToAdd;

            pet.levelUpRune(selectedRuneName, runeLevelsToAdd);
        } else {
            std::cout << "Nieprawidłowy wybór runy.\n";
        }
    }

    pet.displayPetInfo();

    return 0;
}
```
