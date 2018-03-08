---
title: Backup-Befehl (TMSL) | Microsoft Docs
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
ms.assetid: fae1b267-0750-4dc5-9bf0-80ac4d8487a3
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 50e6f8e6f5b01fce2eb0bb6a5dbcd84dd631d994
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="backup-command-tmsl"></a>Befehl "Backup" (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Sichert eine Analysis Services-Datenbank in einer ABF-Sicherungsdatei.  
  
## <a name="request"></a>Anforderung  
  
```  
    {  
        "backup": {  
            "description": "Parameters of Backup command of Analysis Services JSON API",  
            "properties": {  
            "database": {  
                "type": "string"  
            },  
            "file": {  
                "type": "string"  
            },  
            "password": {  
                "type": "string"  
            },  
            "allowOverwrite": {  
                "type": "boolean"  
            },  
            "applyCompression": {  
                "type": "boolean"  
            }  
            },  
. . .   
```  
  
 **Sicherung** verfügt über mehrere Eigenschaften.  
  
||||  
|-|-|-|  
|**Eigenschaft**|**Default**|**Beschreibung**|  
|Datenbank|[Erforderlich]|Der Name des Datenbankobjekts gesichert werden soll.|  
|file|[Erforderlich]|Die Sicherungsdatei/Pfad.|  
|Kennwort|Empty|Das Kennwort zum Verschlüsseln der Sicherungsdatei verwendet werden soll.|  
|allowOverwrite|False|Ein boolescher Wert, der bei "true", gibt an, dass eine Sicherungsdatei, die bereits vorhanden ist, werden überschrieben; andernfalls "false".|  
|applyCompression|Wahr|Ein boolescher Wert, der bei "true", gibt an, dass Dateien komprimiert werden. andernfalls "false".|  
  
## <a name="response"></a>Antwort  
 Gibt ein leeres Ergebnis zurück, wenn der Befehl erfolgreich abgeschlossen wurde. Andernfalls wird eine XMLA-Ausnahme zurückgegeben.  
  
## <a name="examples"></a>Beispiele  
 **Beispiel 1** -Sicherung eine Datei, die Standardsicherungsordner.  
  
```  
{   
   "backup": {   
      "database":"AS_AdventureWorksDW2014",  
      "file":"AS_AdventureWorksDW2014.abf",  
      "password":"secret"  
   }  
}  
```  
  
## <a name="usage-endpoints"></a>Nutzung (Endpunkte)  
 Diese Command-Element wird in einer Anweisung verwendet die [Execute-Methode &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) Aufruf über einen XMLA-Endpunkt verfügbar gemacht werden auf folgende Weise:  
  
-   Als ein XMLA-Fenster in SQL Server Management Studio (SSMS)  
  
-   Als Eingabedatei für die **invoke-Ascmd** PowerShell-Cmdlet  
  
-   Als Eingabe für ein SSIS-Tasks oder SQL Server-Agent-Auftrag  
  
 Sie können ein vorgefertigtes Skript für diesen Befehl aus SSMS generieren, indem Sie auf die Schaltfläche "Skript" im Dialogfeld Datenbank sichern.  
  
 Die [ \[MS-SSAS-T\]: SQL Server Analysis Services-Tabellendatenbank (SQL Server Technische Protocol)](http://go.microsoft.com/fwlink/p/?LinkId=784855) Dokuments Abschnitt 3.1.5.2.2, die die Struktur der Befehle für JSON-tabellarischen Metadaten und Objekte beschreibt. Aktuell enthält dieses Dokument Befehle und Funktionen, die noch nicht im TMSL-Skript implementiert. Finden Sie unter [Tabular Model Scripting Language &#40; TMSL &#41; Verweis](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) für Informationen zu den was unterstützt wird  

## <a name="see-also"></a>Siehe auch  
 [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Sichern und Wiederherstellen von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
