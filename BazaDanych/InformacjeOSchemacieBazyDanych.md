# Informacje o Schemacie Bazy Danych

Poniższy dokument ma na celu przybliżenie czytelnikowi tabel składających się na bazę danych gry. Należy traktować go jako uzupełnienie dla pliku ilustrującego właściwy schemat.

- Tabela **User** ma na celu przechowywanie informacji o graczu. Z racji, iż w żadnym z współcześnie istniejących plików nie istnieje wspomnienie o tym elemencie, w kolumnach znajdują się typowe dla gier sieciowych pola. Uznałem istnieje tej tabeli za ważne, albowiem w założeniach przewidywany jest również model sieciowy.

- Z graczem nieodzownie związana jest jego postać. Można również rzecz, iż jest to jedna z najważniejszych tabel, albowiem to do niej ‘przyspawane’ są wszelkiej maści atrybuty, statystyki i inne zabawy. Istnienie tabeli **Character** można uznawać za pewien punkt wejścia dla właściwego zrozumienia wszelkich systemów rządzących grą.

- Po konsultacji z Panem Janem Biesiadą zdecydowałem się na podział statystyk tworzących nasz core na trzy odrębne kategorie: statystyki ofensywne, statystyki defensywne oraz inne tworzące następujące tabele: **OffensiveStats**, **DefensiveStats** oraz **OtherStats**. Podział ten nie odzwierciedla tego co jest w pliku opisowym, jednakże ma on znaczący sens w kwestii schematu, do czego postaram się Państwo przekonać. Po pierwsze zachowanie tak daleko idącej fragmentacji powoduje że schemat już na etapie rozważań pojedynczego pliku stawał się nieczytelny i trudny do analizy, nawet dla osoby obeznanej w teoretycznym wymiarze naszego projektu. Byłoby to więc sprzeczne z postawionym założeniem, aby schemat był pomocny w rozumieniu, nie zaś je utrudniał. Idąc dalej pracując z tak zbudowaną bazą danych musielibyśmy mierzyć się z licznymi konsekwencjami jak konieczność budowania złożonych zapytań z wieloma JOIN’ami, aby wyciągnąć potrzebną informację, czy też narażalibyśmy się na istnienie wielu wartości NULL. Wierzę więc że moje rozwiązanie pomaga tego uniknąć i jest logiczne w sensie interakcji w grze. W kodzie schematu uwzględniłem również komentarze, które pomogą w ewentualnym ugruntowaniu go w pliku teoretycznym.

- Ten punkt traktuje o systemie profesji w grze rozpoczynając od rozważań teoretycznych i przechodząc do kwestii praktycznych. Jak zapewne zdążyli już Państwo zauważyć są to systemy proste koncepcyjnie w rozumieniu całościowym oraz podobne do siebie, jednakże są one w istocie złożone jeśli rozważymy szczegóły implementacyjne. W przypadku systemu wędkarza chociażby należy przechowywać gdzieś informacje o rybach, przynętach, lokacjach i innych, co oznacza iż każda nowa profesja powoduje znaczące rozrośnięcie się schematu. Mój pomysł na to jest następujący:

  - Tabela **Profession** jest tabelą, która będzie przechowywać informacje o danej profesji np. wędkarza, zielarza, złodzieja.
  - Tabela **CharacterProfession** łączy postać z profesją i przechowuje informacje o levelu jaką gracz ma w danej profesji wraz z exp, aby łatwo można było kontrolować jego postępy.
  - Tabela **Fish** przechowuje informacje o rybach istniejących w świecie gry, ich nazwę, rzadkość i inne istotne z punktu widzenia gry.
  - Tabela **FishingSpot** opisuje konkretne miejsca gdzie można łowić ryby, punkt ten związany jest z wypracowanym przez nas wspólnie wnioskiem.
  - Tabela **Bait** przechowuje informacje o przynętach.
  - Tabela **FishAvailability** to tabela pomocnicza, która ułatwia ustalenie warunków do złowienia danej ryby. W istocie łączy ona więc rybę z miejscem, przynętą, czasem i innymi czynnikami, aby ustalić naszą szansę na udany połów.
  - Tabela **FishLoot** opisuje jakie przedmioty możemy uzyskać z danej ryby. Możliwe, że w tym momencie zastanawiają się Państwo dlaczego by nie połączyć tego z tabelą Fish. Powód takiej decyzji jest prosty, a mianowicie jedna ryba może dropić wiele przedmiotów, więc mamy tu do czynienia z zależnością jeden do wielu. Jest to więc kwestia normalizacji bazy danych.
  - Tabela **FishingLevelBonuses** oraz jej odpowiedniki w innych profesjach są tabelami pomocniczymi, które mają na celu pomóc w balansowaniu gry. Gdyby w kodzie gry zaimplementować na sztywno, że chociażby na 5 poziomie wędkarstwa otrzymuje się 1 dexterity, można tu elastycznie definiować, dla jakich zakresów poziomów obowiązują dane bonusy. W naszych systemach istnieje naprawdę wiele mechanik, które na siebie wpływają, więc uważam to za dobre, jeśli istnieje możliwość by łatwo konfigurować jak i w jakim stopniu to działa.

  Poszczególne profesje są do siebie w wielu aspektach podobne, więc pozwolę sobie nie wyjaśniać już szczegółowo czym są tabele typu Herb i jej podobne. Skupimy się za to na tabelach, które się w jakiś sposób wyróżniają. W razie niejasności kod schematu bazy danych również posiada komentarze, które mogą pomóc.

  - Tabela **ThiefTargetLoot** określa jakie przedmioty można zdobyć z określonego celu.
  - Tabela **ThiefAbilities** jest związana z propozycją, by wprowadzić system umiejętności dla złodzieja.
  Na końcu zajmijmy się systemem pisarza. Może on ulec zmianie w przyszłości zgodnie z ustaleniami, jednakże zrobiłem dla niego już schemat dla spójności. Tabela **WriterLevelBonuses** jest analogiczna do innych związanych z systemem profesji. Opisuje ona po prostu bonusy jakie gracz otrzymuje wraz z pewnym poziomem.
  - Tabela **WriterRecipe** służy do trzymania w bazie danych informacji o konkretnych „przepisach” (rodzajach rzeczy, jakie pisarz potrafi stworzyć).

Przejdźmy do systemu alchemii. Jego zasady są dość intuicyjne i podobne do tych, które można zaobserwować w innych grach. Jest to również część systemu profesji, który w dużej mierze jest już zaimplementowany (patrz opis wyżej). Dodajemy zgodnie z implementacją innych profesji tabelę **AlchemyLevelBonuses**, by śledzić to że co 5 poziomów ulepszane są dane statystyki. Dajemy również podobnie jak w systemie pisarza odwzorowanie przepisów na dane mikstury w tabeli **AlchemyRecipe**.

- W tym punkcie rozważymy kwestie związane ze skillami istniejących w świecie gry oraz ich integracją ze schematem. Plik skille gry jest jednym z najważniejszych, ponieważ odnosi się on do tak zwanego coru. Dodatkowo posiada on informacje nie tylko o skillach, ale i również o klasach, co oznacza, że gracz będzie miał styczność z tymi mechanikami już od początku swojej przygody. Kwestia integracji ze schematem nie jest jednak w tym przypadku trudna i sprowadza się jedynie do kilku nowych tabel i niewielkich modyfikacji już istniejących. Tak oto do tabeli Character doszło **class_id**, ponieważ każda postać ma swoją klasę. Nowe tabele to **Class** opisująca klasy postaci, **WeaponType**, ponieważ chociażby w przypadku Berserkera jego skille zależą od broni, oraz tabela **Skill** przechowująca informacje o skillach.

- Kolejną kluczową kwestią są przedmioty w świecie gry. To ponownie rzecz ściśle związana z corem i taka z którą gracz ma styczność od początku. Dodatkowo tabela ta jest istotna w tym sensie, iż nie da się bez niej zrobić części innych mechanik w świecie gry, albowiem wiele z nich zależy od przedmiotów. Jednocześnie jest to plik trudny do przetworzenia, jeżeli więc popełnie jakiekolwiek błędy, bądź ktoś z teamu będzie mieć jakieś uwagi to z chęcią je przyjmę. Mój pomysł jest następujący:

  - Tabela **Item** będzie przechowywać podstawowe informacje o przedmiocie, czyli np. jego waga, kategoria.
  - Tabela **ItemCategory** będzie kategoryzować przedmioty podobnie jest jest to w pliku, czyli np. hełmy, skrzydła i inne brudasy.
  - Przedmioty powiązane są z różnymi atrybutami i jest tego bardzo dużo. Moje rozwiązanie jest więc takie że tworzę tabelę **Attribute** która będzie przechowywać rodzaj atrybutu oraz tabelę **ItemAttributeValue**, która będzie łączyć przedmiot z wartością atrybutu.  
  - Tabela **EnhancementType** tworzy podwaliny pod systemy takie jak Acumen, Soul Crystal, upgrading i inne tego typu.
  - Tabela **ItemEnhancement** będzie łączyć przedmiot z jego ulepszeniem.
  - Tabela **CharacterItem** łączy gracza z jego przedmiotami; mowa tu o konkretnych instancjach danego przedmiotu, którą posiada gracz.

- Skoro mamy już podwaliny pod system ulepszeń przedmiotów zajmijmy się tym teraz. Zacznijmy od pliku pierwszego od góry czyli Upgrading.docx. Postaramy się przy tym zrobić elastyczny schemat, aby stworzyć spójny system z innymi systemami ulepszeń.
  - Tabela **EnhancementMaterial** będzie zawierać informacje o materiałach potrzebnych do ulepszeń w przypadku systemu upgrading będą to kamyczki.

- Przejdźmy do pliku Acumen.

  - Tabela **AcumenStatType** to tabela statystyk, które mogą być wzmacniane przez kryształ (obliczenia będą po stronie serwera)
  - Tabela **CharacterAcumenCrystal** przechowuje kryształy należące do postaci
  - Tabela **CharacterItemAcumenCrystal** łączy kryształ z przedmiotek i wybraną statystyką

- Plik Enchantowanie jest już zintegrowany ze schematem dzięki wcześniejszemu zamysłowi by stworzyć ten schemat elastycznym.

- Plik EvolutionItems działa nieco inaczej od poprzednich, dlatego też uważam iż lepszym rozwiązaniem jest stworzeniem osobnej tabeli, która będzie obsługiwać ten system.
  - **CharacterItemEvolution** będzie przechowywać aktualny stan ewolucji dla danego egzemplarza przedmiotu.

- Plik Augmentacja kontynuuje opis mechanik służących do ulepszania przedmiotów. Część jego założeń możemy zintegrować z istniejącym schematem np. Augmantation to będzie nowy Enhancement Type. Dodane zostaną dwie tabele **CharacterItemAugmentation** i **CharacterItemAugmentationBonus**. Rolą pierwszej będzie przypisanie kamienia do przedmiotu gracza, drugiej zaś przechowywanie bonusów wylosowanych dla danej augmentacji.

- System trenera skilli zakłada, że każda postać ma swoje umiejętności, które posiadają poszczególne stopnie rozwoju, aby je rozwijać należy odwiedzić trenerów skilli. Tabela **TrainerNPC** przechowuje informacje o trenerach w świecie gry. Tabela **TrainerNPCSkill** łączy trenera z poszczególnymi skillami definiując jakie skille dany trener potrafi szkolić i jaki jest tego koszt. **SkillMinigamePattern** zawiera definicje kształtów, które mogą być opisowe bądź w formie plików graficznych. Obecnie tabela ta połączona jest z tabelą skill, ale jeśli będzie taka potrzeba można ją łatwo rozszerzyć powiązując ją również chociażby z klasą. **SkillMilestone** opisuje wszystkie kamienie milowe dla danego skilla. Pozwala to określać jakieś specjalne efekty, które zyskuje skill po osiągnięciu wybranego poziomu. CharacterSkill przechowuje aktualny poziom skillu. Np. current_level = 6 oznacza, że postać ma skill na 6. poziomie. **CharacterSkillMilestone** to tabela pomocnicza, służy do zaznaczenia, że dana postać (i jej umiejętność) osiągnęła konkretny kamień milowy. Dzięki temu wiemy, czy wszystkie warunki zostały spełnione i kiedy. Może być ona też fajnym dodatkiem w trybie online, aby powiadomić innych graczy na serwerze o czyimś postępie.

- System podbijania skilli to kolejny sposób ulepszania naszych umiejętności tym razem za pomocą run. Nie chciałbym tworzyć już nowych tabel, które by to wszystko przechowywały, więc podjąłem próbę integracji tego z istniejącym już systemem przedmiotów. W praktyce do tabeli z przedmiotami dodałem opcjonalną wartość energii, którą runa będzie dodawała do skilli i nieco zmieniłem tabelę wiążącą gracza ze skillem.

- Pet to fajny system bo można mieć zwierzątko typu floppa, które nam pomaga. Celem jest umożliwienie:
  - Posiadania Peta przez gracza (Character) – wraz z informacją o jego poziomie i doświadczeniu.
  - Różnorodności rodzajów Petów (np. Big Floppa).
  - Bonusów zależnych od poziomu (co 5 poziomów) – analogicznie do FishingLevelBonuses czy WriterLevelBonuses.
  - Możliwości rozbudowy w przyszłości o:
    - Specjalne „astralne przedmioty” (pet gear, pet runes),
    - Umiejętności peta,
    - Ewentualny system questów do zdobycia peta, itd.
  - Tabela **PetType** będzie przechowywać informacje o typie zwierzątka. **PetLevelBonuses** będzie określało bonusy jakie daje nam zwierzątko. **CharacterPet** będzie wiązać postać ze zwierzątkiem. Tabela **PetSkill** związana jest z informacją w pliku, że zwierzątko posiada umiejętności, które będą nas wzmacniać. Jest ona dość ogólna, bo o systemie jest mało informacji, w schemacie jednak zawarłem podstawowe kolumny i sugestie jak to dalej rozwinąć. **CharacterPetSkill** po prostu wiąże skill z konkretnym zwierzątkiem gracza. Tabela **CharacterPetGear** będzie przechowywać przedmioty naszego zwierzątka np. te astralne. Właściwe przedmioty będą przechowywane jak inne itemki.

- System ewolucji skilli jest systemem bardzo prostym i intuicyjnym, bo po prostu tym częściej używamy danego skilla tym on jest silniejszy (widzieli to Państwo pewnie w wielu innych grach tego typu). Z racji, że mamy już odpowiednie tabele określające nasze skille i ich poziom wystarczy rozbudować istniejącą już tabelę o dodatkowe kolumny. Mogą Państwo się zapoznać z tym we właściwym schemacie.

- Nie wiem czy to jakoś pomoże, ale dla mnie system enchantowania skilli przypomina trochę sytuację z my hero academia, że główny bohater niezbyt potrafił kontrolować swoją moc to używając jej łamał sobie kości. Ogólnie znacząca część tego pliku skupia się raczej na wyróżnieniu jakoś tego systemu, a mało jest tam konkretnych informacji. Mój pomysł na implementację tego w bazie danych jest taki, by ponownie rozwinąć tabelę **CharacterSkill** o dodatkowe kolumny. Sugerując się tym jak działa to w pseudokodzie takie rozwiązanie powinno wystarczyć, jeśli ktoś z was uważa inaczej to poprawię.

- Przejdźmy do systemu elementów. To kolejny z tysiąca innych systemów, które mają wzmacniać nasze itemki. Wcześniej by choć trochę uprościć tej schemat zdecydowałem by runy były przechowywane w tabeli Items i tu chciałbym to podejście kontynuować. Dodam więc kolejne kolumny, by przechowywać informacje dla run. Do tego dojdzie tabela **CharacterItemRune**, która będzie tabelą pośredniczącą, czyli wiążącą runę z przedmiotem.

- Przejdźmy do systemu drzewek umiejętności, co prawda niezbyt wiem co to Titan Quest na czym jest on wzorowany, jednakże założenia nie są mi obce. By go obsłużyć oprócz modyfikacji już istniejących tabel dodamy parę nowych. **SkillPrerequisite** będzie określać zależność jakie skille muszą być wcześniej odblokowane, by gracz mógł skorzystać z nowej umiejętności.

- Przejdźmy do systemu personalizacji statystyk. Mamy już tabele **Item**, **CharacterItem** i **CharacterItemEvolution**, teraz chcemy uwzględnić jeszcze statystyki związane z personalizacją. W praktyce to można zapisać jako że dany przedmiot ma wybraną statystykę wystackowaną daną liczbę razy (zgodnie z opisem: Co ciekawe możemy wybierać statystyki wielokrotnie te same nie ma żadnej reguły). Tworzymy więc nową tabelę **CharacterItemPersonalizedStat**, która będzie tabelą pośrednią, która to wszystko łączy.

- Dla zachowania spójności z runami, soul crystals również będę traktował jako itemy. Tworzę dodatkową tabelę **CharacterItemSoulCrystal**, by łączyć soul crystal z itemkiem oraz lekko modyfikuję tabelę Item.

- Ostatnim systemem do rozważenia jest system craftowania, jest to jednocześnie system bardzo złożony, dlatego poświęcimy mu więcej uwagi. W pliku mamy wymienione 13 specjalizacji (kowalstwo, szwactwo, złotnictwo, ciesielstwo, garncarstwo, skórnictwo, magiczne tworzenie, inżynieria, gotowanie, kamieniarstwo, zegarmistrzostwo, szklarstwo, eksperymentalne tworzenie). Każda specjalizacja ma swój poziom, który wzrasta wraz z wykonywaniem minigierek. Poziom danej specjalizacji wpływa na możliwość tworzenia lepszych przedmiotów i daje bonusy do statystyk co 5 poziomów. Aby zostać „dyplomowanym” w Gildii, trzeba w każdej z 13 specjalizacji osiągnąć 75+ poziom i zaliczyć finalny test. Wpierw należy stworzyć tabelę, która przechowa te wszystkie 13 profesji w tym przypadku **CraftingProfession**. Następnie należy powiązać postać z daną profesją; w tym przypadku za pomocą tabeli **CharacterCraftingProfession**. Do tego każdy item powinien mieć swoją recepturę za to odpowiada tabela **CraftingRecipe** i co jest potrzebne do craftingu w tabeli **CraftingRecipeMaterial**.
