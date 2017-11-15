---
title: MSSQL_ENG020574 | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: MSSQL_ENG02574 error
ms.assetid: 4e98f8de-287c-4090-81ee-dc8f80dfa6a1
caps.latest.revision: "11"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7ff57dd45db47b24ebefddec17179d68f5466821
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqleng020574"></a>MSSQL_ENG020574
    
## <a name="message-details"></a>Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|20574|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Fehler bei der Datenüberprüfung für das Abonnement des Abonnenten '%s' für den '%s'-Artikel in der '%s'-Veröffentlichung.|  
  
## <a name="explanation"></a>Erklärung  
 Die Daten des Abonnenten wurden gegen die Daten des Verlegers abgeglichen, und es wurde keine Übereinstimmung der Daten festgestellt. Daher konnte die Überprüfung nicht erfolgreich abgeschlossen werden. Weitere Informationen zur Überprüfung finden Sie unter [Validate Replicated Data](../../relational-databases/replication/validate-replicated-data.md).  
  
## <a name="user-action"></a>Benutzeraktion  
 Es wird empfohlen, folgendermaßen vorzugehen:  
  
-   Ermitteln Sie den Grund für den Fehler bei der Überprüfung.  
  
-   Beheben Sie das zugrunde liegende Problem, das zu dem Fehler geführt hat.  
  
-   Stellen Sie die Konvergenz der Daten her, indem Sie das Abonnement erneut initialisieren oder eine andere geeignete Methode verwenden.  
  
## <a name="see-also"></a>Siehe auch  
 [Fehler- und Ereignisreferenz &#40;Replikation&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
