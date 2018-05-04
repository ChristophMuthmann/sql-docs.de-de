---
title: Definieren von Partitionen im DirectQuery-Modelle | Microsoft Docs
ms.custom: ''
ms.date: 02/22/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5f179ba9-6efb-46ae-90e5-945bbfddb719
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: cd687fc9abdf259f0596e9691beeb27db2706341
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="define-partitions-in-directquery-models"></a>Definieren von Partitionen im DirectQuery-Modellen
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  In diesem Abschnitt wird erläutert, wie Partitionen in DirectQuery-Modellen verwendet werden. Weitere allgemeine Informationen zu Partitionen in tabellarischen Modellen finden Sie unter [Partitionen](../../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
> [!NOTE]  
>  Obwohl eine Tabelle über mehrere Partitionen verfügen kann, kann im DirectQuery-Modus nur eine von ihnen für die Verwendung in der Abfrageausführung festgelegt werden. Die Anforderung einer einzelnen Partition gilt für DirectQuery-Modelle in allen Kompatibilitätsgraden.  
  
## <a name="using-partitions-in-directquery-mode"></a>Verwenden von Partitionen im DirectQuery-Modus  
 Für jede Tabelle müssen Sie eine einzelne Partition angeben, die als DirectQuery-Datenquelle verwendet werden soll.  Wenn mehrere Partitionen vorhanden sind, wenn Sie das Modell wechseln, um den DirectQuery-Modus zu aktivieren, wird die erste Partition, die in der Tabelle erstellt wurde, standardmäßig als DirectQuery-Partition gekennzeichnet. Dies kann später mit dem Partitions-Manager in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]geändert werden.  
  
 Warum soll im DirectQuery-Modus nur eine einzelne Partition zulässig sein?  
  
 In Tabellenmodellen werden (ebenso wie in OLAP-Modellen) die Partitionen einer Tabelle von SQL-Abfragen definiert. Der Entwickler, der die Partitionsdefinition erstellt, muss gewährleisten, dass sich Partitionen nicht überschneiden. Über Analysis Services wird nicht überprüft, ob Datensätze zu einer oder mehreren Partitionen gehören.  
  
 Partitionen in einem zwischengespeicherten Tabellenmodell verhalten sich ebenso. Wenn Sie ein Modell im Arbeitsspeicher verwenden, während auf den Cache zugegriffen wird, werden DAX-Formeln für jede Partition ausgewertet, und die Ergebnisse werden kombiniert. Wenn jedoch bei einem Tabellenmodell der DirectQuery-Modus verwendet wird, ist es nicht möglich, mehrere Partitionen auszuwerten, die Ergebnisse zu kombinieren und sie zum Senden an den relationalen Datenspeicher in eine SQL-Anweisung zu konvertieren. Dies könnte zu einem nicht akzeptablen Leistungsverlust sowie zu möglichen Ungenauigkeiten führen, wenn die Ergebnisse aggregiert werden.  
  
 Aus diesem Grund verwendet der Server für im DirectQuery-Modus beantwortete Abfragen eine einzelne Partition, die als primäre Partition für DirectQuery-Zugriff markiert wurde und als *DirectQuery-Partition*bezeichnet wird.  Die in der Definition dieser Partition angegebene SQL-Abfrage definiert den vollständigen Satz der Daten, die zur Beantwortung von Abfragen im DirectQuery-Modus verwendet werden können.  
  
 Wenn Sie eine Partition nicht explizit definieren, gibt das Modul lediglich eine SQL-Abfrage an die gesamte relationale Datenquelle aus, führt alle satzbasierten Vorgänge aus, die gemäß DAX-Formel vorgeschrieben sind, und gibt die Abfrageergebnisse zurück.  
  
  
## <a name="change-a-directquery-partition"></a>Ändern einer DirectQuery-Partition  
 Da nur eine Partition in einer Tabelle als DirectQuery-Partition festgelegt werden kann, verwendet Analysis Services standardmäßig die erste Partition, die in der Tabelle erstellt wurde. Während der Modellprojekterstellung können Sie die DirectQuery-Partition im Dialogfeld Partitions-Manager in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]ändern. Für bereitgestellte Modelle können Sie die DirectQuery-Partition mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ändern.  
  
#### <a name="change-the-directquery-partition-for-a-tabular-model-project"></a>Ändern der DirectQuery-Partition für ein tabellarisches Modellprojekt  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]im Modell-Designer auf die Tabelle (Registerkarte), die die partitionierte Tabelle enthält.  
  
2.  Klicken Sie auf das Menü **Tabelle** und dann auf **Partitionen**.  
  
3.  Im **Partitions-Manager**wird die Partition, die die aktuelle Partition für direkte Abfragen ist, durch das Präfix **(DirectQuery)** für den Partitionsnamen angegeben.  
  
     Wählen Sie eine andere Partition in der Liste **Partitionen** aus, und klicken Sie dann auf **Als DirectQuery festlegen**. Die Schaltfläche **Als DirectQuery festlegen** wird bei Auswahl der aktuellen DirectQuery-Partition nicht aktiviert, und sie ist nicht sichtbar, wenn das Modell nicht für den DirectQuery-Modus aktiviert wurde.  
  
4.  Ändern Sie bei Bedarf die Verarbeitungsoptionen, und klicken Sie dann auf **OK**.  
  
#### <a name="change-the-directquery-partition-for-a-deployed-tabular-model"></a>Ändern der DirectQuery-Partition für ein bereitgestelltes tabellarisches Modell  
  
1.  Öffnen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]die Modelldatenbank in Objekt-Explorer.  
  
2.  Erweitern Sie den Knoten **Tabellen** , klicken Sie mit der rechten Maustaste auf die partitionierte Tabelle, und wählen Sie **Partitionen**aus.  
  
     Die Partition, die für die Verwendung mit dem DirectQuery-Modus festgelegt ist, besitzt das Präfix (DirectQuery) für den Partitionsnamen.  
  
3.  Um zu einer anderen Partition zu wechseln, klicken Sie auf der Symbolleiste auf das Symbol für **DirectQuery** , um das Dialogfeld **DirectQuery-Partition festlegen** zu öffnen. Das Symbol für DirectQuery auf der Symbolleiste ist nicht verfügbar für Modelle, für die DirectQuery nicht aktiviert wurde.)  
  
4.  Wählen Sie eine andere Partition in der Dropdownliste **Partitionsname** aus, und ändern Sie ggf. die Verarbeitungsoptionen für die Partition.  
  
## <a name="partitions-in-cached-models-and-in-directquery-models"></a>Partitionen in zwischengespeicherten Modellen und DirectQuery-Modellen  
 Wenn Sie eine DirectQuery-Partition konfigurieren, müssen Sie Verarbeitungsoptionen für die Partition angeben.  
  
 Zwei Verarbeitungsoptionen stehen für die DirectQuery-Partition zur Verfügung. Um diese Eigenschaft festzulegen, verwenden Sie den **Partitions-Manager** in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], und wählen Sie die Eigenschaft **Verarbeitungsoption** aus. In der folgenden Tabelle sind die Werte dieser Eigenschaft aufgeführt. Außerdem sind die Effekte jedes einzelnen Werts für den Fall beschrieben, dass ein Wert mit der DirectQueryUsage-Eigenschaft zur Verbindungszeichenfolge kombiniert wird:  
  
|Eigenschaft**Verbindungszeichenfolge** |Eigenschaft**Verarbeitungsoption** |Hinweise|  
|------------------------------------|------------------------------------|-----------|  
|DirectQuery|Kein Verarbeiten dieser Partition|Wenn das Modell ausschließlich DirectQuery verwendet, ist eine Verarbeitung niemals notwendig.<br /><br /> In Hybridmodellen können Sie die DirectQuery-Partition so konfigurieren, dass sie niemals verarbeitet wird. Beispiel: Wenn Sie ein sehr großes Dataset verwenden und dem Cache nicht die vollständigen Ergebnisse hinzufügen möchten, können Sie angeben, dass die DirectQuery-Partition die Vereinigung der Ergebnisse für alle anderen Partitionen in der Tabelle enthalten und dass niemals eine Verarbeitung stattfinden soll. Abfragen, die an die relationale Quelle gerichtet werden, sind nicht betroffen, und in Abfragen für zwischengespeicherte Daten werden Daten aus den anderen Partitionen kombiniert.|  
|DataView=Sample<br /><br /> Gilt für tabellarische Modelle mit beispieldatenansichten|Verarbeitung von Partitionen zulassen|Wenn das Modell Beispieldaten verwendet, können Sie die Tabelle verarbeiten, um ein gefiltertes Dataset zurückzugeben, das während des Modellentwurfs optische Hilfen bereitstellt.|  
|DirectQueryUsage=InMemory With DirectQuery<br /><br /> Gilt für Tabular 1100- oder 1103-Modelle in einer Kombination aus speicherinternem und DirectQuery-Modus|Verarbeitung von Partitionen zulassen|Wenn beim Modell der hybride Modus verwendet wird, sollten Sie für Abfragen für die speicherinterne Datenquelle und für die DirectQuery-Datenquelle die gleiche Partition verwenden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Partitionen](../../analysis-services/tabular-models/partitions-ssas-tabular.md)  
  
  
