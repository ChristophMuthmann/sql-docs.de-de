---
title: MSSQL_ENG021331 | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: MSSQL_ENG021331 error
ms.assetid: 9acd75d9-fda1-44cd-ba17-20295ad53ea0
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3d4cdca217798e40e274a7e45d9643cc9d03e64c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="mssqleng021331"></a>MSSQL_ENG021331
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|21331|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Fehler beim Kopieren der Benutzerskriptdatei auf den Verteiler. (%1!s!)|  
  
## <a name="explanation"></a>Erklärung  
 Dieser Fehler kann auftreten, wenn ein Abonnement manuell initialisiert wird und die Skripts, die durch die Replikation generiert oder in einem Replikationsbefehl angegeben werden, nicht in das angegebene Verzeichnis kopiert werden können. Ursache für den Fehler kann ein Problem mit den Berechtigungen sein: Wenn ein Abonnement ohne Verwendung einer Momentaufnahme initialisiert wird, muss das Konto, über dass der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst auf dem Verleger ausgeführt wird, Schreibberechtigungen für den Momentaufnahmeordner auf dem Verleger besitzen.  
  
## <a name="user-action"></a>Benutzeraktion  
 Stellen Sie sicher, dass der richtige Pfad für den Momentaufnahmeordner angegeben wird und dass das Konto, über das der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst auf dem Verleger ausgeführt wird, über ausreichende Berechtigungen verfügt.  
  
## <a name="see-also"></a>Siehe auch  
 [Specify the Default Snapshot Location &#40;SQL Server Management Studio&#41; (Angeben des standardmäßigen Momentaufnahmespeicherorts &#40;SQL Server Management Studio&#41;)](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)   
 [Fehler- und Ereignisreferenz &#40;Replikation&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Initialisieren eines Transaktionsabonnements ohne Momentaufnahme](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
