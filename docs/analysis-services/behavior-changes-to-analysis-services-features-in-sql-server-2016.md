---
title: "Ver&#228;ndertes Verhalten von Analysis Services-Funktionen in SQL Server 2016 | Microsoft Docs"
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
ms.assetid: 92ebd5cb-afb6-4b62-968f-39f5574a452b
caps.latest.revision: 17
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 17
---
# Ver&#228;ndertes Verhalten von Analysis Services-Funktionen in SQL Server 2016
  *Verhaltensänderungen* beeinflussen die Funktion und Interaktion von Funktionen in der aktuellen Version im Vergleich zu früheren Versionen von SQL Server.  
  
 Beispiele für eine Verhaltensänderung beinhalten Überarbeitungen von Standardwerten, die für das Abschließen einer Upgrade- oder Wiederherstellungsfunktionalität benötigte manuelle Konfiguration oder eine neue Implementierung einer vorhandenen Funktion.  
  
 Funktionsverhalten, die in diesem Release geändert werden, die jedoch kein vorhandenes Modell oder Code nach dem Upgrade unterbrechen, sind hier aufgelistet.  
  
> [!NOTE]  
>  Im Unterschied zu einer *Verhaltensänderung*, verhindert eine *grundlegende Änderung*, dass ein in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] integriertes Datenmodell oder eine Datenanwendung nach dem Upgraden eines Servers, Clienttools oder Modells ausgeführt wird. Die Liste können Sie unter [Wichtige Änderungen von Analysis Services-Funktionen in SQL Server 2016](../analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2016.md) einsehen.  
  
## Analysis Services im SharePoint-Modus  
 Die Ausführung des Assistenten für die PowerPivot-Konfiguration ist nach der Installation nicht mehr erforderlich. Dies gilt für alle unterstützten Versionen von SharePoint, die Modelle aus dem aktuellen [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]-Release von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] laden.  
  
## DirectQuery-Modus für tabellarische Modelle  
 *DirectQuery* ist ein Datenzugriffsmodus für tabellarische Modelle, in dem die Abfrageausführung in einer relationalen Back-End-Datenbank stattfindet, wobei ein Resultset in Echtzeit abgerufen wird. Er wird häufig für sehr große Datasets verwendet, die nicht in den Arbeitsspeicher passen. Er wird zudem verwendet, wenn Daten flüchtig sind und Sie möchten, dass die aktuellsten Daten in Abfragen an ein tabellarisches Modell zurückgegeben werden.  
  
 DirectQuery war als Datenzugriffsmodus in den letzten Releases vorhanden. In [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] wurde die Implementierung geringfügig überarbeitet, vorausgesetzt, das tabellarische Modell weist den Kompatibilitätsgrad 1200 auf. DirectQuery hat weniger Einschränkungen als bisher. Es verfügt außerdem über verschiedene Datenbankeigenschaften.  
  
 Wenn Sie DirectQuery in einem vorhandenen tabellarischen Modell verwenden, können Sie für das Modell dessen aktuellen Kompatibilitätsgrad von 1100 oder 1103 erhalten und DirectQuery weiterhin verwenden, da es für diese Grade implementiert ist. Sie können auch auf den Kompatibilitätsgrad 1200 aktualisieren, um von den in diesem Release von [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] erfolgten Verbesserungen von DirectQuery zu profitieren.  
  
 Es existiert kein direktes Upgrade eines DirectQuery-Modells, da es für die Einstellungen der älteren Kompatibilitätsgrade keine genauen Entsprechungen im neuen Kompatibilitätsgrad 1200 gibt. Wenn Sie über ein vorhandenes tabellarisches Modell verfügen, das im DirectQuery-Modus ausgeführt wird, sollten Sie das Modell in SQL Server Data Tools öffnen, DirectQuery deaktivieren, die Eigenschaft **Kompatibilitätsgrad** auf 1200 festlegen und anschließend die DirectQuery-Eigenschaften erneut konfigurieren, wie für tabellarische 1200-Modelle definiert. Einzelheiten finden Sie unter [DirectQuery-Modus &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md).  
  
## Siehe auch  
 [Abwärtskompatibilität_gelöscht](../Topic/Backward%20Compatibility_deleted.md)   
 [Wichtige Änderungen von Analysis Services-Funktionen in SQL Server 2016](../analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2016.md)   
 [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Herunterladen von SQL Server Data Tools](https://msdn.microsoft.com/en-us/library/mt204009.aspx)  
  
  