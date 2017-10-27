---
title: MSSQLSERVER_2537 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 2537 (Database Engine error)
ms.assetid: 0af6ff69-d75a-4c39-8da2-9bd0695277c6
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9c8ebea64d453e7cf81e45c98398ca5e8208fa29
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver2537"></a>MSSQLSERVER_2537
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|2537|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBCC_RECORD_CHECK_FAILED|  
|Meldungstext|Tabellenfehler: Objekt-ID O_ID, Index-ID I_ID, Partitions-ID PN_ID, Zuordnungseinheits-ID A_ID (TYPE-Typ), Seite P_ID, Zeile ROW_ID. Fehler bei der Datensatzüberprüfung (CHECK_TEXT). Die Werte sind VALUE1 und VALUE2.|  
  
## <a name="explanation"></a>Erklärung  
Bei der Zeile ROW_ID (or a column in the row) ist bei dem durch CHECK_TEXT beschriebenen Test bzw. Bedingungsvorgang ein Fehler aufgetreten.  
  
## <a name="user-action"></a>Benutzeraktion  
  
### <a name="look-for-hardware-failure"></a>Hardwarefehlersuche  
Führen Sie eine Hardwarediagnose aus, und beheben Sie alle Probleme. Überprüfen Sie auch das Systemprotokoll und das Anwendungsprotokoll von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows sowie das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll, um festzustellen, ob der Fehler aufgrund eines Hardwarefehlers aufgetreten ist. Beheben Sie alle hardwarebedingten Probleme, die in den Protokollen enthalten sind.  
  
Lagern Sie verschiedene Hardwarekomponenten aus, um das Problem zu isolieren, falls Beschädigungsprobleme bei permanenten Daten auftreten. Stellen Sie sicher, dass beim System der Schreibcache auf dem Datenträgercontroller nicht aktiviert ist. Wenn Sie vermuten, dass der Schreibcache das Problem ist, wenden Sie sich an den Hardwarehersteller.  
  
Letztendlich kann es vorteilhaft sein, wenn Sie zu einem neuen Hardwaresystem wechseln. Der Wechsel kann die Neuformatierung der Laufwerke und eine Neuinstallation des Betriebssystems beinhalten.  
  
### <a name="restore-from-backup"></a>Sicherungswiederherstellung  
Stellen Sie die Datenbank aus der Sicherung wieder her, wenn das Problem nicht hardwarebezogen ist und eine bekannte intakte Sicherungskopie vorhanden ist.  
  
### <a name="run-dbcc-checkdb"></a>Ausführen von DBCC CHECKDB  
Führen Sie DBCC CHECKDB ohne eine REPAIR-Klausel aus, um das Ausmaß der Beschädigung festzustellen, falls keine fehlerfreie Sicherung verfügbar ist. DBCC CHECKDB empfiehlt die Verwendung einer REPAIR-Klausel. Führen Sie dann DBCC CHECKDB mit der empfohlenen REPAIR-Klausel aus.  
  
> [!CAUTION]  
> Wenden Sie sich an Ihren primären Unterstützungsanbieter, bevor Sie diese Anweisung ausführen, wenn Sie nicht sicher sind, inwiefern sich die Verwendung von DBCC CHECKDB mit einer REPAIR-Klausel auf Ihre Daten auswirkt.  
  
Wenn DBCC CHECKDB mit einer der REPAIR-Klauseln ausgeführt wird und das Problem nicht behebt, wenden Sie sich an Ihren primären Unterstützungsanbieter.  
  
### <a name="results-of-running-repair-options"></a>Ergebnis der Ausführung von REPAIR-Optionen  
REPAIR erstellt den Index neu, wenn ein Index vorhanden ist.  
  
**Vorsicht** Diese Reparatur führt möglicherweise zum Datenverlust.  
  

