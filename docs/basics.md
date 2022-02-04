# Grundlagen

In CiviCRM kann für jeden Kontakt standardmäßig mithilfe von SMARTY - einer
speziellen Syntaxsprache - eine personalisierte Grußformel erzeugt werden (
postalische Begrüßung und E-Mail-Begrüßung). Mit der Erweiterung MoreGreetings
kann die Anzahl der verfügbaren Grußformeln bzw. Grußformelfelder auf bis zu
neun erweitert werden. Die zusätzlichen Grußformeln können in
benutzerdefinierten Feldern gespeichert werden, die individuell benannt werden
können.

In diesen benutzerdefinierten Feldern können mit SMARTY komplexe Formeln (siehe
die [Smarty-Dokumentation] (https://www.smarty.net)) erstellt werden.
MoreGreetings prüft dabei automatisch, ob die Syntax korrekt eingegeben wurde
oder ob ein Fehler vorliegt. Die Einschränkung auf 240/255 Zeichen wie im Falle
von Standard-Grußformeln gilt bei diesen Feldern nicht.

Sobald eine Formel für eine neue Begrüßung korrekt erstellt wurde, können alle
Kontakte in CiviCRM entsprechend aktualisiert werden. Falls gewünscht, kann man
ein Grußformelfeld für einen bestimmten Kontakt auch interaktiv überschreiben
und diese manuelle Änderung vor dem erneuten Überschreiben schützen (
Schreibschutz).
