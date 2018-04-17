---
title: Sp_stored_procedures (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_stored_procedures_TSQL
- sp_stored_procedures
dev_langs:
- TSQL
helpviewer_keywords:
- sp_stored_procedures
ms.assetid: fe52dd83-000a-4665-83fb-7a0024193dec
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fb9ddbb55213fa83a746d73a26e88c9c010f9ba6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spstoredprocedures-transact-sql"></a>sp_stored_procedures (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Liste der gespeicherten Prozeduren in der aktuellen Umgebung zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_stored_procedures [ [ @sp_name = ] 'name' ]   
    [ , [ @sp_owner = ] 'schema']   
    [ , [ @sp_qualifier = ] 'qualifier' ]  
    [ , [@fUsePattern = ] 'fUsePattern' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ **@sp_name =** ] **'***name***'**  
 Der Name der Prozedur zur Rückgabe von Kataloginformationen. *name* ist vom Datentyp **nvarchar(390)**und hat den Standardwert NULL. Mustervergleiche mit Platzhalterzeichen werden unterstützt.  
  
 [  **@sp_owner =** ] **"***Schema***"**  
 Der Name des Schemas, zu dem die Prozedur gehört. *schema* ist vom Datentyp **nvarchar(384)**und hat den Standardwert NULL. Mustervergleiche mit Platzhalterzeichen werden unterstützt. Wenn *owner* nicht angegeben wird, gelten die Standardregeln für die Sichtbarkeit von Prozeduren des zugrunde liegenden DBMS.  
  
 Wenn das aktuelle Schema in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine Prozedur mit dem angegebenen Namen enthält, wird diese Prozedur zurückgegeben. Wird ein nicht gekennzeichneter Name einer gespeicherten Prozedur angegeben, durchsucht [!INCLUDE[ssDE](../../includes/ssde-md.md)] die folgenden Schemas in der angegebenen Reihenfolge nach der Prozedur:  
  
-   Das **sys** -Schema der aktuellen Datenbank.  
  
-   Das Standardschema des aufrufenden Prozesses, wenn er in einem Batch oder in dynamischem SQL ausgeführt wird. Falls der nicht gekennzeichnete Prozedurname im Text einer anderen Prozedurdefinition auftritt, wird als Nächstes das Schema durchsucht, das diese andere Prozedur enthält.  
  
-   Das **dbo** -Schema in der aktuellen Datenbank  
  
 [  **@qualifier =** ] **"***Qualifizierer***"**  
 Der Name des Prozedurqualifizierers. *qualifier* ist vom Datentyp **sysname**und hat den Standardwert NULL. Verschiedene DBMS-Produkte unterstützen eine dreiteilige Namensgebung für Tabellen in der Form (*Qualifizierer***.*** Schema***.*** Namen*. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], *Qualifizierer* stellt den Datenbanknamen dar. Bei einigen anderen Produkten stellt sie den Servernamen der Datenbankumgebung für die Tabelle dar.  
  
 [  **@fUsePattern =** ] **"***fUsePattern***"**  
 Legt fest, ob Unterstrich (_), Prozent (%) oder Klammern ([ oder ]) als Platzhalterzeichen interpretiert werden. *fUsePattern* ist vom Datentyp **bit**. Der Standardwert ist 1.  
  
 **0** = Mustervergleich ist deaktiviert.  
  
 **1** = Mustervergleich ist aktiviert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**PROCEDURE_QUALIFIER**|**sysname**|Der Name des Prozedurqualifizierers. Diese Spalte kann NULL enthalten.|  
|**PROCEDURE_OWNER**|**sysname**|Der Name des Prozedurbesitzers. Diese Spalte gibt immer einen Wert zurück.|  
|**PROCEDURE_NAME**|**nvarchar(134)**|Der Name der Prozedur. Diese Spalte gibt immer einen Wert zurück.|  
|**NUM_INPUT_PARAMS**|**int**|Zur künftigen Verwendung reserviert.|  
|**NUM_OUTPUT_PARAMS**|**int**|Zur künftigen Verwendung reserviert.|  
|**NUM_RESULT_SETS**|**int**|Zur künftigen Verwendung reserviert.|  
|**"HINWEISE"**|**varchar(254)**|Die Beschreibung der Prozedur. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt für diese Spalte keinen Wert zurück.|  
|**PROCEDURE_TYPE**|**smallint**|Der Prozedurtyp. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gibt immer 2,0 zurück. Die folgenden Werte sind möglich:<br /><br /> 0 = SQL_PT_UNKNOWN<br /><br /> 1 = SQL_PT_PROCEDURE<br /><br /> 2 = SQL_PT_FUNCTION|  
  
## <a name="remarks"></a>Hinweise  
 Für eine optimale Interoperabilität sollte der Gatewayclient nur einen SQL-Standardmustervergleich voraussetzen (die Platzhalterzeichen Prozent (%) und Unterstrich (_)).  
  
 Da die Berechtigungen des aktuellen Benutzers zum Ausführungszugriff auf eine bestimmte gespeicherte Prozedur nicht unbedingt überprüft werden, ist der Zugriff nicht unter allen Umständen sichergestellt. Beachten Sie, dass nur eine dreiteilige Benennung verwendet wird. Dies bedeutet, dass nur lokal gespeicherte Prozeduren, werden keine remote gespeicherte Prozeduren (die vierteilige Benennung erfordern) zurückgegeben, bei der Ausführung für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Wenn das Serverattribut ACCESSIBLE_SPROC im Resultset von **sp_server_info**den Wert Y hat, werden nur Informationen zu den gespeicherten Prozeduren zurückgegeben, die der aktuelle Benutzer ausführen kann.  
  
 **sp_stored_procedures** entspricht **SQLProcedures** in ODBC. Die zurückgegebenen Informationen werden nach **PROCEDURE_QUALIFIER**, **PROCEDURE_OWNER**und **PROCEDURE_NAME**geordnet.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert SELECT-Berechtigung für das Schema.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-all-stored-procedures-in-the-current-database"></a>A. Zurückgeben aller gespeicherten Prozeduren in der aktuellen Datenbank  
 Im folgenden Beispiel werden alle gespeicherten Prozeduren in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_stored_procedures;  
```  
  
### <a name="b-returning-a-single-stored-procedure"></a>B. Zurückgeben einer einzelnen gespeicherten Prozedur  
 Im folgenden Beispiel wird ein Resultset für die gespeicherte Prozedur `uspLogError` zurückgegeben.  
  
```  
USE AdventureWorks2012;  
GO  
sp_stored_procedures N'uspLogError', N'dbo', N'AdventureWorks2012', 1;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Prozeduren für Kataloginformationen &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
