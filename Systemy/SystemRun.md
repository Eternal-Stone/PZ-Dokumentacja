# System Run (System ulepszania umiejętności)

System run pozwala graczom personalizować i wzmacniać swoje umiejętności poprzez używanie run. Runy działają podobnie do [systemu enchantowania](SystemEnchantowania.md) – gracze "wlewają" energię z run do umiejętności, podnosząc jej poziom. Gdy umiejętność osiągnie określone poziomy, gracze otrzymują punkty umiejętności, które mogą wydać w drzewku rozwoju tej umiejętności. Dzięki temu mogą odblokować dodatkowe efekty, takie jak:

- Ogłuszenie (Stun)
- Podpalenie (Ignite)
- Obrażenia obszarowe (Splash)
- Inne bonusy

## Konceptualny Przegląd Systemu

### Runy

Runy to przedmioty używane do podnoszenia poziomu umiejętności. Każda runa dodaje określoną ilość energii do umiejętności, stopniowo zwiększając jej siłę i możliwości.

### Poziomy umiejętności

Każda umiejętność posiada poziomy. Po osiągnięciu określonego poziomu gracz otrzymuje punkty umiejętności, które może wykorzystać na dalsze ulepszenia.

### Punkty umiejętności

Zdobywane wraz z poziomami umiejętności, punkty umiejętności mogą być wydane w drzewku rozwoju umiejętności, umożliwiając ich personalizację i dostosowanie do stylu gry.

### Drzewko rozwoju umiejętności

Dla każdej umiejętności istnieje małe drzewko rozwoju, które pozwala graczom na odblokowanie dodatkowych efektów i modyfikatorów, zwiększając ich skuteczność oraz dostosowując je do indywidualnych preferencji.

## Propozycja programu realizującego dany problem

```cpp
class Rune {
public:
    std::string name;
    int energyValue; // Ilość energii dodawanej do umiejętności

    Rune(const std::string& name, int energyValue)
        : name(name), energyValue(energyValue) {}
};

class SkillUpgrade {
public:
    std::string name;
    std::string description;
    int cost; // Koszt w punktach umiejętności
    bool isUnlocked;
    std::vector<SkillUpgrade*> prerequisites;

    SkillUpgrade(const std::string& name, const std::string& description, int cost)
        : name(name), description(description), cost(cost), isUnlocked(false) {}

    bool canUnlock(const std::vector<SkillUpgrade*>& unlockedUpgrades) const;
};
class Skill {
public:
    std::string name;
    int level; // Aktualny poziom umiejętności
    int energy; // Aktualna ilość energii w umiejętności
    int skillPoints; // Dostępne punkty umiejętności do wydania
    std::vector<SkillUpgrade*> upgrades; // Wszystkie możliwe ulepszenia umiejętności
    std::vector<SkillUpgrade*> unlockedUpgrades; // Odblokowane ulepszenia

    Skill(const std::string& name)
        : name(name), level(0), energy(0), skillPoints(0) {}

    void addEnergy(int amount);
    void unlockUpgrade(const std::string& upgradeName);
    void useSkill();
};

class Player {
public:
    std::string name;
    std::unordered_map<std::string, Skill> skills;

    Player(const std::string& name) : name(name) {}

    void addSkill(const Skill& skill);
    void useSkill(const std::string& skillName);
};

bool SkillUpgrade::canUnlock(const std::vector<SkillUpgrade*>& unlockedUpgrades) const {
    for (const auto& prereq : prerequisites) {
        if (std::find(unlockedUpgrades.begin(), unlockedUpgrades.end(), prereq) == unlockedUpgrades.end()) {
            return false;
        }
    }
    return true;
}

void Skill::addEnergy(int amount) {
    energy += amount;

    // Logika podnoszenia poziomu umiejętności
    int requiredEnergyForNextLevel = (level + 1) * 100; // Przykładowo, każdy poziom wymaga 100 energii * poziom
    while (energy >= requiredEnergyForNextLevel) {
        energy -= requiredEnergyForNextLevel;
        level++;
        skillPoints++; // Dodajemy punkt umiejętności
        std::cout << "Umiejętność " << name << " osiągnęła poziom " << level << "! Otrzymano 1 punkt umiejętności.\n";
        requiredEnergyForNextLevel = (level + 1) * 100;
    }
}
void Skill::unlockUpgrade(const std::string& upgradeName) {
    auto it = std::find_if(upgrades.begin(), upgrades.end(), [&](SkillUpgrade* u) { return u->name == upgradeName; });
    if (it != upgrades.end()) {
        SkillUpgrade* upgrade = *it;
        if (upgrade->isUnlocked) {
            std::cout << "Ulepszenie " << upgradeName << " jest już odblokowane.\n";
            return;
        }
        if (upgrade->canUnlock(unlockedUpgrades)) {
            if (skillPoints >= upgrade->cost) {
                skillPoints -= upgrade->cost;
                upgrade->isUnlocked = true;
                unlockedUpgrades.push_back(upgrade);
                std::cout << "Odblokowano ulepszenie " << upgradeName << ".\n";
            } else {
                std::cout << "Nie masz wystarczającej liczby punktów umiejętności.\n";
            }
        } else {
            std::cout << "Nie spełniasz wymagań, aby odblokować ulepszenie " << upgradeName << ".\n";
        }
    } else {
        std::cout << "Nie znaleziono ulepszenia " << upgradeName << ".\n";
    }
}

void Skill::useSkill() {
    std::cout << "Użyto umiejętności " << name << ".\n";

    // Podstawowy efekt umiejętności
    std::cout << "Efekt podstawowy umiejętności.\n";

    // Efekty odblokowanych ulepszeń
    for (const auto& upgrade : unlockedUpgrades) {
        std::cout << "Efekt ulepszenia " << upgrade->name << ": " << upgrade->description << "\n";
    }
}

void Player::addSkill(const Skill& skill) {
    skills[skill.name] = skill;
}

void Player::useSkill(const std::string& skillName) {
    if (skills.find(skillName) != skills.end()) {
        skills[skillName].useSkill();
    } else {
        std::cout << "Nie posiadasz umiejętności " << skillName << ".\n";
    }
}

I tutaj przykład użycia

int main() {
    // Tworzenie gracza
    Player player("Hero");

    // Tworzenie umiejętności
    Skill fireball("Fireball");

    // Dodawanie ulepszeń do umiejętności
    SkillUpgrade stunUpgrade("Stun", "Szansa na ogłuszenie przeciwnika.", 1);
    SkillUpgrade igniteUpgrade("Ignite", "Podpala przeciwnika zadając obrażenia w czasie.", 1);
    SkillUpgrade splashUpgrade("Splash", "Obrażenia obszarowe wokół celu.", 2);

    // Ustalanie zależności między ulepszeniami
    splashUpgrade.prerequisites.push_back(&igniteUpgrade);

    // Dodawanie ulepszeń do umiejętności
    fireball.upgrades.push_back(&stunUpgrade);
    fireball.upgrades.push_back(&igniteUpgrade);
    fireball.upgrades.push_back(&splashUpgrade);

    // Dodawanie umiejętności do gracza
    player.addSkill(fireball);

    // Gracz używa run, aby podbić poziom umiejętności
    Rune fireRune("Fire Rune", 150); // Runa dodaje 150 energii
    player.skills["Fireball"].addEnergy(fireRune.energyValue);

    // Odblokowywanie ulepszeń
    player.skills["Fireball"].unlockUpgrade("Ignite");
    player.skills["Fireball"].unlockUpgrade("Splash"); // Nie powinno się udać bez Ignite

    // Gracz używa umiejętności
    player.useSkill("Fireball");

    return 0;
}
```
