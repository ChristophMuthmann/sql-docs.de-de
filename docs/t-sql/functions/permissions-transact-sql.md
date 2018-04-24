---
title: PERMISSIONS (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PERMISSIONS_TSQL
- PERMISSIONS
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], verifying
- current permission status
- users [SQL Server], permissions status
- checking permission status
- security [SQL Server], permissions
- verifying permission status
- testing permissions
- PERMISSIONS function
ms.assetid: 81625a56-b160-4424-91c5-1ce8b259a8e6
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f785ca7ad10263ed83503ad24fe905212a30dd54
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="permissions-transact-sql"></a>PERMISSIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt einen Wert mit einem Bitmuster zurück, das die Anweisungs-, Objekt- oder Spaltenberechtigungen für den aktuellen Benutzer angibt.  
  
 **Wichtig** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden Sie stattdessen [fn_my_permissions](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md) und [Has_Perms_By_Name](../../t-sql/functions/has-perms-by-name-transact-sql.md). Wenn die PERMISSIONS-Funktion weiterhin verwendet wird, verlangsamt sich möglicherweise die Leistung.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
PERMISSIONS ( [ objectid [ , 'column' ] ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *objectid*  
 Die ID eines sicherungsfähigen Elements. Falls *objectid* nicht angegeben wird, enthält der Bitmusterwert Anweisungsberechtigungen für den aktuellen Benutzer. Andernfalls enthält das Bitmuster Berechtigungen für das sicherungsfähige Element für den aktuellen Benutzer. Das angegebene sicherungsfähige Element muss sich in der aktuellen Datenbank befinden. Verwenden Sie die [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md)-Funktion, um den *objectid*-Wert zu bestimmen.  
  
 **'** *column* **'**  
 Dies ist der optionale Name einer Spalte, für die Berechtigungsinformationen zurückgegeben werden. Bei der Spalte muss es sich um einen gültigen Spaltennamen in der durch *objectid* angegebenen Tabelle handeln.  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>Remarks  
 Mithilfe von PERMISSIONS kann festgestellt werden, ob der aktuelle Benutzer über die Berechtigungen verfügt, die zum Ausführen einer Anweisung oder zum Erteilen einer Berechtigung für einen anderen Benutzer mithilfe von GRANT erforderlich sind.  
  
 Die Berechtigungsinformationen werden in Form eines 32-Bit-Bitmusters zurückgegeben.  
  
 Die niederwertigen 16 Bits spiegeln Berechtigungen wider, die dem Benutzer erteilt wurden, sowie Berechtigungen, die für Windows-Gruppen und feste Serverrollen gelten, deren Mitglied der aktuelle Benutzer ist. So zeigt z.B. ein Rückgabewert von 66 (Hexadezimalwert 0x42) bei nicht angegebenem Wert für *objectid*, dass der Benutzer über Ausführungsberechtigungen für die CREATE TABLE- (Dezimalwert 2) und die BACKUP DATABASE-Anweisung (Dezimalwert 64) verfügt.  
  
 Die höherwertigen 16 Bits spiegeln die Berechtigungen wider, die der Benutzer anderen Benutzern mithilfe von GRANT erteilen kann. Die höherwertigen 16 Bits werden genau wie die in den folgenden Tabellen beschriebenen niederwertigen 16 Bits interpretiert, mit der Ausnahme, dass sie um 16 Bits nach links verschoben (mit 65536 multipliziert) werden. So ist z.B. 0x8 (Dezimalwert 8) das Bit, das INSERT-Berechtigungen anzeigt, wenn ein Wert für *objectid* angegeben wurde. Dagegen zeigt 0x80000 (Dezimalwert 524288) die Möglichkeit zum Erteilen von Einfügerechten (INSERT-Berechtigungen) mithilfe von GRANT an, da 524288 = 8 x 65536.  
  
 Aufgrund der Mitgliedschaft in Rollen besteht die Möglichkeit, dass ein Benutzer keine Berechtigung zum Ausführen einer Anweisung besitzt, diese Berechtigung jedoch trotzdem einem anderen Benutzer erteilen kann.  
  
 Die folgende Tabelle zeigt die für Anweisungsberechtigungen verwendeten Bits (*objectid* ist nicht angegeben).  
  
|Bit (dez)|Bit (hex)|Anweisungsberechtigung|  
|-----------------|-----------------|--------------------------|  
|1|0x1|CREATE DATABASE (nur master-Datenbank)|  
|2|0x2|CREATE TABLE|  
|4|0x4|CREATE PROCEDURE|  
|8|0x8|CREATE VIEW|  
|16|0x10|CREATE RULE|  
|32|0x20|CREATE DEFAULT|  
|64|0x40|BACKUP DATABASE|  
|128|0x80|BACKUP LOG|  
|256|0x100|Reserviert.|  
  
 Die folgende Tabelle zeigt die für Objektberechtigungen verwendeten Bits, die zurückgegeben werden, wenn nur *objectid* angegeben wird.  
  
|Bit (dez)|Bit (hex)|Anweisungsberechtigung|  
|-----------------|-----------------|--------------------------|  
|1|0x1|SELECT ALL|  
|2|0x2|UPDATE ALL|  
|4|0x4|REFERENCES ALL|  
|8|0x8|INSERT|  
|16|0x10|Delete|  
|32|0x20|EXECUTE (nur Prozeduren)|  
|4096|0x1000|SELECT ANY (mindestens eine Spalte)|  
|8192|0x2000|UPDATE ANY|  
|16384|0x4000|REFERENCES ANY|  
  
 Die folgende Tabelle zeigt die für Objektberechtigungen auf Spaltenebene verwendeten Bits, die zurückgegeben werden, wenn Werte sowohl für *objectid* als auch für die Spalte angegeben werden.  
  
|Bit (dez)|Bit (hex)|Anweisungsberechtigung|  
|-----------------|-----------------|--------------------------|  
|1|0x1|SELECT|  
|2|0x2|UPDATE|  
|4|0x4|REFERENCES|  
  
 NULL wird zurückgegeben, wenn ein angegebener Parameter NULL oder ungültig ist (z.B. die Angabe eines Werts für *objectid* oder column, für den keine Objekt-ID bzw. Spalte vorhanden ist). Die Bitwerte für Berechtigungen, die nicht anwendbar sind (z. B. EXECUTE-Berechtigung, Bit 0x20, für eine Tabelle), sind nicht definiert.  
  
 Verwenden Sie den bitweisen AND-Operator (&), um jedes festgelegte Bit in dem von der PERMISSIONS-Funktion zurückgegebenen Bitmuster zu ermitteln.  
  
 Außerdem kann die gespeicherte Systemprozedur sp_helprotect dazu verwendet werden, eine Liste mit Objektberechtigungen für einen Benutzer in der aktuellen Datenbank zurückzugeben.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-the-permissions-function-with-statement-permissions"></a>A. Verwenden der PERMISSIONS-Funktion mit Anweisungsberechtigungen  
 Im folgenden Beispiel wird ermittelt, ob der aktuelle Benutzer die `CREATE TABLE`-Anweisung ausführen kann.  
  
```  
IF PERMISSIONS()&2=2  
   CREATE TABLE test_table (col1 INT)  
ELSE  
   PRINT 'ERROR: The current user cannot create a table.';  
```  
  
### <a name="b-using-the-permissions-function-with-object-permissions"></a>B. Verwenden der PERMISSIONS-Funktion mit Objektberechtigungen  
 Im folgenden Beispiel wird bestimmt, ob der aktuelle Benutzer eine Datenzeile in die `Address`-Tabelle in der `AdventureWorks2012`-Datenbank einfügen darf.  
  
```  
IF PERMISSIONS(OBJECT_ID('AdventureWorks2012.Person.Address','U'))&8=8   
   PRINT 'The current user can insert data into Person.Address.'  
ELSE  
   PRINT 'ERROR: The current user cannot insert data into Person.Address.';  
```  
  
### <a name="c-using-the-permissions-function-with-grantable-permissions"></a>C. Verwenden der PERMISSIONS-Funktion mit erteilbaren Berechtigungen  
 Im folgenden Beispiel wird ermittelt, ob der aktuelle Benutzer einem anderen Benutzer die INSERT-Berechtigung für die `Address`-Tabelle in der `AdventureWorks2012`-Datenbank erteilen kann.  
  
```  
IF PERMISSIONS(OBJECT_ID('AdventureWorks2012.Person.Address','U'))&0x80000=0x80000  
   PRINT 'INSERT on Person.Address is grantable.'  
ELSE  
   PRINT 'You may not GRANT INSERT permissions on Person.Address.';  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_helprotect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [Systemfunktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  
