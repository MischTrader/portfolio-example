## Summary week 2

## Hyperparameter Tuning – Normalization en Architectuur

## Doel
Onderzoeken hoe normalisatielagen interacteren met learning rate en modelcapaciteit in een convolutioneel neuraal netwerk, en in hoeverre normalisatie het trainings- en validatiegedrag stabiliseert.

## Dataset
CIFAR-10 subset (cat, dog, horse), lokaal gepreprocessed.

## Model
Een convolutioneel neuraal netwerk met convolutionele en pooling-lagen, gevolgd door een fully connected classifier. De standaardarchitectuur is uitgebreid met optionele normalisatielagen (BatchNorm) en dropout. De architectuur blijft bewust compact om het effect van hyperparameters en normalisatie duidelijk observeerbaar te houden.

## Hypothese
Ik verwachtte dat normalisatielagen (BatchNorm) de training zouden stabiliseren en de gevoeligheid voor learning rate en modelcapaciteit zouden verminderen. Specifiek veronderstelde ik dat BatchNorm hogere of suboptimale learning rates robuuster maakt door stabielere activaties en gradiënten. Zonder normalisatie verwachtte ik instabiliteit, vooral bij hogere learning rates.

## Experimentopzet
Gridsearch over learning rate × fc_units × norm (None vs BatchNorm)
Elke configuratie getraind voor 5 epochs
Evaluatie op validatieset
Logging via MLflow
Resultaten samengevat in metrics.csv en gevisualiseerd met heatmaps

## Resultaten
[Heatmap] https://github.com/MischTrader/MADS-MachineLearning-course/blob/master/results/plots/ex2_heatmap_lr_fc_norm_batchnorm.png

[Heatmap] https://github.com/MischTrader/MADS-MachineLearning-course/blob/master/results/plots/ex2_heatmap_lr_fc_norm_none.png

## Observatie
De resultaten laten een duidelijk effect van normalisatie zien:
Modellen met BatchNorm behalen consistent hogere validatie-accuracies dan modellen zonder normalisatie.
Zonder normalisatie is de prestatie sterk afhankelijk van de learning rate; bij lr = 0.01 treedt duidelijke instabiliteit op.
BatchNorm maakt het model robuuster over verschillende learning rates en modelgroottes.
De interactie tussen learning rate en fc_units blijft zichtbaar, maar extreme prestatieverschillen worden afgezwakt door normalisatie.

## Verklaring
BatchNorm reduceert interne covariate shift door activaties te normaliseren, wat leidt tot stabielere gradiënten en een robuuster optimalisatieproces. Hierdoor wordt het model minder gevoelig voor de exacte keuze van learning rate. Modelcapaciteit blijft relevant: te kleine modellen onderfitten, terwijl grotere modellen binnen dit beperkte epoch-budget geen proportionele winst opleveren.

## Reflectie
Waar in exercise 1 de learning rate de dominante factor was, toont deze experimentreeks aan dat architecturale keuzes zoals normalisatie een grote invloed hebben op hyperparameter-interacties. BatchNorm vergroot de stabiliteit en generalisatie van het model en verkleint het risico op instabiele training. Dit onderstreept dat effectieve hyperparameter-tuning niet los gezien kan worden van architectuurkeuzes.

## Links
Code & experimenten: https://github.com/MischTrader/MADS-MachineLearning-course/tree/ex2-mlflow-cnn-norm/src
