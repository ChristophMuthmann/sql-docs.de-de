---
title: Delete-Befehl (TMSL) | Microsoft Docs
ms.custom: 
ms.date: 05/30/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 05d3fb14-ea03-4596-ac2e-9ae5bab27b4d
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: edb54bdecdabdfccac8664d3bb8a5e98633f8ddb
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="delete-command-tmsl"></a>Delete-Befehl (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Löscht eine Datenbank oder ein Objekt in der aktuellen Datenbank.   
Löscht das angegebene Objekt und alle untergeordneten Objekte und Sammlungen. Wenn das Objekt nicht vorhanden ist, löst der Befehl einen Fehler aus.  
  
## <a name="request"></a>Anforderung  
 Das gelöschten Objekt wird mithilfe des Objekt-Pfads angegeben. Beim Löschen einer Partition erfordert z. B. die Angabe der Tabellen- und Datenbank-Objekte, die sich davor.  
  
```  
{   
  "delete": {   
    "object": {   
      "database": "AdventureworksDW2016",   
      "table": "Reseller Sales",   
      "partition": "may2011"   
    }   
  }   
}   
```  
  
 Sie können die folgenden Objekte löschen:  
  
 [Datenbankobjekt &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md)  
  
```  
{   
  "delete": {   
    "object": {   
      "database": "AdventureworksDW2016"  
    }   
  }   
}   
```  
  
 [DataSources Object &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md)  
  
```  
{  
  "delete": {  
    "object": {  
      "database": "AdventureworksDW2016",  
      "dataSource": "SqlServer localhost AdventureworksDW2016"  
    }  
  }  
}  
```  
  
 [Tables-Objekt &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md)  
  
```  
{   
  "delete": {   
    "object": {   
      "database": "AdventureworksDW2016",   
      "table": "Reseller Sales",  
    }   
  }   
}   
```  
  
 [Partitionen Object &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md)  
  
```  
{   
  "delete": {   
    "object": {   
      "database": "AdventureworksDW2016",   
      "table": "Reseller Sales",   
      "partition": "may2011"   
    }   
  }   
}   
```  
  
 [Rollen Object &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)  
  
```  
{   
  "delete": {   
    "object": {   
      "database": "AdventureworksDW2016",   
      "role": "Data Reader"  
    }   
  }   
}   
```  
  
## <a name="response"></a>Antwort  
 Gibt ein leeres Ergebnis zurück, wenn der Befehl erfolgreich abgeschlossen wurde. Andernfalls wird eine XMLA-Ausnahme zurückgegeben.  
  
## <a name="examples"></a>Beispiele  
 **Beispiel 1** -Löschen einer Datenbank.  
  
```  
{  
  "delete": {  
    "object": {  
      "database": "AdventureWorksDW2016"  
    }  
  }  
}  
```  
  
 **Beispiel 2** -Löschen einer Verbindung.  
  
```  
{  
  "delete": {  
    "object": {  
      "database": "AdventureWorksDW2016",  
      "dataSource": "SqlServer localhost AdventureworksDW2016"  
    }  
  }  
}  
```  
  
## <a name="usage-endpoints"></a>Nutzung (Endpunkte)  
 Diese Command-Element wird in einer Anweisung verwendet die [Execute-Methode &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) Aufruf über einen XMLA-Endpunkt verfügbar gemacht werden auf folgende Weise:  
  
-   Als ein XMLA-Fenster in SQL Server Management Studio (SSMS)  
  
-   Als Eingabedatei für die **invoke-Ascmd** PowerShell-Cmdlet  
  
-   Als Eingabe für ein SSIS-Tasks oder SQL Server-Agent-Auftrag  
  
 Sie können ein vorgefertigtes Skript für diesen Befehl aus SSMS generieren.  Beispielsweise können Sie eine vorhandene Datenbank auf Rechtsklicken > **Skript** > **Skript für Datenbank als** > **DELETE in**.  
  
 Die [ \[MS-SSAS-T\]: SQL Server Analysis Services-Tabellendatenbank (SQL Server Technische Protocol)](http://go.microsoft.com/fwlink/p/?LinkId=784855) Dokuments Abschnitt 3.1.5.2.2, die die Struktur der Befehle für JSON-tabellarischen Metadaten und Objekte beschreibt. Aktuell enthält dieses Dokument Befehle und Funktionen, die noch nicht im TMSL-Skript implementiert. Finden Sie unter [Tabular Model Scripting Language &#40; TMSL &#41; Verweis](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) für Informationen zu den was unterstützt wird.  

## <a name="see-also"></a>Siehe auch  
 [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
