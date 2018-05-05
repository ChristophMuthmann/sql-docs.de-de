---
title: Synchronize-Befehl (TMSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: a32ff053-f38f-49d7-afdc-e19f59c88135
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a83d10d5f8dce62837b6d86804586f5c5099e10e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="synchronize-command-tmsl"></a>Synchronize-Befehl (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  Synchronisiert eine Analysis Services-Datenbank mit einer anderen vorhandenen Datenbank.  
  
## <a name="request"></a>Anforderung  
 Die Eigenschaften von JSON akzeptiert synchronize-Befehl lauten wie folgt.  
  
```  
{   
   "synchronize":{   
      "database":"AdventureWorksDW_Production",  
      "source":"Provider=MSOLAP.7;Data Source=localhost;Integrated Security=SSPI;Initial Catalog=AdventureWorksDW_Dev",  
      "synchronizeSecurity":"copyAll",  
      "applyCompression":true  
   }  
}  
```  
  
 Die Eigenschaften von JSON akzeptiert synchronize-Befehl lauten wie folgt.  
  
||||  
|-|-|-|  
|**Eigenschaft**|**Standardwert**|**Beschreibung**|  
|database||Der Name des Datenbankobjekts synchronisiert werden.|  
|Quelle||Die Verbindungszeichenfolge für die Verbindung mit dem Quellserver verwendet.|  
|synchronizeSecurity|skipMembership|Ein Enumerationswert, der angibt, wie sicherheitsdefinitionen wie Rollen und Berechtigungen wiederhergestellt. Gültige Werte enthält, SkipMembership, CopyAll, IgnoreSecurity.|  
|applyCompression|Wahr|Ein boolescher Wert, der bei "true", gibt an, dass die Komprimierung während der Synchronisierungsvorgang angewendet wird; andernfalls "false".|  
  
## <a name="response"></a>Antwort  
 Gibt ein leeres Ergebnis zurück, wenn der Befehl erfolgreich abgeschlossen wurde. Andernfalls wird eine XMLA-Ausnahme zurückgegeben.  
  
## <a name="usage-endpoints"></a>Nutzung (Endpunkte)  
 Diese Command-Element wird in einer Anweisung verwendet die [Execute-Methode &#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) Aufruf über einen XMLA-Endpunkt verfügbar gemacht werden auf folgende Weise:  
  
-   Als ein XMLA-Fenster in SQL Server Management Studio (SSMS)  
  
-   Als Eingabedatei für die **invoke-Ascmd** PowerShell-Cmdlet  
  
-   Als Eingabe für ein SSIS-Tasks oder SQL Server-Agent-Auftrag  
  
 Sie können ein vorgefertigtes Skript für diesen Befehl aus SSMS generieren, indem Sie auf die Schaltfläche "Skript" im Dialogfeld Synchronisieren einer Datenbank.  
  
 Die [ \[MS-SSAS-T\]: SQL Server Analysis Services-Tabellendatenbank (SQL Server Technische Protocol)](http://go.microsoft.com/fwlink/p/?LinkId=784855) Dokuments Abschnitt 3.1.5.2.2, die die Struktur der Befehle für JSON-tabellarischen Metadaten und Objekte beschreibt. Aktuell enthält dieses Dokument Befehle und Funktionen, die noch nicht im TMSL-Skript implementiert. Finden Sie unter [Tabular Model Scripting Language &#40;TMSL&#41; Verweis](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) für Informationen zu den was unterstützt wird  
  
## <a name="see-also"></a>Siehe auch  
 [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
