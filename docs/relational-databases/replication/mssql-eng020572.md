---
title: "MSSQL_ENG020572 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG020572 (Fehler)"
ms.assetid: 636566db-ffcf-4109-8c11-15b8c7cb9cd9
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 11
---
# MSSQL_ENG020572
    
## Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|20572|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Das Abonnement des Abonnenten '%s' für den '%s'-Artikel in der '%s'-Veröffentlichung wurde nach einem Datenüberprüfungsfehler neu initialisiert.|  
  
## Erklärung  
 Die Daten des Abonnenten wurden gegen die Daten des Verlegers abgeglichen, und es wurde keine Übereinstimmung der Daten festgestellt. Daher konnte die Überprüfung nicht erfolgreich abgeschlossen werden. Bei der Angabe zur Ausführung einer Überprüfung haben Sie die Option aktiviert, dass im Falle eines Fehlers bei der Überprüfung eine erneute Initialisierung des Abonnements erfolgen soll. Für eine erneute Initialisierung des Abonnements muss eine neue Momentaufnahme auf dem Abonnenten angewendet werden. Weitere Informationen zur Überprüfung finden Sie unter [Überprüfen von replizierten Daten](../../relational-databases/replication/validate-replicated-data.md).  
  
## Benutzeraktion  
 Die Daten auf dem Verleger und auf dem Abonnenten stimmen überein, nachdem die neue Momentaufnahme auf dem Abonnenten angewendet wurde.  
  
## Siehe auch  
 [Fehler und Ereignisreferenz & #40; Replikation & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  