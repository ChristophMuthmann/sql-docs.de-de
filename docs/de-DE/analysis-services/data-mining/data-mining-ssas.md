---
title: Datamining (SSAS) | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 82b5649d8893714b72aa38be381f8d2fbd0833fb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="data-mining-ssas"></a>Data Mining (SSAS)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist seit der Veröffentlichung im Jahr 2000 führend bei Predictive Analytics und stellt in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Data Mining bereit. Die Kombination von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining stellt eine integrierte Plattform für Predictive Analytics mit Datenbereinigung und -vorbereitung, Machine Learning und Berichterstellung bereit. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining umfasst mehrere Standardalgorithmen, einschließlich EM- und K-Means-Clustermodellen, neuronalen Netzwerken, logistischer und linearer Regression, Entscheidungsstrukturen und Naive Bayes-Klassifizierungen. Alle Modelle umfassen Visualisierungen, mit denen Sie Ihre Modelle entwickeln, optimieren und auswerten können.  Die Integration von Data Mining in Business Intelligence-Lösungen unterstützt Sie bei fundierten Entscheidungen zu komplexen Problemen.  
  
## <a name="benefits-of-data-mining"></a>Vorteile des Data Minings  
 Data Mining (auch als Predictive Analytics und Machine Learning bezeichnet) verwendet gut erforschte statistische Prinzipien für die Erkennung von Mustern in Ihren Daten. Indem die in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] enthaltenen Data Mining-Algorithmen auf Daten angewendet werden, können Trends vorhergesagt, Muster identifiziert, Regeln und Empfehlungen aufgestellt, die Abfolge von Ereignissen in komplexen Datasets analysiert und neue Einblicke gewonnen werden.  
  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]ist Data Mining leistungsstark, zugreifbar und integriert in die Tools, die viele für Analyse und Berichtswesen bevorzugen.  
  
## <a name="key-data-mining-features"></a>Wichtige Data Mining-Funktionen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining stellt die folgenden Funktionen zur Unterstützung integrierter Data Mining-Lösungen bereit:  
  
-   Mehrere Datenquellen: Sie können beliebige tabellarische Datenquellen für Data Mining verwenden, einschließlich Tabellenkalkulationen und Textdateien. Darüber hinaus können Sie leicht für OLAP-Cubes, die in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]erstellt wurden, Data Mining durchführen. Sie können jedoch keine Daten aus einer speicherinternen Datenbank verwenden.  
  
-   Integrierte Datenbereinigung, Datenverwaltung und Berichterstellung: [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] stellt Tools zur Profilerstellung und zum Bereinigen von Daten bereit. Sie können ETL-Prozesse zum Bereinigen von Daten als Vorbereitung für die Modellierung erstellen. Außerdem vereinfacht ssISnoversion auch das erneute Trainieren und Aktualisieren von Modellen.  
  
-   Mehrere anpassbare Algorithmen: Neben Algorithmen, beispielsweise für das Clustering, neuronale Netzwerke und Entscheidungsstrukturen, unterstützt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining die Entwicklung eigener benutzerdefinierter Plug-In-Algorithmen.  
  
-   Infrastruktur zum Testen von Modellen: Testen Sie die Modelle und Datasets unter Verwendung wichtiger Statistiktools, wie Kreuzvalidierung, Klassifikationsmatrizen, Prognosegütediagramme und Punktdiagramme. Erstellen und verwalten Sie einfach Test- und Trainingssätze.  
  
-   Abfragen und Drillthrough: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining bietet die DMX-Sprache für die Integration von Vorhersageabfragen in Anwendungen. Sie können auch detaillierte Statistiken und Muster aus den Modellen extrahieren und Drillthroughs zu Falldaten durchführen.  
  
-   Clienttools: Neben den Entwicklungs- und Entwurfsoberflächen von SQL Server können Sie mithilfe der Data Mining-Add-Ins für Excel Modelle erstellen, abfragen und durchsuchen. Alternativ können Sie benutzerdefinierte Clients, einschließlich Webdienste, erstellen.  
  
-   Unterstützung von Skriptsprachen und verwaltete API: Alle Data Mining-Objekte sind vollständig programmierbar. Skripts können mithilfe von MDX, XMLA oder der PowerShell-Erweiterungen für [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]erstellt werden. Verwenden Sie die DMX-Sprache (Data Mining Extensions, Data Mining-Erweiterungen) für die schnelle Abfrageausführung und Skripterstellung.  
  
-   Sicherheit und Bereitstellung: Bietet rollenbasierte Sicherheit durch [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], einschließlich separater Berechtigungen für Drillthroughs zu Modell- und Strukturdaten. Einfache Bereitstellung von Modellen auf anderen Servern, damit Benutzer auf die Muster zugreifen oder Vorhersagen ausführen können  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 In den Themen in diesem Abschnitt werden die Hauptfunktionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Mining sowie verwandte Tasks eingeführt.  
  
-   [Data Mining-Konzepte](../../analysis-services/data-mining/data-mining-concepts.md)  
  
-   [Datamining-Algorithmen & #40; Analysis Services – Datamining & #41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
-   [Miningstrukturen & #40; Analysis Services – Datamining & #41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
-   [Miningmodelle &#40;Analysis Services – Data Mining&#41;](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
-   [Tests und Überprüfung & #40; Datamining & #41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
-   [Datamining-Abfragen](../../analysis-services/data-mining/data-mining-queries.md)  
  
-   [Data Mining-Projektmappen](../../analysis-services/data-mining/data-mining-solutions.md)  
  
-   [Datamining-Tools](../../analysis-services/data-mining/data-mining-tools.md)  
  
-   [Data Mining-Architektur](../../analysis-services/data-mining/data-mining-architecture.md)  
  
-   [Sicherheit (Übersicht) & #40; Datamining & #41;](../../analysis-services/data-mining/security-overview-data-mining.md)  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)  
  
  
