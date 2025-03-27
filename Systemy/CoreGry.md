# Core gry

## System Zarządzania Stanem Gry (Game State Management)

**Opis:**

- Centralny system kontrolujący stan gry, przechowujący informacje o postępach gracza, stanie poziomów, ustawieniach globalnych itp.

**Implementacja:**

- **C++:** Stwórz klasę pochodną od `UGameInstance`, która będzie przechowywać globalne dane gry.
- **Blueprints:** Użyj Blueprintów do zarządzania logiką specyficzną dla poziomu lub UI.
- **Najlepsze Praktyki:**
  - Używaj **Singletonów** ostrożnie, preferując `GameInstance` do przechowywania globalnego stanu.
  - Zadbaj o **serializację** stanu gry dla funkcji zapisu/odczytu.

## System Wejścia (Input System)

**Opis:**

- Centralne zarządzanie wejściem od użytkownika (klawiatura, mysz, gamepad), mapowanie akcji i osi.

**Implementacja:**

- **C++:** Definiuj akcje i osie wejścia w plikach konfiguracyjnych i obsługuj je w klasach C++.
- **Blueprints:** Łącz zdarzenia wejścia z logiką gry w Blueprintach.
- **Najlepsze Praktyki:**
  - Użyj **Input Mapping Contexts** z Unreal Engine 5, aby łatwo zarządzać różnymi schematami sterowania.
  - Wspieraj **remapowanie klawiszy** przez użytkownika.

## System Komponentów Podmiotu (Entity Component System - ECS)

**Opis:**

- Modularne podejście do tworzenia obiektów gry poprzez łączenie komponentów o różnych funkcjach.

**Implementacja:**

- **C++:** Twórz klasy komponentów dziedziczące po `UActorComponent` lub `USceneComponent`.
- **Blueprints:** Twórz niestandardowe komponenty w Blueprintach dla specyficznej logiki.
- **Najlepsze Praktyki:**
  - Wykorzystuj **kompozycję** zamiast dziedziczenia tam, gdzie to możliwe.
  - Projektuj komponenty tak, aby były **samodzielne** i **wielokrotnego użytku**.

## System Zdarzeń i Komunikacji (Event and Messaging System)

**Opis:**

- Mechanizm pozwalający na komunikację między różnymi częściami gry w sposób luźno powiązany.

**Implementacja:**

- **C++:** Wykorzystaj **delegaty** i **multi-cast delegates** do obsługi zdarzeń.
- **Blueprints:** Używaj Event Dispatchers do komunikacji między Blueprintami.
- **Najlepsze Praktyki:**
  - Unikaj ścisłego powiązania między obiektami; używaj wzorca **Observer**.
  - Zapewnij **asynchroniczność** tam, gdzie jest to konieczne.

## System Zapisu i Odczytu Gry (Save/Load System)

**Opis:**

- Mechanizm pozwalający na zapisywanie stanu gry i jego późniejsze odtworzenie.

**Implementacja:**

- **C++:** Twórz klasy pochodne od `USaveGame` i implementuj serializację w C++.
- **Blueprints:** Używaj funkcji Blueprintów do zapisu i odczytu danych gry.
- **Najlepsze Praktyki:**
  - Zdefiniuj **format danych** do przechowywania stanu gry.
  - Zadbaj o **kompatybilność wsteczną** przy aktualizacjach gry.

## System Zarządzania Zasobami (Asset Management)

**Opis:**

- Centralne zarządzanie zasobami gry, takimi jak modele, tekstury, dźwięki.

**Implementacja:**

- **C++:** Użyj `TSoftObjectPtr` i `TSoftClassPtr` do odwoływania się do zasobów w sposób leniwy.
- **Blueprints:** Wykorzystaj **Primary Asset Labels** do grupowania zasobów.
- **Najlepsze Praktyki:**
  - Stosuj **Asset Manager** do ładowania zasobów w locie.
  - Organizuj zasoby w **folderach** i stosuj konwencje nazewnictwa.

## System Statystyk i Atrybutów (Attribute System)

**Opis:**

- Centralny system zarządzający statystykami postaci, wrogów i przedmiotów.

**Implementacja:**

- **C++:** Zaimplementuj **Gameplay Ability System (GAS)** dostępny w Unreal Engine 5.
- **Blueprints:** Użyj Blueprintów do tworzenia konkretnych umiejętności i efektów.
- **Najlepsze Praktyki:**
  - Wykorzystaj **Data Assets** do przechowywania danych statystyk.
  - Projektuj system w sposób **danych napędzanych** (data-driven).

## System AI i Sztucznej Inteligencji

**Opis:**

- Podstawowy system zarządzający zachowaniem wrogów i NPC.

**Implementacja:**

- **C++:** Twórz klasy AI Controllerów i zachowań w C++ dla wydajności.
- **Blueprints:** Wykorzystaj **Behavior Trees** i **Blackboards** do definiowania logiki AI.
- **Najlepsze Praktyki:**
  - Stosuj **wzorce projektowe** takie jak **State** czy **Strategy**.
  - Optymalizuj wydajność poprzez **asynchroniczne przetwarzanie**.

## System Fizyki i Kolizji

**Opis:**

- Odpowiada za realistyczne zachowanie obiektów i wykrywanie kolizji.

**Implementacja:**

- **C++:** Dostosuj ustawienia fizyki i kolizji dla specyficznych potrzeb.
- **Blueprints:** Używaj Blueprintów do prostych interakcji fizycznych.
- **Najlepsze Praktyki:**
  - Optymalizuj **kanały kolizji** i **profili obiektów**.
  - Unikaj nadmiernego użycia **szkieletów fizycznych** tam, gdzie nie jest to konieczne.

## System Animacji

**Opis:**

- Zarządza animacjami postaci, w tym przejściami, blendowaniem i kontrolerami animacji.

**Implementacja:**

- **C++:** Twórz **Anim Instance** i **Anim Notifies** w C++ dla złożonych logik.
- **Blueprints:** Używaj **Animation Blueprints** do tworzenia grafów animacji.
- **Najlepsze Praktyki:**
  - Wykorzystaj **Animation Montages** dla akcji takich jak ataki.
  - Optymalizuj animacje poprzez **Root Motion** tam, gdzie to konieczne.

## System Interfejsu Użytkownika (UI Framework)

**Opis:**

- Zarządza interfejsem użytkownika, w tym HUD, menu, oknami dialogowymi.

**Implementacja:**

- **C++:** Twórz podstawowe klasy UI w C++, dziedzicząc po `UUserWidget`.
- **Blueprints:** Projektuj interfejsy w **UMG (Unreal Motion Graphics)**.
- **Najlepsze Praktyki:**
  - Używaj wzorca **Model-View-Controller (MVC)** lub **Model-View-ViewModel (MVVM)**.
  - Zapewnij **responsywność** interfejsu na różnych rozdzielczościach.

## System Sieciowy i Replikacja (Networking and Replication)

**Opis:**

- Obsługuje funkcje wieloosobowe, synchronizację stanu gry między klientami i serwerem.

**Implementacja:**

- **C++:** Implementuj funkcje sieciowe z użyciem **RPC (Remote Procedure Calls)**.
- **Blueprints:** Oznacz funkcje jako **Replicated** lub **Server/Client** w Blueprintach.
- **Najlepsze Praktyki:**
  - Minimalizuj ilość danych przesyłanych przez sieć.
  - Używaj **Prediction and Reconciliation** dla płynności gry.

## System Zarządzania Danymi (Data Management System)

**Opis:**

- Centralne zarządzanie danymi gry, takimi jak konfiguracje, tabele statystyk, zasoby tekstowe.

**Implementacja:**

- **C++:** Użyj **Data Tables** i **Structs** do definiowania danych.
- **Blueprints:** Ładuj i wykorzystuj dane w Blueprintach.
- **Najlepsze Praktyki:**
  - Stosuj **dane napędzane** podejście, umożliwiające łatwą aktualizację bez zmiany kodu.
  - Organizuj dane w sposób modularny i łatwy do zarządzania.

## System Lokalizacji (Localization System)

**Opis:**

- Umożliwia wsparcie dla wielu języków i kultur.

**Implementacja:**

- **C++ i Blueprints:** Wykorzystaj wbudowany system lokalizacji Unreal Engine.
- **Najlepsze Praktyki:**
  - Używaj **Text Localization Archives** do przechowywania tłumaczeń.
  - Unikaj hardcodowania tekstów w kodzie; używaj `FText` zamiast `FString`.

## System Logowania i Diagnostyki

**Opis:**

- Umożliwia śledzenie zdarzeń, błędów i wydajności gry.

**Implementacja:**

- **C++:** Użyj makr takich jak `UE_LOG` do logowania informacji.
- **Najlepsze Praktyki:**
  - Stosuj różne poziomy logowania: Display, Warning, Error.
  - Zadbaj o czytelność i spójność komunikatów logowania.

## Wykorzystanie Wzorca Projektowego Model-View-Controller (MVC)

**Opis:**

- Struktura ułatwiająca separację logiki biznesowej od prezentacji.

**Implementacja:**

- **C++ i Blueprints:** Podziel kod na modele (dane), widoki (UI) i kontrolery (logika).
- **Najlepsze Praktyki:**
  - Ułatwia testowanie i utrzymanie kodu.
  - Zapewnia skalowalność projektu.

## Zastosowanie Nowoczesnych Technik Programowania w C++

**Opis:**

- Wykorzystanie najnowszych standardów C++ (C++17/C++20) i najlepszych praktyk.

**Implementacja:**

- **C++:**
  - Używaj **smart pointers** (`TSharedPtr`, `TWeakPtr`) zamiast surowych wskaźników.
  - Stosuj **constexpr**, **auto**, **lambda expressions** dla czytelności i efektywności.
- **Najlepsze Praktyki:**
  - Unikaj **circular dependencies**.
  - Przestrzegaj **zasad SOLID** w projektowaniu kodu.

## Integracja z Systemem Build (Unreal Build System)

**Opis:**

- Zapewnienie poprawnej konfiguracji projektu, modułów i zależności.

**Implementacja:**

- **C++:** Konfiguruj pliki `.Build.cs` i `.Target.cs`.
- **Najlepsze Praktyki:**
  - Dziel projekt na **moduły** dla lepszej organizacji.
  - Używaj **Precompiled Headers (PCH)** do przyspieszenia kompilacji.

## System Testowania i Debugowania

**Opis:**

- Mechanizmy pozwalające na testowanie jednostkowe i integracyjne.

**Implementacja:**

- **C++:** Użyj **Functional Testing Framework** w Unreal Engine.
- **Najlepsze Praktyki:**
  - Pisanie **testów jednostkowych** dla krytycznych komponentów.
  - Wykorzystanie **Profilera** do optymalizacji wydajności.

## Dokumentacja i Standardy Kodowania

**Opis:**

- Utrzymanie spójności kodu i ułatwienie współpracy w zespole.

**Implementacja:**

- **C++ i Blueprints:** Stosuj konwencje nazewnictwa zgodne z **Unreal Coding Standard**.
- **Najlepsze Praktyki:**
  - Dokumentuj kod za pomocą komentarzy i narzędzi takich jak **Doxygen**.
  - Używaj **systemu kontroli wersji** (np. Git) z odpowiednimi praktykami commitowania.

## Planowanie Skalowalności i Rozszerzalności

**Opis:**

- Przygotowanie projektu na przyszłe rozszerzenia i zmiany.

**Implementacja:**

- **C++ i Blueprints:**
  - Projektuj kod w sposób **modularny**.
  - Wykorzystuj **interfejsy** (`UInterface`) do definiowania kontraktów między komponentami.
- **Najlepsze Praktyki:**
  - Zastosuj **wzorce projektowe** takie jak **Factory**, **Observer**, **Command**.
  - Unikaj **hardcodowania** wartości; używaj konfiguracji i danych zewnętrznych.

## Wsparcie dla Wieloplatformowości

**Opis:**

- Przygotowanie gry do działania na różnych platformach (PC, konsole, urządzenia mobilne).

**Implementacja:**

- **C++:** Używaj preprocesorów do warunkowego kompilowania kodu dla różnych platform.
- **Najlepsze Praktyki:**
  - Unikaj używania platformowo specyficznych funkcji, jeśli to możliwe.
  - Testuj grę na docelowych platformach od wczesnych etapów.

## Bezpieczeństwo i Optymalizacja

**Opis:**

- Zapewnienie stabilności, bezpieczeństwa i optymalnej wydajności gry.

**Implementacja:**

- **C++:**
  - Zabezpiecz kod przed **wyciekami pamięci**.
  - Optymalizuj **alokacje pamięci** i **zarządzanie zasobami**.
- **Najlepsze Praktyki:**
  - Regularnie profiluj grę pod kątem wydajności.
  - Używaj **mechanizmów zabezpieczeń** Unreal Engine, takich jak **Sanity Checks**.

## Integracja z Narzędziami Zewnętrznymi

**Opis:**

- Wykorzystanie narzędzi do analizy, monitorowania, czy zarządzania treścią.

**Implementacja:**

- **C++ i Blueprints:**
  - Integruj **systemy analityczne** (np. statystyki graczy).
  - Używaj **pluginów** do dodatkowych funkcji.
- **Najlepsze Praktyki:**
  - Upewnij się, że integracje są **modularne** i łatwe do aktualizacji.

## System Aktualizacji i Wersjonowania

**Opis:**

- Mechanizmy pozwalające na łatwe aktualizowanie gry i zarządzanie wersjami.

**Implementacja:**

- **C++:** Implementuj system wersjonowania zasobów i kodu.
- **Najlepsze Praktyki:**
  - Używaj **systemów ciągłej integracji** (CI/CD) do automatyzacji buildów.
  - Dokumentuj zmiany między wersjami.
