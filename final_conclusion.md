# Finaler Projektabschluss: Bitcoin-Preisprognose

**Erstellt:** 2026-07-30T22:48:59.982395+00:00  
**Projektstatus:** Research complete  
**Produktionsfreigabe:** Nicht erteilt  
**Handelsentscheidung:** no_trade  
**Finaler Test geöffnet:** Nein  
**Ausgewertete Horizonte:** h4 (1 Stunde), h16 (4 Stunden), h96 (24 Stunden)

## Forschungsfrage

Untersucht wurde, ob sich aus historischen BTCUSDT-15-Minuten-Kerzen und daraus
abgeleiteten technischen, statistischen, Volumen-, Kalender- und Regime-Features
ein robustes Richtungssignal erzeugen lässt, das realistische Gebühren, Spread
und Slippage in einer leakage-geschützten Walk-Forward-Auswertung überwindet.

## Ergebnisübersicht

| Horizont | Zeitraum | Modell | Kalibrierung | Entscheidung | Economic Gate | Max. robuste Kosten | Aktuelle Kosten tragfähig |
|---:|---|---|---|---|---|---:|---|
| h4 | 1 Stunde | lightgbm | sigmoid | no_trade | Nein | – | Unbekannt |
| h16 | 4 Stunden | catboost | sigmoid | no_trade | Nein | 10.0000 bp | Nein |
| h96 | 24 Stunden | lightgbm | raw | no_trade | Nein | 5.0000 bp | Nein |

## Zentrale Schlussfolgerung

Mit den verwendeten BTCUSDT-15-Minuten-Daten, Features und Modellen bestand kein untersuchter Horizont das wirtschaftliche Walk-Forward-Gate unter den angenommenen realistischen Round-Trip-Kosten. Die fachlich korrekte Entscheidung lautet No Trade. h16 zeigte die höchste explorative Kostenrobustheit. Der finale Test bleibt unangetastet.

Von den untersuchten Horizonten erreichte **h16**
(4 Stunden) mit
**10.0000 bp** die
höchste explorative Kostenrobustheit. Auch dieser Horizont war bei den
angenommenen aktuellen Round-Trip-Kosten von
**31.9744 bp** nicht
wirtschaftlich tragfähig.

## Warum „No Trade“ ein gültiges Resultat ist

Die Pipeline behandelt Nicht-Handeln als explizite Alternative mit einem
Referenz-Objective von null. Ein Schwellenwert wird nur freigegeben, wenn sowohl
die verschachtelten Trainingssegmente als auch das äußere Economic Gate die
vorab definierten Mindestanforderungen erfüllen. Dadurch wird nicht der am
wenigsten schlechte Kandidat künstlich als Handelsstrategie ausgegeben.

## Methodische Schutzmaßnahmen

- chronologische Walk-Forward-Validierung;
- Purging anhand des Target-Endzeitpunkts;
- horizonabhängiges Embargo und Trade-Cooldown;
- Modell- und Kalibrierungsauswahl ohne finalen Test;
- wirtschaftliche Bewertung nach Gebühren, Spread und Slippage;
- separates No-Trade-Gate;
- keine Testfreigabe bei nicht bestandenem Economic Gate;
- unveränderliche Referenz auf die verwendeten Quellartefakte im Manifest.

## Finale Testentscheidung

Der finale Test wurde nicht geöffnet. Dies ist kein unvollständiger
Projektschritt, sondern die korrekte Konsequenz des Evaluationsprotokolls: Kein
Entwicklungskandidat erfüllte die Bedingungen für eine unabhängige finale
Bestätigung.

## Einschränkungen

- nur BTCUSDT Spot;
- nur 15-Minuten-Kerzen;
- überwiegend OHLCV- und aggregierte Trade-Merkmale;
- keine Orderbuch-, Futures-, Funding-, On-Chain- oder Sentimentdaten;
- vereinfachtes Kosten- und Ausführungsmodell;
- keine Short-, Portfolio- oder Live-Execution-Strategie;
- explorative Kosten-Sensitivität auf äußeren Walk-Forward-Daten;

## Zukünftige Arbeiten

- kostenbewusstes Long-/No-Trade-Target;
- direkte Netto-Return-Regression oder Ranking;
- Long-/Short-/No-Trade-Multiclass-Target;
- Orderbuch-, Futures-, Funding- und Open-Interest-Merkmale;
- regimespezifische Modelle und realistische Next-Open-Ausführung;
- separater vorab spezifizierter Bestätigungslauf vor jeder Testöffnung;

Diese Punkte sind bewusst nicht mehr Bestandteil des abgeschlossenen
Experimentumfangs. Ihre Umsetzung würde eine neue Forschungsphase mit neuem,
vorab festgelegtem Protokoll darstellen.

## Reproduzierbarkeit

Die Datei `artifact_manifest.json` enthält Pfade, Dateigrößen, Zeitstempel und
SHA-256-Prüfsummen der eingelesenen Kernartefakte und der erzeugten
Abschlussdateien. `source_runs.json` dokumentiert die eingefrorenen Referenzläufe.

## Dokumentierte Hinweise

- h4: Kein Screening-Gesamtbericht gefunden; die Abschlusswerte wurden aus Einzelartefakten rekonstruiert.
- h4: Keine Machbarkeitsentscheidung gefunden.
- h4: Aktuelle Kosten-Machbarkeit unbekannt.
- h4: Maximale robuste Kostenstufe unbekannt.
