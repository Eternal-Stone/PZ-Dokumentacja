# System Umiejętności Peta

Pet ma swoje umiejętności, które powodują, że gracz staje się silniejszy.

**Specjalizacje umiejętności**:

- **Agresja**: Zwiększa P.Atk, M.Atk, moc umiejętności fizycznych i magicznych.
- **Obrońca**: Zwiększa P.Def, M.Def, redukuje otrzymywane obrażenia z umiejętności.
- **Złotnik**: Zwiększa pozyskiwane złoto.
- **Łowca**: Zwiększa obrażenia przeciwko potworom.
- **Kolos**: Zwiększa HP, MP, odporności na obrażenia krytyczne.
- **Oprawca**: Zwiększa obrażenia w PvP, redukuje otrzymywane obrażenia w PvP.
- **Mądrość**: Zwiększa szanse na pozyskanie przedmiotów z mobów.
- **Zwinność**: Zwiększa szybkość ruchu, obrażenia krytyczne fizyczne i magiczne.

**Poziomy Umiejętności**:

- Maksymalnie **50 poziomów** na umiejętność.
- Pierwsze **25 poziomów** można zdobyć za punkty umiejętności peta.
- Poziomy **26-40** wymagają specjalnych ksiąg wzmocnienia peta.
- Poziomy **41-50** wymagają arcymistrzowskich ksiąg peta (dostępnych z systemu craftowania).

## Sposób obliczania statystyk

```text
n - indeks
```

### Poziomy 1-25

- **Agresja**:
  - P.Atk bonus = P.Atk bonus + 5*n
  - M.Atk bonus = M.Atk bonus + 7*n

- **Obrońca**:
  - P.Def bonus = P.Def bonus + 3*n
  - M.Def bonus = M.Def bonus + 3*n

- **Złotnik**:
  - Bonus gold = Bonus gold + 4*n

- **Łowca**:
  - Siła na potwory bonus = Siła na potwory bonus + 1*n

- **Kolos**:
  - HP bonus = HP bonus + 20*n
  - MP bonus = MP bonus + 20*n

- **Oprawca**:
  - PvP Dmg bonus = PvP Dmg + 1*n

- **Mądrość**:
  - Kleptomancja bonus = Kleptomancja bonus + 1*n

- **Zwinność**:
  - Szybkość ruchu bonus = Szybkość ruchu bonus + 1*n
  - P.Critical Dmg bonus = P.Critical Dmg bonus + 1*n
  - M.Critical Dmg bonus = M.Critical Dmg bonus + 1*n

### Poziomy 26-40

- **Agresja**:
  - P.Atk bonus = P.Atk bonus + 7*n
  - M.Atk bonus = M.Atk bonus + 9*n

- **Obrońca**:
  - P.Def bonus = P.Def bonus + 4*n
  - M.Def bonus = M.Def bonus + 4*n

- **Złotnik**:
  - Bonus gold = Bonus gold + 5*n

- **Łowca**:
  - Siła na potwory bonus = Siła na potwory bonus + 1.5*n

- **Kolos**:
  - HP bonus = HP bonus + 28*n
  - MP bonus = MP bonus + 28*n

- **Oprawca**:
  - PvP Dmg bonus = PvP Dmg + 1.5*n

- **Mądrość**:
  - Kleptomancja bonus = Kleptomancja bonus + 2*n

- **Zwinność**:
  - Szybkość ruchu bonus = Szybkość ruchu bonus + 1.5*n
  - P.Critical Dmg bonus = P.Critical Dmg bonus + 1.5*n
  - M.Critical Dmg bonus = M.Critical Dmg bonus + 1.5*n

### Poziomy 41-50

- **Agresja**:
  - P.Atk bonus = P.Atk bonus + 10*n
  - M.Atk bonus = M.Atk bonus + 14*n

- **Obrońca**:
  - P.Def bonus = P.Def bonus + 6*n
  - M.Def bonus = M.Def bonus + 6*n

- **Złotnik**:
  - Bonus gold = Bonus gold + 8*n

- **Łowca**:
  - Siła na potwory bonus = Siła na potwory bonus + 2*n

- **Kolos**:
  - HP bonus = HP bonus + 40*n
  - MP bonus = MP bonus + 40*n

- **Oprawca**:
  - PvP Dmg bonus = PvP Dmg + 2*n

- **Mądrość**:
  - Kleptomancja bonus = Kleptomancja bonus + 2*n

- **Zwinność**:
  - Szybkość ruchu bonus = Szybkość ruchu bonus + 2*n
  - P.Critical Dmg bonus = P.Critical Dmg bonus + 2*n
  - M.Critical Dmg bonus = M.Critical Dmg bonus + 2*n

## Propozycja programu realizującego dany problem

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <cmath>

class PetSkill {
public:
    std::string name;
    int level;
    const int maxLevel = 50;

    // Bonusy dla różnych statystyk
    double pAtkBonus;
    double mAtkBonus;
    double pDefBonus;
    double mDefBonus;
    double bonusGold;
    double monsterDamageBonus;
    double hpBonus;
    double mpBonus;
    double pvpDamageBonus;
    double pvpDamageReduction;
    double kleptomaniaBonus;
    double movementSpeedBonus;
    double pCriticalDamageBonus;
    double mCriticalDamageBonus;

    PetSkill(const std::string& name) : name(name), level(0), pAtkBonus(0), mAtkBonus(0),
        pDefBonus(0), mDefBonus(0), bonusGold(0), monsterDamageBonus(0),
        hpBonus(0), mpBonus(0), pvpDamageBonus(0), pvpDamageReduction(0),
        kleptomaniaBonus(0), movementSpeedBonus(0),
        pCriticalDamageBonus(0), mCriticalDamageBonus(0) {}

    void levelUp(int levels) {
        if (level + levels > maxLevel) {
            levels = maxLevel - level;
        }
        level += levels;

        calculateBonuses();
    }

    void calculateBonuses() {
        // Resetujemy bonusy
        pAtkBonus = 0;
        mAtkBonus = 0;
        pDefBonus = 0;
        mDefBonus = 0;
        bonusGold = 0;
        monsterDamageBonus = 0;
        hpBonus = 0;
        mpBonus = 0;
        pvpDamageBonus = 0;
        pvpDamageReduction = 0;
        kleptomaniaBonus = 0;
        movementSpeedBonus = 0;
        pCriticalDamageBonus = 0;
        mCriticalDamageBonus = 0;

        int levelRanges[3][2] = { {1, 25}, {26, 40}, {41, 50} };

        for (int i = 0; i < 3; ++i) {
            int startLevel = levelRanges[i][0];
            int endLevel = levelRanges[i][1];

            if (level < startLevel)
                continue;

            int n_start = std::max(startLevel, 1);
            int n_end = std::min(endLevel, level);

            int n = n_end - n_start + 1;

            if (n <= 0)
                continue;

            switchSkillBonuses(n_start, n_end, n, i);
        }
    }

    void switchSkillBonuses(int n_start, int n_end, int n, int rangeIndex) {
        double multiplier = 1.0;

        if (rangeIndex == 0) { // Levels 1-25
            multiplier = 1.0;
        } else if (rangeIndex == 1) { // Levels 26-40
            multiplier = 1.0;
        } else if (rangeIndex == 2) { // Levels 41-50
            multiplier = 1.0;
        }

        for (int lvl = n_start; lvl <= n_end; ++lvl) {
            double n_local = 1.0; // Zmienna pomocnicza do obliczeń

            if (name == "Agresja") {
                if (lvl <= 25) {
                    pAtkBonus += 5 * n_local;
                    mAtkBonus += 7 * n_local;
                } else if (lvl <= 40) {
                    pAtkBonus += 7 * n_local;
                    mAtkBonus += 9 * n_local;
                } else if (lvl <= 50) {
                    pAtkBonus += 10 * n_local;
                    mAtkBonus += 14 * n_local;
                }
            }
            else if (name == "Obrońca") {
                if (lvl <= 25) {
                    pDefBonus += 3 * n_local;
                    mDefBonus += 3 * n_local;
                } else if (lvl <= 40) {
                    pDefBonus += 4 * n_local;
                    mDefBonus += 4 * n_local;
                } else if (lvl <= 50) {
                    pDefBonus += 6 * n_local;
                    mDefBonus += 6 * n_local;
                }
            }
            else if (name == "Złotnik") {
                if (lvl <= 25) {
                    bonusGold += 4 * n_local;
                } else if (lvl <= 40) {
                    bonusGold += 5 * n_local;
                } else if (lvl <= 50) {
                    bonusGold += 8 * n_local;
                }
            }
            else if (name == "Łowca") {
                if (lvl <= 25) {
                    monsterDamageBonus += 1 * n_local;
                } else if (lvl <= 40) {
                    monsterDamageBonus += 1.5 * n_local;
                } else if (lvl <= 50) {
                    monsterDamageBonus += 2 * n_local;
                }
            }
            else if (name == "Kolos") {
                if (lvl <= 25) {
                    hpBonus += 20 * n_local;
                    mpBonus += 20 * n_local;
                } else if (lvl <= 40) {
                    hpBonus += 28 * n_local;
                    mpBonus += 28 * n_local;
                } else if (lvl <= 50) {
                    hpBonus += 40 * n_local;
                    mpBonus += 40 * n_local;
                }
            }
            else if (name == "Oprawca") {
                if (lvl <= 25) {
                    pvpDamageBonus += 1 * n_local;
                    pvpDamageReduction += 1 * n_local;
                } else if (lvl <= 40) {
                    pvpDamageBonus += 1.5 * n_local;
                    pvpDamageReduction += 1.5 * n_local;
                } else if (lvl <= 50) {
                    pvpDamageBonus += 2 * n_local;
                    pvpDamageReduction += 2 * n_local;
                }
            }
            else if (name == "Mądrość") {
                if (lvl <= 25) {
                    kleptomaniaBonus += 1 * n_local;
                } else if (lvl <= 40) {
                    kleptomaniaBonus += 2 * n_local;
                } else if (lvl <= 50) {
                    kleptomaniaBonus += 2 * n_local;
                }
            }
            else if (name == "Zwinność") {
                if (lvl <= 25) {
                    movementSpeedBonus += 1 * n_local;
                    pCriticalDamageBonus += 1 * n_local;
                    mCriticalDamageBonus += 1 * n_local;
                } else if (lvl <= 40) {
                    movementSpeedBonus += 1.5 * n_local;
                    pCriticalDamageBonus += 1.5 * n_local;
                    mCriticalDamageBonus += 1.5 * n_local;
                } else if (lvl <= 50) {
                    movementSpeedBonus += 2 * n_local;
                    pCriticalDamageBonus += 2 * n_local;
                    mCriticalDamageBonus += 2 * n_local;
                }
            }
        }
    }

    void displayBonuses() {
        std::cout << "\n=== Statystyki umiejętności: " << name << " ===\n";
        std::cout << "Poziom umiejętności: " << level << "\n";

        if (name == "Agresja") {
            std::cout << "P.Atk Bonus: " << pAtkBonus << "\n";
            std::cout << "M.Atk Bonus: " << mAtkBonus << "\n";
        }
        else if (name == "Obrońca") {
            std::cout << "P.Def Bonus: " << pDefBonus << "\n";
            std::cout << "M.Def Bonus: " << mDefBonus << "\n";
        }
        else if (name == "Złotnik") {
            std::cout << "Bonus Gold: " << bonusGold << "%\n";
        }
        else if (name == "Łowca") {
            std::cout << "Bonus obrażeń przeciwko potworom: " << monsterDamageBonus << "%\n";
        }
        else if (name == "Kolos") {
            std::cout << "HP Bonus: " << hpBonus << "\n";
            std::cout << "MP Bonus: " << mpBonus << "\n";
        }
        else if (name == "Oprawca") {
            std::cout << "PvP Damage Bonus: " << pvpDamageBonus << "%\n";
            std::cout << "PvP Damage Reduction: " << pvpDamageReduction << "%\n";
        }
        else if (name == "Mądrość") {
            std::cout << "Kleptomania Bonus: " << kleptomaniaBonus << "%\n";
        }
        else if (name == "Zwinność") {
            std::cout << "Szybkość Ruchu Bonus: " << movementSpeedBonus << "%\n";
            std::cout << "P Critical Damage Bonus: " << pCriticalDamageBonus << "%\n";
            std::cout << "M Critical Damage Bonus: " << mCriticalDamageBonus << "%\n";
        }
    }
};

int main() {
    // Lista dostępnych specjalizacji
    std::vector<std::string> specializations = {
        "Agresja", "Obrońca", "Złotnik", "Łowca",
        "Kolos", "Oprawca", "Mądrość", "Zwinność"
    };

    // Tworzenie umiejętności peta
    std::vector<PetSkill> petSkills;
    for (const auto& spec : specializations) {
        petSkills.emplace_back(spec);
    }

    // Wybór umiejętności do podniesienia poziomu
    std::cout << "Wybierz umiejętność do podniesienia poziomu:\n";
    for (size_t i = 0; i < specializations.size(); ++i) {
        std::cout << i + 1 << ". " << specializations[i] << "\n";
    }
    int choice;
    std::cout << "Twój wybór (1-" << specializations.size() << "): ";
    std::cin >> choice;

    if (choice < 1 || choice >(int)specializations.size()) {
        std::cout << "Nieprawidłowy wybór.\n";
        return 1;
    }

    PetSkill& selectedSkill = petSkills[choice - 1];

    int levelsToAdd;
    std::cout << "Podaj liczbę poziomów do dodania dla umiejętności " << selectedSkill.name << ": ";
    std::cin >> levelsToAdd;

    if (levelsToAdd < 1) {
        std::cout << "Liczba poziomów musi być większa od 0.\n";
        return 1;
    }

    selectedSkill.levelUp(levelsToAdd);
    selectedSkill.displayBonuses();

    return 0;
}
```
