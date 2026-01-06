# Summary week 1
# Hyperparameter Tuning – Grid Search

## Doel
Onderzoeken hoe learning rate en modelcapaciteit
het validatiegedrag beïnvloeden.

## Dataset
CIFAR-10 subset (cat, dog, horse), lokaal gepreprocessed.

## Model
Eenvoudig CNN met één fully-connected laag.
De architectuur is gebaseerd op de standaard exercise
en is bewust niet aangepast.

## Hypothese
Een middelgrote learning rate (0.003) gecombineerd met
een middelgroot aantal neuronen (64 units) levert de
beste bias–variance balans op.

## Experimentopzet
- Gridsearch over learning rate × fc_units
- Elke configuratie 5 epochs
- Evaluatie op validatieset
- Logging via TensorBoard

## Resultaten
![Heatmap](plots/heatmap_best_val_acc.png)

Beste configuratie:
- lr = 0.003
- fc_units = 64
- best_val_acc ≈ 0.63

## Reflectie
Learning rate blijkt dominanter dan modelgrootte.
Te kleine modellen onderfitten, grotere modellen
leveren geen extra winst binnen dit epoch-budget.

## Links
- Code & experimenten:
  https://github.com/MischTrader/MADS-MachineLearning-course/tree/ex1-hypertuning-gridsearch

→ Terug naar portfolio homepage
