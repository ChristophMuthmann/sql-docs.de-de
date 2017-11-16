---
title: Analysis Services | Microsoft Docs
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: misc
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- Analysis Services, about Analysis Services - Multidimensional Data
- SSAS
- Analysis Services
- SQL Server Analysis Services, about Analysis Services - Multidimensional Data
- SQL Server Analysis Services
- multidimensional data [Analysis Services]
- SSAS, about Analysis Services - Multidimensional Data
ms.assetid: 49d186f4-4b4d-4a5a-bb1a-e2699c64a731
caps.latest.revision: 60
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8c3a514f91e9af8de54fdbd4d9ef851c72f1911e
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="what-is-analysis-services"></a>Was ist eine Analysis Services?
  Analysis Services ist ein analytisches Datenmodul in Decision Support und Business Analytics, analytischen Daten für Geschäftsberichte und Clientanwendungen wie Excel, Power BI bereitstellt, die durch das Reporting Services-Berichte und andere Daten Visualisierungstools verwendet.  
  
 Ein typischer Workflow enthält, erstellen eine mehrdimensionale oder tabellarische Datenmodell, Bereitstellung des Modells als Datenbank mit einer lokalen SQL Server Analysis Services oder Azure Analysis Services-Serverinstanz, wiederkehrende Datenverarbeitung einrichten und zuweisen Berechtigungen zum Zugriff auf Daten von Endbenutzern zu ermöglichen. Wenn er abgeschlossen ist, kann Ihr semantische Datenmodell von allen Clientanwendungen, die Unterstützung von Analysis Services als Datenquelle zugegriffen werden.  
 
## <a name="analysis-services-on-premises-and-in-the-cloud"></a>Analysis Services lokal und in der Cloud
Analysis Services ist jetzt in der Cloud und als Azure-Dienst verfügbar. Azure Analysis Services unterstützt tabellarische Modelle mit dem Kompatibilitätsgrad 1200 oder höher. DirectQuery, Partitionen, Sicherheit auf Zeilenebene, Bidirektionale Beziehungen und Übersetzungen werden unterstützt. Um mehr über den Dienst zu erfahren, und ihn kostenlos zu testen, wechseln Sie zu [Azure Analysis Services](https://azure.microsoft.com/en-us/services/analysis-services/). 
  
## <a name="server-mode"></a>Servermodus  
 Beim Installieren von Analysis Services mithilfe von SQL Server-Setup, geben Sie während der Konfiguration einen im Servermodus für diese Instanz.  Jeder Modus umfasst verschiedene Funktionen, die für eine bestimmte Analysis Services-Lösung eindeutig sind.   
  
-   **Tabellenmodus** – implementieren speicherinterne relationale Daten modellierungskonstrukten (Modell, Tabellen, Spalten, Measures, Hierarchien).  

-   **Mehrdimensionaler und Data Mining-Modus** – Implementieren von OLAP-Modellierungskonstrukten (Cubes, Dimensionen, Measures). 

-   **Power Pivot-Modus** -implementieren PowerPivot und Excel-Datenmodelle in SharePoint (PowerPivot für SharePoint ist ein Datenmodul der mittleren Ebene, die lädt, abfragt und aktualisiert Datenmodelle in SharePoint gehostet).  
  
 Eine einzelne Instanz kann mit nur einem Modus konfiguriert werden und kann später nicht geändert werden.  Sie können mehrere Instanzen mit unterschiedlichen Modi auf dem gleichen Server installieren, aber Sie müssen das Setup ausführen und Konfigurationseinstellungen für jede Instanz festlegen. Ausführliche Informationen und einen Vergleich der verschiedenen Funktionen, die in jedem der Modi angeboten, finden Sie unter [Vergleichen von tabellarischen und mehrdimensionalen Lösungen](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md).
  
## <a name="authoring-and-managing-solutions"></a>Erstellen und Verwalten von Projektmappen  
 Um ein Modell erstellen und mit einem Server bereitgestellt haben, verwenden Sie SQL Server Data Tools, die entweder einen tabellarischen oder mehrdimensionalen und Data Mining-Projektvorlage auswählen. Die Projektvorlage enthält Ordner für alle in einem Modell erforderlichen Objekte. Assistenten und Designer können Sie viele der grundlegenden Elemente wie z. B. das Herstellen einer Verbindung mit Datenquellen, Beziehungen, Measures und Rollen erstellen. Sobald die Model-Datenbank auf einem Server bereitgestellt wird, verwenden Sie SQL Server Management Studio (SSMS) zum Verarbeiten von Daten konfigurieren, überwachen und verwalten Sie Ihre Server und Datenbanken. Weitere Informationen finden Sie unter [Tools und Anwendungen, die in Analysis Services verwendete](../analysis-services/tools-and-applications-used-in-analysis-services.md). 
  
## <a name="documentation-by-area"></a>Dokumentation nach Bereich  
Im Allgemeinen ist die Dokumentation für Azure Analysis Services in Azure-Dokumentation enthalten. Und SQL Server Analysis Services-Dokumentation ist im Lieferumfang von SQL Server-Dokumentation. Das Erstellen und Bereitstellen der Projekte ist jedoch mindestens für tabellarische Modelle nahezu identisch, unabhängig davon, welche Plattform, die Sie verwenden.  
   
*  [Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/)
*  [Neuigkeiten in SQL Server Analysis Services](../analysis-services/what-s-new-in-analysis-services.md)   
*  [Vergleichen von tabellarischen und mehrdimensionalen Lösungen](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
*  [Tabellarische Modelle](../analysis-services/tabular-models/tabular-models-ssas.md)  
*  [Mehrdimensionale Modelle](../analysis-services/multidimensional-models/multidimensional-models-ssas.md)  
*  [Data Mining](../analysis-services/data-mining/data-mining-ssas.md)  
*  [PowerPivot für SharePoint](../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
*  [Instanzverwaltung](../analysis-services/instances/analysis-services-instance-management.md)    
*  [Tutorials](../analysis-services/analysis-services-tutorials-ssas.md)   
*  [Dokumentation für Entwickler](https://msdn.microsoft.com/library/bb500153(SQL.130).aspx)  
*  [Technische Referenz (SSAS)](../analysis-services/powershell/technical-reference-ssas.md)

