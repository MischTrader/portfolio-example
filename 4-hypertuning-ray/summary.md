## Summary week 4
Hyperparameter Tuning – Architectuur en Stabiliteit (Ray Tune)

# Dit experiment is code-first uitgevoerd; hypothese, analyse en reflectie zijn daarom los vastgelegd in deze summary en het bijbehorende rapport, in plaats van in notebooks.

## Doel
Onderzoeken hoe modelcapaciteit en architecturale keuzes binnen een convolutioneel neuraal netwerk de prestaties en trainingsstabiliteit beïnvloeden. Specifiek richt dit experiment zich op de interactie tussen netwerkdiepte en -breedte, regularisatietechnieken (dropout, batch normalization) en skip connections, met gebruik van Ray Tune voor systematische hypertuning.

## Dataset
CIFAR-10 subset bestaande uit drie klassen (cat, dog, horse), vooraf lokaal gepreprocessed naar PNG-bestanden. Vanwege hardwarebeperkingen is de training uitgevoerd CPU-only met een beperkt aantal epochs.

## Model
Een configureerbaar convolutioneel neuraal netwerk opgebouwd uit een stack van convolutionele blokken gevolgd door een fully connected classifier. De architectuur is parametriseerbaar via configuratie-instellingen, waaronder:
1. aantal convolutionele lagen (2–4)
2. kanaalbreedte (base_channels)
3. grootte van de classifier (fc_units)
4. optionele batch normalization
5. optionele dropout
6. optionele skip connections

Deze opzet maakt het mogelijk om architecturale effecten systematisch te vergelijken binnen één trainingspipeline.

## Hypothese
Ik verwachtte dat modellen met hogere capaciteit betere validatieprestaties behalen, zolang overfitting wordt beperkt. Regularisatietechnieken zoals dropout en batch normalization zouden vooral effect hebben bij grotere modellen. Daarnaast veronderstelde ik dat skip connections de gevoeligheid voor de learning rate verminderen door stabielere training.

## Experimentopzet (huidige status)
Als eerste stap is een configureerbare trainingspipeline opgezet waarin model- en trainingsparameters strikt gescheiden zijn via configuratie-objecten. Met Ray Tune is een hypertuning-setup geïmplementeerd waarin zowel architectuur- als trainingsparameters kunnen worden gevarieerd.
In de huidige fase is een brede oriëntatie opgezet met korte trainingsruns om kansrijke configuraties en instabiele regio’s in de hyperparameter-ruimte te identificeren. Deze fase is bedoeld als richtinggevend en niet voor definitieve conclusies.

## Status
De infrastructuur voor hypertuning met Ray Tune is volledig geïmplementeerd en getest. De brede exploratiefase is voorbereid; een verfijnde tweede fase met vaste trainingsbudgetten en gedetailleerde analyse volgt in een volgende iteratie.

## Reflectie
Dit experiment benadrukt het belang van het scheiden van engineering en experimentontwerp bij hypertuning. Door eerst een robuuste, configureerbare pipeline op te zetten, wordt het mogelijk om hyperparameter-interacties gecontroleerd te onderzoeken. In tegenstelling tot eerdere opdrachten ligt de nadruk hier expliciet op iteratief experimenteren: eerst richting vinden, daarna verfijnen.

Links Code & experimenten: https://github.com/MischTrader/Mischa-Peters-Portfolio/tree/main/4-hypertuning-ray
