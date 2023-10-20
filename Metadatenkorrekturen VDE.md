## Metadatenkorrekturen für VDE-Normen<br>
In die Katalogbestände unter https://ebooks.mpdl.mpg.de wurde kürzlich die MPG-weit lizenzierte Kollektion von VDE-Normen integriert. Dabei bestand eine besondere Herausforderung darin, dass der Anbieter zu diesen elektronischen Ressourcen keine Metadaten in einem standardisierten Austauschformat anbietet. Allerdings stehen über die Plattform Excel-/CSV-Exporte bereit, die bereits umfangreiche Informationen zu den einzelnen Dokumenten enthalten. Für eine Übernahme in den zentralen eBook-Katalog wurden die Metadaten zunächst mittels OpenRefine MAB-konform umstrukturiert und schließlich für das Bibliothekssystem ALEPH ins sequential-Format gewandelt. Auf dieser Grundlage kann die Kollektion mit nur wenigen weiteren Schritten geladen bzw. künftig aktuell gehalten werden.<br>
Weitere Details sowie die entstandenen JSON-Objekte, wie sie nun auch in den Produktivbetrieb übernommen wurden, stehen in einem eigenen GitHub-repository unter https://github.com/stoffelx/VDE_csv2mab bereit.