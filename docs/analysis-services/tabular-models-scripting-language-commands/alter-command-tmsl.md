---
title: Alter-Befehl (TMSL) | Microsoft Docs
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
ms.assetid: 8bdc49f1-209e-4055-be19-c83862b81efa
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 48567b03017e6ded0aba940b64ef1db52e7f78a1
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="alter-command-tmsl"></a>Alter-Befehl (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Ändert ein vorhandenes Objekt, aber nicht dessen untergeordneten Elementen auf einer Analysis Services-Instanz im tabellarischen Modus an.  Wenn das Objekt nicht vorhanden ist, löst der Befehl einen Fehler aus.  
  
 Verwendung **Alter** -Befehl für targeted Updates, z. B. Festlegen einer Eigenschaft für eine Tabelle ohne aller Spalten ebenfalls angeben zu müssen. Mit diesem Befehl ähnelt **CreateOrReplace**, aber ohne eine vollständige Objektdefinition angeben zu müssen.  
  
 Für Objekte, die Eigenschaften mit Lese-/ Schreibzugriff, wenn Sie eine Lese-/ Schreibzugriff-Eigenschaft angeben, müssen alle in der sie mit der neuen oder vorhandenen Werte angeben. Sie können AMO PowerShell verwenden, zum Abrufen einer Eigenschaftenliste. 
  
## <a name="request"></a>Anforderung  
 **Alter** keine Attribute haben. Eingaben enthalten das Objekt, das geändert werden, gefolgt von der Definition des geänderten Objekts.  
  
 Das folgende Beispiel veranschaulicht die Syntax zum Ändern einer Eigenschaft für ein Partition-Objekt. Der Objektpfad legt fest, welche Partition Objekt ist, die über Name / Wert-Paare von übergeordneten Objekten geändert werden. Die zweite Eingabe ist ein Partitionsobjekt, das den neuen Eigenschaftswert angibt.  
  
```  
{   
  "alter": {   
    "object": {   
      "database": "\<database-name>",   
      "table": "\<table-name>",   
      "partition": "\<partition-name>"   
    },   
    "partition": {   
      "name": "\<new-partition-name>",   
       . . .  << other properties   
    }   
  }   
}   
```  
  
 Die Struktur der Anforderung hängt von dem Objekt ab. **Alter** mit der folgenden Objekte verwendet werden können:  
  
 [Datenbankobjekt &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md) Umbenennen einer Datenbank.  
  
```  
"alter": {   
    "object": {   
      "database": "\<database-name>"  
    },   
    "database": {   
      "name": "\<new-database-name>",   
    }   
  }   
```  
  
 [DataSources Object &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md) Benennen Sie eine Verbindung ein untergeordnetes Objekt der Datenbank ist.  
  
```  
{   
   "alter":{   
      "object":{   
         "database":"AdventureWorksTabular1200",  
         "dataSource":"SqlServer localhost AdventureworksDW2016"  
      },  
      "dataSource":{   
         "name":"A new connection name"  
      }  
   }  
}  
```  
  
 [Tables-Objekt &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md) Finden Sie unter **Beispiel 1** unten.  
  
 [Partitionen Object &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md) Finden Sie unter **Beispiel 2** unten.  
  
 [Rollen Object &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md) Ändern eine Eigenschaft für ein Role-Objekt.  
  
```  
{   
   "alter":{   
      "object":{   
         "database":"AdventureWorksTabular1200",  
         "role":"DataReader"  
      },  
      "role":{   
         "name":"New Name"  
      }  
   }  
}  
```  
  
## <a name="response"></a>Antwort  
 Gibt ein leeres Ergebnis zurück, wenn der Befehl erfolgreich abgeschlossen wurde. Andernfalls wird eine XMLA-Ausnahme zurückgegeben.  
  
## <a name="examples"></a>Beispiele  
 Die folgenden Beispiele veranschaulichen die Skripts, die Sie in einem XMLA-Fenster in Management Studio ausführen oder verwenden Sie als Eingabe in [Invoke-ASCmd-Cmdlet](../../analysis-services/powershell/invoke-ascmd-cmdlet.md) in AMO PowerShell.  
  
 **Beispiel 1** -dieses Skript ändert die Name-Eigenschaft für eine Tabelle.  
  
```  
{   
  "alter": {   
    "object": {   
      "database": "AdventureWorksDW2016",   
      "table": "DimDate"  
    },   
    "table": {   
      "name": "DimDate2"  
    }   
  }   
}  
```  
  
 Sofern von einer lokales benannten Instanz (Instanzname ist "tabellarisch") und eine JSON-Datei mit der Alter-Skript, mit diesem Befehl einen Tabellennamen von DimDate in DimDate2 geändert:  
  
 `invoke-ascmd -inputfile '\\my-computer\my-shared-folder\altertablename.json' -server 'localhost\Tabular'`  
  
 **Beispiel 2** – dieses Skript wird eine Partition, z. B. am Jahresende, wenn das aktuelle Jahr Vorjahr wird umbenannt. Achten Sie darauf, dass alle Eigenschaften angeben. Wenn Sie lassen **Quelle** nicht angegeben, es kann alle Unterbrechen der vorhandenen Partitionsdefinitionen.  
  
 Es sei denn, Sie erstellen, und Ersetzen Sie dabei, oder ändern das Datenquellenobjekt selbst, einer beliebigen Datenquelle verwiesen wird, in Ihrem Skript (z. B. in das unten gezeigte Skript Partition) muss eine vorhandene **DataSource** Objekt in Ihrem Modell. Wenn Sie die Datenquelle ändern müssen, holen Sie dies als separater Schritt ein.  
  
```  
{   
  "alter": {   
    "object": {   
      "database": "InternetSales",   
      "table": "DimDate",  
      "partition": "CurrentYear"  
    },   
    "partition": {   
      "name": "Year2009",  
       "source": {  
             "query":  "SELECT [dbo].[DimDate].* FROM [dbo].[DimDate] WHERE [dbo].[DimDate].CalendarYear = 2009",  
              "dataSource": "SqlServer localhost AdventureworksDW2016"  
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
  
 Sie können kein vorgefertigtes Skript für diesen Befehl aus SSMS generieren. Stattdessen können Sie beginnen mit einem Beispiel oder einen eigenen Handler erstellen.  
  
 Die [ \[MS-SSAS-T\]: SQL Server Analysis Services-Tabellendatenbank (SQL Server Technische Protocol)](http://go.microsoft.com/fwlink/p/?LinkId=784855) Dokuments Abschnitt 3.1.5.2.2, die die Struktur der Befehle für JSON-tabellarischen Metadaten und Objekte beschreibt. Aktuell enthält dieses Dokument Befehle und Funktionen, die noch nicht im TMSL-Skript implementiert. Finden Sie unter ([Tabular Model Scripting Language &#40; TMSL &#41; Verweisen auf](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)) für Informationen zu den was unterstützt wird.  

## <a name="see-also"></a>Siehe auch  
 [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  

