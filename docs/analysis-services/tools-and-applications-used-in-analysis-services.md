---
title: "In Analysis Services verwendete Tools und Anwendungen | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: 0ddb3b7a-7464-4d04-8659-11cb2e4cf3c3
caps.latest.revision: 17
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 17
---
# In Analysis Services verwendete Tools und Anwendungen
  Suchen Sie nach den Tools und Anwendungen, die Sie benötigen, um Analysis Services-Modelle zu erstellen und zugeordnete Datenbanken in einer Analysis Services-Instanz zu verwalten.  
  
## Analysis Services-Modell-Designer  
 Tabellarische und mehrdimensionale Modelle werden aus Projektvorlagen in einer Lösung erstellt, die in einer Visual Studio-Shell erstellt wurde. Die Projektvorlage stellt die Entwürfe für das Erstellen von Tabellen, Beziehungen, Cubes, Dimensionen und Rollen bereit, aus denen eine Analysis Services-Lösung besteht. Die Shell stellt den visuellen Arbeitsbereich, die Eigenschaftenseiten und das Befehlsframework bereit, in dem das Projekt erstellt wird. Der Modell-Designer, der sowohl Shell als auch Vorlagen bietet, ist einen kostenloser Webdownload.  
  
 Modelle verfügen über eine Einstellung des Kompatibilitätsgrades, der die Funktionsverfügbarkeit bestimmt und welches Release von Analysis Services das Modell ausführt.  Der Modell-Designer bestimmt zum Teil, ob Sie einen angegebenen Kompatibilitätsgrad angeben können.  
  
 Tabellarische Modelle, die die neueste Funktionalität in SQL Server 2016 verwenden, wie z.B. BIM-Dateien in JSON-Tabellenformat und bidirektionales Kreuzfiltern, müssen bei Kompatibilitätsgrad 1200 in der Version von SQL Server Data Tools für Visual Studio 2015 erstellt werden, die gleichzeitig mit SQL Server 2016 (Download-Link siehe unten) geliefert wird.  
  
 Wenn Sie einen niedrigeren Kompatibilitätsgrad benötigen, weil Sie vielleicht ein Modell mit einer früheren Version von Analysis Services bereitstellen möchten, können Sie weiterhin den Modell-Designer in SSDT für Visual Studio 2015 verwenden. Neuere Versionen des Toolsupports erstellen jeden Modelltyp (tabellarisch oder mehrdimensional) mit jedem Kompatibilitätsgrad, den Sie benötigen. Es ist nicht erforderlich, ältere Tools nur zum Erstellen oder Bearbeiten eines älteren Modells zu behalten.  
  
### Herunterladen des Modell-Designers  
 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], zuvor bekannt als SQL Server Data Tools für Business Intelligence (SSDT-BI) und davor als Business Intelligence Development Studio (BIDS), wird verwendet, um Analysis Services-Modelle zu erstellen.  
  
||  
|-|  
|**[Herunterladen von SSDT für Visual Studio 2015](https://msdn.microsoft.com/mt429383)**|  
  
 Anstatt frühere Versionen des Designers zu verwenden, wird empfohlen, SQL Server Data Tools für Visual Studio 2015 zu verwenden. Es enthält Projektvorlagen für alle SQL Server-Inhaltstypen, wie die relationale Datenbank, Analysis Services-Modelle, Reporting Services-Berichte sowie Integration Services-Pakete.  
  
 SSDT wird in der Visual Studio 2015 Shell ausgeführt. Wenn Sie bereits Visual Studio 2015 besitzen, fügt SSDT Setup nur die Projektvorlagen hinzu. Wenn Sie Visual Studio 2015 nicht besitzen, werden sowohl die Shell als auch die Vorlagen installiert.  
  
 Wenn auf Ihrem Computer eine frühere Version von SSDT-BI oder BIDS installiert ist, wird die neuere Version parallel zur vorherigen Version installiert.  
  
 Nachdem Sie SSDT installiert haben, sollten die Business Intelligence-Vorlagen im Dialogfeld „Neues Projekt“ angezeigt werden.  
  
 ![Neue Projektvorlagen in SSDT](../analysis-services/media/ssdt-biprojects.png "Neue Projektvorlagen in SSDT")  
  
## Verwaltungstools  
  
### Hier können Sie SQL Server Management Studio herunterladen.  
 Management Studio ist das primäre Verwaltungstool für alle SQL Server-Funktionen, einschließlich Analysis Services. Dies ist nun ein separater Download.  
  
||  
|-|  
|**[Hier können Sie SQL Server Management Studio herunterladen.](https://msdn.microsoft.com/library/mt238290.aspx)**|  
  
 In SQL Server 2016 schließt Management Studio erweiterte Ereignisse (xEvents) für Analysis Services ein und bietet dadurch eine einfache Alternative zur SQL Server Profiler-Ablaufverfolgung, die zur Überwachung der Aktivität und Diagnose von Serverproblemen verwendet wird. Weitere Informationen finden Sie unter [Überwachen von Analysis Services mit den erweiterten Ereignissen von SQL Server](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md).  
  
### SQL Server Profiler  
 Auch wenn er zugunsten von xEvents offiziell als veraltet eingestuft ist, bietet SQL Server Profiler ein vertrautes Konzept zum Überwachen von Verbindungen, der MDX-Abfrageausführung und anderer Servervorgänge. SQL Server Profiler wird standardmäßig installiert. Sie finden ihn mit SQL Server-Anwendungen bei den Apps in Windows Server 2012.  
  
### PowerShell  
 Mithilfe von PowerShell-Befehlen können Sie viele Verwaltungsaufgaben durchführen. Weitere Informationen finden Sie unter [PowerShell-Skripts in Analysis Services](../analysis-services/instances/powershell-scripting-in-analysis-services.md).  
  
### Community- und Drittanbietertools  
 Community-Codebeispiele finden Sie auf der [Analysis Services-Codeplex-Seite](http://sqlsrvanalysissrvcs.codeplex.com/). [Foren](http://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlanalysisservices) können hilfreich sein, wenn Sie Empfehlungen für Drittanbietertools suchen, die Analysis Services unterstützen.  
  
## Siehe auch  
 [Kompatibilitätsgrad einer mehrdimensionalen Datenbank &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  