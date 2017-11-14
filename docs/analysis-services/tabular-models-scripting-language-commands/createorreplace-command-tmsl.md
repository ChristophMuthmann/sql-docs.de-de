---
title: CreateOrReplace-Befehl (TMSL) | Microsoft Docs
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
ms.assetid: f77a0e04-461a-4fa8-b997-78057e410d56
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 62d90be2b4fe8aea96534c7c4d8b2b4617ac1ea1
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="createorreplace-command-tmsl"></a>CreateOrReplace-Befehl (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Erstellt oder ersetzt das angegebene Objekt und alle untergeordneten Objekte, die angegeben werden. Nicht vorhandene Objekte werden erstellt. Vorhandene Objekte werden mit der neuen Definition ersetzt.  
  
 Wenn Sie eine Schreib /-Leseeigenschaft angeben, müssen Sie alle diese implizit enthalten. Die Auslassung eines Objekts Lese-/ Schreibzugriff gilt einen Löschvorgang.  
  
## <a name="request"></a>Anforderung  
 Die Struktur der Anforderung hängt von dem Objekt ab. Ein Objekt, das ein übergeordnetes Element ist muss alle seine untergeordneten Elemente enthalten, obwohl die vollständige Objektdefinitionen von gleichgeordneten Elementen und Eltern nicht erforderlich sind.  
  
 [Datenbankobjekt &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md)  
  
 Ersetzt eine vorhandene Datenbank mit einer umbenannten, minimale Datenbankdefinition, die den Namen, geänderten Modelleigenschaften und eine Verbindung angibt. Da die Objektdefinition keine Tabellen, Partitionen oder Beziehungen enthalten, werden all diese Objekte gelöscht.  
  
```  
{  
  "createOrReplace": {  
    "object": {  
      "database": "AdventureWorksTabular1200"  
    },  
    "database": {  
      "name": "TestCreateOrReplaceDB",  
      "id": "newID",  
      "compatibilityLevel": 1200,  
      "model": {  
        "defaultMode": "import",  
        "culture": "en-US",  
        "dataSources": [  
          {  
            "name": "SqlServer localhost AdventureworksDW2016",  
            "connectionString": "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=AdventureworksDW2016;Integrated Security=SSPI;Persist Security Info=false",  
            "impersonationMode": "impersonateAccount",  
            "account": "   ",  
            "annotations": [  
              {  
                "name": "ConnectionEditUISource",  
                "value": "SqlServer"  
              }  
            ]  
          }  
        ]  
      }  
    }  
  }  
}  
```  
  
 [DataSources Object &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md) Ein Verbindungsname ersetzt.  
  
```  
{  
  "createOrReplace": {  
    "object": {  
      "database": "TestCreateOrReplaceDB",  
      "dataSource": "SqlServer localhost AdventureworksDW2016"  
    },  
    "dataSource": {  
      "name": "New connection name",  
      "connectionString": "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=AdventureworksDW2016;Integrated Security=SSPI;Persist Security Info=false",  
      "impersonationMode": "impersonateAccount",  
      "account": "   ",  
      "annotations": [  
        {  
          "name": "ConnectionEditUISource",  
          "value": "SqlServer"  
        }  
      ]  
    }  
  }  
}  
```  
  
 [Tables-Objekt &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md) Überschreibt vorhandenen Tabellen, nur die angegebene Aktivität zu verlassen.  
  
```  
{  
  "createOrReplace": {  
    "object": {  
      "database": "AdventureWorksTabular1200"  
    },  
    "database": {  
      "name": "AdventureWorksTabular1200",  
      "id": "New-AdventureWorksTabular1200",  
      "compatibilityLevel": 1200,  
      "model": {  
        "defaultMode": "import",  
        "culture": "en-US",  
        "dataSources": [  
          {  
            "name": "SqlServer localhost AdventureworksDW2016",  
            "connectionString": "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=AdventureworksDW2016;Integrated Security=SSPI;Persist Security Info=false",  
            "impersonationMode": "impersonateAccount",  
            "account": "   ",  
            "annotations": [  
              {  
                "name": "ConnectionEditUISource",  
                "value": "SqlServer"  
              }  
            ]  
          }  
        ],  
        "tables": [  
          {  
            "name": "Date",  
            "columns": [  
              {  
                "name": "DateKey",  
                "dataType": "int64",  
                "sourceColumn": "DateKey",  
                "sourceProviderType": "Integer"  
              },  
              {  
                "name": "FullDateAlternateKey",  
                "dataType": "dateTime",  
                "sourceColumn": "FullDateAlternateKey",  
                "formatString": "General Date",  
                "sourceProviderType": "DBDate"  
              },  
              {  
                "name": "CalendarYear",  
                "dataType": "int64",  
                "sourceColumn": "CalendarYear",  
                "sourceProviderType": "SmallInt"  
              }  
            ],  
            "partitions": [  
              {  
                "name": "DimDate",  
                "dataView": "full",  
                "source": {  
                  "query": " SELECT [dbo].[DimDate].* FROM [dbo].[DimDate] ",  
                  "dataSource": "SqlServer localhost AdventureworksDW2016"  
                }  
              }  
            ],  
            "annotations": [  
              {  
                "name": "_TM_ExtProp_QueryDefinition",  
                "value": " SELECT [dbo].[DimDate].* FROM [dbo].[DimDate] "  
              },  
              {  
                "name": "_TM_ExtProp_DbTableName",  
                "value": "DimDate"  
              },  
              {  
                "name": "_TM_ExtProp_DbSchemaName",  
                "value": "dbo"  
              }  
            ]  
          }  
        ]  
     }  
   }  
 }  
}   
```  
  
 [Partitionen Object &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md)  
  
 Ersetzen Sie einen Partitionsnamen an. Partitionsobjekte verfügen über drei Lese-/ Schreibzugriff-Eigenschaften: name, Quelle und Beschreibung. Wenn Sie eine Schreib /-Leseeigenschaft angeben, müssen Sie alle diese implizit enthalten. Die Auslassung eines Objekts Lese-/ Schreibzugriff gilt einen Löschvorgang.  
  
 Da die Definition des Objekts die Partition ist, wird nur die benannten Partition und die Definition beeinträchtigt. Andere Tabellen, Beziehungen und Partitionen sind nicht betroffen.  
  
 Es sei denn, Sie erstellen, und Ersetzen Sie dabei, oder ändern das Datenquellenobjekt selbst, einer beliebigen Datenquelle verwiesen wird, in Ihrem Skript (z. B. in das unten gezeigte Skript Partition) muss eine vorhandene **DataSource** Objekt in Ihrem Modell. Wenn Sie die Datenquelle ändern müssen, fügen Sie ihn auf  
  
```  
{  
  "createOrReplace": {  
    "object": {  
      "database": "AdventureWorksTabular1200",  
      "table": "FactSalesQuota",  
      "partition": "FactSalesQuota - 2011"  
    },  
    "partition": {  
      "name": "Sales Quota for 2011",  
      "mode": "import",  
      "dataView": "full",  
      "source": {  
        "query": [  
          "SELECT [dbo].[FactSalesQuota].* FROM [dbo].[FactSalesQuota]",  
          "JOIN DimDate as DD",  
          "on DD.DateKey = FactSalesQuota.DateKey",  
          "WHERE DD.CalendarYear='2011'"  
        ],  
        "dataSource": "SqlServer localhost AdventureworksDW2016"  
      }  
    }  
  }  
}  
```  
  
 [Rollen Object &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md) Ersetzt eine Rollendefinition durch die Elemente enthält.  
  
```  
{  
  "createOrReplace": {  
    "object": {  
      "database": "AdventureWorksTabular1200",  
      "role": "DataReader"  
    },  
    "role": {  
      "name": "DataReader",  
      "modelPermission": "read",  
      "members": [  
        {  
          "memberName": "ADVENTUREWORKS\\InternalSalesGrp"  
        }  
      ]  
    }  
  }  
}  
```  
  
## <a name="response"></a>Antwort  
 Gibt ein leeres Ergebnis zurück, wenn der Befehl erfolgreich abgeschlossen wurde. Andernfalls wird eine XMLA-Ausnahme zurückgegeben.  
  
## <a name="examples"></a>Beispiele  
 **Beispiel 1** -erstellt eine neue Datenbank, eine vorhandene Datenbank mit demselben Namen überschreiben.  
  
```  
{  
  "createOrReplace": {  
    "object": {  
      "database": "AdventureWorksTabular1200"  
    },  
    "database": {  
      "name": "AdventureWorksTabular1200",  
      "id": "AdventureWorksTabular1200",  
      "compatibilityLevel": 1200,  
      "model": {  
        "defaultMode": "directQuery",  
        "culture": "en-US",  
        "dataSources": [  
          {  
            "name": "SqlServer localhost AdventureworksDW2016",  
            "connectionString": "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=AdventureworksDW2016;Integrated Security=SSPI;Persist Security Info=false",  
            "impersonationMode": "impersonateAccount",  
            "account": "   ",  
            "annotations": [  
              {  
                "name": "ConnectionEditUISource",  
                "value": "SqlServer"  
              }  
            ]  
          }  
        ],  
        "tables": [  
          {  
            "name": "DimDate",  
            "columns": [  
              {  
                "name": "DateKey",  
                "dataType": "int64",  
                "sourceColumn": "DateKey",  
                "sourceProviderType": "Integer"  
              },  
              {  
                "name": "FullDateAlternateKey",  
                "dataType": "dateTime",  
                "sourceColumn": "FullDateAlternateKey",  
                "formatString": "General Date",  
                "sourceProviderType": "DBDate"  
              },  
              {  
                "name": "CalendarYear",  
                "dataType": "int64",  
                "sourceColumn": "CalendarYear",  
                "sourceProviderType": "SmallInt"  
              }  
            ],  
            "partitions": [  
              {  
                "name": "DimDate",  
                "dataView": "full",  
                "source": {  
                  "query": " SELECT [dbo].[DimDate].* FROM [dbo].[DimDate] ",  
                  "dataSource": "SqlServer localhost AdventureworksDW2016"  
                }  
              }  
            ],  
            "annotations": [  
              {  
                "name": "_TM_ExtProp_QueryDefinition",  
                "value": " SELECT [dbo].[DimDate].* FROM [dbo].[DimDate] "  
              },  
              {  
                "name": "_TM_ExtProp_DbTableName",  
                "value": "DimDate"  
              },  
              {  
                "name": "_TM_ExtProp_DbSchemaName",  
                "value": "dbo"  
              }  
            ]  
          },  
          {  
            "name": "DimEmployee",  
            "columns": [  
              {  
                "name": "EmployeeKey",  
                "dataType": "int64",  
                "sourceColumn": "EmployeeKey",  
                "sourceProviderType": "Integer"  
              },  
              {  
                "name": "SalesTerritoryKey",  
                "dataType": "int64",  
                "sourceColumn": "SalesTerritoryKey",  
                "sourceProviderType": "Integer"  
              },  
              {  
                "name": "FirstName",  
                "dataType": "string",  
                "sourceColumn": "FirstName",  
                "sourceProviderType": "WChar"  
              },  
              {  
                "name": "LastName",  
                "dataType": "string",  
                "sourceColumn": "LastName",  
                "sourceProviderType": "WChar"  
              },  
              {  
                "name": "MiddleName",  
                "dataType": "string",  
                "sourceColumn": "MiddleName",  
                "sourceProviderType": "WChar"  
              },  
              {  
                "name": "SalesPersonFlag",  
                "dataType": "boolean",  
                "sourceColumn": "SalesPersonFlag",  
                "formatString": "\"TRUE\";\"TRUE\";\"FALSE\"",  
                "sourceProviderType": "Boolean"  
              },  
              {  
                "name": "DepartmentName",  
                "dataType": "string",  
                "sourceColumn": "DepartmentName",  
                "sourceProviderType": "WChar"  
              }  
            ],  
            "partitions": [  
              {  
                "name": "DimEmployee",  
                "dataView": "full",  
                "source": {  
                  "query": " SELECT [dbo].[DimEmployee].* FROM [dbo].[DimEmployee] ",  
                  "dataSource": "SqlServer localhost AdventureworksDW2016"  
                }  
              }  
            ],  
            "annotations": [  
              {  
                "name": "_TM_ExtProp_QueryDefinition",  
                "value": " SELECT [dbo].[DimEmployee].* FROM [dbo].[DimEmployee] "  
              },  
              {  
                "name": "_TM_ExtProp_DbTableName",  
                "value": "DimEmployee"  
              },  
              {  
                "name": "_TM_ExtProp_DbSchemaName",  
                "value": "dbo"  
              }  
            ]  
          },  
          {  
            "name": "FactSalesQuota",  
            "columns": [  
              {  
                "name": "SalesQuotaKey",  
                "dataType": "int64",  
                "sourceColumn": "SalesQuotaKey",  
                "sourceProviderType": "Integer"  
              },  
              {  
                "name": "EmployeeKey",  
                "dataType": "int64",  
                "sourceColumn": "EmployeeKey",  
                "sourceProviderType": "Integer"  
              },  
              {  
                "name": "DateKey",  
                "dataType": "int64",  
                "sourceColumn": "DateKey",  
                "sourceProviderType": "Integer"  
              },  
              {  
                "name": "CalendarYear",  
                "dataType": "int64",  
                "sourceColumn": "CalendarYear",  
                "sourceProviderType": "SmallInt"  
              },  
              {  
                "name": "SalesAmountQuota",  
                "dataType": "decimal",  
                "sourceColumn": "SalesAmountQuota",  
                "formatString": "\\$#,0.00;(\\$#,0.00);\\$#,0.00",  
                "sourceProviderType": "Currency",  
                "annotations": [  
                  {  
                    "name": "Format",  
                    "value": "\<Format Format=\"Currency\" Accuracy=\"2\" ThousandSeparator=\"True\">\<Currency LCID=\"1033\" DisplayName=\"$ English (United States)\" Symbol=\"$\" PositivePattern=\"0\" NegativePattern=\"0\" /></Format>"  
                  }  
                ]  
              },  
              {  
                "name": "Date",  
                "dataType": "dateTime",  
                "sourceColumn": "Date",  
                "formatString": "General Date",  
                "sourceProviderType": "DBTimeStamp"  
              }  
            ],  
            "partitions": [  
              {  
                "name": "FactSalesQuota",  
                "dataView": "full",  
                "source": {  
                  "query": " SELECT [dbo].[FactSalesQuota].* FROM [dbo].[FactSalesQuota] ",  
                  "dataSource": "SqlServer localhost AdventureworksDW2016"  
                }  
              },  
              {  
                "name": "FactSalesQuota - 2011",  
                "mode": "import",  
                "dataView": "sample",  
                "source": {  
                  "query": [  
                    "SELECT [dbo].[FactSalesQuota].* FROM [dbo].[FactSalesQuota]",  
                    "JOIN DimDate as DD",  
                    "on DD.DateKey = FactSalesQuota.DateKey",  
                    "WHERE DD.CalendarYear='2011'"  
                  ],  
                  "dataSource": "SqlServer localhost AdventureworksDW2016"  
                },  
                "annotations": [  
                  {  
                    "name": "QueryEditorSerialization",  
                    "value": [  
                      "\<?xml version=\"1.0\" encoding=\"UTF-16\"?>\<Gemini xmlns=\"QueryEditorSerialization\"><AnnotationContent><![CDATA[<RSQueryCommandText>SELECT [dbo].[FactSalesQuota].* FROM [dbo].[FactSalesQuota]",  
                      "JOIN DimDate as DD",  
                      "on DD.DateKey = FactSalesQuota.DateKey",  
                      "WHERE DD.CalendarYear='2011'</RSQueryCommandText><RSQueryCommandType>Text</RSQueryCommandType><RSQueryDesignState></RSQueryDesignState>]]></AnnotationContent></Gemini>"  
                    ]  
                  }  
                ]  
              }  
            ],  
            "annotations": [  
              {  
                "name": "_TM_ExtProp_QueryDefinition",  
                "value": " SELECT [dbo].[FactSalesQuota].* FROM [dbo].[FactSalesQuota] "  
              },  
              {  
                "name": "_TM_ExtProp_DbTableName",  
                "value": "FactSalesQuota"  
              },  
              {  
                "name": "_TM_ExtProp_DbSchemaName",  
                "value": "dbo"  
              }  
            ]  
          }  
        ],  
        "relationships": [  
          {  
            "name": "4426b078-193f-4a59-bc52-33f990bfb7da",  
            "fromTable": "FactSalesQuota",  
            "fromColumn": "DateKey",  
            "toTable": "DimDate",  
            "toColumn": "DateKey"  
          },  
          {  
            "name": "cde1e139-4553-4d0a-a025-1cd98e35aab2",  
            "fromTable": "FactSalesQuota",  
            "fromColumn": "EmployeeKey",  
            "toTable": "DimEmployee",  
            "toColumn": "EmployeeKey"  
          }  
        ]  
      }  
    }  
  }  
}  
  
```  
  
## <a name="usage-endpoints"></a>Nutzung (Endpunkte)  
 Diese Command-Element wird in einer Anweisung verwendet die [Execute-Methode &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) Aufruf über einen XMLA-Endpunkt verfügbar gemacht werden auf folgende Weise:  
  
-   Als ein XMLA-Fenster in SQL Server Management Studio (SSMS)  
  
-   Als Eingabedatei für die **invoke-Ascmd** PowerShell-Cmdlet  
  
-   Als Eingabe für ein SSIS-Tasks oder SQL Server-Agent-Auftrag  
  
 Sie können ein vorgefertigtes Skript für diesen Befehl aus SSMS generieren.  Beispielsweise können Sie eine vorhandene Datenbank auf Rechtsklicken > **Skript** > **Skript für Datenbank als** > **erstellen oder zu ersetzen,**.  
  
 Die [ \[MS-SSAS-T\]: SQL Server Analysis Services-Tabellendatenbank (SQL Server Technische Protocol)](http://go.microsoft.com/fwlink/p/?LinkId=784855) Dokuments Abschnitt 3.1.5.2.2, die die Struktur der Befehle für JSON-tabellarischen Metadaten und Objekte beschreibt. Aktuell enthält dieses Dokument Befehle und Funktionen, die noch nicht im TMSL-Skript implementiert. Finden Sie unter [Tabular Model Scripting Language &#40; TMSL &#41; Verweis](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) für Informationen zu den was unterstützt wird  

## <a name="see-also"></a>Siehe auch  
 [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  

