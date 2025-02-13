# Notes de rédaction.

Nous n'allons pas attaquer dirctement les TAGS
Ceux-ci sont réservés pour gérer l'interface et exécuter un test de fonctionnement.

Nous allons travailler avec la structure ``GVL_Abox.uaAboxInterface``, ce qui d'une certaine manière simplifie le travail, mais aussi garanti le cmême comportement avec l'interface côté PLC Siemens.

Nous travaillons dans le programme ``PLC_PRG``.

La SDS / DS est donnée avec les variables globales du type:

```iecst
emConveyor.cm01.bSensor := GVL_Abox.uaAboxInterface.uaDigitalIn.Input_0_4;	//  UA_DigitalInput_32_Input_0_4;
```