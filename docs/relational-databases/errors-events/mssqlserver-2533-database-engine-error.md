---
title: MSSQLSERVER_2533 | Microsoft-Dokumentation
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
helpviewer_keywords: 2533 (Database Engine error)
ms.assetid: 0418352c-0ab2-4dc7-b8b9-5c3bad94560c
caps.latest.revision: "19"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 88ad8c6e591b249323f8dce0c26b60dc2e1677d6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver2533"></a>MSSQLSERVER_2533
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|2533|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBCC_PAGE_WAS_NOT_SEEN|  
|Meldungstext|Tabellenfehler: Seite P_ID, die der Objekt-ID O_ID zugeordnet ist, Index-ID I_ID, Partitions-ID PN_ID, Zuordnungseinheits-ID A_ID (TYPE-Typ) wurde nicht betrachtet. Die Seite ist möglicherweise ungültig oder enthält eine falsche Zuordnungseinheits-ID im Header.|  
  
## <a name="explanation"></a>Erklärung  
Eine Seite wird der Zuordnungseinheits-ID *A_ID* zugeordnet, aber diese Zuordnungseinheits-ID befindet sich nicht im Header der Seite. Der Header hat eine andere Zuordnungseinheits-ID. Wenn die Zuordnungseinheits-ID im Header der Seite einem gültigen Objekt zugewiesen ist, tritt für die Seite möglicherweise ein entsprechender MSSQLEngine_2534-Fehler auf.  
  
## <a name="user-action"></a>Benutzeraktion  
  
### <a name="look-for-hardware-failure"></a>Hardwarefehlersuche  
Führen Sie eine Hardwarediagnose aus, und beheben Sie alle Probleme. Überprüfen Sie auch das Systemprotokoll und das Anwendungsprotokoll von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows sowie das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll, um festzustellen, ob der Fehler aufgrund eines Hardwarefehlers aufgetreten ist. Beheben Sie alle hardwarebedingten Probleme, die in den Protokollen enthalten sind.  
  
Lagern Sie verschiedene Hardwarekomponenten aus, um das Problem zu isolieren, falls Beschädigungsprobleme bei permanenten Daten auftreten. Stellen Sie sicher, dass beim System der Schreibcache auf dem Datenträgercontroller nicht aktiviert ist. Wenden Sie sich an Ihren Hardwarehersteller, falls Sie beim Schreibcache das Problem vermuten.  
  
Letztendlich kann es vorteilhaft sein, wenn Sie zu einem neuen Hardwaresystem wechseln. Der Wechsel kann die Neuformatierung der Laufwerke und eine Neuinstallation des Betriebssystems beinhalten.  
  
### <a name="restore-from-backup"></a>Sicherungswiederherstellung  
Stellen Sie die Datenbank aus der Sicherung wieder her, wenn das Problem nicht hardwarebezogen ist und eine bekannte intakte Sicherungskopie vorhanden ist.  
  
### <a name="run-dbcc-checkdb"></a>Ausführen von DBCC CHECKDB  
Führen Sie DBCC CHECKDB ohne eine REPAIR-Klausel aus, um das Ausmaß der Beschädigung festzustellen, falls keine fehlerfreie Sicherung verfügbar ist. DBCC CHECKDB empfiehlt die Verwendung einer REPAIR-Klausel. Führen Sie dann DBCC CHECKDB mit der entsprechenden REPAIR-Klausel aus, um die Beschädigung zu reparieren.  
  
> [!CAUTION]  
> Wenden Sie sich an Ihren primären Unterstützungsanbieter, bevor Sie diese Anweisung ausführen, wenn Sie nicht sicher sind, inwiefern sich die Verwendung von DBCC CHECKDB mit einer REPAIR-Klausel auf Ihre Daten auswirkt.  
  
Wenn DBCC CHECKDB mit einer der REPAIR-Klauseln ausgeführt wird und das Problem nicht behebt, wenden Sie sich an Ihren primären Unterstützungsanbieter.  
  
### <a name="results-of-running-repair-options"></a>Ergebnis der Ausführung von REPAIR-Optionen  
REPAIR hebt die Zuordnung der Seite auf. Wenn die Seite aus einer Zuordnungseinheit für Daten in Zeilen stammte, wird der Index, falls vorhanden, neu erstellt.  
  
> [!CAUTION]  
> Diese Reparatur führt möglicherweise zum Datenverlust.  
  
## <a name="see-also"></a>Siehe auch  
[MSSQLSERVER_2534](~/relational-databases/errors-events/mssqlserver-2534-database-engine-error.md)  
  
