---
title: DBCC CHECKCATALOG (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|database-console-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DBCC_CHECKCATALOG_TSQL
- DBCC CHECKCATALOG
- CHECKCATALOG_TSQL
- CHECKCATALOG
dev_langs:
- TSQL
helpviewer_keywords:
- catalogs [SQL Server], consistency checks
- checking catalog consistency
- DBCC CHECKCATALOG statement
- integrity [SQL Server], catalogs
- consistency [SQL Server], catalogs
ms.assetid: 8076eb4e-f049-44bf-9a35-45cdd6ef0105
caps.latest.revision: 51
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6e5f9258cc9b2c74407968703be1c2c2901ae4b3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="dbcc-checkcatalog-transact-sql"></a>DBCC CHECKCATALOG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Überprüft die Katalogkonsistenz innerhalb der angegebenen Datenbank. Die Datenbank muss online sein.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DBCC CHECKCATALOG   
[   
    (   
    database_name | database_id | 0  
    )  
]  
    [ WITH NO_INFOMSGS ]   
```  
  
## <a name="arguments"></a>Argumente  
 *database_name* | *database_id* | 0  
 Der Name oder die ID der Datenbank, für die die Katalogkonsistenz überprüft werden soll. Erfolgt keine Eingabe, oder wird 0 angegeben, wird die aktuelle Datenbank verwendet. Datenbanknamen müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) entsprechen.  
  
 WITH NO_INFOMSGS  
 Alle Informationsmeldungen werden unterdrückt.  
  
## <a name="remarks"></a>Remarks  
Nach der Fertigstellung des Befehls DBCC CATALOG wird eine Meldung ins [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll geschrieben. Wurde der DBCC-Befehl erfolgreich ausgeführt, zeigt die Meldung den erfolgreichen Abschluss und die Ausführungsdauer des Befehls an. Wurde der DBCC-Befehl aufgrund eines Fehlers vor Abschluss der Überprüfung beendet, zeigt die Meldung an, dass der Befehl beendet wurde. Außerdem wird ein Statuswert und die Ausführungsdauer des Befehls angegeben. In der folgenden Tabelle sind die Statuswerte aufgeführt und beschrieben, die in der Meldung enthalten sein können.
  
|Status|Description|  
|-----------|-----------------|  
|0|Fehlernummer 8930 wurde ausgelöst. Dies weist auf beschädigte Metadaten hin, die die Beendigung des DBCC-Befehls verursacht haben.|  
|1|Fehlernummer 8967 wurde ausgelöst. Ein interner DBCC-Fehler ist aufgetreten.|  
|2|Beim Reparieren einer Datenbank im Notfallmodus ist ein Fehler aufgetreten.|  
|3|Dies weist auf beschädigte Metadaten hin, die die Beendigung des DBCC-Befehls verursacht haben.|  
|4|Eine Assertations- oder Zugriffsverletzung wurde entdeckt.|  
|5|Ein unbekannter Fehler ist aufgetreten, der den DBCC-Befehl beendet hat.|  
  
DBCC CHECKCATALOG führt verschiedene Konsistenzprüfungen zwischen System-Metadatentabellen aus. DBCC CHECKCATALOG verwendet eine interne Datenbankmomentaufnahme, um die für die Ausführung dieser Überprüfungen erforderliche Transaktionskonsistenz bereitzustellen. Weitere Informationen finden Sie unter [Anzeigen der Größe der Datei mit geringer Dichte einer Datenbankmomentaufnahme &#40;SQL Server&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md) und im Abschnitt „Verwenden einer internen Datenbankmomentaufnahme mit DBCC“ unter [DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md).
Wenn eine Momentaufnahme nicht erstellt werden kann, erwirbt DBCC CHECKCATALOG eine exklusive Datenbanksperre, um die erforderliche Konsistenz zu erhalten. Wenn Inkonsistenzen gefunden werden, können diese nicht repariert werden, und die Datenbank muss von einer Sicherung wiederhergestellt werden.
  
> [!NOTE]  
> Beim Ausführen von DBCC CHECKCATALOG werden für **tempdb** keine Prüfungen vorgenommen. Der Grund hierfür liegt darin, dass aus Leistungsgründen für **tempdb** keine Datenbankmomentaufnahmen verfügbar sind. Dies bedeutet, dass die erforderliche Transaktionskonsistenz nicht erhalten werden kann. Verwenden Sie den Server wieder, um Probleme in **tempdb** mit Metadaten zu beseitigen.  
  
> [!NOTE]  
> DBCC CHECKCATALOG überprüft keine FILESTREAM-Daten. FILESTREAM speichert BLOBs (Binary Large Objects) im Dateisystem.  
  
DBCC CHECKCATALOG wird auch im Rahmen von [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) ausgeführt.
  
## <a name="result-sets"></a>Resultsets  
Falls keine Datenbank angegeben ist, gibt DBCC CHECKCATALOG Folgendes zurück:
  
```
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
Falls [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] als Datenbankname angegeben ist, gibt DBCC CHECKCATALOG Folgendes zurück:
  
```
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** oder der festen Datenbankrolle **db_owner**.  
  
## <a name="examples"></a>Beispiele  
Im folgenden Beispiel wird die Katalogintegrität in der aktuellen Datenbank und in der `AdventureWorks`-Datenbank überprüft.
  
```sql
-- Check the current database.  
DBCC CHECKCATALOG;  
GO  
-- Check the AdventureWorks2012 database.  
DBCC CHECKCATALOG (AdventureWorks2012);  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[Systemtabellen &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)
  
