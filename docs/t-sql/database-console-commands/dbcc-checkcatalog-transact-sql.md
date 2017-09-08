---
title: DBCC CHECKCATALOG (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f63850a2cf39d783daee65431da349d04cba3b03
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-checkcatalog-transact-sql"></a>DBCC CHECKCATALOG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 *Database_name* | *Database_id* | 0  
 Der Name oder die ID der Datenbank, für die die Katalogkonsistenz überprüft werden soll. Erfolgt keine Eingabe, oder wird 0 angegeben, wird die aktuelle Datenbank verwendet. Datenbanknamen müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 WITH NO_INFOMSGS  
 Alle Informationsmeldungen werden unterdrückt.  
  
## <a name="remarks"></a>Hinweise  
Nach der Fertigstellung des Befehls DBCC CATALOG wird eine Meldung ins [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Fehlerprotokoll geschrieben. Wurde der DBCC-Befehl erfolgreich ausgeführt, zeigt die Meldung den erfolgreichen Abschluss und die Ausführungsdauer des Befehls an. Wurde der DBCC-Befehl aufgrund eines Fehlers vor Abschluss der Überprüfung beendet, zeigt die Meldung an, dass der Befehl beendet wurde. Außerdem wird ein Statuswert und die Ausführungsdauer des Befehls angegeben. In der folgenden Tabelle sind die Statuswerte aufgeführt und beschrieben, die in der Meldung enthalten sein können.
  
|Status|Description|  
|-----------|-----------------|  
|0|Fehlernummer 8930 wurde ausgelöst. Dies weist auf beschädigte Metadaten hin, die die Beendigung des DBCC-Befehls verursacht haben.|  
|1|Fehlernummer 8967 wurde ausgelöst. Ein interner DBCC-Fehler ist aufgetreten.|  
|2|Beim Reparieren einer Datenbank im Notfallmodus ist ein Fehler aufgetreten.|  
|3|Dies weist auf beschädigte Metadaten hin, die die Beendigung des DBCC-Befehls verursacht haben.|  
|4|Eine Assertations- oder Zugriffsverletzung wurde entdeckt.|  
|5|Ein unbekannter Fehler ist aufgetreten, der den DBCC-Befehl beendet hat.|  
  
DBCC CHECKCATALOG führt verschiedene Konsistenzprüfungen zwischen System-Metadatentabellen aus. DBCC CHECKCATALOG verwendet eine interne Datenbankmomentaufnahme, um die für die Ausführung dieser Überprüfungen erforderliche Transaktionskonsistenz bereitzustellen. Weitere Informationen finden Sie unter [Anzeigen der Größe der Datei mit geringer Dichte einer Datenbank-Momentaufnahme &#40; Transact-SQL &#41; ](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md) und im Abschnitt "DBCC interne Datenbankmomentaufnahme" in [DBCC &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-transact-sql.md).
Wenn eine Momentaufnahme nicht erstellt werden kann, erwirbt DBCC CHECKCATALOG eine exklusive Datenbanksperre, um die erforderliche Konsistenz zu erhalten. Wenn Inkonsistenzen gefunden werden, können diese nicht repariert werden, und die Datenbank muss von einer Sicherung wiederhergestellt werden.
  
> [!NOTE]  
>  Ausführen von DBCC CHECKCATALOG für **Tempdb** Überprüfungen ausgeführt. Dies liegt daran, dass aus Leistungsgründen keine datenbankmomentaufnahmen verfügbar sind **Tempdb**. Dies bedeutet, dass die erforderliche Transaktionskonsistenz nicht erhalten werden kann. Wiederverwenden des Servers zum Auflösen einer beliebigen **Tempdb** Metadaten zu beseitigen.  
  
> [!NOTE]  
>  DBCC CHECKCATALOG überprüft keine FILESTREAM-Daten. FILESTREAM speichert BLOBs (Binary Large Objects) im Dateisystem.  
  
DBCC CHECKCATALOG wird auch ausgeführt, im Rahmen des [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md).
  
## <a name="result-sets"></a>Resultsets  
Falls keine Datenbank angegeben ist, gibt DBCC CHECKCATALOG Folgendes zurück:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
Falls [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] als Datenbankname angegeben ist, gibt DBCC CHECKCATALOG Folgendes zurück:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Sysadmin** festen Serverrolle oder die **Db_owner** festen Datenbankrolle "".  
  
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
  
## <a name="see-also"></a>Siehe auch  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[Systemtabellen &#40; Transact-SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)
  

