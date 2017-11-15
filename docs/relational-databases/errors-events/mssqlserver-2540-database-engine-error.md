---
title: MSSQLSERVER_2540 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 2540 (Database Engine error)
ms.assetid: eb5ee2be-acbb-4fb7-9b45-dc6200bde06e
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 81eb9dc44150be278d798fed8a286808d509b868
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver2540"></a>MSSQLSERVER_2540
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|2540|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBCC_REPAIR_ERROR_NOT_REPAIRABLE|  
|Meldungstext|Dieser Fehler kann nicht automatisch vom System behoben werden.|  
  
## <a name="explanation"></a>Erklärung  
Diese Fehlermeldung weist auf Probleme hin, die nicht automatisch behoben werden können, z. B. beschädigte Metadaten, beschädigte PFS-Seiten (Page Free Space) oder Beschädigungen in bestimmten kritischen Systembasistabellen.  
  
## <a name="user-action"></a>Benutzeraktion  
  
### <a name="look-for-hardware-failure"></a>Hardwarefehlersuche  
Führen Sie eine Hardwarediagnose aus, und beheben Sie alle Probleme. Überprüfen Sie auch das Systemprotokoll und das Anwendungsprotokoll von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows sowie das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll, um festzustellen, ob der Fehler aufgrund eines Hardwarefehlers aufgetreten ist. Beheben Sie alle hardwarebedingten Probleme, die in den Protokollen enthalten sind.  
  
Lagern Sie verschiedene Hardwarekomponenten aus, um das Problem zu isolieren, falls Beschädigungsprobleme bei permanenten Daten auftreten. Stellen Sie sicher, dass beim System der Schreibcache auf dem Datenträgercontroller nicht aktiviert ist. Wenden Sie sich an Ihren Hardwarehersteller, falls Sie beim Schreibcache das Problem vermuten.  
  
Letztendlich kann es vorteilhaft sein, wenn Sie zu einem neuen Hardwaresystem wechseln. Der Wechsel kann die Neuformatierung der Laufwerke und eine Neuinstallation des Betriebssystems beinhalten.  
  
### <a name="restore-from-backup"></a>Sicherungswiederherstellung  
Stellen Sie die Datenbank aus der Sicherung wieder her, wenn das Problem nicht hardwarebezogen ist und eine bekannte intakte Sicherungskopie vorhanden ist.  
  
### <a name="run-dbcc-checkdb"></a>Ausführen von DBCC CHECKDB  
Nicht verfügbar. Dieser Fehler kann nicht automatisch repariert werden.  
  
