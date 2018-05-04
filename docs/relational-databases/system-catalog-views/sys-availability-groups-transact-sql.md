---
title: availability_groups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.availability_groups_TSQL
- availability_groups_TSQL
- sys.availability_groups
- availability_groups
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_groups catalog view
ms.assetid: da7fa55f-c008-45d9-bcfc-3513b02d9e71
caps.latest.revision: 42
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c3874bde2c43ddcba3e0ef365ff371a54ffcb8ad
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sysavailabilitygroups-transact-sql"></a>sys.availability_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede verfügbarkeitsgruppe, für die die lokale Instanz von SQL Server ein verfügbarkeitsreplikat hostet. Jede Zeile enthält eine zwischengespeicherte Kopie der Metadaten der Verfügbarkeitsgruppe.  
   
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|Eindeutiger Bezeichner (GUID) der Verfügbarkeitsgruppe.|  
|**name**|**sysname**|Der Name der Verfügbarkeitsgruppe. Dies ist ein vom Benutzer angegebener Name, der innerhalb des Windows Server-Failoverclusters (WSFC) eindeutig sein muss.|  
|**resource_id**|**nvarchar(40)**|Ressourcen-ID für die WSFC-Clusterressource.|  
|**resource_group_id**|**nvarchar(40)**|Ressourcengruppen-ID für die WSFC-Clusterressourcengruppe der Verfügbarkeitsgruppe.|  
|**failure_condition_level**|**int**|Benutzerdefinierte fehlerbedingungsebene unter dem ein automatisches Failover ausgelöst werden, muss eines der ganzzahligen Werten in der Tabelle direkt unterhalb dieser Tabelle dargestellt.<br /><br /> Die Fehlerbedingungsebenen (1-5) reichen von der Ebene 1 mit den wenigsten Einschränkungen bis zur Ebene 5 mit den meisten Einschränkungen. Jede Bedingungsebene umfasst stets auch sämtliche weniger restriktiven Ebenen. Daher schließt die strengste Bedingungsebene 5 die vier Bedingungsebenen mit weniger Einschränkungen (1-4) ein, Ebene 4 schließt die Ebenen 1-3 ein usw.<br /><br /> Um diesen Wert zu ändern, verwenden Sie die FAILURE_CONDITION_LEVEL-Option von der [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung.|  
|**health_check_timeout**|**int**|Wartezeit (in Millisekunden) für die [Sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) gespeicherten Systemprozedur Serverzustand-Informationen zurückgegeben werden, bevor die Serverinstanz angenommen wird, dass Sie langsam oder blockiert werden. Der Standardwert ist 30000 Millisekunden (oder 30 Sekunden).<br /><br /> Um diesen Wert zu ändern, verwenden Sie die HEALTH_CHECK_TIMEOUT-Option von der [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung.|  
|**automated_backup_preference**|**tinyint**|Bevorzugter Speicherort zum Durchführen von Sicherungen auf den Verfügbarkeitsdatenbanken in dieser Verfügbarkeitsgruppe. Im folgenden sind die möglichen Werte und deren Beschreibungen.<br /><br /> <br /><br /> 0: primäre. Sicherungen sollten immer auf dem primären Replikat erfolgen.<br /><br /> 1: nur sekundär. Die Durchführung von Sicherungen auf einem sekundären Replikat wird bevorzugt.<br /><br /> 2: Sekundär bevorzugen. Die Durchführung von Sicherungen auf einem sekundären Replikat wird bevorzugt, aber die Durchführung von Sicherungen auf dem primären Replikat wird akzeptiert, wenn kein sekundäres Replikat für Sicherungsvorgänge verfügbar ist. Dies ist das Standardverhalten.<br /><br /> 3: eines der Replikate. Keine Präferenz, ob Sicherungen auf dem primären Replikat oder einem sekundären Replikat durchgeführt werden.<br /><br /> <br /><br /> Weitere Informationen finden Sie unter [Aktive sekundäre Replikate: Sicherung auf sekundären Replikaten &#40;Always On-Verfügbarkeitsgruppen&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)wichtig sind.|  
|**automated_backup_preference_desc**|**nvarchar(60)**|Beschreibung des **Automated_backup_preference**, eine von:<br /><br /> PRIMARY<br /><br /> SECONDARY_ONLY<br /><br /> SECONDARY<br /><br /> Keine|  
|**version**|**smallint**|Die Version der Metadaten der verfügbarkeitsgruppe im Windows-Failovercluster gespeichert. Diese Versionsnummer wird erhöht, wenn neue Funktionen hinzugefügt werden.|  
|**basic_features**|**bit**|Gibt an, ob dies eine Basis-verfügbarkeitsgruppe ist. Weitere Informationen finden Sie unter [Basis-Verfügbarkeitsgruppen &#40;Always On-Verfügbarkeitsgruppen&#41;](../../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).|  
|**dtc_support**|**bit**|Gibt an, ob die DTC-Unterstützung für diese verfügbarkeitsgruppe aktiviert wurde. Die **DTC_SUPPORT** Option **CREATE AVAILABILITY GROUP** diese Einstellung steuert.|  
|**db_failover**|**bit**|Gibt an, ob die verfügbarkeitsgruppe ein Failover für Datenbank-integritätszuständen unterstützt. Die **DB_FAILOVER** Option **CREATE AVAILABILITY GROUP** diese Einstellung steuert.|  
|**is_distributed**|**bit**|Gibt an, ob dies eine verteilte verfügbarkeitsgruppe ist. Weitere Informationen finden Sie unter [Verteilte Verfügbarkeitsgruppen &#40;AlwaysOn-Verfügbarkeitsgruppen&#41;](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md).|  
  
## <a name="failure-condition-level--values"></a>Fehler-Bedingung Ebenenwerte  
 Die folgende Tabelle beschreibt die möglichen fehlerbedingungsebenen für die **Failure_condition_level** Spalte.  
  
|Wert|Fehlerbedingung|  
|-----------|-----------------------|  
|1|Gibt an, dass in einem der folgenden Fälle ein automatisches Failover initiiert werden muss:<br /><br /> <br /><br /> – Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst ist ausgefallen.<br /><br /> -Das Leasing der verfügbarkeitsgruppe für die Verbindung mit dem wsfc-Failovercluster läuft ab, da keine ACK-Meldung von der Serverinstanz empfangen wird. Weitere Informationen finden Sie unter [How It Works: SQL Server AlwaysOn Lease Timeout](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx).|  
|2|Gibt an, dass in einem der folgenden Fälle ein automatisches Failover initiiert werden muss:<br /><br /> <br /><br /> – Die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verbindet sich nicht mit dem Cluster und der vom Benutzer angegebene **Health_check_timeout** Schwellenwert für die verfügbarkeitsgruppe wurde überschritten.<br /><br /> -Das verfügbarkeitsreplikat ist im Status "Fehler".|  
|3|Gibt an, dass ein automatisches Failover bei kritischen internen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlern initiiert werden soll, z. B. verwaisten Spinlocks, schwerwiegenden Schreibzugriffsverletzungen oder zu vielen Sicherungen.<br /><br /> Dies ist der Standardwert.|  
|4|Gibt an, dass ein automatisches Failover bei mittelschweren internen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlern initiiert werden soll, z. B. bei dauerhaft unzureichendem Arbeitsspeicher im internen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Ressourcenpool.|  
|5|Gibt an, dass ein automatisches Failover bei sämtlichen qualifizierten Fehlerbedingungen initiiert werden soll, einschließlich:<br /><br /> <br /><br /> -Erschöpfung der SQL Engine-Arbeitsthreads.<br /><br /> -Erkennung eines unlösbaren Deadlocks.|  
  
## <a name="security"></a>Sicherheit  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW ANY DEFINITION-Berechtigung für die Serverinstanz.  
  
## <a name="see-also"></a>Siehe auch  
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [Always On-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Überwachen von Verfügbarkeitsgruppen & #40; Transact-SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Überwachen von Verfügbarkeitsgruppen &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
