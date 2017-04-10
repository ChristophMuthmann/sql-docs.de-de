---
title: "MSSQL_ENG020574 | Microsoft Docs"
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
  - "MSSQL_ENG02574 (Fehler)"
ms.assetid: 4e98f8de-287c-4090-81ee-dc8f80dfa6a1
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 11
---
# MSSQL_ENG020574
    
## Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|20574|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Fehler bei der Datenüberprüfung für das Abonnement des Abonnenten '%s' für den '%s'-Artikel in der '%s'-Veröffentlichung.|  
  
## Erklärung  
 Die Daten des Abonnenten wurden gegen die Daten des Verlegers abgeglichen, und es wurde keine Übereinstimmung der Daten festgestellt. Daher konnte die Überprüfung nicht erfolgreich abgeschlossen werden. Weitere Informationen zur Überprüfung finden Sie unter [Überprüfen von replizierten Daten](../../relational-databases/replication/validate-replicated-data.md).  
  
## Benutzeraktion  
 Es wird empfohlen, folgendermaßen vorzugehen:  
  
-   Ermitteln Sie den Grund für den Fehler bei der Überprüfung.  
  
-   Beheben Sie das zugrunde liegende Problem, das zu dem Fehler geführt hat.  
  
-   Stellen Sie die Konvergenz der Daten her, indem Sie das Abonnement erneut initialisieren oder eine andere geeignete Methode verwenden.  
  
## Siehe auch  
 [Fehler und Ereignisreferenz & #40; Replikation & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  