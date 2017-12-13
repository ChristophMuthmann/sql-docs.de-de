---
title: "Anforderungen und Überlegungen für Analysis Services-Bereitstellung | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- memory [Analysis Services]
- scalability [Analysis Services]
- space [Analysis Services]
- Analysis Services deployments, requirements
- deploying [Analysis Services], requirements
- disk space [Analysis Services]
- requirements [Analysis Services]
- processors [Analysis Services]
- system requirements [Analysis Services]
- availability [Analysis Services]
ms.assetid: ef1387a5-5137-4ef4-b731-fec347e5f5ed
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: ca6771f8ea74bdff21f67704a1d45915b6d73cf6
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="requirements-and-considerations-for-analysis-services-deployment"></a>Anforderungen und Überlegungen für die Bereitstellung von Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Die Leistung und Verfügbarkeit einer Lösung hängt von vielen Faktoren ab, einschließlich der Funktionen der zugrunde liegenden Hardware, die Topologie der serverbereitstellung, die Merkmale der Projektmappe (z. B. mit der Verteilung von Partitionen auf mehrere Server oder mit dem ROLAP-Speicher, die direkten Zugriff auf das relationale Modul erfordert), Vereinbarungen zum Servicelevel und der Komplexität des Datenmodells.  
  
## <a name="memory-and-processor-requirements"></a>Arbeitsspeicher- und Prozessoranforderungen  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] benötigt unter folgenden Umständen zusätzliche Arbeitsspeicher- und Prozessorressourcen:  
  
-   Wenn große oder komplexe Cubes verarbeitet werden. Diese benötigen eine größere Menge von Arbeitsspeicher- und Prozessorressourcen als kleine oder einfache Cubes.  
  
-   Wenn die Anzahl der Cubes in einer einzelnen Datenbank zunimmt.  
  
-   Wenn die Anzahl der Datenbanken in einer einzelnen Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zunimmt.  
  
-   Wenn die Anzahl der Instanzen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] auf einem einzelnen Computer zunimmt.  
  
-   Wenn die Anzahl der Benutzer zunimmt, die gleichzeitig auf die [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Ressourcen zugreifen.  
  
 Wie viel Arbeitsspeicher- und Prozessorressourcen für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zur Verfügung stehen, hängt von der SQL Server-Edition, dem Betriebssystem, den Hardwarefunktionen sowie davon ab, ob Sie virtuelle oder physische Prozessoren verwenden. Weitere Informationen finden Sie unter den folgenden Links:  
  
 [Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
 [Rechenkapazitätsgrenzen von bestimmten Editionen von SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)  
  
 [Von den SQL Server 2016-Editionen unterstützte Funktionen](../../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)  
  
 [Spezifikationen der maximalen Kapazität &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/olap-physical/maximum-capacity-specifications-analysis-services.md)  
  
## <a name="disk-space-requirements"></a>Anforderungen an den Datenträgerspeicher  
 Verschiedene Aspekte der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Installation und die Tasks, die sich auf Objektverarbeitung beziehen, erfordern unterschiedlichen Speicherplatz. In der folgenden Liste werden diese Anforderungen beschrieben.  
  
 Cubes  
 Cubes, die große Faktentabellen besitzen, verlangen mehr Speicherplatz als Cubes mit kleinen Faktentabellen. Entsprechend (wenn auch in geringerem Umfang) erfordern Cubes mit zahlreichen großen Dimensionen mehr Speicherplatz als Cubes mit einer geringeren Anzahl von Dimensionselementen. Im Allgemeinen können Sie erwarten, dass eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank ungefähr 20 Prozent des Speicherplatzes erfordert, der für die gleichen Daten benötigt wird, die in der zugrunde liegenden relationalen Datenbank gespeichert sind.  
  
 Aggregationen  
 Aggregationen erfordern proportional zu den hinzugefügten Aggregationen zusätzlichen Speicherplatz – je mehr Aggregationen vorhanden sind, desto mehr Speicherplatz ist erforderlich. Wenn Sie das Erstellen nicht erforderlicher Aggregationen vermeiden, sollte der für Aggregationen benötigte Speicherplatz in der Regel ungefähr 10 Prozent der Größe der Daten nicht übersteigen, die in der zugrunde liegenden relationalen Datenbank gespeichert sind.  
  
 Data Mining  
 Standardmäßig speichern Miningstrukturen das Dataset, mit dem sie trainiert werden, auf dem Datenträger zwischen. Um diese zwischengespeicherten Daten vom Datenträger zu entfernen, können Sie die Verarbeitungsoption **Klarstruktur verarbeiten** für das Miningstrukturobjekt verwenden. Weitere Informationen finden Sie unter [Anforderungen und Überlegungen zur Verarbeitung &#40;Data Mining&#41;](../../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md).  
  
 Objektverarbeitung  
 Während der Verarbeitung speichert [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Kopien der Objekte, die aktuell verarbeitet werden, in der Verarbeitungstransaktion auf dem Datenträger, bis die Verarbeitung abgeschlossen ist. Nachdem die Verarbeitung abgeschlossen ist, ersetzen die verarbeiteten Kopien der Objekte die ursprünglichen Objekte. Daher müssen Sie ausreichend zusätzlichen Speicherplatz für eine zweite Kopie jedes Objekts vorsehen, das verarbeitet werden soll. Wenn Sie z.&nbsp;B. die Verarbeitung eines gesamten Cubes in einer einzigen Transaktion planen, benötigen Sie ausreichend Speicherplatz zum Speichern einer zweiten Kopie des gesamten Cubes.  
  
##  <a name="BKMK_Availability"></a> Überlegungen zur Verfügbarkeit  
 In einer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Umgebung ist ein Cube oder Miningmodell möglicherweise für die Abfrage nicht verfügbar, weil ein Hardware- oder Softwarefehler aufgetreten ist. Ein Cube kann auch nicht verfügbar sein, weil er verarbeitet werden muss.  
  
### <a name="providing-availability-in-the-event-of-hardware-or-software-failures"></a>Gewährleisten der Verfügbarkeit im Fall von Hardware- oder Softwarefehlern  
 Die Hardware oder Software kann aus verschiedenen Gründen ausfallen. Das Wahren der Verfügbarkeit Ihrer [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Installation bezieht sich jedoch nicht nur auf die Problembehandlung der Quellen dieser Fehler, sondern auch auf das Bereitstellen alternativer Ressourcen, die dem Benutzer die weitere Verwendung des Systems ermöglichen, wenn ein Fehler auftritt. Cluster- und Lastenausgleichsserver werden normalerweise zum Bereitstellen der alternativen Ressourcen verwendet, die zum Wahren der Verfügbarkeit erforderlich sind, wenn Hardware- oder Softwarefehler auftreten.  
  
 Um die Verfügbarkeit im Fall eines Hardware- oder Softwarefehlers zu gewährleisten, sollten Sie das Bereitstellen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in einem Failovercluster in Betracht ziehen. In einem Failovercluster führt [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Clustering ein Failover auf einen sekundären Knoten durch, wenn der primäre Knoten aus einem bestimmten Grund einen Fehler aufweist oder neu gestartet werden muss. Nach dem schnell eintretenden Failover greifen Benutzer beim Ausführen einer Abfrage auf eine Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zu, die auf dem sekundären Knoten ausgeführt wird. Weitere Informationen zu Failoverclustern finden Sie unter [Windows Server Technologies:  Failover Clusters](http://technet.microsoft.com/library/cc732488\(v=WS.10\).aspx)(Windows Server-Technologien: Failovercluster).  
  
 Eine andere Lösung bei Verfügbarkeitsproblemen besteht im Bereitstellen des [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekts auf zwei oder mehr Produktionsservern. Anschließend können Sie die Netzwerklastenausgleich-Funktion von Windows-Servern zum Kombinieren der Produktionsserver in einem einzigen Cluster verwenden. In einem NLB-Cluster leitet der NLB-Dienst Benutzerabfragen an die Server um, die noch verfügbar sind, wenn ein Server im Cluster aufgrund von Hardware- oder Softwareproblemen nicht verfügbar ist.  
  
### <a name="providing-availability-while-processing-structural-changes"></a>Gewährleisten der Verfügbarkeit während der Verarbeitung struktureller Änderungen  
 Bestimmte Änderungen an einem Cube können bewirken, dass der Cube bis zu seiner Verarbeitung nicht verfügbar ist. Wenn Sie z.&nbsp;B. strukturelle Änderungen an einer Dimension in einem Cube vornehmen, muss selbst dann, wenn Sie die Dimension erneut verarbeiten, jeder Cube, der die geänderte Dimension verwendet, ebenfalls verarbeitet werden. Bis Sie diese Cubes verarbeitet haben, können sie nicht durch Benutzer abgefragt werden; es können auch keine Miningmodelle abgefragt werden, die auf einem Cube basieren, der die geänderte Dimension aufweist.  
  
 Wenn Sie die Verfügbarkeit gewährleisten möchten, während die Verarbeitung struktureller Änderungen erfolgt, die sich auf einen oder mehrere Cubes in einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt auswirken können, sollten Sie die Integration eines Stagingservers und das Verwenden des Assistenten zum Synchronisieren einer Datenbank in Betracht ziehen. Mit dieser Funktion können Sie Daten und Metadaten auf einem Stagingserver aktualisieren und dann eine Onlinesynchronisierung des Produktionsservers und des Stagingservers durchführen. Weitere Informationen finden Sie unter [Synchronize Analysis Services Databases](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md).  
  
 Wenn Sie inkrementelle Aktualisierungen der Quelldaten transparent verarbeiten möchten, aktivieren Sie proaktives Zwischenspeichern. Durch proaktives Zwischenspeichern werden Cubes mit neuen Quelldaten aktualisiert, ohne dass manuelle Verarbeitung erforderlich ist bzw. die Verfügbarkeit von Cubes beeinträchtigt wird. Weitere Informationen finden Sie unter [Proaktives Zwischenspeichern &#40;Partitionen&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
##  <a name="BKMK_Scalability"></a> Skalierbarkeitsüberlegungen  
 Mehrere Instanzen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] auf dem gleichen Computer können zu Leistungsproblemen führen. Eine Option zum Lösen dieser Probleme kann im Vergrößern der Prozessor-, Arbeitsspeicher- und Datenträgerressourcen auf dem Server bestehen. Möglicherweise müssen Sie jedoch auch die Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] über mehrere Computer hinweg skalieren.  
  
### <a name="scaling-analysis-services-across-multiple-computers"></a>Skalieren von Analysis Services über mehrere Computer hinweg  
 Es gibt mehrere Möglichkeiten, um eine Installation von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] über mehrere Computer hinweg zu skalieren. In der folgenden Liste werden diese Optionen beschrieben.  
  
-   Wenn mehrere Instanzen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] auf einem Computer vorhanden sind, können Sie eine oder mehrere Instanzen auf einen anderen Computer verschieben.  
  
-   Wenn mehrere [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbanken auf einem Computer vorhanden sind, können Sie eine oder mehrere der Datenbanken in eine eigene Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] auf einen separaten Computer verschieben.  
  
-   Wenn eine oder mehrere relationale Datenbanken Daten für eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank bereitstellen, können Sie diese Datenbanken auf einen separaten Computer verschieben. Bevor Sie die Datenbanken verschieben, berücksichtigen Sie die gegebene Netzwerkgeschwindigkeit und Bandbreite zwischen der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Datenbank und den zugrunde liegenden Datenbanken. Wenn das Netzwerk langsam oder überlastet ist, wirkt sich das Verschieben der zugrunde liegenden Datenbanken auf einen separaten Computer negativ auf die Verarbeitungsleistung aus.  
  
-   Wenn sich die Verarbeitung auf die Abfrageleistung auswirkt, die Verarbeitung jedoch nicht zu Zeiten verringerter Abfragelast durchgeführt werden kann, sollten Sie das Verschieben der Verarbeitungstasks auf einen Stagingserver in Erwägung ziehen und dann eine Onlinesynchronisierung des Produktionsservers und des Stagingservers ausführen. Weitere Informationen finden Sie unter [Synchronize Analysis Services Databases](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md). Sie können die Verarbeitung mithilfe von Remotepartitionen auch auf mehrere Instanzen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verteilen. Das Verarbeiten von Remotepartitionen verwendet Prozessor- und Speicherressourcen auf dem Remoteserver anstelle von Ressourcen auf dem lokalen Computer. Weitere Informationen zur Verwaltung von Remotepartitionen finden Sie unter [Erstellen und Verwalten einer Remotepartition &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md).  
  
-   Wenn die Abfrageleistung schlecht ist, die Prozessor- und Speicherressourcen auf dem lokalen Server jedoch nicht vergrößert werden können, können Sie ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt auf zwei oder mehr Produktionsservern bereitstellen. Anschließend können Sie Netzwerklastenausgleich zum Kombinieren der Server in einem einzigen Cluster verwenden. In einem NLB-Cluster werden Abfragen automatisch auf alle Server im NLB-Cluster verteilt.  
  
  
