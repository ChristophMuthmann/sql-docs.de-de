---
title: "SQL Server Profiler zum Überwachen von Datamining mit | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Profiler [SQL Server Profiler], Analysis Services
ms.assetid: 655ac93c-5c5c-4565-914b-915327f7d349
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 96b5485ebddba8823f262ba6a2229018d82a72fd
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="using-sql-server-profiler-to-monitor-data-mining-analysis-services---data-mining"></a>Verwenden von SQL Server Profiler zum Überwachen von Data Mining (Analysis Services – Data Mining)
  Wenn Sie über die erforderlichen Berechtigungen verfügen, können Sie SQL Server Profiler zum Überwachen von Data Mining-Aktivitäten verwenden, die als Anforderungen an eine Instanz von SQL Server Analysis Services gesendet werden. Zu Data Mining-Aktivitäten können die Verarbeitung von Modellen oder Strukturen, Vorhersage- und Inhaltsabfragen sowie die Erstellung neuer Modelle oder Strukturen gehören.  
  
 SQL Server Profiler verwendet eine **Ablaufverfolgung** , um von verschiedenen Clients stammende Anforderungen zu überwachen – einschließlich [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], SQL Server Management Studio, Web-Dienste oder die Data Mining-Add-Ins für Excel. Dabei müssen jedoch alle Aktivitäten dieselbe SQL Server Analysis Services-Instanz nutzen. Sie müssen für jede zu überwachende Instanz von SQL Server Analysis Services eine separate Ablaufverfolgung erstellen. Allgemeine Informationen zu Ablaufverfolgungen und der Verwendung von SQL Server Profiler finden Sie unter [Verwenden von SQL Server Profiler zum Überwachen von Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md).  
  
 Spezifische Hilfestellungen zu den verschiedenen Typen von zu erfassenden Ereignissen finden Sie unter [Erstellen von Profilerablaufverfolgungen für Replay &#40;Analysis Services&#41;](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md).  
  
## <a name="using-traces-to-monitor-data-mining"></a>Verwenden von Ablaufverfolgungen zum Überwachen von Data Mining  
 Wenn Sie Daten in einer Ablaufverfolgung aufzeichnen, können Sie festlegen, ob die Daten in einer Datei, einer Tabelle oder einer Instanz von SQL Server gespeichert werden sollen. Unabhängig davon, welche Methode Sie zum Speichern der Daten wählen, können Sie die Ablaufverfolgung mithilfe von SQL Server Profiler anzeigen und nach Ereignissen filtern. In der folgenden Tabellen werden einige Ereignisse und Unterklassen der Standard-Ablaufverfolgung von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] aufgeführt, die beim Data Mining von Interesse sind.  
  
|EventClass|EventSubclass|Description|  
|----------------|-------------------|-----------------|  
|**Query Begin**<br /><br /> **Abfrageende**|**0 - MDXQuery**|Enthält den Text aller Aufrufe an von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gespeicherten Prozeduren.|  
|**Query Begin**<br /><br /> **Abfrageende**|**1 - DMXQuery**|Enthält den Text und die Ergebnisse von Data Mining Extension (DMX)-Anweisungen.|  
|**Progress Report Begin**<br /><br /> **Progress Report End**|**34 - DataMiningProgress**|Liefert Informationen über den Status des Data Mining-Algorithmus: Wenn Sie beispielsweise ein Clustering-Modell erstellen, erhalten Sie eine Statusmeldung, die besagt, welcher Kandidaten-Cluster gerade erstellt wird.|  
|**Query Begin**<br /><br /> **Abfrageende**|EXECUTESQL|Enthält den Text der Transact-SQL-Abfrage, die gerade ausgeführt wird.|  
|**Query Begin**<br /><br /> **Abfrageende**|**2 - SQLQuery**|Enthält den Text beliebiger Abfragen für Schemarowsets in Form von Systemtabellen.|  
|**DISCOVER Begin**<br /><br /> **DISCOVER End**|Mehrere|Enthält den Text der DMX-Funktionsaufrufe oder der in XMLA gekapselten DISCOVER-Anweisungen.|  
|**Fehler**|(none)|Enthält den Text von Fehlern, die vom Server an den Client gesendet werden.<br /><br /> Fehlermeldungen, die das Präfix **Fehler (Data Mining):** oder **Information (Data Mining):** aufweisen, werden spezifisch als Antwort auf DMX-Anforderungen erstellt. Es reicht jedoch nicht aus, nur diese Fehlermeldungen anzuzeigen. Andere Fehler, die zum Beispiel vom Parser erzeugt worden sind, können ebenfalls mit Data Mining zu tun haben, verfügen jedoch nicht über ein derartiges Präfix.|  
  
 Durch die Anzeige der Befehlsanweisungen im Ablaufverfolgungsprotokoll können Sie auch die Syntax komplexer Anweisungen überprüfen, die vom Client an den [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Server gesendet werden – darunter auch Aufrufe an vom System gespeicherten Prozeduren. Diese Informationen können Ihnen bei der Fehlerbehebung helfen. Sie haben auch die Möglichkeit, gültige Anweisungen als Vorlage zum Erstellen neuer Vorhersageabfragen oder Modelle zu verwenden. Einige Beispiele für gespeicherte Prozeduraufrufe, die Sie über eine Ablaufverfolgung aufzeichnen können, finden Sie unter [Beispiele für Clusteringmodellabfragen](../../analysis-services/data-mining/clustering-model-query-examples.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen einer Instanz von Analysis Services](../../analysis-services/instances/monitor-an-analysis-services-instance.md)   
 [Überwachen von Analysis Services mit den erweiterten Ereignissen von SQL Server](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)  
  
  
