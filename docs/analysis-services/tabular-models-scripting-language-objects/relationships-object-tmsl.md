---
title: Beziehungen-Objekt (TMSL) | Microsoft Docs
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 7588565f-ea34-4402-8be9-331188bdb8c2
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b54b8749604cd8a5a17ee219326d814dc76131c4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="relationships-object-tmsl"></a>Beziehungen-Objekt (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Definiert eine Beziehung zwischen einer Quelle und Ziel-Tabelle die Möglichkeit, die Kardinalität angeben und die Richtung des Filter-Abfrage und Sicherheit.  
  
## <a name="object-definition"></a>Objektdefinition  
 Alle Objekte verfügen über einen gemeinsamen Satz von Eigenschaften, einschließlich Name, Typ, Beschreibung, eine eigenschaftsauflistung und Anmerkungen. **Beziehung** Objekte verfügen außerdem über die folgenden Eigenschaften.  
  
 isActive  
 Ein boolescher Wert, der angibt, ob die Beziehung als aktiv oder inaktiv gekennzeichnet ist. Eine aktive Beziehung wird automatisch zum Filtern von Tabellen verwendet. Eine inaktive Beziehung kann explizit über die USERELATIONSHIP-Funktion von DAX-Berechnungen verwendet werden.  
  
 crossFilteringBehavior  
 Gibt an, wie Beziehungen das Filtern von Daten beeinflussen. Finden Sie unter [bidirektionale kreuzfilter für tabellarische Modelle in SQL Server 2016 Analysis Services](../../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) für Weitere Informationen. Gültige Werte sind:  
  
-   OneDirection (1) – "To" am Ende der Beziehung ausgewählten Zeilen filtern automatisch Scans der Tabelle "Von" am Ende der Beziehung.  
  
-   Werden (2): wird an beiden Enden der Beziehung automatisch die andere Tabelle gefiltert.  
  
-   Automatic (3) – das Modul analysiert die Beziehungen und wählen Sie eine der Verhalten mithilfe von Heuristik.  
  
 joinOnDateBehavior  
 Gibt bei der Verknüpfung von zwei Datums-/Uhrzeitspalten an, ob Datums- und Uhrzeitbestandteile oder nur Datumsbestandteile verknüpft werden sollen.  
  
-   DateAndTime (1) - beim Verknüpfen von zwei Datums-/ Uhrzeitspalten verknüpfen auf Datums- und Uhrzeitteile.  
  
-   DatePartOnly (2): bei der Verbindung von zwei Datums-/ Uhrzeitspalten nur verknüpfen.  
  
 relyOnReferentialIntegrity  
 Nicht verwendet, für künftige Verwendung vorbehalten.  
  
 securityFilteringBehavior  
 Eine Enumeration, die angibt, wie Beziehungen das Filtern von Daten beim Auswerten von Ausdrücken für Sicherheit auf Zeilenebene beeinflussen. Gültige Werte sind:  
  
-   OneDirection (1) – "To" am Ende der Beziehung ausgewählten Zeilen filtern automatisch Scans der Tabelle "Von" am Ende der Beziehung.  
  
-   Werden (2): wird an beiden Enden der Beziehung automatisch die andere Tabelle gefiltert.  
  
## <a name="usage"></a>Verwendung  
 Beziehungsobjekte kommen in [Alter-Befehl &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md), [Erstellen Befehl &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md), [CreateOrReplace-Befehl &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md), und [Befehl &#40; löschen TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md).  
  
 Beim Erstellen, ersetzen oder Ändern eines Relationship-Objekts geben Sie alle Lese-/ Schreibzugriff Eigenschaften der Objektdefinition. Eine Lese-/ Schreibzugriff-Eigenschaft nicht angegeben, gilt einen Löschvorgang.  
  
## <a name="full-syntax"></a>Gesamte Syntax  
 Im folgenden ist das schemendarstellung eines Relationship-Objekts.  
  
```  
"relationships": {  
          "type": "array",  
          "items": {  
            "anyOf": [  
              {  
                "description": "SingleColumnRelationship object of Tabular Object Model (TOM)",  
                "type": "object",  
                "properties": {  
                  "name": {  
                    "type": "string"  
                  },  
                  "isActive": {  
                    "type": "boolean"  
                  },  
                  "type": {  
                    "enum": [  
                      "singleColumn"  
                    ]  
                  },  
                  "crossFilteringBehavior": {  
                    "enum": [  
                      "oneDirection",  
                      "bothDirections",  
                      "automatic"  
                    ]  
                  },  
                  "joinOnDateBehavior": {  
                    "enum": [  
                      "dateAndTime",  
                      "datePartOnly"  
                    ]  
                  },  
                  "relyOnReferentialIntegrity": {  
                    "type": "boolean"  
                  },  
                  "securityFilteringBehavior": {  
                    "enum": [  
                      "oneDirection",  
                      "bothDirections"  
                    ]  
                  },  
                  "fromCardinality": {  
                    "enum": [  
                      "none",  
                      "one",  
                      "many"  
                    ]  
                  },  
                  "toCardinality": {  
                    "enum": [  
                      "none",  
                      "one",  
                      "many"  
                    ]  
                  },  
                  "fromColumn": {  
                    "type": "string"  
                  },  
                  "fromTable": {  
                    "type": "string"  
                  },  
                  "toColumn": {  
                    "type": "string"  
                  },  
                  "toTable": {  
                    "type": "string"  
                  },  
                  "annotations": {  
                    "type": "array",  
                    "items": {  
                      "description": "Annotation object of Tabular Object Model (TOM)",  
                      "type": "object",  
                      "properties": {  
                        "name": {  
                          "type": "string"  
                        },  
                        "value": {  
                          "anyOf": [  
                            {  
                              "type": "string"  
                            },  
                            {  
                              "type": "array",  
                              "items": {  
                                "type": "string"  
                              }  
                            }  
                          ]  
                        }  
                      },  
                      "additionalProperties": false  
                    }  
                  }  
                },  
                "additionalProperties": false  
              }  
            ]  
          }  
        }  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Beziehungen erstellen](../../integration-services/data-flow/transformations/create-relationships.md)  
  
  
