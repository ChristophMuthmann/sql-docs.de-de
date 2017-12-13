---
title: DataSources-Objekt (TMSL) | Microsoft Docs
ms.custom: 
ms.date: 05/30/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 1357ae7e-30a4-481a-831c-7b046fe15aa4
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d1a28cf4fcb0f9cd7ba5d00f74e6957302768c17
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="datasources-object-tmsl"></a>DataSources-Objekt (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Definiert eine Verbindung mit einer Datenquelle, die vom Modell entweder während des Imports zum Hinzufügen von Daten für das Modell oder in Pass-through-Abfragen über DirectQuery-Modus verwendet werden.  Modelle im DirectQuery-Modus können nur einen haben **DataSource** Objekt.  
  
 Es sei denn, Sie erstellen, und Ersetzen Sie dabei, oder ändern das Datenquellenobjekt selbst, einer beliebigen Datenquelle verwiesen wird, in Ihrem Skript (z. B. in der Partition Skript) muss eine vorhandene **DataSource** Objekt in Ihrem Modell.  
  
## <a name="object-definition"></a>Objektdefinition  
 Alle Objekte verfügen über einen gemeinsamen Satz von Eigenschaften, einschließlich Name, Typ, Beschreibung, eine eigenschaftsauflistung und Anmerkungen. **DataSource** Objekte verfügen außerdem über die folgenden Eigenschaften.  
  
 Typ  
 Der DataSource-Typ. Derzeit ist der einzige gültige Wert Provider (1) - normale Verbindungszeichenfolge.  
  
 connectionString  
 Die Verbindungszeichenfolge, die minimal gibt den Server und die Datenbank, jedoch kann auch andere Eigenschaften, die von der externen RDBMS, z. B. eine Daten-Anbieter oder ein Benutzerkonto unterstützt einschließen. Dieser Wert ist erforderlich. Finden Sie unter ["SqlConnectionStringBuilder"-Klasse](https://msdn.microsoft.com/en-us/library/ms254500\(v=vs.110\).aspx) ausführliche Informationen zu SQL Server-Datenbank-Verbindungszeichenfolgen-Eigenschaften.  
  
 ImpersonationMode-Wert  
 Gibt an, ob Analysis Services die Identität des Benutzers, der die Abfrage anfordert Identitätswechsel verwenden soll. Diese Eigenschaft ist ein numerischer Wert, der angibt, die Anmeldeinformationen für den Identitätswechsel verwenden. Folgende Enumerationswerte sind möglich:  
  
-   Standard (1) - Server verwendet die identitätswechselmethode, die es hält für den Kontext geeignet sein, in dem der Identitätswechsel verwendet wird.  
  
-   ImpersonateAccount (2) - Server verwendet das angegebene Benutzerkonto.  
  
-   ImpersonateAnonymous (3) - verwendet der Server das anonyme Benutzerkonto an.  Diese Option wird nicht empfohlen, aber manchmal in HTTP-Szenarien verwendet, durch benutzerdefinierte Anwendungen, die die Authentifizierung ausführen.  
  
-   ImpersonateCurrentUser (4) - Server verwendet das Benutzerkonto, dem der Client als eine Verbindung herstellt.  
  
-   Konfiguriert (5) - ImpersonateServiceAccount verwendet der Server das Benutzerkonto, dem als der Server ausgeführt wird.  
  
-   ImpersonateUnattendedAccount (6) – wird verwendet, auf der Server ein unbeaufsichtigtes Benutzerkonto. Dies wird für Power Pivot und tabellarischen Modellen verwendet, die in einer SharePoint-Umgebung ausgeführt.  
  
 DirectQuery-Modus kann ImpersonateCurrentuser verwenden, wenn Analysis Services für die vertrauenswürdige Delegierung konfiguriert ist oder  
                      konfiguriert ImpersonateServiceAccount, wenn die abfrageanforderung im Sicherheitskontext des Analysis Services-Dienstkontos ausgeführt wird. Finden Sie unter [Configure Analysis Services for Kerberos constrained Delegation](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md).  
  
 account  
 Für den Identitätswechsel verwendet. Ein Windows- oder Datenbank Konto mit einem gültigen Anmeldenamen mit Leseberechtigungen für die externe Datenbank an.  
  
 Kennwort  
 Eine verschlüsselte Zeichenfolge, die das Kennwort des Kontos.  
  
 maxConnections  
 Die maximale Anzahl von gleichzeitig mit der Datenquelle zu öffnenden Verbindungen.  
  
 isolation  
 Die Art der Isolation, die beim Ausführen von Befehlen für die Datenquelle verwendet wird. Gültige Werte sind ReadCommitted (1) oder Momentaufnahme (2).  
  
 timeout  
 Eine ganze Zahl, die angibt, das Timeout in Sekunden für Befehle in der Datenquelle ausgeführt werden.  
  
 Provider  
 Eine optionale Zeichenfolge, die den Namen des verwalteten Anbieters identifiziert für die Verbindung mit der relationalen Datenbank verwendet, wenn nicht anders angegeben, in der Verbindungszeichenfolge.  
  
## <a name="usage"></a>Verwendung  
 **DataSource** Objekte dienen [Alter-Befehl &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md), [Erstellen Befehl &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md), [CreateOrReplace-Befehl &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md), [Befehl &#40; löschen TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md), [Befehl &#40; aktualisieren TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md), und [MergePartitions-Befehl &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/mergepartitions-command-tmsl.md).  
  
 Ein **DataSource** Objekt ist eine Eigenschaft eines Modells, aber es kann auch als Eigenschaft eines Datenbankobjekts ausgehend von der 1: 1-Zuordnung zwischen Modell und Datenbank angegeben werden.  Geben Sie die Partitionen auf Grundlage der SQL-Abfragen auch eine **DataSource**, nur für einen reduzierten Satz von Eigenschaften.  
  
 Beim Erstellen, ersetzen oder ändern ein Datenquellenobjekt, geben Sie alle Lese-/ Schreibzugriff Eigenschaften der Objektdefinition. Eine Lese-/ Schreibzugriff-Eigenschaft nicht angegeben, gilt einen Löschvorgang.  
  
## <a name="examples"></a>Beispiele  
 **Beispiel 1** -eine Verbindung mit einem *FoodMart* Datenbank auf einer benannten Instanz von *Sales* auf einem Netzwerkserver mit dem Namen *"SERVER01"*.  
  
```  
"dataSources": [  
      {  
        "name": "SqlServer Server01 FoodMart",  
        "connectionString": "Provider=SQLNCLI11;Data Source=Server01\Sales;Initial Catalog=Foodmart;Integrated Security=SSPI;Persist Security Info=false",  
        "impersonationMode": "impersonateServiceAccount",  
      }  
]  
```  
  
## <a name="full-syntax"></a>Gesamte Syntax  
 Im folgenden ist die schemendarstellung des ein Datenquellenobjekt eines Modells.  
  
```  
"dataSources": {  
          "type": "array",  
          "items": {  
            "anyOf": [  
              {  
                "description": "ProviderDataSource object of Tabular Object Model (TOM)",  
                "type": "object",  
                "properties": {  
                  "name": {  
                    "type": "string"  
                  },  
                  "description": {  
                    "type": "string"  
                  },  
                  "type": {  
                    "enum": [  
                      "provider"  
                    ]  
                  },  
                  "connectionString": {  
                    "type": "string"  
                  },  
                  "impersonationMode": {  
                    "enum": [  
                      "default",  
                      "impersonateAccount",  
                      "impersonateAnonymous",  
                      "impersonateCurrentUser",  
                      "impersonateServiceAccount",  
                      "impersonateUnattendedAccount"  
                    ]  
                  },  
                  "account": {  
                    "type": "string"  
                  },  
                  "password": {  
                    "type": "string"  
                  },  
                  "maxConnections": {  
                    "type": "integer"  
                  },  
                  "isolation": {  
                    "enum": [  
                      "readCommitted",  
                      "snapshot"  
                    ]  
                  },  
                  "timeout": {  
                    "type": "integer"  
                  },  
                  "provider": {  
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
        },  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [DirectQuery-Modus &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Konfigurieren von HTTP-Zugriff auf Analysis Services unter Internetinformationsdienste &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
  
