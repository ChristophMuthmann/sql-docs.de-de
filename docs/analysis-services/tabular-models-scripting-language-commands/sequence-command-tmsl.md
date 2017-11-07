---
title: Sequence-Befehl (TMSL) | Microsoft Docs
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
ms.assetid: 898d6ec2-9b40-441b-be2b-5728d1d2882e
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e7fc7f1541131ac6a8e7249940a31104e50f0b09
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="sequence-command-tmsl"></a>Sequence-Befehls (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Verwenden der **Sequenz** Befehl aus, um einen aufeinander folgenden Satz von Vorgängen in einer Instanz von Analysis Services im Batchmodus ausgeführt.  Der gesamte Befehl und aller seiner Komponenten müssen in der Reihenfolge für die Transaktion erfolgreich abschließen.  
  
 Die folgenden Befehle können ausgeführt werden sequenziell, mit Ausnahme von der **aktualisieren** Befehl die parallel auf mehrere Objekte gleichzeitig zu verarbeiten ausgeführt wird.  
  
-   [Erstellen Sie Befehl &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md)  
  
-   [CreateOrReplace-Befehl &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md)  
  
-   [Alter-Befehl &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md)  
  
-   [Löschen Sie Befehl &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md)  
  
-   [Refresh-Befehl &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md)  
  
-   [Befehl "Backup" &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/backup-command-tmsl.md)  
  
-   [RESTORE-Befehl &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/restore-command-tmsl.md)  
  
-   [Fügen Sie an-Befehl &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/attach-command-tmsl.md)  
  
-   [Detach-Befehl &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/detach-command-tmsl.md)  
  
## <a name="request"></a>Anforderung  
 **MaxParallelism** ist eine optionale Eigenschaft, die bestimmt, ob **aktualisieren** Vorgänge sequenziell oder parallel ausgeführt werden.  
  
 Das Standardverhalten ist die Verwendung von Parallelismus wie möglich. Durch das Einbetten von **aktualisieren** in **Sequenz**, können Sie steuern, die genaue Anzahl der Threads, die während der Verarbeitung, einschließlich, beschränken den Vorgang an nur einem Thread verwendet.  
  
> [!NOTE]  
>  Die zugewiesene Ganzzahl **MaxParallelism** bestimmt die maximale Anzahl von Threads, die während der Verarbeitung verwendet. Gültige Werte sind eine positive ganze Zahl. Festlegen des Werts 1 gleich nicht parallel (ein Thread verwendet).  
  
 Nur **aktualisieren** parallel ausgeführt wird. Wenn Sie ändern **MaxParallelism** um eine feste Anzahl von Threads zu verwenden, achten Sie darauf, überprüfen die Eigenschaften auf der [Befehl &#40; aktualisieren TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md) um die potenziellen Auswirkungen zu verstehen. Es ist möglich, zum Festlegen von Eigenschaften auf eine Weise, die Parallelität verwendungsdatensammlungssystem, auch wenn Sie mehrere Threads verfügbar gemacht haben. Die folgende Sequenz von Aktualisierungstypen erhalten Sie, den besten Grad an Parallelität:  
  
-   Geben Sie zunächst die Aktualisierung für alle Objekte, die mit ClearValues  
  
-   Geben Sie anschließend die Aktualisierung für alle Objekte, die mit DataOnly  
  
-   Geben Sie zuletzt Aktualisierung für alle Objekte, die mit vollständig "," Calculate "," Automatic "oder" hinzufügen  
  
 Eine Variante für dieses unterbrochen Parallelität.  
  
```  
{   
  "sequence":    
    {   
      "maxParallelism": 3,   
      "operations": [   
        {   
          "mergepartitions": {   
            "sources": [   
              {   
                "database": "salesdatabase",   
                "table": "Sales",   
                "partition": "partition1"   
              },   
              {   
                "database": "salesdatabase",   
                "table": "Sales",   
                "partition": "partition2"   
              }   
            ]   
          }   
        },   
        {   
          "refresh": {   
            "type": "calculate",   
            "object": {   
             "database": "salesdatabase"   
            }   
          }   
        }   
      ]   
    }      
}   
```  
  
## <a name="response"></a>Antwort  
 Gibt ein leeres Ergebnis zurück, wenn der Befehl erfolgreich abgeschlossen wurde. Andernfalls wird eine XMLA-Ausnahme zurückgegeben.  
  
## <a name="usage-endpoints"></a>Nutzung (Endpunkte)  
 Diese Command-Element wird in einer Anweisung verwendet die [Execute-Methode &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) Aufruf über einen XMLA-Endpunkt verfügbar gemacht werden auf folgende Weise:  
  
-   Als ein XMLA-Fenster in SQL Server Management Studio (SSMS)  
  
-   Als Eingabedatei für die **invoke-Ascmd** PowerShell-Cmdlet  
  
-   Als Eingabe für ein SSIS-Tasks oder SQL Server-Agent-Auftrag  
  
 Sie können kein vorgefertigtes Skript für diesen Befehl aus SSMS generieren. Stattdessen können Sie beginnen mit einem Beispiel oder einen eigenen Handler erstellen.  
  
 Die [ \[MS-SSAS-T\]: SQL Server Analysis Services-Tabellendatenbank (SQL Server Technische Protocol)](http://go.microsoft.com/fwlink/p/?LinkId=784855) Dokuments Abschnitt 3.1.5.2.2, die die Struktur der Befehle für JSON-tabellarischen Metadaten und Objekte beschreibt. . Aktuell enthält dieses Dokument Befehle und Funktionen, die noch nicht im TMSL-Skript implementiert. Finden Sie unter ([Tabular Model Scripting Language &#40; TMSL &#41; Verweisen auf](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)) für Informationen zu den was unterstützt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  

