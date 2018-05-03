---
title: Analysis Services Adventure Works-Lernprogramm (1400) | Microsoft Docs
description: Führt die Adventure Works-Lernprogramm für Analysis Services
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: a8de5c5fc59de248e53f4c80e81c4dd32e0ce732
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="tabular-modeling-1400-compatibility-level"></a>Tabellenmodellierung (Kompatibilitätsgrad 1400)

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Dieses Lernprogramm enthält Lektionen zum Erstellen und Bereitstellen von einem tabellarischen Modell auf der [1400 Kompatibilitätsgrad](../tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md). Wenn Sie Analysis Services und tabellarischer Modelle vertraut sind, ist das Abschluss dieses Lernprogramms die schnellste Methode erhalten Sie Informationen zum Erstellen und Bereitstellen eines grundlegenden tabellarischen Modells mithilfe von Visual Studio aus. Nachdem Sie die Voraussetzungen erfüllt sein, direkt sollte zwei bis drei Stunden dauern.  
  
## <a name="what-you-learn"></a>Was Sie lernen   
  
-   Gewusst wie: Erstellen eines neuen Projekts für tabellarische Modelle auf der **1400 Kompatibilitätsgrad** in Visual Studio mit SSDT.
  
-   Vorgehensweise beim Importieren von Daten aus einer relationalen Datenbank in eine arbeitsbereichsdatenbank für tabellarische Modelle-Projekt.  
  
-   Erstellen und Verwalten von Beziehungen zwischen Tabellen im Modell.  
  
-   Vorgehensweise: Erstellen von berechneten Spalten, Measures und Key Performance Indicators, die Benutzern wichtige Geschäftsmetriken zu analysieren.  
  
-   Zum Erstellen und Verwalten von Perspektiven und Hierarchien, die Benutzern weitere einfacher Modelldaten durchsuchen, durch die Bereitstellung von Geschäfts- und anwendungsspezifischen Blickpunkten fehlschlagen.  
  
-   Erstellen von Partitionen, mit denen sich Tabellendaten in kleinere logische Teile aufteilen lassen, die unabhängig von anderen Partitionen verarbeitet werden können.  
  
-   Sichern von Modellobjekten und -daten durch die Erstellung von Rollen mit Benutzerelementen.  
  
-   Gewusst wie: Bereitstellen eines tabellarischen Modells in einer **Azure Analysis Services** Server oder **SQL Server 2017 Analysis Services** Server mithilfe von SSDT.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  

Um dieses Lernprogramm abzuschließen, müssen wie folgt vor:  
  
-   Ein Azure Analysis Services-Server oder eine SQL Server 2017 Analysis Services-Server im tabellarischen Modus. Registrieren Sie sich für eine kostenlose [Azure Analysis Services-Testversion](https://azure.microsoft.com/services/analysis-services/) und [Erstellen eines Servers](https://docs.microsoft.com/azure/analysis-services/analysis-services-create-server) oder herunterladen, eine kostenlose [Developer Edition von SQL Server 2017](https://www.microsoft.com/sql-server/sql-server-downloads).

-   Ein [Azure SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/create-data-warehouse-portal) mit der **AdventureWorksDW-Beispieldatenbank**, oder eine lokale SQL Server Data Warehouse mit einer [AdventureWorksDW-Beispieldatenbank](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks). Wenn AdventureWorksDW-Datenbank auf einer lokalen SQL Server-Data Warehouse zu installieren, verwenden Sie die Version der Beispiel-Datenbank, die ab, entspricht mit Ihrer Version des Servers. 

    **Wichtig:** , wenn Sie die Beispieldatenbank auf einer lokalen SQL Server-Data Warehouse installieren und Ihr Modell auf einem Azure Analysis Services-Server Bereitstellen einer [On-Premises Data Gateway](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway) ist erforderlich.

-   Die neueste Version des [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx). Oder, wenn Sie bereits Visual Studio 2017 verfügen, können Sie herunterladen und installieren [Microsoft Analysis Services-Projekten](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects) Paket (VSIX). Für dieses Lernprogramm sind Verweise auf SSDT und Visual Studio Synonym. 

-   Die neueste Version des [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).    

-   Eine Clientanwendung, z. B. [Power BI Desktop](https://powerbi.microsoft.com/desktop/) oder Excel. 

## <a name="scenario"></a>Szenario  

Dieses Lernprogramm basiert auf dem Adventure Works Cycles, einem fiktiven Unternehmen. Adventure Works ist ein großes, multinationales Fertigungsunternehmen, die produziert und vertreibt Fahrräder, Teilen und Zubehör für kommerzielle Märkte in Nordamerika, Europa und Asien. Das Unternehmen beschäftigt 500 Arbeiter. Darüber hinaus Verkaufsteams Adventure Works mehrere regionalen gesamte marktbasis. Ihr Projekt wird zum Erstellen eines tabellarischen Modells für Vertrieb und marketing Benutzer um internetumsatzdaten in der AdventureWorksDW-Datenbank zu analysieren.  
  
Um das Lernprogramm abgeschlossen haben, müssen Sie verschiedene Lektionen abschließen. Es gibt Aufgaben, in der jeweiligen Lektion. Abschließen jeder Aufgabe in der Reihenfolge ist zum Abschließen der Lektion erforderlich. Während in einer bestimmten Lektion gibt es möglicherweise mehrere Aufgaben, die einem ähnlichen Ergebnis zu erreichen, aber wie jede Aufgabe etwas anders ist. Diese Methode zeigt, dass es ist häufig mehr als eine Möglichkeit zum Abschluss einer Aufgabe, und fordern Sie mithilfe von Fähigkeiten, die Sie in vorherigen Lektionen und Aufgaben gelernt haben.  
  
Die Lektionen ist, führt Sie durch die Erstellung eines grundlegenden tabellarischen Modells unter Verwendung von vielen in SSDT enthaltenen Features. Da jede Lektion auf der jeweils vorherigen Lektion aufbaut, sollten Sie die Lektionen in der entsprechenden Reihenfolge bearbeiten.
  
Dieses Lernprogramm bietet keine Lektionen zur Verwaltung eines Servers im Azure-Portal Verwalten von einem Server oder die Datenbank mithilfe von SSMS oder mithilfe einer Clientanwendung zum Durchsuchen von Modelldaten. 


## <a name="lessons"></a>Lektionen  

Dieses Tutorial umfasst die folgenden Lektionen:  
  
|Lektion|Für den Abschluss voraussichtlich benötigte Zeit|  
|----------|------------------------------|  
|[1. Erstellen eines neuen tabellenmodellprojekts](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md)|10 Minuten|  
|[2: Get Data](../tutorial-tabular-1400/as-lesson-2-get-data.md)|10 Minuten|  
|[3: Als Datumstabelle markieren](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md)|3 Minuten|  
|[4: Beziehungen erstellen](../tutorial-tabular-1400/as-lesson-4-create-relationships.md)|10 Minuten|  
|[5: Erstellen von berechneten Spalten](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md)|15 Minuten|
|[6: Erstellen von Measures](../tutorial-tabular-1400/as-lesson-6-create-measures.md)|30 Minuten|  
|[7 - erstellen Sie Key Performance Indicators (KPI)](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md)|15 Minuten|  
|[8: Erstellen von Perspektiven](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md)|5 Minuten|  
|[9: Erstellen von Hierarchien](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)|20 Minuten|  
|[10: Erstellen von Partitionen](../tutorial-tabular-1400/as-lesson-10-create-partitions.md)|15 Minuten|  
|[11: Erstellen von Rollen](../tutorial-tabular-1400/as-lesson-11-create-roles.md)|15 Minuten|  
|[12: Analysieren in Excel](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md)|5 Minuten| 
|[13: Bereitstellen](../tutorial-tabular-1400/as-lesson-13-deploy.md)|5 Minuten|  
  
## <a name="supplemental-lessons"></a>Ergänzende Lektionen  

Diese Lektionen sind nicht erforderlich, um das Lernprogramm abgeschlossen haben, jedoch können bei besseren Verständnis erweiterte tabellenmodellerstellung Funktionen hilfreich sein.  
  
|Lektion|Für den Abschluss voraussichtlich benötigte Zeit|  
|----------|------------------------------|  
|[Detailzeilen](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)|10 Minuten|
|[Dynamische Sicherheit](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)|30 Minuten|
|[Unregelmäßige Hierarchien](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)|20 Minuten| 

  
## <a name="next-steps"></a>Nächste Schritte  

Um zu beginnen, finden Sie unter [Lektion 1: erstellen ein neuen tabellenmodellprojekts](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md).  
  
  
  

