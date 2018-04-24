---
title: GRANT (Objektberechtigungen) (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], system objects
- system objects [SQL Server]
- GRANT statement, system objects
ms.assetid: 9d4e89f4-478f-419a-8b50-b096771e3880
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 367193c6f806cdc3106bd99170e1aa8c3f589057
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="grant-system-object-permissions-transact-sql"></a>GRANT (Berechtigungen für Systemobjekte) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erteilt Berechtigungen für Systemobjekte wie z. B. im System gespeicherte Prozeduren, erweiterte gespeicherte Prozeduren, Funktionen und Sichten.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
GRANT { SELECT | EXECUTE } ON [ sys.]system_object TO principal   
```  
  
## <a name="arguments"></a>Argumente  
 [ sys.] .  
 Der sys-Qualifizierer ist nur erforderlich, wenn auf Katalogsichten und dynamische Verwaltungssichten verwiesen wird.  
  
 *system_object*  
 Gibt das Objekt an, für das die Berechtigung erteilt wird.  
  
 *principal*  
 Gibt den Prinzipal an, für den die Berechtigung erteilt wird.  
  
## <a name="remarks"></a>Remarks  
 Mit dieser Anweisung können Berechtigungen für bestimmte gespeicherte Prozeduren, erweiterte gespeicherte Prozeduren, Tabellenwertfunktionen, Skalarfunktionen, Sichten, Katalogsichten, Kompatibilitätssichten, INFORMATION_SCHEMA-Sichten, dynamische Verwaltungssichten und Systemtabellen erteilt werden, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert wurden. Alle Systemobjekte sind als eindeutiger Datensatz in der Ressourcendatenbank des Servers (mssqlsystemresource) vorhanden. Die Ressourcendatenbank ist schreibgeschützt. Ein Link zum Objekt wird in einem Datensatz im sys-Schema jeder Datenbank verfügbar gemacht. Die Berechtigung zum Ausführen oder Auswählen eines Systemobjekts kann erteilt, verweigert und aufgehoben werden.  
  
 Durch das Erteilen der Berechtigung zum Ausführen oder Auswählen eines Objekts müssen nicht alle Berechtigungen bereitgestellt werden, die zum Verwenden des Objekts erforderlich sind. Von den meisten Objekten werden Vorgänge ausgeführt, für die zusätzliche Berechtigungen erforderlich sind. Ein Benutzer, dem die EXECUTE-Berechtigung für sp_addlinkedserver erteilt wurde, kann z. B. nur dann einen Verbindungsserver erstellen, wenn der Benutzer auch ein Mitglied der festen Serverrolle sysadmin ist.  
  
 Die Standardnamensauflösung löst nicht qualifizierte Prozedurnamen für die Ressourcendatenbank auf. Daher ist der sys-Qualifizierer nur erforderlich, wenn Katalogsichten und dynamische Verwaltungssichten angegeben werden.  
  
 Das Erteilen von Berechtigungen für Trigger und für Spalten von Systemobjekten wird nicht unterstützt.  
  
 Berechtigungen für Systemobjekte werden bei Upgrades von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beibehalten.  
  
 Systemobjekte werden in der [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) -Katalogsicht angezeigt. Die Berechtigungen für Systemobjekte werden in der [sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) -Katalogsicht in der Masterdatenbank angezeigt.  
  
 Die folgende Abfrage gibt Informationen zu Berechtigungen für Systemobjekte zurück:  
  
```  
SELECT * FROM master.sys.database_permissions AS dp   
    JOIN sys.system_objects AS so  
    ON dp.major_id = so.object_id  
    WHERE dp.class = 1 AND so.parent_object_id = 0 ;  
GO  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL SERVER-Berechtigung.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-granting-select-permission-on-a-view"></a>A. Gewähren der SELECT-Berechtigung für eine Sicht  
 Im folgenden Beispiel wird dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen `Sylvester1` die Berechtigung zum Auswählen einer Sicht erteilt, in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen aufgeführt sind. Dann wird die zusätzliche Berechtigung erteilt, die zum Anzeigen von Metadaten für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldenamen erforderlich ist, die sich nicht im Besitz des Benutzers befinden.  
  
```  
USE AdventureWorks2012;  
GRANT SELECT ON sys.sql_logins TO Sylvester1;  
GRANT VIEW SERVER STATE to Sylvester1;  
GO  
```  
  
### <a name="b-granting-execute-permission-on-an-extended-stored-procedure"></a>B. Gewähren der EXECUTE-Berechtigung für eine erweiterte gespeicherte Prozedur  
 Im folgenden Beispiel wird `EXECUTE` die `xp_readmail`-Berechtigung für `Sylvester1` erteilt.  
  
```  
GRANT EXECUTE ON xp_readmail TO Sylvester1;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sys.system_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [REVOKE (Berechtigungen für Systemobjekte) &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-system-object-permissions-transact-sql.md)   
 [DENY (Berechtigungen für Systemobjekte) &#40;Transact-SQL&#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)  
  
  
