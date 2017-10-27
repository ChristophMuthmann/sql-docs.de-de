---
title: SQL Server, SQL Errors-Objekt | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Errors object
- SQLServer:SQL Errors
ms.assetid: 6e5273ca-29cb-4618-88a2-70b9b8d6cf76
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d8cde07237e3794e4643f117e12f531d25ef5bf8
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-sql-errors-object"></a>SQL Server, SQL-Fehler-Objekt
  Durch das Objekt **SQLServer:SQL Errors** in Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] werden Indikatoren zum Überwachen von **SQL-Fehlern**zur Verfügung gestellt.  
  
 In dieser Tabelle werden die Leistungsindikatoren von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SQL-Fehler** beschrieben.  
  
|Leistungsindikatoren von SQL-Fehler bei SQL Server|Beschreibung|  
|------------------------------------|-----------------|  
|**Fehler/Sekunde**|Anzahl der Fehler/Sekunde.|  
  
 Jeder Leistungsindikator in dem Objekt enthält die folgenden Instanzen:  
  
|Element|Definition|  
|----------|----------------|  
|**_Total**|Informationen zu allen Fehlern.|  
|**DB Offline Errors**|Es werden schwere Fehler nachverfolgt, die dazu führen, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Datenbank offline schaltet.|  
|**Info Errors**|Informationen, die sich auf Fehlermeldungen beziehen, die den Benutzern als Informationen zur Verfügung gestellt werden, verursachen jedoch keine Fehler.|  
|**Kill Connection Errors**|Es werden schwere Fehler nachverfolgt, die dazu führen, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die aktuelle Verbindung unterbricht.|  
|**User Errors**|Informationen zu Benutzerfehlern.|  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  

