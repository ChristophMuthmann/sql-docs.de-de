---
title: Refresh-Befehl (TMSL) | Microsoft Docs
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
ms.assetid: 97ff6ba8-c236-4ba6-8220-b0fcb9e1dc5c
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 001f9bcf731212b98070a6fb09e5f46206094394
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="refresh-command-tmsl"></a>Refresh-Befehl (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Verarbeitet Objekte in der aktuellen Datenbank.   
**Aktualisieren Sie** immer parallel ausgeführt werden, es sei denn, Sie ihn mit Drosselung [Sequence-Befehl &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/sequence-command-tmsl.md).  
  
 Sie können einige Eigenschaften einiger Objekte während eines Datenaktualisierungsvorgangs überschreiben:  
  
-   Ändern der **QueryDefinition** Eigenschaft von einem **Partition** Objekt zum Importieren von Daten mithilfe eines Ausdrucks für dynamische Filter.  
  
-   Geben Sie Anmeldeinformationen für die Datenquelle als Teil ein **aktualisieren** -Befehl, in der **"ConnectionString"** Eigenschaft eine **DataSource** Objekt. Dieser Ansatz kann werden als sicherer, Anmeldeinformationen zur Verfügung gestellt und vorübergehend für die Dauer des Vorgangs verwendet werden, anstatt gespeichert.  
  
 Finden Sie unter den Beispielen in diesem Thema veranschaulicht diese Eigenschaft überschreibt.  
  
> [!NOTE]  
>  Im Gegensatz zu mehrdimensionalen Verarbeitung gibt es keine spezielle Behandlung von Fehlern für die Verarbeitung von Tabellen bei der Verarbeitung.  

  
## <a name="request"></a>Anforderung  
 **Aktualisieren Sie** nimmt eine Typdefinition für Parameter und -Objekt.  
  
```  
    {  
        "refresh": {  
            "description": "Parameters of Refresh command of Analysis Services JSON API",  
            "properties": {  
            "type": {  
                "enum": [  
                "full",  
                "clearValues",  
                "calculate",  
                "dataOnly",  
                "automatic",  
                "add",  
                "defragment"  
                ]  
            },  
            "objects": {  
. . .   
```  
  
 Die **Typ** Parametersätze ein Bereichs auf den Verarbeitungsvorgang.  
  
||||  
|-|-|-|  
|**Aktualisierungstyp**|**Gilt für**|**Description**|  
|Volle|-Datenbank<br />Tabelle<br />Partition|Hiermit werden für alle Partitionen in der angegebenen Partition, Tabelle oder Datenbank die Daten aktualisiert und alle abhängigen Elemente neu berechnet. Hiermit werden für eine Berechnungspartition die Partition und alle abhängigen Elemente neu berechnet.|  
|clearValues|-Datenbank<br />Tabelle<br />Partition|Hiermit werden Werte in diesem Objekt und allen abhängigen Elementen gelöscht.|  
|berechnen|-Datenbank<br />Tabelle<br />Partition|Hiermit werden dieses Objekt und alle abhängigen Elemente neu berechnet, aber nur, wenn erforderlich. Dieser Wert erzwingt keine Neuberechnung, mit Ausnahme von veränderlichen Formeln.|  
|dataOnly|-Datenbank<br />Tabelle<br />Partition|Hiermit werden Daten in diesem Objekt aktualisiert und alle abhängigen Objekte gelöscht.|  
|automatic|-Datenbank<br />Tabelle<br />Partition|Wenn das Objekt aktualisiert und neu berechnet werden muss, werden hiermit das Objekt und alle abhängigen Elemente aktualisiert und neu berechnet. Gilt, wenn die Partition in einem anderen Zustand als „bereit“ ist.|  
|add|Partition|Hiermit werden Daten an diese Partition angehängt, und alle abhängigen Elemente werden neu berechnet. Dieser Befehl gilt nur für reguläre Partitionen, nicht für Berechnungspartitionen.|  
|Defragmentieren|-Datenbank<br />Tabelle|Hiermit werden die Daten in der angegebenen Tabelle defragmentiert. Beim Hinzufügen oder Entfernen von Daten zu bzw. aus einer Tabelle verbleiben in den Wörterbüchern für jede Spalte Werte, die nicht mehr in den tatsächlichen Spaltenwerten vorhanden sind. Die Defragmentierung bereinigt die Werte in den Wörterbüchern, die nicht mehr verwendet werden.|  
  
 Sie können die folgenden Objekte aktualisieren:  
  
 [Datenbankobjekt &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md) Verarbeiten eine Datenbank.  
  
```  
{  
  "refresh": {  
    "type": "automatic",  
    "objects": [  
      {  
        "database": "AdventureWorksTabular1200"  
      }  
    ]  
  }  
}  
```  
  
 [Tables-Objekt &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md) Verarbeiten eine einzelne Tabelle.  
  
```  
{  
  "refresh": {  
    "type": "automatic",  
    "objects": [  
      {  
        "database": "AdventureWorksTabular1200",  
        "table": "Date"  
      }  
    ]  
  }  
}  
```  
  
 [Partitionen Object &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md) Innerhalb einer Tabelle eine einzelne Partition zu verarbeiten.  
  
```  
{  
  "refresh": {  
    "type": "automatic",  
    "objects": [  
      {  
        "database": "AdventureWorksTabular1200",  
        "table": "FactSalesQuota",  
        "partition": "FactSalesQuota"  
      },  
      {  
        "database": "AdventureWorksTabular1200",  
        "table": "FactSalesQuota",  
        "partition": "FactSalesQuota - 2011"  
      }  
    ]  
  }  
}  
```  
  
## <a name="response"></a>Antwort  
 Gibt ein leeres Ergebnis zurück, wenn der Befehl erfolgreich abgeschlossen wurde. Andernfalls wird eine XMLA-Ausnahme zurückgegeben.  
  
## <a name="examples"></a>Beispiele  
 Überschreiben der **"ConnectionString"** und Abfragedefinition einer Partition.  
  
```  
{   
    "refresh": {   
        "type": "data",   
        "objects": [   
            {   
                "database": "tmtestdb",   
                "table": "sales"   
            },   
            {   
                "database": "tmtestdb",   
                "table": "customer"   
            }   
        ],   
        "overrides": [   
            {   
                "dataSources": [ // Bindings for Data Sources   
                    {   
                        "object": {   
                            "database": "tmtestdb",   
                            "dataSource": "contoso"   
                        },   
                        "dataSource": {   
                        "connectionString": "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=contoso;Integrated Security=SSPI;Persist Security Info=false"   
"   
                        }   
                    }   
                ],   
                "partitions": [ // Bindings for Partitions   
                    {   
                        "object": {   
                            "database": "tmtestdb",   
                            "table": "sales",   
                            "partition": "2015"   
                        },   
                        "partition": {   
                            "source": {   
                                "query": [  
                                     "SELECT sales.salesamount, customer.customername FROM sales",  
                                     "JOIN customer on custKey = sales.custkey",  
                                     "JOIN date on date.DateKey = customer.OrderDate",  
                                     "WHERE date.CalendarYear='2015'"  
                                  ],  
                            }   
                        }   
                    }   
                ]   
            }   
        ]   
    }   
}   
```  
  
 Bereich bestimmte überschreibt, indem Sie den Typparameter auf einen **DataOnly** aktualisieren, Metadaten bleibt intakt.  
  
```  
{   
        "refresh" : {   
            "type" : "dataOnly",   
            "objects" : [   
                {   
                    "database" : "TMTestDB",   
                    "table" : "Customer"   
                },   
                {   
                    "database" : "TMTestDB",   
                    "table" : "Sales"   
                }   
            ],   
            "overrides" : [{   
                "scope" : {   
                    "database" : "TMTestDB",   
                    "table" : "Sales"   
                },   
                "dataSources" : [{   
                    "originalObject" : {   
                        "dataSource" : "SqlServer sqlcldb2 AS_foodmart_2000"   
                    },   
                    "connectionString" : "Provider=SQLNCLI11;Data Source=sqlcldb2;Initial Catalog=AS_foodmart_2000;Integrated Security=SSPI;Persist Security Info=false"   
                }]   
            }]   
        }   
    }   
```  
  
## <a name="usage-endpoints"></a>Nutzung (Endpunkte)  
 Diese Command-Element wird in einer Anweisung verwendet die [Execute-Methode &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) Aufruf über einen XMLA-Endpunkt verfügbar gemacht werden auf folgende Weise:  
  
-   Als ein XMLA-Fenster in SQL Server Management Studio (SSMS)  
  
-   Als Eingabedatei für die **invoke-Ascmd** PowerShell-Cmdlet  
  
-   Als Eingabe für ein SSIS-Tasks oder SQL Server-Agent-Auftrag  
  
 Sie können ein vorgefertigtes Skript für diesen Befehl aus SSMS generieren.  Sie können z. B. Klicken die **Skript** in einem Dialogfeld für die Verarbeitung.  
  
 Die [ \[MS-SSAS-T\]: SQL Server Analysis Services-Tabellendatenbank (SQL Server Technische Protocol)](http://go.microsoft.com/fwlink/p/?LinkId=784855) Dokuments Abschnitt 3.1.5.2.2, die die Struktur der Befehle für JSON-tabellarischen Metadaten und Objekte beschreibt. Aktuell enthält dieses Dokument Befehle und Funktionen, die noch nicht im TMSL-Skript implementiert. Finden Sie unter ([Tabular Model Scripting Language &#40; TMSL &#41; Verweisen auf](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)) für Informationen zu den was unterstützt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Verarbeiten von Optionen und Einstellungen &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)  
  
  
