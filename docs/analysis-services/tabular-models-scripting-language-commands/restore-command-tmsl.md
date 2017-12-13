---
title: RESTORE-Befehl (TMSL) | Microsoft Docs
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
ms.assetid: 360a1567-67ae-459d-8865-9a2bef8d4186
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 45e4461956c78278d367715e8ef665821d487e3f
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="restore-command-tmsl"></a>RESTORE-Befehl (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Eine Analysis Services-Datenbank wiederhergestellt aus einer Sicherungsdatei.  
  
## <a name="request"></a>Anforderung  
  
```  
    {  
"restore": {  
            "description": "Parameters of Restore command of Analysis Services JSON API",  
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
            "dbStorageLocation": {  
                "type": "string"  
            },  
            "allowOverwrite": {  
                "type":boolean  
            },  
            "readWriteMode": {  
                "enum": [  
                "readWrite",  
                "readOnly",  
                "readOnlyExclusive"  
                ]  
. . .   
```  
  
 **Wiederherstellen** verfügt über mehrere Eigenschaften.  
  
||||  
|-|-|-|  
|**Eigenschaft**|**Default**|**Description**|  
|database|[Erforderlich]|Der Name des Datenbankobjekts wiederhergestellt werden.|  
|file|[Erforderlich]|Die Sicherungsdatei/Pfad.|  
|Kennwort|Empty|Das Kennwort zum Entschlüsseln der Sicherungsdatei verwendet werden soll.|  
|allowOverwrite|False|Ein boolescher Wert, der bei "true", gibt an, dass eine Sicherungsdatei, die bereits vorhanden ist, werden überschrieben; andernfalls "false".|  
|readWriteMode|ReadWrite|Ein Enumerationswert, der Zugriffsmodi darf die Datenbank angibt.<br /><br /> **Enumerationswerte werden wie folgt aus:**<br /><br /> ReadWrite – ist Lese-/ Schreib-Zugriff zulässig.<br /><br /> ReadOnly – ist nur-Lese-Zugriff zulässig.<br /><br /> ReadOnlyExclusive – ist nur-Lese exklusiver Zugriff zulässig.|  
|dbStorageLocation|Empty|Speicherort für die wiederhergestellte Datenbank.|  
  
## <a name="response"></a>Antwort  
 Gibt ein leeres Ergebnis zurück, wenn der Befehl erfolgreich abgeschlossen wurde. Andernfalls wird eine XMLA-Ausnahme zurückgegeben.  
  
## <a name="example"></a>Beispiel  
 **Beispiel 1** -Wiederherstellen einer Datenbank aus einem lokalen Ordner.  
  
```  
{   
   "restore": {   
      "database":"AdventureWorksDW2014",  
      "file":"c:\\awdbdwfile.abf",  
      "security":"...",  
      "allowOverwrite":"true",  
      "password":"..",  
      "locations":"d:\\SQL Server Analysis Services\\data\\",  
      "storageLocation":".."  
   }  
}  
```  
  
## <a name="usage-endpoints"></a>Nutzung (Endpunkte)  
 Diese Command-Element wird in einer Anweisung verwendet die [Execute-Methode &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) Aufruf über einen XMLA-Endpunkt verfügbar gemacht werden auf folgende Weise:  
  
-   Als ein XMLA-Fenster in SQL Server Management Studio (SSMS)  
  
-   Als Eingabedatei für die **invoke-Ascmd** PowerShell-Cmdlet  
  
-   Als Eingabe für ein SSIS-Tasks oder SQL Server-Agent-Auftrag  
  
 Sie können ein vorgefertigtes Skript für diesen Befehl aus SSMS generieren, durch Klicken auf die Schaltfläche "Skript" im Dialogfeld "Wiederherstellen".  
  
 Die [ \[MS-SSAS-T\]: SQL Server Analysis Services-Tabellendatenbank (SQL Server Technische Protocol)](http://go.microsoft.com/fwlink/p/?LinkId=784855) Dokuments Abschnitt 3.1.5.2.2, die die Struktur der Befehle für JSON-tabellarischen Metadaten und Objekte beschreibt. Aktuell enthält dieses Dokument Befehle und Funktionen, die noch nicht im TMSL-Skript implementiert. Finden Sie unter [Tabular Model Scripting Language &#40; TMSL &#41; Verweis](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) für Informationen zu den was unterstützt wird  
  
## <a name="see-also"></a>Siehe auch  
 [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Sichern und Wiederherstellen von Analysis Services-Datenbanken](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
