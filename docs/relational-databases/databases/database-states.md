---
title: Datenbankstatus | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/14/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: SQL13.SWB.DATABASESTATES.F1
helpviewer_keywords:
- emergency database state [SQL Server]
- verifying database states
- viewing database states
- displaying database states
- database states [SQL Server]
- current database state
- offline database state [SQL Server]
- suspect database state
- recovery pending database state [SQL Server]
- states [SQL Server], databases
- online database state
- states [SQL Server]
- restoring database state [SQL Server]
ms.assetid: b7f1f111-ca73-4a89-b567-a98d64d6ecb3
caps.latest.revision: "20"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e6acde3a545115bc189da2cfdad0297789fea6a1
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="database-states"></a>Datenbankstatus
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Eine Datenbank weist immer einen bestimmten Status auf. Dazu gehören z. B. ONLINE, OFFLINE oder SUSPECT. Um den aktuellen Status einer Datenbank zu überprüfen, wählen Sie die **state_desc** -Spalte in der [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht oder die **Status** -Eigenschaft in der [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) -Funktion aus.  
  
## <a name="database-state-definitions"></a>Datenbankstatusdefinitionen  
 Die folgende Tabelle definiert den Datenbankstatus.  
  
|Status|Definition|  
|-----------|----------------|  
|ONLINE|Die Datenbank ist für den Zugriff bereit. Die primäre Dateigruppe ist online, auch wenn die Rollbackphase der Wiederherstellung möglicherweise noch nicht abgeschlossen ist.|  
|OFFLINE|Die Datenbank ist nicht verfügbar. Eine Datenbank wird durch explizite Benutzeraktionen offline geschaltet und bleibt offline, bis weitere Benutzeraktionen durchgeführt werden. Die Datenbank kann z. B. offline geschaltet werden, um eine Datei auf einen neuen Datenträger zu verschieben. Die Datenbank wird dann erneut online geschaltet, nachdem der Verschiebevorgang abgeschlossen wurde.|  
|RESTORING|Eine oder mehrere Dateien der primären Dateigruppe werden wiederhergestellt, oder eine oder mehrere sekundäre Dateien werden offline wiederhergestellt. Die Datenbank ist nicht verfügbar.|  
|RECOVERING|Die Datenbank wird aktuell wiederhergestellt. Der Wiederherstellungsvorgang ist ein vorübergehender Zustand; die Datenbank wird automatisch online geschaltet, wenn die Wiederherstellung erfolgreich war. Sollte die Wiederherstellung einen Fehler erzeugen, erhält die Datenbank den Status Fehlerverdächtig. Die Datenbank ist nicht verfügbar.|  
|RECOVERY PENDING|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hat während der Wiederherstellung einen ressourcenbezogenen Fehler erkannt. Die Datenbank ist nicht beschädigt, möglicherweise fehlen jedoch Dateien, oder Systemressourceneinschränkungen verhindern ihren Start. Die Datenbank ist nicht verfügbar. Es sind weitere Aktionen durch den Benutzer erforderlich, um den Fehler zu beheben und den Wiederherstellungsvorgang erfolgreich abzuschließen.|  
|SUSPECT|Mindestens die primäre Dateigruppe weist den Status Fehlerverdächtig auf und ist möglicherweise beschädigt. Die Datenbank kann während des Starts von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]nicht wiederhergestellt werden. Die Datenbank ist nicht verfügbar. Es sind weitere Aktionen durch den Benutzer erforderlich, um das Problem zu beheben.|  
|EMERGENCY|Der Benutzer hat die Datenbank geändert und den Status NOTFALL festgelegt. Die Datenbank befindet sich im Einzelbenutzermodus und wird möglicherweise repariert oder wiederhergestellt. Die Datenbank ist als READ_ONLY markiert, die Protokollierung deaktiviert und der Zugriff auf Mitglieder der festen Serverrolle **sysadmin** beschränkt. Der Status EMERGENCY wird hauptsächlich zu Problembehandlungszwecken verwendet. Für eine Datenbank, die als fehlerverdächtig markiert ist, kann z. B. der Status NOTFALL festgelegt werden. Dies kann dem Systemadministrator schreibgeschützten Zugriff auf die Datenbank ermöglichen. Nur Mitglieder der festen Serverrolle **sysadmin** können für eine Datenbank den Status EMERGENCY festlegen.|  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
 [Spiegelungsstatus &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)  
  
 [Dateistatus](../../relational-databases/databases/file-states.md)  
  
  
