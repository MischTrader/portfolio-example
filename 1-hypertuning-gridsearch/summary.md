# Summary week 1
# Hyperparameter Tuning – Grid Search

## Doel
Onderzoeken hoe learning rate en modelcapaciteit
het validatiegedrag beïnvloeden.

## Dataset
CIFAR-10 subset (cat, dog, horse), lokaal gepreprocessed.

## Model
Eenvoudig CNN met één fully-connected laag.
De architectuur is gebaseerd op de standaard exercise en is bewust niet aangepast.
De gebruikte architectuur is bewust eenvoudig gehouden (een feedforward netwerk met één verborgen laag), 
zodat het effect van hyperparameters duidelijk observeerbaar blijft en niet wordt gemaskeerd door architecturale complexiteit.

## Hypothese
Ik verwachtte dat de learning rate en het aantal fully connected units (modelcapaciteit) met elkaar interacteren.
Specifiek veronderstelde ik dat bij een hogere learning rate een te klein of juist te groot model instabiel zou trainen, 
terwijl een middelgrote modelcapaciteit robuuster zou zijn.
Bij een te hoge learning rate verwachtte ik slechtere prestaties door het overschrijden (overshooting) 
van het optimum tijdens optimalisatie.

## Experimentopzet
- Gridsearch over learning rate × fc_units
- Elke configuratie 5 epochs
- Evaluatie op validatieset
- Logging via TensorBoard

## Resultaten
![Heatmap] https://github.com/MischTrader/MADS-MachineLearning-course/blob/master/results/plots/heatmap_best_val_acc.png

## Observatie
- De heatmap laat een duidelijke interactie zien tussen learning rate (lr) en fc_units:
- De beste validatie-accuracies worden behaald bij lr = 0.003, onafhankelijk van het exacte aantal units.
- Bij lr = 0.01 stort de validatie-accuracy in, met name bij fc_units = 32.
- Bij lr = 0.001 zijn de resultaten stabiel, maar consistent lager dan bij lr = 0.003.
- Een middelgroot model (fc_units = 64) presteert het best of vrijwel het best voor alle learning rates.
- Dit bevestigt dat de learning rate de dominante hyperparameter is, terwijl de modelcapaciteit 
  het effect van de learning rate kan versterken of afzwakken.

## Verklaring
De learning rate bepaalt de grootte van de updates in de parameter-ruimte tijdens training.
Bij lr = 0.01 zijn deze updates te groot, waardoor het model het optimum overschrijdt en slecht generaliseert. Dit effect is sterker zichtbaar bij kleinere modellen, 
die minder representatiekracht hebben om instabiliteit op te vangen.

Bij lr = 0.003 is de balans optimaal:
groot genoeg om snel te leren,
klein genoeg om stabiel te blijven.
De invloed van het aantal units is secundair maar duidelijk zichtbaar:
te weinig units leidt tot onderfitting,
te veel units levert binnen dit beperkte epoch-budget geen duidelijke prestatiewinst op.
Dit verklaart waarom fc_units = 64 consistent goed presteert en waarom juist de interactie tussen learning rate en modelcapaciteit cruciaal is bij hypertuning, 
zelfs voor relatief eenvoudige modellen.

## Reflectie
Learning rate blijkt dominanter dan modelgrootte.
Te kleine modellen onderfitten, grotere modellen
leveren geen extra winst binnen dit epoch-budget.

## Links
- Code & experimenten:
  https://github.com/MischTrader/MADS-MachineLearning-course/tree/ex1-hypertuning-gridsearch

→ Terug naar portfolio homepage
