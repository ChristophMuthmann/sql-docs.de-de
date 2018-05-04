---
title: Detach-Befehl (TMSL) | Microsoft Docs
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
ms.assetid: 413b49cb-ea8f-415c-a059-ce692b7771a1
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 4421d4e82c1c26fd4f435322aec38445b59331f2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="detach-command-tmsl"></a>Detach-Befehl (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
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
|**Eigenschaft**|**Standardwert**|**Beschreibung**|  
|database|[Erforderlich]|Der Name des Datenbankobjekts kann nur getrennt werden.|  
|Kennwort|Empty|Das Kennwort zum Verschlüsseln geheimer Schlüssel in der Datenbank getrennt.|  
  
## <a name="response"></a>Antwort  
 Gibt ein leeres Ergebnis zurück, wenn der Befehl erfolgreich abgeschlossen wurde. Andernfalls wird eine XMLA-Ausnahme zurückgegeben.  
  
## <a name="usage-endpoints"></a>Nutzung (Endpunkte)  
 Diese Command-Element wird in einer Anweisung verwendet die [Execute-Methode &#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) Aufruf über einen XMLA-Endpunkt verfügbar gemacht werden auf folgende Weise:  
  
-   Als ein XMLA-Fenster in SQL Server Management Studio (SSMS)  
  
-   Als Eingabedatei für die **invoke-Ascmd** PowerShell-Cmdlet  
  
-   Als Eingabe für ein SSIS-Tasks oder SQL Server-Agent-Auftrag  
  
 Sie können ein vorgefertigtes Skript für diesen Befehl aus SSMS generieren, indem Sie auf die Schaltfläche "Skript" im Dialogfeld "Trennen".  
  
 Die [ \[MS-SSAS-T\]: SQL Server Analysis Services-Tabellendatenbank (SQL Server Technische Protocol)](http://go.microsoft.com/fwlink/p/?LinkId=784855) Dokuments Abschnitt 3.1.5.2.2, die die Struktur der Befehle für JSON-tabellarischen Metadaten und Objekte beschreibt. Aktuell enthält dieses Dokument Befehle und Funktionen, die noch nicht im TMSL-Skript implementiert. Finden Sie unter ([Tabular Model Scripting Language &#40;TMSL&#41; Verweis](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)) für Informationen zu den was unterstützt wird.  

## <a name="see-also"></a>Siehe auch  
 [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Anfügen und Trennen von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
  
