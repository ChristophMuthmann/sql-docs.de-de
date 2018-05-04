---
title: Datamining-Designer | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4f14ec670668253fa9e37db9647d5ef511150816
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="data-mining-designer"></a>Data Mining-Designer
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Der Data Mining-Designer ist die primäre Umgebung, in der Sie in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]mit Miningmodellen arbeiten. Sie können auf den Designer zugreifen, indem Sie eine vorhandene Miningstruktur auswählen oder indem Sie den Data Mining-Assistenten verwenden, um eine neue Miningstruktur und ein neues Miningmodell zu erstellen. Sie können mit dem Data Mining-Designer folgende Aufgaben ausführen:  
  
-   Modifizieren der Miningstruktur und des Miningmodells, die ursprünglich vom Data Mining-Assistenten erstellt wurden.  
  
-   Erstellen neuer Modelle basierend auf vorhandenen Miningstrukturen.  
  
-   Trainieren und Durchsuchen von Miningmodellen.  
  
-   Vergleichen von Modellen mithilfe von Genauigkeitsdiagrammen.  
  
-   Erstellen von Vorhersageabfragen basierend auf Miningmodellen.  
  
## <a name="mining-structure-tab"></a>Miningstruktur (Registerkarte)  
 Verwenden Sie die Registerkarte **Miningstruktur** , um Spalten hinzuzufügen und die Eigenschaften einer vorhandenen Miningstruktur zu ändern. Die folgenden Tasks und Themen enthalten weitere Informationen zum Arbeiten mit Miningstrukturen:  
  
 [Miningstrukturen & #40; Analysis Services – Datamining & #41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
 [Tasks und Anweisungen für Miningstrukturen](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
## <a name="mining-models-tab"></a>Miningmodelle (Registerkarte)  
 Verwenden Sie die Registerkarte **Miningmodelle** , um vorhandene Miningmodelle zu verwalten und neue Modelle zu erstellen. Miningmodelle basieren stets auf einer vorhandenen Miningstruktur.  
  
 Auf der Registerkarte **Miningmodelle** können Sie den Algorithmustyp ändern, Spalten, die der Modellstruktur zugeordnet sind, hinzufügen oder entfernen, algorithmusspezifische Spalteneigenschaften zuweisen, die Verwendung der Miningmodellspalte angeben sowie Algorithmusparameter anpassen, die dem Miningmodell zugeordnet sind. Sie können die Miningstruktur zusammen mit den ausgewählten Modellen oder mit allen verknüpften Modellen verarbeiten.  
  
 In den folgenden Themen finden Sie weitere Informationen zum Arbeiten mit Miningmodellen:  
  
 [Miningmodelle & #40; Analysis Services – Datamining & #41;](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
 [Miningmodelltasks und Anweisungen Mining](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
## <a name="mining-model-viewer-tab"></a>Miningmodell-Viewer (Registerkarte)  
 Verwenden Sie die Registerkarte **Miningmodell-Viewer** , um Ihre Miningmodelle optisch zu analysieren. Jedes Miningmodell ist einem benutzerdefinierten Viewer zugeordnet, der Inhalte anzeigt, die für das Modell spezifisch sind. Sie können den Miningmodellinhalt auch anzeigen, indem Sie den Viewer für den Inhalt verwenden.  
  
 In den folgenden Themen finden Sie weitere Informationen zum Anzeigen von Miningmodellen mit den Data Mining-Viewern:  
  
 [Datamining-Modell-Viewer](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
 [Miningmodell-Viewer miningmodelltasks und Anweisungen](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)  
  
## <a name="mining-accuracy-chart-tab"></a>Mininggenauigkeitsdiagramm (Registerkarte)  
 Verwenden Sie die Registerkarte **Mininggenauigkeitsdiagramm** , um die Vorhersagegenauigkeit eines einzelnen Miningmodells zu testen oder die Wirksamkeit mehrerer Miningmodelle in einer Miningstruktur zu vergleichen. Die Registerkarte enthält Tools zum Filtern der Daten, zum Auswählen der Miningmodelle und zum Anzeigen der Ergebnisse in einem Lift- oder Gewinndiagramm oder einer Klassifikationsmatrix.  
  
 Weitere Informationen zum Testen und Überprüfen von Miningmodellen finden Sie in den folgenden Themen:  
  
 [Tests und Überprüfung & #40; Datamining & #41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
 [Tests und Überprüfung Tasks und Anweisungen für & #40; Datamining & #41;](../../analysis-services/data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)  
  
## <a name="mining-model-prediction-tab"></a>Miningmodellvorhersage (Registerkarte)  
 Die Registerkarte **Miningmodellvorhersage** enthält den Generator für Vorhersageabfragen, mit dem Sie eine DMX-Vorhersageabfrage (Data Mining Extensions; Data Mining-Erweiterungen) erstellen können. Die Registerkarte enthält Tools zum Angeben von Miningmodellen und Eingabetabellen, zum Zuordnen der Spalten des Miningmodells mit Spalten in der Eingabetabelle, zum Hinzufügen von Funktionen zu einer Abfrage und zum Angeben von Kriterien für jede Spalte.  
  
 Nachdem Sie eine Abfrage entworfen haben, können Sie verschiedene Sichten der Registerkarte verwenden, um die Ergebnisse der Abfrage anzuzeigen und die Abfrage manuell zu ändern. Sie können die Ergebnisse der Abfrage auch in einer Tabelle in einer Datenbank speichern.  
  
 Weitere Informationen zum Erstellen von Data Mining-Abfragen finden Sie in den folgenden Themen:  
  
 [Datamining-Abfragen](../../analysis-services/data-mining/data-mining-queries.md)  
  
 [Datamining-Abfragetasks und Anweisungen](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Lösungen](../../analysis-services/data-mining/data-mining-solutions.md)  
  
  
