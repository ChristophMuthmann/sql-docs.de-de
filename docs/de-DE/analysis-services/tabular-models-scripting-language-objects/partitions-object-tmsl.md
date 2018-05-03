---
title: Partitionen-Objekt (TMSL) | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: df1da0d2-d824-42ba-b9dc-47fbd8edc10f
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bc820929603cadb400bd19f3afa4d04a6222fb89
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="partitions-object-tmsl"></a>Partitionen-Objekt (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Definiert eine Partition oder logische Segmentierung, der das Rowset für die Tabelle. Eine Partition besteht aus einer SQL-Abfrage zum Importieren von Daten für die Beispieldaten in der modellierungsumgebung oder als vollständige Abfrage für Pass-through-Ausführung von Abfragen über DirectQuery verwendet.  
  
 Eigenschaften für die Partition wird bestimmt, wie die Daten für die Tabelle als Quelle fungiert.  In der Objekthierarchie ist das übergeordnete Objekt einer Partition ein Table-Objekt.  
  
## <a name="object-definition"></a>Objektdefinition  
 Alle Objekte verfügen über einen gemeinsamen Satz von Eigenschaften, einschließlich Name, Typ, Beschreibung, eine eigenschaftsauflistung und Anmerkungen. **Partition** Objekte verfügen außerdem über die folgenden Eigenschaften.  
  
 Typ  
 Der Typ der Partition. Gültige Werte sind numerisch und umfassen Folgendes:  
  
-   Daten in dieser Partition-Abfragen (1) – wird abgerufen, indem Sie eine Abfrage für eine **DataSource**. Die **DataSource** muss eine Datenquelle, die in der Datei model.bim definiert sein.  
  
-   Berechnete (2) – werden Daten in dieser Partition durch Ausführen eines berechneten Ausdrucks aufgefüllt.  
  
-   None (3) – Daten in dieser Partition werden ausgefüllt, indem ein Rowset von Daten auf dem Server als Teil des Aktualisierungsvorgangs übertragen werden.  
  
 mode  
 Definiert den Abfragemodus der Partition an. Gültige Werte sind **importieren**, **DirectQuery**, oder **Standard** (geerbt). Dieser Wert ist erforderlich.  
  
|||  
|-|-|  
|**Importieren**|Gibt die Abfrage, die Anforderungen für die in-Memory-Analysemodul Speichern von importierten Daten ausgegeben werden.|  
|**DirectQuery**|Pass-through Ausführung von Abfragen für eine externe relationale Datenbank. DirectQuery-Modus verwendet Partitionen, um Beispieldaten verwendet, die während des Modellentwurfs bereitzustellen. Wenn auf einem Produktionsserver bereitgestellt wird, sollten Sie zurück zum vollständigen Datenansicht wechseln. Denken Sie daran, dass DirectQuery-Modus eine Partition pro Tabelle und eine Datenquelle pro Modell erforderlich ist.|  
|**default**|Legen Sie diese Option, wenn Sie weiter oben in der Objektstruktur auf das Modell oder Datenbankebene Modi wechseln möchten. Wenn Sie die Standardeinstellung auswählen, werden der Abfragemodus Import oder DirectQuery.|  
  
 Quelle  
 Gibt den Ort der Daten abgefragt werden. Gültige Werte sind **Abfrage berechnet**, oder **keine**. Dieser Wert ist erforderlich.  
  
|||  
|-|-|  
|**Keine**|Zum Modus "Import", wobei Daten geladen und im Arbeitsspeicher gespeichert.|  
|**query**|Für DirectQuery-Modus ist dies eine SQL-Abfrage, die in der relationalen Datenbank in des Modells angegeben ausgeführt **DataSource**. Finden Sie unter [DataSources Objekt &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md).|  
|**Berechnet**|Berechnete Tabellen stammen aus einem Ausdruck angegeben wird, wenn die Tabelle erstellt wird. Dieser Ausdruck wird die Quelle der für die berechnete Tabelle erstellte Partition betrachtet.|  
  
 "DataView"  
 Für DirectQuery-Partitionen wird eine zusätzliche DataView-Eigenschaft, ob die Abfrage, die Daten abruft eine Stichprobe oder des vollständigen Datasets. Gültige Werte sind **vollständige**, **Beispiel**, oder **Standard** (geerbt). Wie bereits erwähnt, werden nur während der datenmodellierung und Testen der Beispiele verwendet. Finden Sie unter [Hinzufügen von Beispieldaten zu einem DirectQuery-Modell im Entwurfsmodus](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md) für Weitere Informationen.  
  
## <a name="usage"></a>Verwendung  
 Partition-Objekten dienen [Alter-Befehl &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md), [Create-Befehl &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md), [CreateOrReplace-Befehl &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md), [Delete-Befehl &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md), [Refresh-Befehl &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md), und [MergePartitions-Befehl &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/mergepartitions-command-tmsl.md).  
  
 Beim Erstellen, ersetzen oder ändern ein Partition-Objekt, geben Sie alle Lese-/ Schreibzugriff Eigenschaften der Objektdefinition. Eine Lese-/ Schreibzugriff-Eigenschaft nicht angegeben, gilt einen Löschvorgang. Lese-/ Schreibzugriff Eigenschaften gehören Name, Beschreibung, Modus und Quelle.  
  
## <a name="examples"></a>Beispiele  
 **Beispiel 1** – einen einfachen Partitionsstruktur einer Tabelle (nicht auf eine Faktentabelle).  
  
```  
"partitions": [  
          {  
            "name": "Customer",  
            "source": {  
              "query": "SELECT [dbo].[Customer].* FROM [dbo].[Customer]",  
              "dataSource": "SqlServer localhost FoodmartDB"  
            }  
]  
```  
  
 **Beispiel 2** - partitionierte Faktendaten basiert normalerweise auf einer WHERE-Klausel, die nicht überlappende Partitionen für Daten aus derselben Tabelle erstellt.  
  
```  
"partitions": [  
          {  
            "name": "sales_fact_2015",  
            "source": {  
              "query": "SELECT [dbo].[sales_fact_2015].* FROM [dbo].[sales_fact_2015] WHERE [dbo].[sales_fact_2015].[Quarter]=4",                                                                                          
              "dataSource": "SqlServer localhost FoodmartDB"  
            },  
          }  
        ]  
```  
  
 **Beispiel 3** -eine berechnete Tabelle basierend auf einer DAX-Ausdruck.  
  
```  
"partitions": [  
          {  
            "name": "CalcTable1",  
            "source": {  
              "type": "calculated",  
              "expression": "'Product Class'"  
            },  
            }  
]  
```  
  
## <a name="full-syntax"></a>Vollständige Syntax  
 Im folgenden ist die schemendarstellung eines Partition-Objekts.  
  
```  
"partitions": {  
                "type": "array",  
                "items": {  
                  "description": "Partition object of Tabular Object Model (TOM)",  
                  "type": "object",  
                  "properties": {  
                    "name": {  
                      "type": "string"  
                    },  
                    "description": {  
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
                    },  
                    "mode": {  
                      "enum": [  
                        "import",  
                        "directQuery",  
                        "default"  
                      ]  
                    },  
                    "dataView": {  
                      "enum": [  
                        "full",  
                        "sample",  
                        "default"  
                      ]  
                    },  
                    "source": {  
                      "anyOf": [  
                        {  
                          "description": "QueryPartitionSource object of Tabular Object Model (TOM)",  
                          "type": "object",  
                          "properties": {  
                            "type": {  
                              "enum": [  
                                "query",  
                                "calculated",  
                                "none"  
                              ]  
                            },  
                            "query": {  
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
                            },  
                            "dataSource": {  
                              "type": "string"  
                            }  
                          },  
                          "additionalProperties": false  
                        },  
                        {  
                          "description": "CalculatedPartitionSource object of Tabular Object Model (TOM)",  
                          "type": "object",  
                          "properties": {  
                            "type": {  
                              "enum": [  
                                "query",  
                                "calculated",  
                                "none"  
                              ]  
                            },  
                            "expression": {  
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
                      ]  
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
              },  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
