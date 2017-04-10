---
title: "MSSQL_ENG014157 | Microsoft Docs"
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
  - "MSSQL_ENG014157 (Fehler)"
ms.assetid: 1a0890cf-d977-43e0-a2ba-9c5ff1a8f856
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# MSSQL_ENG014157
    
## Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|14157|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Das Abonnement des Abonnenten '%1!s!' für die %2!s!-Veröffentlichung ist abgelaufen und wurde gelöscht.|  
  
## Erklärung  
 Ein Abonnent muss innerhalb der angegebenen Beibehaltungsdauer für die Veröffentlichung mit dem Verleger synchronisiert werden. Falls ein Abonnent nicht innerhalb dieses Zeitraums synchronisiert wird, läuft das Abonnement ab. Weitere Informationen finden Sie unter [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
## Benutzeraktion  
 Das Abonnement muss neu erstellt und initialisiert werden, damit der Abonnent wieder Datenänderungen empfangen kann:  
  
-   Informationen zum Erstellen von Abonnements finden Sie unter [abonnieren Publikationen](../../relational-databases/replication/subscribe-to-publications.md).  
  
-   Informationen zum Initialisieren von Abonnements finden Sie unter [Initialisieren eines Abonnements](../../relational-databases/replication/initialize-a-subscription.md).  
  
 Wenn die Abonnementdatenbank Änderungen enthält, die noch nicht mit dem Verleger synchronisiert wurden, können Sie mit [tablediff Utility](../../tools/tablediff-utility.md) (Hilfsprogramm) ermitteln, welche Zeilen in der Veröffentlichungs- bzw. Abonnementdatenbanken unterschiedlich sind.  
  
 Sie können die Beibehaltungsdauer für die Veröffentlichung erhöhen, um zu vermeiden, dass Abonnements ablaufen. Geben Sie keinen zu hohen Wert ein, da dies zur Speicherung von mehr Daten und Metadaten und damit einer Beeinträchtigung der Leistung führen kann. Weitere Informationen finden Sie unter [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
## Siehe auch  
 [Fehler und Ereignisreferenz & #40; Replikation & #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  