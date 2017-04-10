---
title: "MSSQL_ENG021330 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG021330 (Fehler)"
ms.assetid: e2bb2e21-62a7-4689-b68b-bdfba3fdd985
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# MSSQL_ENG021330
    
## Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|21330|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Fehler beim Erstellen eines Unterverzeichnisses unter dem Replikationsarbeitsverzeichnis. (%1!s!)|  
  
## Erklärung  
 Dieser Fehler kann auftreten, wenn ein Abonnement manuell initialisiert wird und es beim Erstellen des Verzeichnisses, in dem die Replikationsskripts gespeichert werden, zu einem Problem kommt. Ursache für den Fehler kann ein Problem mit den Berechtigungen sein: Wenn ein Abonnement ohne Verwendung einer Momentaufnahme initialisiert wird, muss das Konto, über dass der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst auf dem Verleger ausgeführt wird, Schreibberechtigungen für den Momentaufnahmeordner auf dem Verleger besitzen.  
  
## Benutzeraktion  
 Stellen Sie sicher, dass der richtige Pfad für den Momentaufnahmeordner angegeben wird und dass das Konto, über das der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst auf dem Verleger ausgeführt wird, über ausreichende Berechtigungen verfügt.  
  
## Siehe auch  
 [Geben Sie den Standard-Snapshotspeicherort & #40. SQL Server Management Studio & #41;](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)   
 [Fehler und Ereignisreferenz & #40; Replikation & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Initialisieren eines Transaktionsabonnements ohne Momentaufnahme](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  