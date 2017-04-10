---
title: "Fortschrittsbericht-Ereigniskategorie | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "Fortschrittsereignisse [Analysis Services]"
  - "Fortschrittsbericht (Ereigniskategorie)"
  - "Ereignisklassen [Analysis Services], Fortschrittsberichte"
ms.assetid: c130f160-28ef-49bc-9ee6-da47dc9aab2a
caps.latest.revision: 23
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 23
---
# Fortschrittsbericht-Ereigniskategorie
  Die Progress Reports-Ereigniskategorie enthält die in der folgenden Tabelle beschriebenen Ereignisklassen.  
  
|Ereignisklasse|Ereignis-ID|Description|  
|-----------------|--------------|-----------------|  
|Progress Report Begin|5|Sammelt alle Progress Report Begin-Ereignisse seit dem Start der Ablaufverfolgung.|  
|Progress Report End|6|Sammelt alle Progress Report End-Ereignisse seit dem Start der Ablaufverfolgung.|  
|Progress Report Current|7|Sammelt alle Progress Report Current-Ereignisse seit dem Start der Ablaufverfolgung. Beispielsweise enthalten während der Verarbeitung die Current Reports Verarbeitungsinformationen zu den verarbeiteten Objekten (Dimensionen, Partitionen, Cube usw.).|  
|Progress Report Error|8|Sammelt alle Progress Report Error-Ereignisse seit dem Start der Ablaufverfolgung.|  
  
 Jedes Progress Report Begin-Ereignis beginnt mit einem Datenstrom aus Progress-Ereignissen und wird durch ein Progress Report End-Ereignis beendet. Der Datenstrom kann jede beliebige Anzahl von Progress Report Current- und Progress Report Error-Ereignissen enthalten.  
  
 Informationen zu den Spalten, die den einzelnen Progress Reports-Ereignisklassen zugeordnet sind, finden Sie unter [Progress Reports Data Columns](../../analysis-services/trace-events/progress-reports-data-columns.md).  
  
## Siehe auch  
 [Analysis Services-Ablaufverfolgungsereignisse](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  