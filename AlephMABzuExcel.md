## Aufbereitung von Titellisten im MAB2-Format (aus ILS Aleph) als Excel-Liste

### Idee
Im Zuge von Migrationsvorbereitungen müssen gelegentlich Titelmengen aus dem Bibliothekssystem Aleph erzeugt und analysiert werden. Die Such- und Exportservices von Aleph geben die gefundenen Titel als XML-Dateien aus, die sich nicht zur schnellen Analyse eignen. Ziel war daher, mit OpenRefine diese XML-Dateien in Excel-Tabellen umzuwandeln.
Die gewünschten Tabellen enthalten:
- je eine Spalte für jedes MAB-Feld (sowie die aleph-internen Felder CAT und DEL)
  - sollte ein MAB-Feld im Titelsatz mehrfach vorkommen, soll der Inhalt in einer Zelle zusammengefasst und mit . - getrennt werden (Punkt Spatium Bindestrich Spatium) *Achtung!* für bestimmte Auswertungen kann es sinnvoller sein, die Inhalte sich wiederholender Felder nicht zusammen zu fassen, dafür ist dieses Skript nicht geeignet!
  - aus den Spaltenbennenungen soll das entsprechende MAB-Feld hervorgehen
- jeder Titelsatz soll in einer Zeile dargestellt werden

### Datei in OpenRefine laden
1. OpenRefine starten, XML-Datei für Import auswählen und als Format XML auswählen.
2. Erstes Element auswählen (i.d.R. "<section-02> <col1>LDR-1</col1>...")
3. Projekt benennen und anlegen
4. Formatierung, hierzu kann die folgende JSON-History als Grundlage verwendet werden
    - erstellt für die Arbeit mit Titeldaten aus dem K10plus, bei lokaler Katalogisierung in Aleph kommen möglicherweise weitere MAB-Felder vor und das Skript muss angepasst werden 

#### JSON-History (als Vorlage)

[
  {
    "op": "core/key-value-columnize",
    "keyColumnName": "section-02 - col1",
    "valueColumnName": "section-02 - col2",
    "noteColumnName": "",
    "description": "Columnize by key column section-02 - col1 and value column section-02 - col2 with note column "
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "CAT-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column CAT-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "DEL-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column DEL-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "711-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 711-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "902-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 902-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "077b1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 077b1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "376-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 376-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "501-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 501-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "529z1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 529z1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "700g1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 700g1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "061-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 061-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "062-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 062-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "076a1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 076a1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "534z1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 534z1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "545-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 545-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "087o1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 087o1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "540-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 540-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "540a1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 540a1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "419-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 419-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "370a1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 370a1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "088r1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 088r1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "907-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 907-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "700b1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 700b1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "620b1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 620b1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "527z1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 527z1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "077a1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 077a1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "064a1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 064a1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "025-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 025-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "025o1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 025o1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "740u1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 740u1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "700-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 700-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "517-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 517-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "078e1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 078e1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "947-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 947-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "942-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 942-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "932-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 932-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "927-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 927-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "922-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 922-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "917-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 917-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "912-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 912-1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "711a1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 711a1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "655e1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 655e1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "376b1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 376b1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "077e1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 077e1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "531z1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 531z1"
  },
  {
    "op": "core/multivalued-cell-join",
    "columnName": "564-1",
    "keyColumnName": "LDR-1",
    "separator": ". - ",
    "description": "Join multi-valued cells in column 564-1"
  }
]
