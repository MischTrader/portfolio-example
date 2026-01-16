## Verslag – Ethiek en algoritmische bias in de Breeze datingapp

## 1. Casusbeschrijving

De datingapp Breeze maakt gebruik van een algoritme dat gebruikers aan elkaar voorstelt op basis van profielkenmerken en historisch like-gedrag. Uit onderzoek en een oordeel van het College voor de Rechten van de Mens blijkt dat het algoritme mogelijk leidt tot indirecte discriminatie van gebruikers met een donkere huidskleur of een niet-Nederlandse achtergrond. Deze groepen zouden structureel minder vaak worden voorgesteld, wat resulteert in minder matches en daarmee ongelijke kansen binnen het platform (College voor de Rechten van de Mens, 2023).

## 2. Eerste indruk van de ethische problematiek
Mijn eerste indruk is dat de morele kern van deze casus ligt in de spanning tussen individuele voorkeuren en collectieve verantwoordelijkheid. Hoewel gebruikers vrij zijn in hun partnerkeuze, wordt het problematisch wanneer een algoritme deze voorkeuren systematisch versterkt en omzet in structurele ongelijkheid. De technische oorzaak lijkt te liggen in het trainen van het model op historisch like-gedrag, waarin maatschappelijke vooroordelen reeds aanwezig zijn. In maatschappelijke context raakt dit aan bredere discussies over discriminatie, algoritmische besluitvorming en de verantwoordelijkheid van platforms om mensenrechten te waarborgen, zelfs wanneer negatieve effecten niet intentioneel zijn.

## 3. DAG-model van het dilemma
Onderstaand DAG-model laat zien hoe indirecte discriminatie kan ontstaan zonder expliciet gebruik van beschermde kenmerken.
<img width="593" height="578" alt="image" src="https://github.com/user-attachments/assets/b6303637-0b59-49de-8926-9eddbffe6b27" />

## Uitleg:
De sociale identiteit van gebruikers beïnvloedt culturele voorkeuren, die op hun beurt het like-gedrag sturen. Dit gedrag vormt de trainingsdata voor het algoritme. Het algoritme bepaalt vervolgens wie zichtbaar wordt (exposure), wat directe gevolgen heeft voor het aantal matches. Via een feedback-loop worden deze uitkomsten opnieuw onderdeel van de data, waardoor bestaande ongelijkheden zich versterken. Regulering en ethische interventies kunnen ingrijpen op zowel het model als de exposure-fase.

## 4. Reflectie: gemiste aspecten na het DAG-model
Na het opstellen van de DAG werd duidelijk dat exposure een cruciale, maar vaak onderschatte factor is. De eerste indruk richtte zich vooral op bias in data en modeltraining, maar het model maakt zichtbaar dat ongelijke zichtbaarheid op zichzelf al tot ongelijkheid leidt, zelfs zonder verschillen in voorkeur of kwaliteit. Daarnaast werd de rol van feedback-loops duidelijker: succes of falen in het verleden bepaalt toekomstige kansen, wat cumulatieve ongelijkheid veroorzaakt.

##  5. Aanbeveling aan de data scientist
Aan een data scientist die met een vergelijkbare opdracht te maken krijgt, zou ik aanraden om fairness expliciet als ontwerpeis op te nemen. Dit betekent: vooraf bepalen welke vorm van gelijkheid wordt nagestreefd (bijvoorbeeld gelijke exposure), het uitvoeren van fairness-analyses per subgroep, en het actief monitoren van feedback-loops. Daarnaast is transparantie essentieel: documenteer welke data worden gebruikt, welke aannames het model maakt en waar mogelijke bias kan ontstaan. Tot slot is samenwerking met juridische en ethische experts noodzakelijk, omdat technische optimalisatie alleen onvoldoende is om maatschappelijke schade te voorkomen (Barocas, Hardt, & Narayanan, 2019).

## Referenties (APA)
1. Barocas, S., Hardt, M., & Narayanan, A. (2019). Fairness and machine learning. https://fairmlbook.org
2. College voor de Rechten van de Mens. (2023, 6 september). Dating-app Breeze mag en moet algoritme aanpassen om discriminatie te voorkomen. https://www.mensenrechten.nl/actueel/nieuws/2023/09/06/dating-app-breeze-mag-en-moet-algoritme-aanpassen-om-discriminatie-te-voorkomen
3. Europese Unie. (2016). Algemene verordening gegevensbescherming (EU) 2016/679. https://eur-lex.europa.eu
