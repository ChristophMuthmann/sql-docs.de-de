---
title: Datamining-Tools | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 26e3d36a68197607d788ca1170a2fd509698221d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="data-mining-tools"></a>Data Mining-Tools
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] stellt die folgenden Tools zum Erstellen von Data Mining-Lösungen bereit:  
  
-   Der **Data Mining-Assistent** in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] erleichtert das Erstellen von Miningstrukturen und Miningmodellen aus relationalen Datenquellen oder mehrdimensionalen Daten in Würfeln.  
  
     Im Assistenten wählen Sie die zu verwendenden Daten aus und wenden dann bestimmte Data Mining-Techniken an, z. B. Clustering, neuronale Netzwerke oder Zeitreihenmodellierungen.  
  
-   **Modell-Viewer** werden in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]bereitgestellt, um Miningmodelle nach deren Erstellung untersuchen zu können.  Sie können Modelle mit spezifischen Viewern durchsuchen, die auf den jeweiligen Algorithmus zugeschnitten sind, oder mit dem Viewer für Modellinhalte eine tiefer gehende Analyse vornehmen.  
  
-   Der **Generator für Vorhersageabfragen** wird in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] bereitgestellt, um Sie beim Erstellen von Vorhersageabfragen zu unterstützen. Außerdem können Sie die Genauigkeit von Modellen an einem zurückgehaltenen Dataset oder externen Daten überprüfen oder anhand einer Kreuzvalidierung die Qualität des Datasets bewerten.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ist die Schnittstelle, über die Sie vorhandene Data Mining-Lösungen verwalten, die auf einer Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]bereitgestellt wurden. Sie können Strukturen und Modelle erneut verarbeiten, um die enthaltenen Daten zu aktualisieren.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] beinhaltet Tools, die Sie verwenden können, um Daten zu bereinigen, Tasks zu automatisieren (z. B. für das Erstellen von Vorhersagen oder das Aktualisieren von Modellen) und Text Mining-Lösungen zu erstellen.  
  
 In den folgenden Abschnitten finden Sie weitere Informationen zu den Data Mining-Tools in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="data-mining-wizard"></a>Data Mining-Assistent  
 Verwenden Sie den Data Mining-Assistenten, um Ihre ersten Data Mining-Lösungen zu erstellen. Der Assistent ist einfach zu verwenden und führt Sie durch das Erstellen einer Data Mining-Struktur und eines verknüpften Ausgangsminingmodells und umfasst Tasks wie das Auswählen eines Algorithmustyps und einer Datenquelle sowie die Definition der Falldaten für die Analyse.  
  
 **Weitere Informationen:** [Data Mining-Assistent &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/data-mining-wizard-analysis-services-data-mining.md)  
  
## <a name="data-mining-designer"></a>Data Mining-Designer  
 Nachdem Sie mit dem Data Mining-Assistenten eine Miningstruktur und ein Miningmodell erstellt haben, können Sie den Data Mining-Designer aus [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verwenden, um mit bereits vorhandenen Modellen und Strukturen zu arbeiten.  
  
 Der Designer enthält Tools für die folgenden Tasks:  
  
-   Ändern der Eigenschaften von Miningstrukturen, Hinzufügen von Spalten und Erstellen von Spaltenaliasen, Ändern der Methode zur Klasseneinteilung oder der erwarteten Verteilung von Werten.  
  
-   Hinzufügen neuer Modelle zu einer vorhandenen Struktur, Kopieren von Modellen, Ändern von Modelleigenschaften oder Metadaten und Definieren von Filtern für ein Miningmodell.  
  
-   Durchsuchen der Muster und Regeln im Modell und Untersuchen der Zuordnungen oder Entscheidungsstrukturen. Abrufen von ausführlichen Statistiken  
  
     Benutzerdefinierte Viewer werden für jede Modellversion bereitgestellt, sodass Sie die Daten analysieren und durch das Data Mining identifizierte Muster untersuchen können.  
  
-   Überprüfen von Modellen durch das Erstellen von Prognosegütediagrammen oder Analysieren der Gewinnkurve von Modellen. Vergleichen von Modellen mithilfe von Klassifikationsmatrizen oder Überprüfen eines Datasets und seiner Modelle mit der Kreuzvalidierung.  
  
-   Erstellen von Vorhersagen und Inhaltsabfragen für vorhandene Miningmodelle. Erstellen von einmaligen Abfragen oder Einrichten von Abfragen, um Vorhersagen für ganze Tabellen mit externen Daten zu generieren.  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
 Nachdem Sie Miningmodelle erstellt und auf einem Server bereitgestellt haben, können Sie die [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] -Datenbank, die die Data Mining-Objekte hostet, mit [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verwalten. Sie können auch weiterhin Tasks ausführen, die das Modell verwenden, z. B. Untersuchen der Modelle, Verarbeiten von neuen Daten und Erstellen von Vorhersagen.  
  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] enthält auch Abfrage-Editoren, die Sie verwenden können, um DMX-Abfragen (Data Mining Extensions) zu entwerfen und auszuführen oder mithilfe von XMLA Data Mining-Objekte zu bearbeiten.  
  
## <a name="integration-services-data-mining-tasks-and-transformations"></a>Data Mining-Aufgaben und -Transformationen von Integration Services  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] stellt viele Komponenten bereit, die Data Mining unterstützen.  
  
 Einige Tools in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] wurden entworfen, um die Automatisierung allgemeiner Data Mining-Tasks zu erleichtern. Dies umfasst Tasks für Vorhersagen, Modellerstellung und Verarbeitung. Beispiel:  
  
-   Erstellen eines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakets, das jedes Mal das Modell automatisch aktualisiert, wenn das Dataset mit neuen Kunden aktualisiert wird  
  
-   Durchführen einer benutzerdefinierten Segmentierung oder Erstellen benutzerdefinierter Stichproben von Falldatensätzen.  
  
-   Automatisches Generieren von Modellen aus übergebenen Parametern.  
  
 Sie können Data Mining jedoch auch in einem Paketworkflow als Eingabe für andere Prozesse verwenden. Beispiel:  
  
-   Verwenden von Wahrscheinlichkeitswerten, die vom Modell generiert werden, um Ergebnisse für Text Mining oder andere Klassifizierungstasks zu bewerten.  
  
-   Automatisches Generieren von Vorhersagen, die auf früheren Daten basieren, und Bewerten der Gültigkeit neuer Daten anhand dieser Werte.  
  
-   Verwenden der logistischen Regression, um eine Risikoeinteilung für eingehende Kunden vorzunehmen.  
  
 **Weitere Informationen:** [Verwandte Projekte für Data Mining-Lösungen](../../analysis-services/data-mining/related-projects-for-data-mining-solutions.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen & #40; DMX & #41; Referenz](../../dmx/data-mining-extensions-dmx-reference.md)   
 [Miningmodelltasks und Anweisungen Mining](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Miningmodell-Viewer miningmodelltasks und Anweisungen](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Datamining-Lösungen](../../analysis-services/data-mining/data-mining-solutions.md)  
  
  
