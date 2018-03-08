---
title: Datenbankmodulfehler MSSQLSERVER_802 | Microsoft Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 802 (Database Engine error)
ms.assetid: 5892ed24-4dcb-4bf9-a8a4-a7ca898832d5
caps.latest.revision: "20"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 229bf928d06e606bb91332968f313202ab54d92b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver802---database-engine-error"></a>Datenbankmodulfehler MSSQLSERVER_802
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|802|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|NO_BUFS|  
|Meldungstext|Nicht genügend Arbeitsspeicher im Pufferpool.|  
  
## <a name="explanation"></a>Erklärung  
Diese Meldung wird verursacht, wenn der Pufferpool voll ist und nicht weiter vergrößert werden kann.  
  
## <a name="user-action"></a>Benutzeraktion  
In der folgenden Liste werden allgemeine Schritte erläutert, die bei der Problembehandlung von Arbeitsspeicherfehlern helfen:  
  
1.  Überprüfen Sie, ob andere Anwendungen oder Dienste Arbeitsspeicher auf dem Server beanspruchen. Rekonfigurieren Sie weniger kritische Anwendungen oder Dienste, damit sie weniger Speicher beanspruchen.  
  
2.  Beginnen Sie die Sammlung der Leistungsindikatoren für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**: Puffer-Manager** und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**: Speicher-Manager**.  
  
3.  Überprüfen Sie die folgenden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Speicherkonfigurationsparameter:  
  
    -   **Max. Serverarbeitsspeicher**  
  
    -   **Min. Serverarbeitsspeicher**  
  
    -   **Min. Arbeitsspeicher pro Abfrage**  
  
    Beachten Sie alle ungewöhnlichen Einstellungen, und korrigieren Sie sie bei Bedarf. Konto für erhöhte Arbeitsspeicheranforderungen für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Die Standardeinstellungen werden unter "Festlegen von Serverkonfigurationsoptionen" in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Onlinedokumentation aufgeführt.  
  
4.  Verfolgen Sie die Ausgabe von DBCC MEMORYSTATUS und deren Veränderungen beim Anzeigen der Fehlermeldungen.  
  
5.  Überprüfen Sie die Arbeitsauslastung (Anzahl der gleichzeitigen Sitzungen, aktuell ausgeführte Abfragen).  
  
Durch die folgenden Aktionen kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mehr Arbeitsspeicher zur Verfügung gestellt werden:  
  
-   Wenn Anwendungen neben [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sehr ressourcenaufwändig sind, versuchen Sie, diese Anwendungen zu beenden oder auf einem getrennten Server auszuführen.  
  
-   Wenn Sie **Max. Serverarbeitsspeicher** konfiguriert haben, erhöhen Sie die Einstellung.  
  
Führen Sie die folgenden DBCC-Befehle aus, um mehrere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Speichercaches freizugeben.  
  
-   DBCC FREESYSTEMCACHE  
  
-   DBCC FREESESSIONCACHE  
  
-   DBCC FREEPROCCACHE  
  
Wenn das Problem weiterhin besteht, müssen Sie weitere Untersuchungen ausführen und möglicherweise die Arbeitsauslastung reduzieren.  
  
