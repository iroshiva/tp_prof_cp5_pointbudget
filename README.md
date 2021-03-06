# Point Budget

Ce projet concerne l'élaboration d'un MCD et d'un MLD pour un site comparatif de consommation de gaz, électricité, box internet et téléphonie.

## Modèle Conceptuel des Données (MCD)

Réalisation du MCD avec MOCODO (cf pb_mcd.svg)<br/><br/>

> VILLE: code. postal<br/>VIT DANS, 01 UTILISATEUR, 11 VILLE<br/>UTILISATEUR: id. utilisateur, nom, prénom, mot de passe, numéro de téléphone, email<br/><br/>PEUT FAIRE, 01 SIMULATION, 0N UTILISATEUR <br/><br/>SIMULATION: id. simulation, montant épargné<br/><br/>1_PEUT CONTENIR, 01 SIMULATION, 01 SIMULATION GAZ<br/>2_PEUT CONTENIR, 01 SIMULATION, 01 SIMULATION ELECTRICITÉ<br/>3_PEUT CONTENIR, 01 SIMULATION, 01 SIMULATION BOX INTERNET<br/>4_PEUT CONTENIR, 01 SIMULATION, 01 SIMULATION TELEPHONE<br/><br/>SIMULATION GAZ: id. simu gaz, prix actuel, consommation annuelle en kwh, épargne réalisée, superficie logement, type de chauffage, énergie utilisée pour l'eau chaude et la cuisson, nombre de personne logement, qualité d'isolation<br/>SIMULATION ELECTRICITÉ: id. simu elec, prix actuel, consommation annuelle en kwh, puissance du compteur kVA, épargne réalisée, superficie logement, type de chauffage, énergie utilisée pour la cuisson, énergie utilisée pour l'eau chaude, nombre de personne logement, qualité d'isolation<br/>SIMULATION BOX INTERNET: id. simu box internet, prix mensuel, épargne réalisée, option télé, appel fixe en France, appel mobile en France<br/>SIMULATION TELEPHONE: id. simu tel, prix mensuel, nombre de Go, épargne réalisée, engagement, appels/SMS/MMS Europe, appels/SMS.MMS Etranger, internet à l'étranger<br/><br/>1_COMPARAISON, 0N SIMULATION GAZ, 0N CONTRATS GAZ <br/>2_COMPARAISON, 0N SIMULATION ELECTRICITÉ, 0N CONTRATS ELECTRICITÉ<br/>3_COMPARAISON, 0N SIMULATION BOX INTERNET, 0N CONTRATS BOX INTERNET <br/>4_COMPARAISON, 0N SIMULATION TELEPHONE, 0N CONTRATS TELEPHONE<br/><br/>CONTRATS GAZ: id. contrat gaz, nom opérateur, nom de l'offre, prix par mois, prix kwh<br/>CONTRATS ELECTRICITÉ: id. contrat elec, nom opérateur, nom de l'offre, puissance compteur kVA, prix par mois, prix kwh<br/>CONTRATS BOX INTERNET: id. contrat box internet, nom opérateur, nom de l'offre, prix par mois, engagement, type internet, appel fixe France, appel mobile France, appel étranger, frais d'installation, frais de résiliation<br/>CONTRATS TELEPHONE: id. contrat tel, nom opérateur, nom de l'offre, frais de mise en service, prix carte sim, engagement, avec téléphone, prix, nombre de giga, appels/SMS/MMS France, appel/SMS/MMS Europe, giga europe, appels/SMS/MMS International, internet à l'International<br/><br/>


## Modèle Logique de Données (MLD)

- City (CityId, Name, Zip_Code, Insee_Code)
- User (UserId, First_Name, Last_Name, Password, Phone_Number, Email, #CityId)
- Full_Simulations (FullSimulationId, TotalCostSaved, Validated, #UserId)
- Box_Simulations (BoxSimulationId, ActualPricePaid, BoxCostSaved, Tv, CallFixFr, CallMobFr, #FullSimulationId)
- Mobil_Simulations (MobilSimulationId, ActualPricePaid, MobilCostSaved, Engagement, CallsEurope, CallsInternational, NetInternational,BundleGo, #FullSimulationId)
- Gas_Simulations (GasSimulationId, ActualPricePaid, GasCostSaved, FloorSpace, HeatType, WaterCookingType, ResidentsNumber, GasUse, IsolationType, #FullSimulationId)
- Ele_Simulations (EleSimulationId, ActualPricePaid, EleCostSaved, FloorSpace, HeatType, WaterType, CookingType, ResidentsNumber, EleUse, IsolationType, #FullSimulationId)
- Box_Contracts (BoxContractId, Supplier, OfferName, PriceMonth, Commitment, InternetType, Tv, CallFixeFr, CallMobileFr, CallForeign, OpeningFee, TerminationFee)
- Mobil_Contracts (MobilContractId, Supplier, OfferName, LineServicePrice, SimCardPrice, Commitment, BundlePrice, BundleGbyte, CallsFrance, CallsEurope, GbyteEurope, CallsInternational, NetInternationalInternetType)
- Gas_Contracts (GasContractId, Supplier, OfferName, SubscriptionBasePerMonth, KwhBasePrice)
- Ele_Contracts (EleContractId, Supplier, OfferName, KvaPower, SubscriptionBasePerMonth, KwhBasePrice)
- 1_COMPARAISON (#GasSimulationId, #GasContractId, Savings)
- 2_COMPARAISON (#EleSimulationId, #EleContractId, Savings)
- 3_COMPARAISON (#BoxSimulationId, #BoxContractId, Savings)
- 4_COMPARAISON (#MobilSimulationId, #MobilContractId, Savings)