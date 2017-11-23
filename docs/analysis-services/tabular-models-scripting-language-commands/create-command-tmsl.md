---
title: CREATE-Befehl (TMSL) | Microsoft Docs
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
ms.assetid: e3024f89-ebfa-47e4-9893-708f379fd9b8
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ae07d8b17fc659bb8a8bc2bef1cdcb6421606c29
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="create-command-tmsl"></a>CREATE-Befehl (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Erstellt das angegebene Objekt und alle untergeordneten Objekte, die angegeben werden. Wenn das Objekt bereits vorhanden ist, löst der Befehl einen Fehler aus.  
  
## <a name="request"></a>Anforderung  
 Die Struktur der Anforderung hängt von dem Objekt ab. Ein Objekt, das ein übergeordnetes Element ist muss alle seine untergeordneten Elemente enthalten, obwohl die vollständige Objektdefinitionen von gleichgeordneten Elementen und Eltern nicht erforderlich sind.  
  
 [Datenbankobjekt &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md) Hinzufügen einer Datenbank zu einem Server.  
  
```  
{   
  "create": {   
    "database": {   
      "name": "AdventureworksDW2016",   
      "description": "<description>",   
      "tables": [   
        { },   
        { },   
        { }   
      ],   
      "relationships": [   
        { },   
        { }   
      ]   
    }   
  }   
}  
```  
  
 [DataSources Object &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md)  
  
```  
{  
  "create": {  
    "parentObject": {  
      "database": "AdventureworksDW2016"  
    },  
    "dataSource": {  
      "name": "SqlServer localhost AdventureworksDW2016",  
      "connectionString": "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=AdventureworksDW2016;Integrated Security=SSPI;Persist Security Info=false",  
      "impersonationMode": "impersonateAccount",  
      "account": "<account name>",  
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
  
 [Tables-Objekt &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md) Spalten einer Tabelle hinzufügen.  
  
```  
{   
  "create": {   
    "parentObject": {   
      "database": "AdventureworksDW2016",   
      "table": "DimSales"  
    },   
    "columns": {   
      "type": ["calculated"  | "data" ]  
      "name": "\<column-name>",   
       "expression":  "<DAX expression>"  
    }   
  }   
}   
```  
  
 [Partitionen Object &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md) Hinzufügen einer Partition auf einer Tabelle des übergeordneten Objekts.  
  
```  
{  
  "create": {  
    "parentObject": {  
      "database": "AdventureWorksTabular1200",  
      "table": "Date"  
    },  
    "partition": {  
      "name": "Date 2",  
      "source": {  
        "query": "SELECT [dbo].[DimDate].* FROM [dbo].[DimDate]",  
        "dataSource": "SqlServer localhost AdventureworksDW2016"  
      }  
    }  
  }  
}  
```  
  
 [Rollen Object &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md) Minimal Hinzufügen einer Rolle in einer Datenbank, jedoch ohne Domänenmitgliedschaft oder der Filter.  
  
```  
{  
  "create": {  
    "parentObject": {  
      "database": "AdventureWorksDW2016"  
    },  
    "role": {  
      "name": "DataReader",  
      "modelPermission": "read"  
    }  
  }  
}  
```  
  
 Mit Ausnahme der **Datenbank** -Objekt, das zu erstellende Objekt ist untergeordnetes Element eines angegebenen **ParentObject**. Das übergeordnete Element der **Datenbank** Objekt ist immer die **Server** Objekt.  
  
 Server wird aus dem Kontext ausgegangen. Z. B. Wenn Sie in Management Studio oder AMO PowerShell das Skript ausführen, würde die Server-Verbindung in der Sitzung oder als Parameter angegeben werden.  
  
## <a name="response"></a>Antwort  
 Gibt ein leeres Ergebnis zurück, wenn der Befehl erfolgreich abgeschlossen wurde. Andernfalls wird eine XMLA-Ausnahme zurückgegeben.  
  
## <a name="examples"></a>Beispiele  
 **Beispiel 1** -Hinzufügen einer Rolle, die Mitgliedschaft und einen Filter angibt.  
  
```  
{   
   "create":{   
      "parentObject":{   
         "database":"AdventureWorksTabular1200"  
      },  
      "role":{  
         "name":"DataReader",  
         "modelPermission":"read",  
         "members":[   
            {  
               "memberName": "account-01",  
               "memberId":"S-1-5-21-1111111111-2222222222-33333333-444444"  
            },  
            {   
               "memberName": "account-02",  
               "memberId":"S-2-5-21-1111111111-2222222222-33333333-444444"  
            }  
         ],  
         "tablePermissions":[   
            {   
               "name":"Date",  
               "filterExpression":"CalendarYear('2011')"  
            }  
         ]  
      }  
   }  
}  
```  
  
## <a name="usage-endpoints"></a>Nutzung (Endpunkte)  
 Diese Command-Element wird in einer Anweisung verwendet die [Execute-Methode &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) Aufruf über einen XMLA-Endpunkt verfügbar gemacht werden auf folgende Weise:  
  
-   Als ein XMLA-Fenster in SQL Server Management Studio (SSMS)  
  
-   Als Eingabedatei für die **invoke-Ascmd** PowerShell-Cmdlet  
  
-   Als Eingabe für ein SSIS-Tasks oder SQL Server-Agent-Auftrag  
  
 Sie können ein vorgefertigtes Skript für diesen Befehl aus SSMS generieren.  Beispielsweise können Sie eine vorhandene Datenbank auf Rechtsklicken > **Skript** > **Skript für Datenbank als** > **CREATE in**.  
  
 Die [ \[MS-SSAS-T\]: SQL Server Analysis Services-Tabellendatenbank (SQL Server Technische Protocol)](http://go.microsoft.com/fwlink/p/?LinkId=784855) Dokuments Abschnitt 3.1.5.2.2, die die Struktur der Befehle für JSON-tabellarischen Metadaten und Objekte beschreibt. Aktuell enthält dieses Dokument Befehle und Funktionen, die noch nicht im TMSL-Skript implementiert. Finden Sie unter ([Tabular Model Scripting Language &#40; TMSL &#41; Verweisen auf](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)) für Informationen zu den was unterstützt wird.  

## <a name="see-also"></a>Siehe auch  
 [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
