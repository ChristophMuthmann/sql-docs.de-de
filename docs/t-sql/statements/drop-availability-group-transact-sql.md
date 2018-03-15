---
title: DROP AVAILABILITY GROUP (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_AVAILABILITY_GROUP_TSQL
- DROP AVAILABILITY GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], Transact-SQL statements
- DROP AVAILABILITY GROUP statement
- Availability Groups [SQL Server], dropping
ms.assetid: c1600289-c990-454a-b279-dba0ebd5d63e
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 82fdb4b104a0be0aa0d6469ccdd23f361f55618b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="drop-availability-group-transact-sql"></a>DROP AVAILABILITY GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Entfernt die angegebene Verfügbarkeitsgruppe und alle dazugehörigen Replikate. Wenn eine Serverinstanz, auf der eines der Verfügbarkeitsreplikate gehostet wird, offline ist, wenn Sie eine Verfügbarkeitsgruppe löschen, so wird das lokale Verfügbarkeitsreplikat von der Serverinstanz gelöscht, nachdem diese online geschaltet wurde. Wird eine Verfügbarkeitsgruppe gelöscht, wird auch der zugeordnete Verfügbarkeitsgruppenlistener gelöscht, falls vorhanden.  
  
> [!IMPORTANT]  
>  Entfernen Sie die Verfügbarkeitsgruppe wenn möglich nur, während eine Verbindung mit der Serverinstanz besteht, die das primäre Replikat hostet. Wenn die Verfügbarkeitsgruppe aus dem primären Replikat gelöscht wird, sind Änderungen in den früheren primären Datenbanken (ohne Hochverfügbarkeitsschutz) zulässig. Durch Löschen einer Verfügbarkeitsgruppe aus einem sekundären Replikat erhält das primäre Replikat den Status **RESTORING**. Änderungen an den Datenbanken sind nicht zulässig.  
  
 Informationen zu alternativen Methoden zum Löschen einer Verfügbarkeitsgruppe finden Sie unter [Entfernen einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DROP AVAILABILITY GROUP group_name   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *group_name*  
 Gibt den Namen der Verfügbarkeitsgruppe an, die gelöscht werden soll.  
  
## <a name="limitations-and-recommendations"></a>Einschränkungen und Empfehlungen  
  
-   Für die Ausführung von **DROP AVAILABILITY GROUP** muss das Feature für Always On-Verfügbarkeitsgruppen auf der Serverinstanz aktiviert sein. Weitere Informationen finden Sie unter [Aktivieren und Deaktivieren von AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).  
  
-   **DROP AVAILABILITY GROUP** kann nicht als Teil von Batches oder innerhalb der Transaktionen ausgeführt werden. Auch Ausdrücke und Variablen werden nicht unterstützt.  
  
-   Eine Verfügbarkeitsgruppe kann aus jedem WSFC-Knoten (Windows Server-Failoverclustering) gelöscht werden, der über die richtigen Sicherheitsanmeldeinformationen für die Verfügbarkeitsgruppe verfügt. Auf diese Weise können Sie eine Verfügbarkeitsgruppe löschen, wenn keine ihrer Verfügbarkeitsreplikate mehr vorhanden ist.  
  
    > [!IMPORTANT]  
    >  Löschen Sie eine Verfügbarkeitsgruppe nicht, wenn der WSFC-Cluster (Windows Server Failover Clustering) kein Quorum hat. Wenn Sie eine Verfügbarkeitsgruppe löschen müssen, solange der Cluster über kein Quorum verfügt, wird die Metadaten-Verfügbarkeitsgruppe, die im Cluster gespeichert ist, nicht entfernt. Nachdem der Cluster das Quorum wiedererlangt hat, müssen Sie die Verfügbarkeitsgruppe erneut löschen, um diese aus dem WSFC-Cluster zu entfernen.  
  
-   Auf einem sekundären Replikat sollte **DROP AVAILABILITY GROUP** nur im Notfall verwendet werden. Das liegt daran, dass durch Löschen einer Verfügbarkeitsgruppe die Verfügbarkeitsgruppe offline geschaltet wird. Wenn Sie die Verfügbarkeitsgruppe aus einem sekundären Replikat löschen, kann das primäre Replikat nicht bestimmen, ob der **OFFLINE**-Status aufgrund des Quorumverlusts, eines erzwungenen Failovers oder eines **DROP AVAILABILITY GROUP**-Befehls aufgetreten ist. Das primäre Replikat geht in den Status **RESTORING** über, um eine mögliche Split Brain-Situation zu verhindern. Weitere Informationen finden Sie unter [Funktionsweise: DROP AVAILABILITY GROUP-Verhaltensweisen](http://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (Blog von CSS SQL Server-Ingenieuren).  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die **ALTER AVAILABILITY GROUP**-Berechtigung für die Verfügbarkeitsgruppe, die **CONTROL AVAILABILITY GROUP**-Berechtigung, die **ALTER ANY AVAILABILITY GROUP**-Berechtigung oder die **CONTROL SERVER**-Berechtigung. Um eine Verfügbarkeitsgruppe zu löschen, die nicht von der lokalen Serverinstanz gehostet wird, benötigen Sie die **CONTROL SERVER**-Berechtigung oder die **CONTROL**-Berechtigung für diese Verfügbarkeitsgruppe.  
  
## <a name="examples"></a>Beispiele  
 Mit dem folgenden Beispiel wird die Verfügbarkeitsgruppe `AccountsAG` gelöscht.  
  
```  
DROP AVAILABILITY GROUP AccountsAG;  
```  
  
##  <a name="RelatedContent"></a> Verwandte Inhalte  
  
-   [Funktionsweise: DROP AVAILABILITY GROUP-Verhaltensweisen](http://blogs.msdn.com/b/psssql/archive/2012/06/13/how-it-works-drop-availability-group-behaviors.aspx) (Blog von CSS SQL Server-Ingenieuren)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [Entfernen einer Verfügbarkeitsgruppe &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-an-availability-group-sql-server.md)  
  
  
