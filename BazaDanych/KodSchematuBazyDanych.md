# Kod Schematu Bazy Danych

Poniższy dokument ma charakter uzupełniający dla kwestii schematu bazy danych. Zawiera on całościowy kod go tworzący, co uznaję za pożyteczne, albowiem staram się umieszczać w nim komentarze dla czytelnika oraz znajdują się na nim informacje niedostępne z widoku samego schematu. Plik ten będzie aktualizowany na bieżąco wraz ze zmianami, które będą miały sens w rozumieniu całościowym, tak aby analiza go była pomocną, nie zaś utrudnieniem.

Kod można dowolnie testować i modyfikować na stronie **`dbdiagram.io`**.

```sql
/////////////////////////////////////////////////////////
// PODSTAWOWE TABELE UŻYTKOWNIKA I POSTACI
/////////////////////////////////////////////////////////


Table User {
  id INT [pk, increment]
  username VARCHAR(50) [unique, not null]
  email VARCHAR(100) [unique, not null]
  password VARCHAR(255) [not null]
  registration_date DATETIME [default: `CURRENT_TIMESTAMP`]
}


Table Class {
  id INT [pk, increment]
  name VARCHAR(100) [not null, unique]
  description TEXT
}


Table Character {
  id INT [pk, increment]
  user_id INT [not null, ref: > User.id]
  class_id INT [not null, ref: > Class.id]
  name VARCHAR(50) [not null]
  level INT [default: 1]
  experience INT [default: 0]
}


/////////////////////////////////////////////////////////
// STATYSTYKI POSTACI
/////////////////////////////////////////////////////////


Table OffensiveStats {
  id INT [pk, increment]
  character_id INT [not null, ref: > Character.id]


  // Podstawowe statystyki
  strength INT [default: 0]
  dexterity INT [default: 0]
  intelligence INT [default: 0]
  mentality INT [default: 0]
  physical_accuracy INT [default: 0]


  // Statystyki ofensywne
  increased_damage_to_rulers INT [default: 0]
  increased_damage_to_statues INT [default: 0]
  increased_damage_to_ancients INT [default: 0]
  increased_damage_to_humans INT [default: 0]
  precision INT [default: 0]
  destruction INT [default: 0]
  aggression INT [default: 0]
  domination INT [default: 0]
  auto_attack_damage_bonus INT [default: 0]
  aoe_damage INT [default: 0]
  physical_attack INT [default: 0]
  magical_attack INT [default: 0]


  // Ataki żywiołów
  fire_attack INT [default: 0]
  water_attack INT [default: 0]
  earth_attack INT [default: 0]
  wind_attack INT [default: 0]
  holy_attack INT [default: 0]
  dark_attack INT [default: 0]


  // PvP/PvE ofensywne
  pvp_physical_damage INT [default: 0]
  pvp_magical_damage INT [default: 0]
  pve_physical_damage INT [default: 0]
  pve_magical_damage INT [default: 0]
}


Table DefensiveStats {
  id INT [pk, increment]
  character_id INT [not null, ref: > Character.id]


  vitality INT [default: 0]
  resistance_to_humans INT [default: 0]
  resistance_to_critical_damage INT [default: 0]
  tenacity INT [default: 0]
  max_hp_percent DECIMAL(5,2) [default: 0.00]


  fire_resistance INT [default: 0]
  water_resistance INT [default: 0]
  earth_resistance INT [default: 0]
  wind_resistance INT [default: 0]
  holy_resistance INT [default: 0]
  dark_resistance INT [default: 0]


  physical_defense INT [default: 0]
  magical_defense INT [default: 0]
  physical_evasion INT [default: 0]
}


Table OtherStats {
  id INT [pk, increment]
  character_id INT [not null, ref: > Character.id]


  luck INT [default: 0]
  charisma INT [default: 0]


  gold_bonus INT [default: 0]
  kleptomancy INT [default: 0]
  mining_power INT [default: 0]
  harvest INT [default: 0]


  reputation INT [default: 0]
  pvp_pk_points INT [default: 0]
  raid_points INT [default: 0]
  recommendations INT [default: 0]
}


/////////////////////////////////////////////////////////
// PROFESJE I POWIĄZANIA Z POSTACIĄ
/////////////////////////////////////////////////////////


Table Profession {
  id INT [pk, increment]
  name VARCHAR(50) [not null, unique] // np. Fisherman, Herbalist, Miner, Thief
  description TEXT
}


Table CharacterProfession {
  id INT [pk, increment]
  character_id INT [not null, ref: > Character.id]
  profession_id INT [not null, ref: > Profession.id]
  level INT [default: 0]    // Poziom danej profesji (0-100)
  experience INT [default: 0] // Doświadczenie danej profesji
}


/////////////////////////////////////////////////////////
// SYSTEM WĘDKARZA (Fisherman)
/////////////////////////////////////////////////////////


Table Fish {
  id INT [pk, increment]
  name VARCHAR(100) [not null]
  rarity INT [default: 1]
  required_fishing_level INT [default: 0]
}


Table FishingSpot {
  id INT [pk, increment]
  name VARCHAR(100) [not null]
  description TEXT
  required_fishing_level INT [default: 0]
  environment_type VARCHAR(50)
}


Table Bait {
  id INT [pk, increment]
  name VARCHAR(100) [not null, unique]
  description TEXT
}


Table FishAvailability {
  id INT [pk, increment]
  fish_id INT [not null, ref: > Fish.id]
  fishing_spot_id INT [not null, ref: > FishingSpot.id]
  day_time_condition VARCHAR(50) // np. "night", "full_moon"
  bait_id INT [null, ref: > Bait.id]
}


Table FishLoot {
  id INT [pk, increment]
  fish_id INT [not null, ref: > Fish.id]
  item_name VARCHAR(100) [not null]
  drop_chance DECIMAL(5,2) [default: 100.00]
}


Table FishingLevelBonuses {
  id INT [pk, increment]
  min_level INT [not null]
  max_level INT [not null]
  dexterity_bonus INT [default: 0]
  precision_bonus INT [default: 0]
  evasion_bonus INT [default: 0]
  m_accuracy_bonus DECIMAL(5,2) [default: 0.00]
  p_accuracy_bonus DECIMAL(5,2) [default: 0.00]
  fishing_power_bonus INT [default: 0]
}


/////////////////////////////////////////////////////////
// SYSTEM ZIELARZA (Herbalist)
/////////////////////////////////////////////////////////


Table Herb {
  id INT [pk, increment]
  name VARCHAR(100) [not null]
  rarity INT [default: 1]
  required_herbalist_level INT [default: 0]
}


Table HerbLocation {
  id INT [pk, increment]
  name VARCHAR(100) [not null]
  description TEXT
  required_herbalist_level INT [default: 0]
  environment_type VARCHAR(50)
}


Table HerbAvailability {
  id INT [pk, increment]
  herb_id INT [not null, ref: > Herb.id]
  herb_location_id INT [not null, ref: > HerbLocation.id]
  day_time_condition VARCHAR(50)
}


Table HerbLoot {
  id INT [pk, increment]
  herb_id INT [not null, ref: > Herb.id]
  item_name VARCHAR(100) [not null]
  drop_chance DECIMAL(5,2) [default: 100.00]
}


Table HerbalistLevelBonuses {
  id INT [pk, increment]
  min_level INT [not null]
  max_level INT [not null]
  mentality_bonus INT [default: 0]
  kleptomancy_bonus INT [default: 0]
  harvest_bonus INT [default: 0]
  mp_bonus INT [default: 0] // można stosować dodatkową logikę mnożenia
}


/////////////////////////////////////////////////////////
// SYSTEM GÓRNIKA (Miner)
/////////////////////////////////////////////////////////


Table Ore {
  id INT [pk, increment]
  name VARCHAR(100) [not null]
  rarity INT [default: 1]
  required_mining_level INT [default: 0]
}


Table MineLocation {
  id INT [pk, increment]
  name VARCHAR(100) [not null]
  description TEXT
  required_mining_level INT [default: 0]
  environment_type VARCHAR(50)
}


Table OreAvailability {
  id INT [pk, increment]
  ore_id INT [not null, ref: > Ore.id]
  mine_location_id INT [not null, ref: > MineLocation.id]
  day_time_condition VARCHAR(50)
}


Table OreLoot {
  id INT [pk, increment]
  ore_id INT [not null, ref: > Ore.id]
  item_name VARCHAR(100) [not null]
  drop_chance DECIMAL(5,2) [default: 100.00]
}


Table MiningLevelBonuses {
  id INT [pk, increment]
  min_level INT [not null]
  max_level INT [not null]
  strength_bonus INT [default: 0]
  aggression_bonus INT [default: 0]
  domination_bonus INT [default: 0]
  mining_power_bonus INT [default: 0]
}


/////////////////////////////////////////////////////////
// SYSTEM ZŁODZIEJA (Thief)
/////////////////////////////////////////////////////////


// Typy celów dla złodzieja (np. zamek, pułapka, NPC)
Table ThiefTargetType {
  id INT [pk, increment]
  name VARCHAR(50) [not null, unique] // "lock", "trap", "npc"
  description TEXT
}


// Konkretny cel do okradzenia/otwarcia/rozbrojenia
Table ThiefTarget {
  id INT [pk, increment]
  name VARCHAR(100) [not null]
  thief_target_type_id INT [not null, ref: > ThiefTargetType.id]
  required_thief_level INT [default: 0]
  difficulty INT [default: 1] // Wpływa na minigry
  // Można dodać warunki, pory dnia, wydarzenia podobnie jak w innych profesjach
}


Table ThiefTargetLoot {
  id INT [pk, increment]
  thief_target_id INT [not null, ref: > ThiefTarget.id]
  item_name VARCHAR(100) [not null]
  drop_chance DECIMAL(5,2) [default: 100.00]
}


Table ThiefLevelBonuses {
  id INT [pk, increment]
  min_level INT [not null]
  max_level INT [not null]
  dexterity_bonus INT [default: 0]
  intelligence_bonus INT [default: 0]
  luck_bonus INT [default: 0]
  charisma_bonus DECIMAL(5,2) [default: 0.00]
  thief_bonus INT [default: 0]
  pvp_physical_dmg_bonus DECIMAL(5,2) [default: 0.00]
  pvp_magical_dmg_bonus DECIMAL(5,2) [default: 0.00]
}


// Opcjonalnie umiejętności złodzieja
Table ThiefAbilities {
  id INT [pk, increment]
  name VARCHAR(100) [not null, unique]
  description TEXT
  required_thief_level INT [default: 0]
}


/////////////////////////////////////////////////////////
// SYSTEM Pisarza (Writer)
/////////////////////////////////////////////////////////
Table WriterLevelBonuses {
  id INT [pk, increment]
  min_level INT [not null]
  max_level INT [not null]


  // Bonusy
  luck_bonus INT [default: 0]
  charisma_bonus DECIMAL(5,2) [default: 0.00]
  writer_bonus INT [default: 0]
  pve_physical_dmg_bonus DECIMAL(5,2) [default: 0.00]
  pve_magical_dmg_bonus DECIMAL(5,2) [default: 0.00]
}


Table WriterRecipe {
  id INT [pk, increment]
  name VARCHAR(100) [not null, unique]   // np. "Zwykły Pergamin"
  difficulty INT [default: 1]           // 1=łatwa, 2=średnia, 3=trudna
  required_writer_level INT [default: 0] // minimalny poziom pisarza
  material_cost INT [default: 0]        // ilość materiałów
  recipe_type VARCHAR(50) [null]        // np. "pergamin", "ksiega", "scroll_enchant", ...
  product_item_id INT [null, ref: > Item.id] // - jeśli chcemy wskazać konkretny przedmiot
}


//System Alchemii


Table AlchemyLevelBonuses {
  id INT [pk, increment]
  min_level INT [not null]
  max_level INT [not null]


  // Bonusy co 5 poziomów
  intelligence_bonus INT [default: 0]
  physical_resistance_bonus DECIMAL(5,2) [default: 0.00]
  alchemy_bonus INT [default: 0]
  tenacity_bonus DECIMAL(5,2) [default: 0.00]
}


Table AlchemyRecipe {
  id INT [pk, increment]
  name VARCHAR(100) [not null, unique]   // np. "Mikstura Leczenia"
  difficulty INT [default: 1]           // 1=łatwa, 2=średnia, 3=trudna
  required_alchemy_level INT [default: 0] // minimalny poziom alchemii
  material_cost INT [default: 0]        // ile składników potrzeba
  recipe_type VARCHAR(50) [null]        // np. "mikstura", "maść", "oliwa"...
  product_item_id INT [null, ref: > Item.id] // jeśli chcemy wskazać konkretny przedmiot wynikowy
}


Table WeaponType {
  id INT [pk, increment]
  name VARCHAR(100) [not null, unique]
  description TEXT
}


Table Skill {
  id INT [pk, increment]
  class_id INT [not null, ref: > Class.id]
  weapon_type_id INT [null, ref: > WeaponType.id] // jeśli umiejętność zależy od broni
  name VARCHAR(100) [not null]
  description TEXT
   skill_type VARCHAR(50) [not null, default: 'Offensive'] // 'Offensive' lub 'Defensive'
}


Table Item {
  id INT [pk, increment]
  item_category_id INT [not null, ref: > ItemCategory.id]
  grade VARCHAR(50) [null]        // niektóre przedmioty mają grade (np. C, B, A, S...)
  lvl INT [null]                  // niektóre przedmioty (peleryny, pasy, koszule, brooch, itp.)
  name VARCHAR(100) [not null]
  type VARCHAR(100) [null]        // typ w obrębie kategorii, np. rodzaj broni, rodzaj runy
  weight DECIMAL(10,2) [default: 0.00]
  prize DECIMAL(10,2) [default: 0.00]
  remelting DECIMAL(10,2) [default: 0.00] // możliwość przetopienia itp.
  durations INT [null]            // dla niektórych przedmiotów jak potions, scrolls, runes, food
  // Nowa kolumna – tylko dla run (lub dowolnych przedmiotów),
  // określająca, ile energii dodaje do skilla
  energy_value INT [null]


  // NOWE kolumny dla run:
  element_type VARCHAR(50) [null] // np. "Fire", "Water", "Earth", "Wind", "Holy", "Dark"
  rune_degree INT [null]          // 1..10


  //Soul Crystal
  soul_crystal_level_required INT [null]   // np. 12?
  soul_crystal_stat VARCHAR(100) [null]    // "Strength", "Dexterity", ...
  soul_crystal_multiplier DECIMAL(5,2) [null]  
  is_powerful BOOL [default: false]
}


Table CharacterItem {
  id INT [pk, increment]
  character_id INT [not null, ref: > Character.id]
  item_id INT [not null, ref: > Item.id]
  quantity INT [default: 1]
}


Table ItemCategory {
  id INT [pk, increment]
  name VARCHAR(100) [not null, unique] // np. Weapon, Helmet, Chest, Pants, Boots, Gloves, Shield, Earring, Ring, Amulet, Cloak, Belt, Shirt, Brooch, Bracelet, Seed, ArtifactBook, SoulOrb, NobleGem, Talisman, Artifact, SoulOrbis, Skin, Relic, Potion, Scroll, Rune, Food, Material, Other
  description TEXT
}


Table Attribute {
  id INT [pk, increment]
  name VARCHAR(100) [not null, unique] // np. P.Atk, M.Atk, P.Def, M.Def, HP, MP, CP, Crit Rate, Crit Damage, Attack Speed, Casting Speed, Accuracy, Evasion, etc.
  description TEXT
  // Możemy w razie potrzeby dodać kolumny opisujące atrybut np. typ (fizyczny/magiczny), czy procentowy.
}


Table ItemAttributeValue {
  id INT [pk, increment]
  item_id INT [not null, ref: > Item.id]
  attribute_id INT [not null, ref: > Attribute.id]
  value DECIMAL(10,4) [default: 0.0000]
}


Table EnhancementType {
  id INT [pk, increment]
  name VARCHAR(100) [not null, unique] // np. evolution, enchanting, upgrading, augmentation, soul crystal, acumen, element system, personalisation statistic, Soul system
  description TEXT
}


Table ItemEnhancement {
  id INT [pk, increment]
  item_id INT [not null, ref: > Item.id]
  enhancement_type_id INT [not null, ref: > EnhancementType.id]


  // Dla upgradu wykorzystamy current_level do trzymania aktualnego +n
  current_level INT [default: 0]


  // Możemy dodać pole oznaczające czy przedmiot jest zablokowany przed dalszym ulepszeniem
  locked BOOL [default: false]
}


// Ta tabela przechowuje wszystkie typy materiałów do ulepszeń.
// Dla upgradu będą to kamienie z różnymi grade’ami i efektami.
// W przyszłości można dodać nowe typy materiałów do innych ulepszeń.
Table EnhancementMaterial {
  id INT [pk, increment]
  name VARCHAR(100) [not null, unique]   // nazwa kamienia/materialu
  enhancement_type_id INT [not null, ref: > EnhancementType.id] // Jaki typ ulepszenia wspiera ten materiał (np. upgrade)
  grade VARCHAR(50) [null] // D, C, B, A, S, Blessed S, X, itd.
 
  // Poniższe kolumny są szczególnie przydatne dla upgradu:
  success_chance_mod DECIMAL(5,2) [default: 0.00] // modyfikator szansy na success (np. +5% = 5.00)
  failure_penalty VARCHAR(100) [null] // np. 'decrease_level', 'no_penalty', 'destroy', itp.
  destroy_on_fail BOOL [default: false] // czy niszczy przedmiot przy porażce


  A_index INT [null] // Dodatkowa kolumna dla augmentacji, określająca indeks A kamienia
}


// Tabela rodzajów statystyk, które mogą być wzmacniane przez kryształ.
// Można dodać kolumnę "stat_group", by pogrupować statystyki, które się wzajemnie wykluczają.
Table AcumenStatType {
  id INT [pk, increment]
  name VARCHAR(100) [not null, unique] // np. "P. ATK bonus", "M. ATK bonus", "P. Skill Power bonus"
  stat_group VARCHAR(50) [null] // np. "atk_type", "skill_power_type", etc. - ułatwi logice blokowanie pewnych kombinacji
  description TEXT
}


// Kryształy przenikliwości należące do postaci.
// Każdy kryształ ma poziom (1-15).
// Można je przenosić między itemami, więc nie są trwale związane z przedmiotem.
Table CharacterAcumenCrystal {
  id INT [pk, increment]
  character_id INT [not null, ref: > Character.id]
  level INT [not null, default: 1] // poziom kryształu 1-15
  // W przyszłości można dodać kolumny typu nazwa kryształu, rodzaj kryształu, jeżeli będzie potrzeba.
}


// Powiązanie kryształu z przedmiotem i wybraną statystyką, którą wzmacnia.
// Limit 3 kryształów na przedmiot będzie kontrolowany logiką aplikacji.
// "Aktywowanie ulepszeń kryształem w pewnej grupie blokuje pozostałe" - logika w aplikacji sprawdzi stat_group.
Table CharacterItemAcumenCrystal {
  id INT [pk, increment]
  character_item_id INT [not null, ref: > CharacterItem.id]
  character_acumen_crystal_id INT [not null, ref: > CharacterAcumenCrystal.id]
  acumen_stat_type_id INT [not null, ref: > AcumenStatType.id]
 
  // Można dodać kolumnę indicating czy aktualnie aktywny, jeśli jest taki wymóg.
  // Na razie zakładamy, że obecność rekordu oznacza aktywację na tym itemie.
}


// Tabela przechowuje aktualny stan ewolucji danego egzemplarza przedmiotu.
// evolution_step (n) - rośnie wraz z każdym podniesieniem jakości lub przejściem na wyższy grade.
// current_grade - aktualny grade (D, C, B, A, S, Blessed S, X ...)
// current_quality - aktualna jakość (kiepska, zwykła, wspaniała, doskonała)
 
Table CharacterItemEvolution {
  id INT [pk, increment]
  character_item_id INT [not null, ref: > CharacterItem.id]
  evolution_step INT [default: 1]   // zaczynamy od 1 dla D kiepskiej jakości
  current_grade VARCHAR(50) [not null, default: 'D']
  current_quality VARCHAR(50) [not null, default: 'Kiepska']
}


// Przypisanie kamienia augmentacyjnego do danego przedmiotu u gracza.
// Przechowujemy informację o rerollach i ewentualnie o koszcie.
// current_reroll_cost może być liczony dynamicznie, ale można go też trzymać w bazie,
// jeśli chcemy zapamiętać stan między sesjami gracza.
Table CharacterItemAugmentation {
  id INT [pk, increment]
  character_item_id INT [not null, ref: > CharacterItem.id]
  enhancement_material_id INT [not null, ref: > EnhancementMaterial.id] // kamień augmentacyjny
  reroll_count INT [default: 0]
  current_reroll_cost DECIMAL(10,2) [default: 0.00]
}


// Bonusy wylosowane dla danej augmentacji.
// Każdy rekord to jeden bonus (atrybut) przypisany do augmentowanego przedmiotu.
// value wyliczane po stronie aplikacji, w oparciu o formuły i A_index z EnhancementMaterial.
// Przy rerollu usuwamy stare rekordy i dodajemy nowe.
Table CharacterItemAugmentationBonus {
  id INT [pk, increment]
  character_item_augmentation_id INT [not null, ref: > CharacterItemAugmentation.id]
  attribute_id INT [not null, ref: > Attribute.id]
  value DECIMAL(10,4) [default: 0.0000]
}


/////////////////////////////////////////////////////////
// SYSTEM TRENERA SKILLI
// 1) TRAINER NPC
/////////////////////////////////////////////////////////
// Każdy trener w grze - NPC, do którego idzie gracz, by trenować skill
// (można rozszerzyć o region mapy, quest line, itp.)


Table TrainerNPC {
  id INT [pk, increment]
  name VARCHAR(100) [not null] // "Master Eragon", "Legendary Berserker", etc.
  trainer_rank VARCHAR(50) [null] // np. "Basic", "Advanced", "Legendary"
  location_description TEXT // opis, gdzie się znajduje
}


/////////////////////////////////////////////////////////
// 2) TABELA ŁĄCZĄCA TRENERA Z KONKRETNYMI SKILLAMI
// w których może szkolić, i ewentualnym kosztem bazowym
/////////////////////////////////////////////////////////


Table TrainerNPCSkill {
  id INT [pk, increment]
  trainer_npc_id INT [not null, ref: > TrainerNPC.id]
  skill_id INT [not null, ref: > Skill.id]
 
  // Bazowy koszt w złocie za trening
  base_gold_cost DECIMAL(10,2) [default: 0.00]


  // max_mileston_supported to opcjonalna kolumna
  // jeżeli dany trener szkoli tylko do pewnego poziomu skillu.
  max_milestone_supported INT [null]
}


/////////////////////////////////////////////////////////
// 3) TABELA Z WZORCAMI RYSUNKÓW (MINIGIER)
/////////////////////////////////////////////////////////
// Każda klasa/skill może mieć przypisany kształt, który trzeba
// "narysować" w minigrze. Tabela ta ma związek ze skill_id
//


Table SkillMinigamePattern {
  id INT [pk, increment]
  skill_id INT [not null, ref: > Skill.id]
  pattern_name VARCHAR(100) [not null] // "Zygzak Berserkera", "Tarcza Rycerza" etc.
  pattern_description TEXT
  // Można dodać np. plik graficzny, w formie linku do zasobu
  pattern_graphic_path TEXT [null]
}


/////////////////////////////////////////////////////////
// 4) MILESTONES - DEFINIUJĄ KAMIENIE MILOWE ROZWOJU DANEG0 SKILLU
// (np. co 10 poziomów do 80, a potem 7 questowych, itp.)
/////////////////////////////////////////////////////////


Table SkillMilestone {
  id INT [pk, increment]
  skill_id INT [not null, ref: > Skill.id]
 
  milestone_level INT [not null] // np. 10, 20, 30...
  name VARCHAR(100) [null]       //Przykładowy efekt np. "Podbicie I", "Legendary V", itp.
  requirement_description TEXT    // opis wymagań (np. quest, księga, item)


  // Można dodać trainer_rank_required,
  // by definitywnie powiedzieć, czy do odblokowania milestone'u
  // potrzebny jest trener o ranku "Legendary".
  trainer_rank_required VARCHAR(50) [null]
}


/////////////////////////////////////////////////////////
// 5) STAN SKILLU U POSTACI - KTÓRY POZIOM (ORAZ ILE MILESTONE'ÓW)
/////////////////////////////////////////////////////////


Table CharacterSkill {
  id INT [pk, increment]
  character_id INT [not null, ref: > Character.id]
  skill_id INT [not null, ref: > Skill.id]
 
  // Reprezentuje "aktualny poziom" danej umiejętności.
  current_level INT [default: 0]
  current_energy INT [default: 0] // ile energii z run zebrano
  skill_points INT [default: 0]   // jeśli chcesz skill pointy


   // EWOLUCJA SKILLA: poziom ewolucji i licznik użyć
  evolution_level INT [default: 1]   // 1..100
  usage_experience INT [default: 0]  // bieżące "xp" z używania skilla


   // NOWE kolumny: enchant skilla
  enchant_level INT [default: 0]     // 0..30
  enchant_tome_type INT [null]       // 1=Novice, 2=Adept, 3=Master, 4=Archmage, 5=Legendary


   // NOWE pole do systemu skill tree:
  is_unlocked BOOL [default: false]
    // => false oznacza, że skill jest "niedostępny".
}




/////////////////////////////////////////////////////////
// 6) ZAAWANSOWANE ŚLEDZENIE MILESTONE'ÓW, JEŚLI CHCEMY WIEDZIEĆ,
// KTÓRE KAMIENIE MILOWE POSTAĆ UKOŃCZYŁA DLA DANEGO SKILLU
/////////////////////////////////////////////////////////


Table CharacterSkillMilestone {
  id INT [pk, increment]
  character_skill_id INT [not null, ref: > CharacterSkill.id]
  skill_milestone_id INT [not null, ref: > SkillMilestone.id]
 
  // flaga lub data potwierdzająca ukończenie milestone'u
  completed_at DATETIME [default: `CURRENT_TIMESTAMP`]
 
  // Można dodać info, jak ukończono milestone: quest, legendary book etc.
  completion_method VARCHAR(100) [null]
}




//System Peta


Table PetType {
  id INT [pk, increment]
  name VARCHAR(100) [not null, unique]  // np. Big Floppa
  description TEXT                      // opis roli peta, fabularny
  max_level INT [not null, default: 200] // maks poziom np. 200
}


Table PetLevelBonuses {
  id INT [pk, increment]
  pet_type_id INT [not null, ref: > PetType.id]


  // Zakres poziomów (min_level, max_level), lub "co 5 poziomów"
  min_level INT [not null]
  max_level INT [not null]


  // Bonusy, np. pAtk, mAtk, status, determination, domination, hpMp
  p_atk_bonus INT [default: 0]
  m_atk_bonus INT [default: 0]
  status_bonus INT [default: 0]
  determination_bonus INT [default: 0]
  domination_bonus INT [default: 0]
  hp_mp_bonus INT [default: 0]
}


Table CharacterPet {
  id INT [pk, increment]
  character_id INT [not null, ref: > Character.id]
  pet_type_id INT [not null, ref: > PetType.id]


  current_level INT [default: 1]
  current_experience INT [default: 0]
  // ewentualnie jeśli chcemy imie dla zwierzątka
  pet_name VARCHAR(100) [null]
  //jesli gracz moze miec wiele zwierzatek decydujemy
  //ktore jest aktywne
  is_active BOOL [default: false]


  // Potencjalnie: date_of_birth jak chcemy bardziej
  //zzyc gracza ze zwierzatkiem
}


Table PetSkill {
  id INT [pk, increment]
  pet_type_id INT [not null, ref: > PetType.id]
  name VARCHAR(100) [not null]
  description TEXT
  // ewentualnie "skill_level", "cooldown", "mana_cost", itp.
}


Table CharacterPetSkill {
  id INT [pk, increment]
  character_pet_id INT [not null, ref: > CharacterPet.id]
  pet_skill_id INT [not null, ref: > PetSkill.id]
  skill_level INT [default: 0] // 0..50 (według pseudokodu)
  // ewentualnie is_unlocked BOOL [default: false], itp.
}


Table CharacterPetGear {
  id INT [pk, increment]
  character_pet_id INT [not null, ref: > CharacterPet.id]
  item_id INT [not null, ref: > Item.id]
 
  // np. slot_name: "collar_slot", "rune_slot", "astral_artifact_slot"
  slot_name VARCHAR(50) [not null]
}


Table CharacterItemRune {
  id INT [pk, increment]
  target_item_id INT [not null, ref: > CharacterItem.id]   // Miecz, Zbroja, Pierścień
  rune_item_id INT [not null, ref: > CharacterItem.id]     // Konkretny egzemplarz runy
  inserted_at DATETIME [default: `CURRENT_TIMESTAMP`]
}


Table CharacterPetRune {
  id INT [pk, increment]
  character_pet_id INT [not null, ref: > CharacterPet.id]
  rune_item_id INT [not null, ref: > CharacterItem.id]
  current_level INT [default: 0]
}


Table SkillPrerequisite {
  id INT [pk, increment]
  skill_id INT [not null, ref: > Skill.id]
  prerequisite_skill_id INT [not null, ref: > Skill.id]
  required_level INT [default: 1] // opcjonalnie, jeśli wymagamy jakiegoś poziomu skillu
}


Table CharacterItemPersonalizedStat {
  id INT [pk, increment]
  character_item_id INT [not null, ref: > CharacterItem.id]
  attribute_id INT [not null, ref: > Attribute.id]  // Miejsce StatType zastępuje Attribute.id
  stack_count INT [default: 1]
}




//Soul Crystal


Table CharacterItemSoulCrystal {
  id INT [pk, increment]


  // docelowy item, do którego wkładamy SoulCrystal
  target_item_id INT [not null, ref: > CharacterItem.id]


  // egzemplarz soul crystala (który gracz ma w ekwipunku, item_category='SoulCrystal')
  soul_crystal_item_id INT [not null, ref: > CharacterItem.id]


  // poziom – 1..12
  current_level INT [default: 1]


  inserted_at DATETIME [default: `CURRENT_TIMESTAMP`]
}




//System Craftingu


Table CraftingProfession {
  id INT [pk, increment]
  name VARCHAR(100) [not null, unique] // "Kowalstwo", "Szwactwo", "Zlotnictwo", ...
  description TEXT
  // np. kategoria: "Metalwork", "Textile", "Jewelry", ...
  category VARCHAR(50) [null]
}


Table CharacterCraftingProfession {
  id INT [pk, increment]
  character_id INT [not null, ref: > Character.id]
  crafting_profession_id INT [not null, ref: > CraftingProfession.id]


  current_level INT [default: 1]        // 1..100
  current_experience INT [default: 0]   // rośnie wraz z minigrami
  // ewentualnie "is_completed BOOL" - czy osiągnięto 75+ i ukończono finalny test
}


Table CraftingRecipe {
  id INT [pk, increment]
  crafting_profession_id INT [not null, ref: > CraftingProfession.id]
 
  name VARCHAR(100) [not null]        //nazwa
  required_level INT [default: 1]      // minimalny poziom w tej profesji
  result_item_id INT [not null, ref: > Item.id]
  // Wskazuje, jaki przedmiot powstanie (jeśli w systemie itemów)
 
  // ewentualnie: time_to_craft INT, success_chance DECIMAL(5,2), etc.
  // opis TEXT
}


Table CraftingRecipeMaterial {
  id INT [pk, increment]
  crafting_recipe_id INT [not null, ref: > CraftingRecipe.id]
  item_id INT [not null, ref: > Item.id]
  quantity INT [default: 1]
}

