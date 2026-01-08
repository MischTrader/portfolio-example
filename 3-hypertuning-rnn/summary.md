## Summary week 3
RNN Architectuur – Representatie, Pooling en Conv1D

## Doel
Onderzoeken hoe verschillende representaties van sequentiële data binnen een RNN-architectuur de prestaties beïnvloeden bij gesture-classificatie. Specifiek is gekeken naar (1) de keuze van de temporele representatie (laatste timestep versus pooling) en (2) het effect van een Conv1D-laag vóór een GRU om lokale temporele patronen te extraheren.

## Dataset
Gesture-dataset (accelerometerdata), bestaande uit variabele-lengte tijdreeksen met drie inputkanalen. De data is gepaddede en verwerkt met een vaste batch size, waarbij training en validatie consistent zijn gehouden over alle experimenten.

## Model
De baseline bestaat uit een GRU gevolgd door een lineaire classifier. Deze architectuur is stapsgewijs uitgebreid:

1. GRU last-step – gebruikt alleen de laatste timestep van de sequentie
2. GRU mean pooling – average pooling over alle timesteps van de GRU-output
3. Conv1D → GRU → mean pooling – een Conv1D-laag met ReLU vóór de GRU om lokale temporele patronen te extraheren

Alle modellen gebruiken identieke hyperparameters (hidden size, learning rate, epochs) om architecturale effecten zuiver te vergelijken.

## Hypothese
Ik verwachtte dat:

- De last-step representatie gevoelig is voor padding en variabele sequentielengtes.
- Mean pooling over tijd een robuustere sequentierepresentatie oplevert.
- Een Conv1D-laag vóór de GRU lokale temporele structuren (zoals korte acceleratiepieken) explicieter kan modelleren, wat de classificatieprestatie verder verbetert.

## Experimentopzet
- Vergelijking van drie modelvarianten: gru_last, gru_mean, conv1d_gru_mean
- Training voor 30 epochs met early stopping
- Evaluatie op validatieset
- Logging van loss en accuracy via MLflow
- Runs gegroepeerd binnen één experiment (gestures-ex3) voor directe vergelijking

## Resultaten
De MLflow-resultaten laten een duidelijke prestatieverbetering zien per architectuurstap:
GRU last-step: validatie-accuracy ≈ 0.96–0.97
GRU mean pooling: validatie-accuracy ≈ 0.98
Conv1D + GRU mean pooling: validatie-accuracy ≈ 0.99

Daarnaast vertoont het Conv1D-model een snellere convergentie en lagere validatie-loss.

## Observatie
De last-step aanpak blijkt suboptimaal bij gepaddede sequenties: relevante informatie uit eerdere timesteps wordt genegeerd. Mean pooling over tijd levert een stabielere en informatievere representatie op. Het toevoegen van Conv1D vóór de GRU verbetert de prestaties verder, wat suggereert dat lokale temporele patronen belangrijk zijn voor gesture-herkenning.

## Verklaring
Mean pooling reduceert de afhankelijkheid van sequentielengte en padding door informatie over alle timesteps te aggregeren. Conv1D fungeert als een lokale feature extractor die korte-termijn temporele structuren leert voordat de GRU de globale sequentiedynamiek modelleert. Deze combinatie verlaagt de belasting op de RNN en verbetert zowel efficiëntie als generalisatie.

## Reflectie
Waar eerdere experimenten vooral focusten op optimalisatie en hyperparameters, laat deze week zien dat architecturale representatiekeuzes binnen RNN’s cruciaal zijn. Kleine aanpassingen in hoe sequenties worden samengevat of voorbewerkt (pooling, Conv1D) leiden tot significante prestatiewinst. Dit onderstreept het belang van het expliciet nadenken over tensorvormen en informatieflow in sequentiële modellen.

Code & experimenten: https://github.com/MischTrader/MADS-MachineLearning-course/tree/master/notebooks/ex3
