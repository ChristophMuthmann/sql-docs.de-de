---
title: MSSQLSERVER_7984 | Microsoft-Dokumentation
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
- 7984 (Database Engine error)
ms.assetid: e3192f56-e4e2-41da-b132-65f1e7540b1a
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2d5f6e5010c18c2bed4169a0fe8fdaefb3b49d14
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver7984"></a>MSSQLSERVER_7984
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|7984|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|DBCC2_PRE_CHECKS_BAD_PAGE_TYPE|  
|Meldungstext|Vorabüberprüfungen für Systemtabelle: Objekt-ID O_ID. Die Seite P_ID hat den unerwarteten Seitentyp PAGETYPE. Die CHECK-Anweisung wurde aufgrund eines irreparablen Fehlers beendet.|  
  
## <a name="explanation"></a>Erklärung  
Eine Seite eines anderen Typs als DATA_PAGE wurde auf der Datenebene des angegebenen Objekts gefunden. Dieser Fehler wird während der ersten Phase der Überprüfungen durch den Befehl DBCC CHECKDB ausgelöst. Während dieser Phase führt DBCC CHECKDB einfache Überprüfungen auf den Datenseiten kritischer Systembasistabellen aus.  
  
> [!NOTE]  
> Wenn Fehler in den Systemtabellen gefunden werden, können diese nicht behoben werden. Deshalb wird der Befehl DBCC CHECKDB sofort beendet.  
  
## <a name="user-action"></a>Benutzeraktion  
  
### <a name="look-for-hardware-failure"></a>Hardwarefehlersuche  
Führen Sie eine Hardwarediagnose aus, und beheben Sie alle Probleme. Überprüfen Sie auch das Systemprotokoll und das Anwendungsprotokoll von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows sowie das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll, um festzustellen, ob der Fehler aufgrund eines Hardwarefehlers aufgetreten ist. Beheben Sie alle hardwarebedingten Probleme, die in den Protokollen enthalten sind.  
  
Lagern Sie verschiedene Hardwarekomponenten aus, um das Problem zu isolieren, falls Beschädigungsprobleme bei permanenten Daten auftreten. Stellen Sie sicher, dass beim System der Schreibcache auf dem Datenträgercontroller nicht aktiviert ist. Wenden Sie sich an Ihren Hardwarehersteller, falls Sie beim Schreibcache das Problem vermuten.  
  
Letztendlich kann es vorteilhaft sein, wenn Sie zu einem neuen Hardwaresystem wechseln. Der Wechsel kann die Neuformatierung der Laufwerke und eine Neuinstallation des Betriebssystems beinhalten.  
  
### <a name="restore-from-backup"></a>Sicherungswiederherstellung  
Stellen Sie die Datenbank aus der Sicherung wieder her, wenn das Problem nicht hardwarebezogen ist und eine bekannte intakte Sicherungskopie vorhanden ist.  
  
### <a name="run-dbcc-checkdb"></a>Ausführen von DBCC CHECKDB  
Nicht verfügbar. Dieser Fehler kann nicht automatisch repariert werden. Wenn Sie die Datenbank nicht von einer Sicherung wiederherstellen können, wenden Sie sich an den [!INCLUDE[msCoName](../../includes/msconame-md.md)] Support Services (CSS).  
  

