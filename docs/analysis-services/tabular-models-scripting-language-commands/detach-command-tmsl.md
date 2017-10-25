---
title: Detach-Befehl (TMSL) | Microsoft Docs
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 413b49cb-ea8f-415c-a059-ce692b7771a1
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dfa0440270971b80d6cd1f6789534cedb6f976ad
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="detach-command-tmsl"></a>Detach-Befehl (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Trennt eine Analysis Services-Datenbank von einem Server an.  
  
## <a name="request"></a>Anforderung  
  
```  
{   
   "detach": {    
      "database":"AdventureWorksDW2014",  
      "password": "secret"  
   }  
}  
```  
  
 Die Eigenschaften von JSON akzeptiert detach-Befehl lauten wie folgt.  
  
||||  
|-|-|-|  
|**Eigenschaft**|**Default**|**Description**|  
|database|[Erforderlich]|Der Name des Datenbankobjekts kann nur getrennt werden.|  
|Kennwort|Empty|Das Kennwort zum Verschlüsseln geheimer Schlüssel in der Datenbank getrennt.|  
  
## <a name="response"></a>Antwort  
 Gibt ein leeres Ergebnis zurück, wenn der Befehl erfolgreich abgeschlossen wurde. Andernfalls wird eine XMLA-Ausnahme zurückgegeben.  
  
## <a name="usage-endpoints"></a>Nutzung (Endpunkte)  
 Diese Command-Element wird in einer Anweisung verwendet die [Execute-Methode &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) Aufruf über einen XMLA-Endpunkt verfügbar gemacht werden auf folgende Weise:  
  
-   Als ein XMLA-Fenster in SQL Server Management Studio (SSMS)  
  
-   Als Eingabedatei für die **invoke-Ascmd** PowerShell-Cmdlet  
  
-   Als Eingabe für ein SSIS-Tasks oder SQL Server-Agent-Auftrag  
  
 Sie können ein vorgefertigtes Skript für diesen Befehl aus SSMS generieren, indem Sie auf die Schaltfläche "Skript" im Dialogfeld "Trennen".  
  
 Die [ \[MS-SSAS-T\]: SQL Server Analysis Services-Tabellendatenbank (SQL Server Technische Protocol)](http://go.microsoft.com/fwlink/p/?LinkId=784855) Dokuments Abschnitt 3.1.5.2.2, die die Struktur der Befehle für JSON-tabellarischen Metadaten und Objekte beschreibt. Aktuell enthält dieses Dokument Befehle und Funktionen, die noch nicht im TMSL-Skript implementiert. Finden Sie unter ([Tabular Model Scripting Language &#40; TMSL &#41; Verweisen auf](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)) für Informationen zu den was unterstützt wird.  

## <a name="see-also"></a>Siehe auch  
 [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Anfügen und Trennen von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
  

