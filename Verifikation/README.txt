README
Technische Verifikation -- Ontologiebasierte Reifegradbestimmung (Kapitel 6.2)
================================================================================

Dieses Paket enthält die Dateien zur technischen Verifikation des FDM-Reifegradmodells.
Mit den OWL-Ontologien wird gezeigt, dass das Reifegradmodell maschinell ausgewertet
werden kann, dass die Zusammenführung mehrerer Projektontologien zu einem konsistenten
Ergebnis führt und dass die kumulative Reifegradlogik auch bei lückenhafter
Praktikenbelegung korrekt funktioniert (Negativtestfall Projekt 5).


DATEIBESCHREIBUNGEN
-------------------

Projekt1.owl -- Projekt4.owl
    Vier OWL-Ontologien für fiktive Forschungsprojekte mit vollständig belegten
    Praktiken je Prozessbereich. Alle Dateien verwenden dasselbe Schema (Klassen,
    Properties, SWRL-Regeln) und unterscheiden sich ausschließlich in den angewendeten
    Praktiken (wendenPraktikAn), die dem jeweiligen IST-Reifegrad in den fünf
    Prozessbereichen Planung, Erhebung, Analyse & Synthese, Archivierung und Zugang
    entsprechen. Die Soll- und Ist-Werte stimmen in allen vier Projekten überein.

    Projekt 1: Planung 5, Erhebung 4, Analyse & Synthese 5, Archivierung 3, Zugang 2 (158 Praktiken)
    Projekt 2: Planung 2, Erhebung 3, Analyse & Synthese 2, Archivierung 4, Zugang 5 (130 Praktiken)
    Projekt 3: Planung 3, Erhebung 5, Analyse & Synthese 4, Archivierung 2, Zugang 3 (146 Praktiken)
    Projekt 4: Planung 4, Erhebung 1, Analyse & Synthese 1, Archivierung 3, Zugang 2  (61 Praktiken)

Projekt5.owl
    Negativtestfall. Das Projekt belegt bewusst lückenhafte Praktiken, um zu prüfen,
    ob die kumulative Reifegradlogik auch dann korrekt greift, wenn Praktiken höherer
    Reifegrade ohne die Voraussetzungen niedrigerer angewendet werden.

    Belegung und erwartetes Ergebnis:
    - Planung:            RG1 + RG2 vollständig, RG3 fehlt, RG4 vollständig -> inferiert RG2
    - Erhebung:           RG1 + RG2 + RG3 vollständig                        -> inferiert RG3
    - Analyse & Synthese: RG1 + RG2 vollständig, RG3 fehlt, RG4 vollständig -> inferiert RG2
    - Archivierung:       keine Praktiken                                     -> inferiert RG0
    - Zugang:             RG1 + RG2 vollständig                              -> inferiert RG2

    Projekt 5 erfüllt mit 98 Praktiken mehr als Projekt 4 (61 Praktiken), erzielt aber
    aufgrund der Lücken in der Praktikenkette einen niedrigeren Reifegrad. Dies belegt,
    dass nicht die Anzahl der Praktiken, sondern die vollständige Erfüllung der
    kumulativen Kette für die Reifegradbestimmung ausschlaggebend ist.

Merged_AlleProjekte.owl
    Zusammengeführte OWL-Ontologie, die alle fünf Forschungsprojekte in einer
    gemeinsamen Wissensbasis vereint. Das Schema ist einmalig vorhanden; die
    Projekt-Individuen mit ihren Praktiken sind gemeinsam in der ABox abgelegt.
    Diese Datei ist der Ausgangspunkt für den Reasoner-Lauf.

Merged_AlleProjekte_Inferiert.owl
    Inferierte Version der zusammengeführten Ontologie, erzeugt durch den
    HermiT-Reasoner in Protégé. Alle durch die SWRL-Regeln abgeleiteten
    erzieltReifegrad-Tripel liegen als assertierte Fakten vor und sind die
    Grundlage für die SPARQL-Abfrage.

SPARQL.txt
    SPARQL-Abfrage zur Auswertung der inferierten Reifegrade. Sie wird auf
    Merged_AlleProjekte_Inferiert.owl ausgeführt (in Protégé unter
    Tools > SPARQL Query) und gibt für jedes Projekt den erreichten Reifegrad
    je Prozessbereich aus. Das Ergebnis entspricht der Soll-Ist-Tabelle aus
    Kapitel 6.2 und belegt die Korrektheit der ontologiebasierten
    Reifegradbestimmung einschließlich des Negativtestfalls.
