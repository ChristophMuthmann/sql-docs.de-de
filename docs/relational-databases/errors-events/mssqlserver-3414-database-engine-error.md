---
title: MSSQLSERVER_3414 | Microsoft-Dokumentation
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
- 3414 (Database Engine error)
ms.assetid: f25852f9-b91c-4356-b817-78bec9ec8db4
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c9d5b20ded79569fedd804df81403802a8f2785d
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver3414"></a>MSSQLSERVER_3414
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|3414|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|REC_GIVEUP|  
|Meldungstext|Fehler bei der Wiederherstellung. Die '%.*ls'-Datenbank (Datenbank-ID %d) kann daher nicht neu gestartet werden. Diagnostizieren und beheben Sie die Wiederherstellungsfehler, oder führen Sie eine Wiederherstellung von einer als fehlerfrei bekannten Sicherung aus. Falls die Fehler nicht behoben werden oder unerwartete Fehler auftreten, wenden Sie sich an den technischen Support.|  
  
## <a name="explanation"></a>Erklärung  
Die angegebene Datenbank wurde wiederhergestellt, konnte jedoch nicht gestartet werden, da Fehler bei der Wiederherstellung auftraten. Durch diesen Fehler wurde die Datenbank in den SUSPECT-Status geschaltet. Die primäre Dateigruppe und möglicherweise weitere Dateigruppen sind fehlerverdächtig und u. U. beschädigt. Die Datenbank kann während Starts von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht wiederhergestellt werden und ist daher nicht verfügbar. Eine Aktion seitens des Benutzers ist erforderlich, um das Problem zu beheben.  
  
Falls dieser Fehler für **tempdb**auftritt, wird die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz heruntergefahren.  
  
## <a name="user-action"></a>Benutzeraktion  
Dieser Fehler kann auf vorübergehende Systemschwierigkeiten zurückzuführen sein, die beim Versuch, die Serverinstanz zu starten oder eine Datenbank wiederherzustellen, aufgetreten sind. Es kann jedoch auch ein dauerhafter Fehler vorliegen, der bei jedem Versuch auftritt, die Datenbank zu starten. Um Informationen zur Ursache zu erhalten, überprüfen Sie das Windows-Ereignisprotokoll auf einen vorangehenden Fehler, der Aufschluss über den aktuellen Fehler geben könnte.  
  
Um Informationen zur Ursache dieses Auftretens von Fehler 3414 zu erhalten, überprüfen Sie das Windows-Ereignisprotokoll auf einen vorangehenden Fehler, der Aufschluss über den aktuellen Fehler geben könnte. Die entsprechende Benutzeraktion hängt davon ab, ob die Informationen im Windows-Ereignisprotokoll angeben, dass der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehler durch eine vorübergehende Bedingung oder einen dauerhaften Fehler verursacht wurde. Informationen zu den Benutzeraktionen zum Beheben von Fehler 3414 finden Sie in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation.  
  
## <a name="see-also"></a>Siehe auch  
[ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
[DBCC CHECKDB &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[Vollständige Datenbankwiederherstellungen &#40;einfaches Wiederherstellungsmodell&#41;](~/relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
[MSSQLSERVER_824](~/relational-databases/errors-events/mssqlserver-824-database-engine-error.md)  
[sys.databases &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  

