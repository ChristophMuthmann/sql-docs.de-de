---
title: Data Mining-Abfragetasks | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.dataminingquerytask.f1
helpviewer_keywords:
- prediction queries [Integration Services]
- Data Mining Query task [Integration Services]
ms.assetid: f489348c-2008-4f66-8c2c-c07c3029439a
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0b171b2ce21054b6cca5f2de64fa1d04f4fa00c9
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="data-mining-query-task"></a>Data Mining-Abfragetask
  Der Data Mining-Abfragetask führt Vorhersageabfragen basierend auf in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]erstellten Data Mining-Modellen aus. Die Vorhersageabfrage erstellt mithilfe von Miningmodellen eine Vorhersage für neue Daten. Beispielsweise kann eine Vorhersageabfrage vorhersagen, wie viele Segelboote in den Sommermonaten voraussichtlich verkauft werden, oder sie kann eine Liste potenzieller Kunden generieren, die mit hoher Wahrscheinlichkeit ein Segelboot kaufen werden.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] stellt Tasks bereit, die andere Business Intelligence-Vorgänge ausführen, z.B. das Ausführen von DDL-Anweisungen (Data Definition Language, Datendefinitionssprache) und das Verarbeiten analytischer Objekte.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu weiteren Business Intelligence-Tasks zu erhalten:  
  
-   [DDL ausführen (Analysis Services-Task)](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Analysis Services-Verarbeitungstask](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
## <a name="prediction-queries"></a>Vorhersageabfragen  
 Bei der Abfrage handelt es sich um eine DMX-Anweisung (Data Mining Extensions). Die DMX-Sprache ist eine Erweiterung der SQL-Sprache, die das Arbeiten mit Miningmodellen unterstützt. Weitere Informationen zum Verwenden der DMX-Sprache finden Sie unter [Data Mining-Erweiterungen &#40;DMX&#41; – Referenz](../../dmx/data-mining-extensions-dmx-reference.md).  
  
 Der Task kann mehrere Miningmodelle abfragen, die auf der gleichen Miningstruktur basieren. Ein Miningmodell wird mithilfe eines der Data Mining-Algorithmen von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] erstellt. Die Miningstruktur des Data Mining-Abfragetasks kann mehrere Miningmodelle einschließen, die mit verschiedenen Algorithmen erstellt wurden. Weitere Informationen finden Sie unter [Miningstrukturen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md) und [Data Mining-Algorithmen &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
 Die Vorhersageabfrage, die der Data Mining-Abfragetask ausführt, gibt als Ergebnis eine einzelne Zeile oder ein Dataset zurück. Eine Abfrage, die eine einzelne Zeile zurückgibt, wird als SINGLETON-Abfrage bezeichnet: Beispielsweise gibt die Abfrage zur Vorhersage, wie viele Segelboote in den Sommermonaten verkauft werden, eine Zahl zurück. Weitere Informationen zu Vorhersageabfragen, die eine einzelne Zeile zurückgeben, finden Sie unter [Data Mining-Abfragetools](../../analysis-services/data-mining/data-mining-query-tools.md).  
  
 Die Abfrageergebnisse werden in Tabellen gespeichert. Falls eine Tabelle mit dem vom Data Mining-Abfragetask angegebenen Namen bereits vorhanden ist, kann der Task eine neue Tabelle erstellen, wobei der gleiche Name verwendet und eine Zahl angefügt wird, oder der Tabelleninhalt kann überschrieben werden.  
  
 Wenn die Ergebnisse eine Schachtelung einschließen, wird das Ergebnis vor dem Speichern vereinfacht. Durch das Vereinfachen eines Ergebnisses wird das geschachtelte Resultset in eine Tabelle geändert. Beispielsweise werden durch das Vereinfachen eines geschachtelten Ergebnisses mit einer **Customer** -Spalte und einer geschachtelten **Product** -Spalte der **Customer** -Spalte Zeilen hinzugefügt, um eine Tabelle zu erstellen, die Produktdaten für jeden Kunden enthält. Beispielsweise wird ein Kunde mit drei verschiedenen Produkten zu einer Tabelle mit drei Zeilen, wobei der Kunde in jeder Zeile wiederholt und in jeder Zeile ein anderes Produkt hinzugefügt wird. Falls das FLATTENED-Schlüsselwort ausgelassen wird, enthält die Tabelle nur die **Customer** -Spalte und nur eine einzige Zeile pro Kunde. Weitere Informationen finden Sie unter [SELECT &#40;DMX&#41;](../../dmx/select-dmx.md).  
  
## <a name="configuration-of-the-data-mining-query-task"></a>Konfiguration des Data Mining-Abfragetasks  
 Der Data Mining-Abfragetask erfordert zwei Verbindungen. Die erste Verbindung ist ein [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Verbindungs-Manager, der eine Verbindung mit einer Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oder mit einem [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Projekt herstellt, die bzw. das die Miningstruktur und das Miningmodell enthält. Die zweite Verbindung ist ein OLE DB-Verbindungs-Manager, der eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank herstellt, die die Tabelle enthält, in die der Task schreibt. Weitere Informationen finden Sie unter [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md) und [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer festlegen können:  
  
-   [Editor für Data Mining-Abfragetasks &#40;Registerkarte „Miningmodell“&#41;](../../integration-services/control-flow/data-mining-query-task-editor-mining-model-tab.md)  
  
-   [Editor für Data Mining-Abfragetasks &#40;Registerkarte „Abfrage“&#41;](../../integration-services/control-flow/data-mining-query-task-editor-query-tab.md)  
  
-   [Editor für Data Mining-Abfragetasks &#40;Registerkarte „Ausgabe“&#41;](../../integration-services/control-flow/data-mining-query-task-editor-output-tab.md)  
  
> [!NOTE]  
>  Der Transformations-Editor für Data Mining-Abfragen weist keine Seite mit Ausdrücken auf. Verwenden Sie stattdessen das Fenster **Eigenschaften** für den Zugriff auf die Tools zum Erstellen und Verwalten von Eigenschaftsausdrücken für Eigenschaften des Data Mining-Abfragetasks.  
  
 Klicken Sie auf das folgende Thema, um weitere Informationen zum Festlegen dieser Eigenschaften im [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer zu erhalten:  
  
-   [Festlegen der Eigenschaften eines Tasks oder Containers](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-data-mining-query-task"></a>Programmgesteuerte Konfiguration des Data Mining-Abfragetasks  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zum programmgesteuerten Festlegen dieser Eigenschaften zu erhalten:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.DMQueryTask.DMQueryTask>  
  
  
