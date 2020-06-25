# Augabenstellung
Erstellung eines Bash-Skriptes zu bereinigung der Datei 2020-05-23-Article_list_dirty.tsv. Es wird davon ausgegangen das sich die Ursprunsdatei auf dem Desktop befindet.

# Erster Befehl
Die oben gennante Datei befinden sich im Ordner Desktop, daher wird als erster Schritt in das verzeichnet gewechselt:
cd ~/Desktop

# Zweiter Befehl
Überflüssige Zeilen löschen
less 2020-05-23-Article_list_dirty.tsv | cut -f 5,12 > 2020-05-23-Article_list_dirtyTEMP2.tsv 

# Dritter Befehl
Entfernt alle Zeichen die ein "eng" enthalten
grep -v eng 2020-05-23-Article_list_dirtyTEMP2.tsv >  2020-05-23-Article_list_dirtyTEMP3.tsv 

# vierter Befehl
Entfernt alle Zeichen die "issn" enthalten, Groß- Kleinschreibung ist dabei nicht relavant. Ebenfalls werden alle ":" entfernt so wie überflüssigen Leerzeichen am Anfang der Zeilen.
sed 's/issn//ig;s/:/ /g;s/^[ \t]*//;s/date//ig' 2020-05-23-Article_list_dirtyTEMP3.tsv > 2020-05-23-Article_list_dirtyTEMP4.tsv 

# fünfter Befehl
Da noch reduntante Zeilen vorhanden sind, werden diese mit folgendem Befehl entfernt:
sort -u 2020-05-23-Article_list_dirtyTEMP4.tsv >2020-05-23-Article_list_dirty.tsv 
Dies entfernt ebenfalls unötige leere Zeilen.

# Sechsters Befehl
Die Zwischen gepeicherten Dateien müssen im anschluss gelöscht werden:
rm 2020-05-23-Article_list_dirtyT*


# Fertiges Script
cd ~/Desktop
less 2020-05-23-Article_list_dirty.tsv | cut -f 5,12 > 2020-05-23-Article_list_dirtyTEMP2.tsv
grep -v eng 2020-05-23-Article_list_dirtyTEMP2.tsv >  2020-05-23-Article_list_dirtyTEMP3.tsv 
sed 's/issn//ig;s/:/ /g;s/^[ \t]*//;s/date//ig' 2020-05-23-Article_list_dirtyTEMP3.tsv > 2020-05-23-Article_list_dirtyTEMP4.tsv
sort -u 2020-05-23-Article_list_dirtyTEMP4.tsv >2020-05-23-Article_list_dirty.tsv
rm 2020-05-23-Article_list_dirtyT*
