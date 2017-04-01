---
title: "Wichtige &#196;nderungen von Analysis Services-Funktionen in SQL Server 2016 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Aktuelle Änderungen [Analysis Services]"
  - "Aktualisieren von Analysis Services"
ms.assetid: aeb02542-5a6c-458c-a110-13413dd3e9d9
caps.latest.revision: 55
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 53
---
# Wichtige &#196;nderungen von Analysis Services-Funktionen in SQL Server 2016
  Eine *wichtige Änderung* bewirkt, dass ein Datenmodell, Anwendungscode oder Skript nach dem Aktualisieren des Modells oder Servers nicht mehr funktioniert.  
  
> [!NOTE]  
>  Im Gegensatz dazu erfolgt bei einer *Verhaltensänderung* eine Änderung des Codes, wodurch ein Modell oder eine Anwendung weiterhin funktioniert, sich gegenüber einer früheren Version jedoch anders verhält.  Zu den Verhaltensweisen, die sich ändern können, zählen beispielsweise geänderte Standardwerte oder das Untersagen einer bisher erlaubten Konfiguration von Eigenschaften oder Optionen. Informationen zu Verhaltensänderungen in dieser Version finden Sie unter [Verändertes Verhalten von Analysis Services-Funktionen in SQL Server 2016](../analysis-services/behavior-changes-to-analysis-services-features-in-sql-server-2016.md).  
  
## .NET 4.0-Versionsupgrade  
 Die Clientbibliotheken von Analysis Services Management Objects (AMO), ADOMD.NET und Tabular Object Model (TOM) in [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] sind jetzt auf die .NET 4.0-Runtime ausgerichtet. Dies kann für Anwendungen, die auf .NET 3.5 ausgerichtet sind, eine wichtige Änderung sein. Anwendungen, die neuere Versionen dieser Assemblys verwenden, müssen jetzt auf .NET 4.0 oder höher ausgerichtet sein.  
  
## AMO-Versionsupgrade  
 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] ist ein Versionsupgrade für [Analysis Services Management Objects &#40;AMO&#41;](../Topic/Analysis%20Services%20Management%20Objects%20\(AMO\).md) und stellt unter bestimmten Umständen eine wichtige Änderung dar.  Vorhandener Code und Skripts, die AMO aufrufen, werden bei einem Upgrade von einer vorherigen Version wie bisher ausgeführt. Wenn Sie jedoch Ihre Anwendung *rekompilieren* und auf eine bestimmte [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)]-Instanz ausrichten möchten, müssen Sie den folgenden Namespace hinzufügen, damit Ihr Code oder Skript funktionsfähig wird:  
  
```  
  
using Microsoft.AnalysisServices;  
using Microsoft.AnalysisServices.Core;  
  
```  
  
 Der Namespace [Microsoft.AnalysisServices.Core](../Topic/Microsoft.AnalysisServices.Core.md) ist jetzt jedes Mal erforderlich, wenn Sie die Microsoft.AnalysisServices-Assembly in Ihrem Code referenzieren. Objekte, die zuvor nur im **Microsoft.AnalysisServices**-Namespace enthalten waren, werden in dieser Version in den Core-Namespace verschoben, wenn das Objekt in tabellarischen und mehrdimensionalen Szenarien auf die gleiche Weise verwendet wird.  Beispielsweise werden serverorientierte APIs zum Core-Namespace verschoben.  
  
 Obgleich jetzt mehrere Namespaces vorhanden sind, existieren alle in derselben Assembly (Microsoft.AnalysisServices.dll).  
  
## Änderungen an XEvent DISCOVER  
 Um das XEvent DISCOVER-Streaming in SSMS für [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] besser zu unterstützen, wird `DISCOVER_XEVENT_TRACE_DEFINITION` durch folgende XEvent-Ablaufverfolgungen ersetzt:  
  
-   DISCOVER_XEVENT_PACKAGES  
  
-   DISCOVER_XEVENT_OBJECT  
  
-   DISCOVER_XEVENT_OBJECT_COLUMNS  
  
-   DISCOVER_XEVENT_SESSION_TARGETS  
  
## Siehe auch  
 [Analysis Services Backward Compatibility](../analysis-services/analysis-services-backward-compatibility.md)  
  
  