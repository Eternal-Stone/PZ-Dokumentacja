# Changelog

Podczas tworzenia dokumentacji bazy danych szczególny nacisk został położony na transparentność, aby każdy członek zespołu mógł bez większych przeszkód odnaleźć się w plikach oraz zrozumieć proces myślowy stojący za aktualizacją poszczególnych komponentów. **Changelog** jest plikiem, w którym informuje się o zmianach dokonanych w poszczególnych aktualizacjach, wspierając osiągnięcie powyższych założeń.

## Zmiany

- Dokonano zmian w schemacie bazy danych Tabele tworzące core zostały stworzone według innej koncepcji. Dodano tabele związane z profesjami, które będą dalej rozwijane i modyfikowane.
- System profesji jest prawie ukończony. Dodano tabele dla przedmiotów oraz część systemów związanych z ich ulepszaniem.
- W schemacie uwzględniono wiele kolejnych systemów. Do katalogu został dodany plik wskazujący, które systemy są już zintegrowane ze schematem. Część istniejących tabel została zmodyfikowana w celu ich integracji z nowymi mechanikami. Więcej informacji znajduje się w pliku [Informacje o Schemacie Bazy Danych](InformacjeOSchemacieBazyDanych.md).
- Kolejne pliki z listy zostały rozważone. Dodano wiele nowych tabel, a istniejące zostały zmodyfikowane.
- Wszystkie pliki z listy zostały przeanalizowane. Schemat może mimo to jeszcze ulec zmianie. W kodzie zaproponowano dodatkowe kolumny, które mogą być przydatne w zależności od zakresu implementacji po stronie bazy danych. **Soul Crystals i Runy zostały zintegrowane z przedmiotami**. To rozwiązanie zmniejszyło wielkość schematu. Może jednak prowadzić do występowania wielu NULL w tabelach. Nasz przyjaciel ChatGPT zasugerował, że jest to normalne w przypadku dużych gier MMORPG, jednak ewentualna przebudowa jest nadal rozważana. Jeśli pojawią się sugestie ze strony zespołu, zostaną one przyjęte do dalszej analizy.
