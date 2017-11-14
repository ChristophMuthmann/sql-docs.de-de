---
title: "Partitionen (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 708b9bdf-8c0b-4476-809a-8f616be23a58
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 729c24cf80e99f6f0e2596c51bfbc8bdf2490d0d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="partitions"></a>Partitionen
  Durch Partitionen wird eine Tabelle logisch unterteilt. Jede Partition kann unabhängig von anderen Partitionen verarbeitet (aktualisiert) werden. Mithilfe des Dialogfelds Partitionen in SSDT während der Modellerstellung erstellte Partitionen gelten für die arbeitsbereichsdatenbank des Modells. Beim Bereitstellen des Modells werden die für die Arbeitsbereichsdatenbank des Modells definierten Partitionen in der bereitgestellten Modelldatenbank dupliziert. Sie können weitere erstellen und Verwalten von Partitionen für eine bereitgestellte Modelldatenbank mithilfe des Dialogfelds Partitionen in SSMS.  In diesem Thema werden Partitionen beschrieben erstellt während der Modellerstellung mithilfe des Dialogfelds Partitions-Manager in SSDT. Informationen zum Erstellen und Verwalten von Partitionen für ein bereitgestelltes Modell finden Sie unter [erstellen und Verwalten von Partitionen tabellarischen Modell](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md).  
  
##  <a name="bkmk_benefits"></a> Vorteile  
 Durch Partitionen in tabellarischen Modellen werden Tabellen in logische Partitionsobjekte unterteilt. Anschließend kann jede Partition unabhängig von anderen Partitionen verarbeitet werden. Eine Tabelle kann z. B. bestimmte Rowsets mit Daten enthalten, die selten geändert werden, während andere Rowsets Daten enthalten, die häufig geändert werden. In diesen Fällen ist es nicht erforderlich, sämtliche Daten zu verarbeiten, wenn tatsächlich nur ein Teil der Daten verarbeitet werden soll. Mit Partitionen können Daten, die häufig verarbeitet werden müssen, und Daten, die weniger häufig verarbeitet werden müssen, voneinander getrennt werden.  
  
 Bei einem effizienten Modellentwurf werden Partitionen genutzt, um unnötige Verarbeitungsschritte und die daraus resultierende Belastung der Analysis Services-Serverprozessoren zu eliminieren und gleichzeitig sicherzustellen, dass bestimmte Daten so häufig verarbeitet und aktualisiert werden, dass immer die neuesten Daten aus den Datenquellen bereitgestellt werden. Die Implementierung und Verwendung von Partitionen während der Modellerstellung kann sich erheblich von der Implementierung und Verwendung von Partitionen für bereitgestellte Modelle unterscheiden. Sie sollten bedenken, dass Sie während der Modellerstellungsphase möglicherweise nur mit einem Bruchteil der Daten arbeiten, die letztendlich im bereitgestellten Modell enthalten sind.  
  
### <a name="processing-partitions"></a>Verarbeitung von Partitionen  
 Tritt auf, Verarbeitung, für bereitgestellte Modelle mithilfe von SSMS oder durch Ausführen eines Skripts aus dem der Verarbeitungsbefehl sowie Verarbeitungsoptionen und-Einstellungen angegeben. Beim Erstellen von Modellen mithilfe von SSDT können Sie Verarbeitungsvorgänge mithilfe des Befehls Verarbeiten der Symbolleiste oder im Modell ausführen. Ein Verarbeitungsvorgang kann für eine Partition, eine Tabelle oder beides angegeben werden.  
  
 Beim Ausführen eines Verarbeitungsvorgangs wird unter Verwendung der Datenverbindung eine Verbindung mit der Datenquelle hergestellt. In die Modelltabellen werden neue Daten importiert, es werden Beziehungen und Hierarchien für die einzelnen Tabellen neu erstellt, und Berechnungen in berechneten Spalten und Measures werden neu berechnet.  
  
 Indem Sie eine Tabelle weiter in logische Partitionen unterteilen, können Sie selektiv bestimmen, welche Daten in den einzelnen Partitionen, wann und wie verarbeitet werden. Wenn Sie ein Modell bereitstellen, Verarbeitung der Partitionen manuell mithilfe des Dialogfelds Partitionen in SSMS abgeschlossen werden kann, oder mithilfe eines Skripts, das einen Verarbeitungsbefehl ausführt.  
  
### <a name="partitions-in-the-model-workspace-database"></a>Partitionen in der Arbeitsbereichsdatenbank des Modells  
 Sie können neue Partitionen erstellen, bearbeiten, Zusammenführen oder Löschen von Partitionen, die mit der Partitions-Manager in SSDT. Je nach dem Kompatibilitätsgrad des Modells, die Sie erstellen, Partitions-Manager bietet zwei Modi zum Auswählen von Tabellen, Zeilen und Spalten für eine Partition: für Tabellenmodelle 1400, Partitionen mit einer M-Abfrage definiert sind oder können Sie im Entwurfsmodus um zu öffnen Abfrage-Editor. Für tabellarische 1100 verwenden 1103, 1200-Modelle tabellenvorschaumodus und SQL-Abfragemodus. 
  
### <a name="partitions-in-a-deployed-model-database"></a>Partitionen in der Datenbank eines bereitgestellten Modells  
 Wenn Sie ein Modell bereitstellen, werden die Partitionen für die bereitgestellte Modelldatenbank als Datenbankobjekte in SSMS angezeigt. Sie können erstellen, bearbeiten, Zusammenführen und Löschen von Partitionen für ein bereitgestelltes Modell mithilfe des Dialogfelds Partitionen in SSMS. Verwalten von Partitionen für ein bereitgestelltes Modell in SSMS ist außerhalb des Bereichs der in diesem Thema. Informationen zum Verwalten von Partitionen in SSMS finden Sie unter [erstellen und Verwalten von Partitionen tabellarischen Modell](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md).  
  
##  <a name="bkmk_related_tasks"></a> Verwandte Aufgaben  
  
|Thema|Description|  
|-----------|-----------------|  
|[Erstellen und Verwalten von Partitionen in der Arbeitsbereichsdatenbank](../../analysis-services/tabular-models/create-and-manage-partitions-in-the-workspace-database-ssas-tabular.md)|Beschreibt das Erstellen und Verwalten von Partitionen in der arbeitsbereichsdatenbank des Modells mithilfe des Partitions-Manager in SSDT.|  
|[Verarbeiten von Partitionen in der Arbeitsbereichsdatenbank](../../analysis-services/tabular-models/process-partitions-in-the-workspace-databse-ssas-tabular.md)|Beschreibt, wie Partitionen in der Arbeitsbereichsdatenbank des Modells verarbeitet (aktualisiert) werden.|  
  
## <a name="see-also"></a>Siehe auch  
 [DirectQuery-Modus](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Verarbeiten von Daten](../../analysis-services/tabular-models/process-data-ssas-tabular.md)  
  
  

