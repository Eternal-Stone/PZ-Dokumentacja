# System Drzewek Umiejętności

Chciałbym przedstawić propozycję systemu drzewek umiejętności, który jest elastyczny i nie posiada ograniczeń poziomowych czy punktowych. System ten będzie wzorowany ideowo na "Titan Quest", z uwzględnieniem 8 umiejętności ofensywnych i 5 defensywnych dla każdej klasy.

## Struktura Systemu

- **Klasy postaci (Classes):** Każda klasa posiada unikalne drzewko umiejętności.
- **Umiejętności (Skills):** Każda umiejętność ma swoje własne właściwości, efekty i relacje z innymi umiejętnościami.
- **Drzewka umiejętności (Skill Trees):** Umiejętności są zorganizowane w drzewka, które mogą mieć zależności (np. wymaganie wcześniejszego odblokowania innej umiejętności).

## Przechowywanie Informacji

- **Klasy i struktury:**
  - **`Skill`**: Klasa reprezentująca pojedynczą umiejętność.
  - **`SkillTree`**: Klasa lub struktura przechowująca listę umiejętności dla danej klasy postaci.
  - **`Player`**: Klasa reprezentująca gracza, zawierająca informacje o odblokowanych umiejętnościach.
- **Atrybuty klasy `Skill`:**
  - `std::string name;` – nazwa umiejętności.
  - `std::string description;` – opis umiejętności.
  - `std::vector&lt;std::string> prerequisites;` – lista nazw umiejętności wymaganych do odblokowania tej umiejętności.
  - `bool isUnlocked;` – czy umiejętność jest odblokowana.
  - `std::function&lt;void(Player&)> effect;` – funkcja reprezentująca efekt umiejętności.

## Obliczanie Wartości

- **Skalowanie umiejętności:** Umiejętności mogą skalować się w oparciu o statystyki gracza lub inne czynniki.
- **Efekty umiejętności:** Każda umiejętność ma określony efekt, który może być reprezentowany jako funkcja modyfikująca statystyki gracza.

## Propozycja programu realizującego dany problem

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <unordered_map>
#include <functional>

class Player {
public:
    std::string className;
    std::unordered_map<std::string, int> stats;
    std::vector<std::string> unlockedSkills;

    Player(const std::string& className) : className(className) {
        // Inicjalizacja statystyk gracza
        stats["Health"] = 100;
        stats["Mana"] = 50;
        stats["Strength"] = 10;
        stats["Defense"] = 5;
        // ... inne statystyki
    }

    void applyEffect(const std::function<void(Player&)>& effect) {
        effect(*this);
    }

    void displayStats() {
        std::cout << "Statystyki gracza:\n";
        for (const auto& stat : stats) {
            std::cout << stat.first << ": " << stat.second << "\n";
        }
    }
};

class Skill {
public:
    std::string name;
    std::string description;
    std::vector<std::string> prerequisites;
    bool isUnlocked;
    std::function<void(Player&)> effect;

    Skill(const std::string& name,
          const std::string& description,
          const std::vector<std::string>& prerequisites,
          const std::function<void(Player&)>& effect)
        : name(name), description(description), prerequisites(prerequisites), isUnlocked(false), effect(effect) {}

    bool canUnlock(const Player& player) const {
        for (const auto& prereq : prerequisites) {
            if (std::find(player.unlockedSkills.begin(), player.unlockedSkills.end(), prereq) == player.unlockedSkills.end()) {
                return false;
            }
        }
        return true;
    }

    void unlock(Player& player) {
        if (canUnlock(player)) {
            isUnlocked = true;
            player.unlockedSkills.push_back(name);
            std::cout << "Umiejętność " << name << " została odblokowana!\n";
        } else {
            std::cout << "Nie spełniasz wymagań, aby odblokować umiejętność " << name << ".\n";
        }
    }

    void use(Player& player) {
        if (isUnlocked) {
            effect(player);
            std::cout << "Użyto umiejętności " << name << ".\n";
        } else {
            std::cout << "Umiejętność " << name << " nie jest odblokowana.\n";
        }
    }
};

class SkillTree {
public:
    std::unordered_map<std::string, Skill> skills;

    void addSkill(const Skill& skill) {
        skills[skill.name] = skill;
    }

    void unlockSkill(const std::string& skillName, Player& player) {
        if (skills.find(skillName) != skills.end()) {
            skills[skillName].unlock(player);
        } else {
            std::cout << "Nie znaleziono umiejętności " << skillName << ".\n";
        }
    }

    void useSkill(const std::string& skillName, Player& player) {
        if (skills.find(skillName) != skills.end()) {
            skills[skillName].use(player);
        } else {
            std::cout << "Nie znaleziono umiejętności " << skillName << ".\n";
        }
    }

    void displaySkills() const {
        std::cout << "=== Drzewko Umiejętności ===\n";
        for (const auto& pair : skills) {
            const Skill& skill = pair.second;
            std::cout << "Umiejętność: " << skill.name << "\n";
            std::cout << "Opis: " << skill.description << "\n";
            std::cout << "Odblokowana: " << (skill.isUnlocked ? "Tak" : "Nie") << "\n";
            std::cout << "Wymagania: ";
            if (skill.prerequisites.empty()) {
                std::cout << "Brak";
            } else {
                for (const auto& prereq : skill.prerequisites) {
                    std::cout << prereq << " ";
                }
            }
            std::cout << "\n\n";
        }
    }
};

int main() {
    // Tworzenie gracza
    Player player("Mage");

    // Tworzenie drzewka umiejętności dla Maga
    SkillTree mageSkillTree;

    // Definiowanie umiejętności ofensywnych
    mageSkillTree.addSkill(Skill("Fireball", "Rzuca kulę ognia zadając obrażenia przeciwnikowi.",
        {}, [](Player& p) {
            // Efekt umiejętności
            std::cout << "Zadajesz 50 punktów obrażeń ogniem.\n";
        }));

    mageSkillTree.addSkill(Skill("Flame Wave", "Tworzy falę ognia palącą wszystkich wrogów przed tobą.",
        {"Fireball"}, [](Player& p) {
            std::cout << "Zadajesz 70 punktów obrażeń ogniem wszystkim wrogom przed tobą.\n";
        }));

    // ... Dodaj pozostałe umiejętności ofensywne

    // Definiowanie umiejętności defensywnych
    mageSkillTree.addSkill(Skill("Mana Shield", "Tworzy tarczę pochłaniającą obrażenia kosztem many.",
        {}, [](Player& p) {
            std::cout << "Aktywujesz tarczę many.\n";
        }));

    mageSkillTree.addSkill(Skill("Elemental Resistance", "Zwiększa odporność na żywioły.",
        {"Mana Shield"}, [](Player& p) {
            std::cout << "Twoje odporności na żywioły wzrosły.\n";
            p.stats["Defense"] += 10;
        }));

    // ... Dodaj pozostałe umiejętności defensywne

    // Wyświetlenie drzewka umiejętności
    mageSkillTree.displaySkills();

    // Przykład odblokowania i użycia umiejętności
    mageSkillTree.unlockSkill("Fireball", player);
    mageSkillTree.useSkill("Fireball", player);

    mageSkillTree.unlockSkill("Flame Wave", player);
    mageSkillTree.useSkill("Flame Wave", player);

    player.displayStats();

    return 0;
}
```
