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

## Experimentopzet 
Als eerste stap is een configureerbare trainingspipeline opgezet waarin model- en trainingsparameters strikt gescheiden zijn via configuratie-objecten. Met Ray Tune is een hypertuning-setup geïmplementeerd waarin zowel architectuur- als trainingsparameters kunnen worden gevarieerd.
In de huidige fase is een brede oriëntatie opgezet met korte trainingsruns om kansrijke configuraties en instabiele regio’s in de hyperparameter-ruimte te identificeren. Deze fase is bedoeld als richtinggevend en niet voor definitieve conclusies.

## Observatie fase 1
De resultaten uit fase 1 laten zien dat modellen met drie convolutionele lagen consistent beter presteren dan ondiepere of diepere varianten binnen het beperkte epoch-budget. Vooral configuraties met base_channels van 48 of 64 en batch normalization tonen stabielere validatieprestaties. Hoge learning rates leiden regelmatig tot slechtere prestaties, wat wijst op instabiliteit bij deze architecturen. Op basis van deze observaties is in fase 2 gekozen voor een verfijnde zoekruimte waarin n_conv is gefixeerd op 3 en alleen kansrijke waarden voor base_channels en learning rate zijn onderzocht, met een vast trainingsbudget voor alle configuraties.[phase1.csv](https://github.com/MischTrader/MADS-MachineLearning-course/blob/master/results/ex4_Ray/exports/phase1.csv)

## Resultaten fase 2
De fase-2 experimenten tonen aan dat modellen met drie convolutionele lagen en een middelgrote capaciteit (base_channels = 48) de beste validatieprestaties behalen binnen een vast trainingsbudget van 12 epochs. De hoogste validatie-accuracy (~0.73) werd bereikt door een model met batch normalization, zonder dropout of skip connections, en een learning rate rond 5×10⁻⁴. [phase2.csv](https://github.com/MischTrader/MADS-MachineLearning-course/blob/master/results/ex4_Ray/exports/phase2.csv)

## Observatie
Batch normalization blijkt een consistente positieve bijdrage te leveren aan zowel prestatie als trainingsstabiliteit. In tegenstelling tot de initiële hypothese leveren dropout en skip connections in deze configuratie geen duidelijke winst op. Grotere modellen laten geen proportionele prestatieverbetering zien, wat wijst op afnemend rendement bij toenemende capaciteit binnen dit epoch-budget.

## Verklaring
Batch normalization stabiliseert activaties en gradiënten, waardoor het optimalisatieproces robuuster wordt voor variaties in learning rate en modelcapaciteit. Dropout introduceert extra ruis tijdens training, wat bij relatief kleine datasets en beperkte trainingsduur kan leiden tot onderbenutting van de modelcapaciteit. Skip connections zijn vooral effectief bij diepere netwerken, en hun beperkte effect hier is consistent met de relatief geringe netwerkdiepte.

## Reflectie (definitief)
Dit experiment laat zien dat hyperparameter-tuning pas betekenisvol wordt wanneer architectuurkeuzes expliciet worden meegenomen. Waar in fase 1 vooral richting werd bepaald, maakt fase 2 duidelijk dat meer complexiteit niet automatisch betere prestaties oplevert. De resultaten benadrukken het belang van gecontroleerde experimenten met vaste trainingsbudgetten en onderstrepen dat regularisatietechnieken contextafhankelijk zijn. In een volgende iteratie zou een groter epoch-budget of een diepere architectuur kunnen worden onderzocht om het effect van skip connections verder te evalueren.

Links Code & experimenten: https://github.com/MischTrader/Mischa-Peters-Portfolio/tree/main/4-hypertuning-ray
