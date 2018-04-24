---
title: CREATE DATABASE (Parallel Data Warehouse) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 40cacde4-ac72-45f7-9564-d76e2b4a741a
caps.latest.revision: 13
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 41ed767a4acd2dbe4b202e94ed054da46810e14a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-database-parallel-data-warehouse"></a>CREATE DATABASE (Parallel Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Erstellt eine neue Datenbank auf einer [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]-Appliance. Verwenden Sie diese Anweisung, um alle Dateien zu erstellen, die einer Appliancedatenbank zugeordnet sind, und um die Optionen für die maximale Größe und die automatische Vergrößerung der Datenbanktabellen und des Transaktionsprotokolls festzulegen.  
  
 ![Symbol zum Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions &#40;Transact-SQL&#41; (Transact-SQL-Syntaxkonventionen (Transact-SQL))](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
CREATE DATABASE database_name   
WITH (   
    [ AUTOGROW = ON | OFF , ]   
    REPLICATED_SIZE = replicated_size [ GB ] ,  
    DISTRIBUTED_SIZE = distributed_size [ GB ] ,  
    LOG_SIZE = log_size [ GB ] )  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Der Name der neuen Datenbank. Weitere Informationen zu zulässigen Datenbanknamen finden Sie unter „Object Naming Rules“ (Regeln für die Objektbenennung) und „Reserved Database Names“ (Reservierte Datenbanknamen) in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 AUTOGROW = ON | **OFF**  
 Gibt an, ob die Parameter *replicated_size*, *distributed_size* und *log_size* für diese Datenbank automatisch je nach Bedarf über ihre angegebenen Größen hinweg vergrößert werden. Der Standardwert lautet **OFF**.  
  
 Wenn AUTOGROW auf ON festgelegt ist, vergrößern sich *replicated_size*, *distributed_size* und *log_size* nach Bedarf (nicht in Blöcken der zuerst angegebenen Größe) bei jeder Dateneingabe, jedem Update oder anderen Aktionen, die mehr Speicherplatz als den bereits zugewiesenen erfordern.  
  
 Wenn AUTOGROW auf OFF festgelegt ist, verändern sich die Größen nicht automatisch. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] gibt einen Fehler zurück, wenn eine Aktion versucht wird, die erfordert, dass sich *replicated_size*, *distributed_size* oder *log_size* über ihren angegebenen Wert hinweg vergrößern.  
  
 AUTOGROW ist für alle Größen entweder auf ON oder auf OFF festgelegt. Es ist beispielsweise nicht möglich, AUTOGROW für *log_size* auf ON und für *replicated_size* auf OFF festzulegen.  
  
 *replicated_size* [ GB ]  
 Eine positive Zahl. Legt die Größe (eine ganze Zahl oder Dezimalzahl Gigabytes) für den gesamten Speicherplatz fest, der replizierten Tabellen und den entsprechenden Daten *auf jedem Computeknoten* zugewiesen wurde. Die minimalen und maximalen Anforderungen für *replicated_size* finden Sie unter „Minimum and Maximum Values“ (Minimale und maximale Werte) in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Wenn AUTOGROW auf ON festgelegt ist, können sich replizierte Tabellen über diese Begrenzung hinaus vergrößern.  
  
 Wenn AUTOGROW auf OFF festgelegt ist, wird ein Fehler zurückgegeben, wenn ein Benutzer versucht, eine neue replizierte Tabelle zu erstellen, Daten in eine bestehende replizierte Tabelle einzufügen oder eine bestehende replizierte Tabelle auf eine Weise zu aktualisieren, durch die die Größe über *replicated_size* hinweg steigen würde.  
  
 *distributed_size* [ GB ]  
 Eine positive Zahl. Die Größe, als ganze Zahl oder Dezimalzahl Gigabytes, für den gesamten Speicherplatz, der verteilten Tabellen (und den entsprechenden Daten) *auf der gesamten Appliance* zugewiesen wurde. Die minimalen und maximalen Anforderungen für *distributed_size* finden Sie unter „Minimum and Maximum Values“ (Minimale und maximale Werte) in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Wenn AUTOGROW auf ON festgelegt ist, können sich verteilte Tabellen über diese Begrenzung hinaus vergrößern.  
  
 Wenn AUTOGROW auf OFF festgelegt ist, wird ein Fehler zurückgegeben, wenn ein Benutzer versucht, eine neue verteilte Tabelle zu erstellen, Daten in eine bestehende verteilte Tabelle einzufügen oder eine bestehende verteilte Tabelle auf eine Weise zu aktualisieren, durch die die Größe über *distributed_size* hinweg steigen würde.  
  
 *log_size* [ GB ]  
 Eine positive Zahl. Die Größe (als ganze Zahl oder Dezimalzahl Gigabytes) für das Transaktionsprotokoll *auf der gesamten Appliance*.  
  
 Die minimalen und maximalen Anforderungen für *log_size* finden Sie unter „Minimum and Maximum Values“ (Minimale und maximale Werte) in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Wenn AUTOGROW auf ON festgelegt ist, kann sich die Protokolldatei über diese Begrenzung hinaus vergrößern. Verwenden Sie die Anweisung [DBCC SHRINKLOG (Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md), um die Größe der Protokolldateien auf deren Originalgröße zu verkleinern.  
  
 Wenn AUTOGROW auf OFF festgelegt ist, wird an den Benutzer ein Fehler zurückgegeben, wenn eine Aktion ausgeführt wird, durch die sich die Protokollgröße auf einem einzelnen Computeknoten über *log_size* hinaus steigern würde.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die **CREATE ANY DATABASE**-Berechtigung in der Masterdatenbank oder die Mitgliedschaft in der festen Serverrolle **sysadmin**.  
  
 Im folgenden Beispiel wird dem Datenbankbenutzer Fay die Berechtigung zum Erstellen einer Datenbank erteilt.  
  
```  
USE master;  
GO  
GRANT CREATE ANY DATABASE TO [Fay];  
GO  
```  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Datenbanken werden mit dem Datenbank-Kompatibilitätsgrad 120, also dem Kompatibilitätsgrad für [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], erstellt. Dadurch wird sichergestellt, dass die Datenbank alle [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]-Funktionen verwenden kann, die PDW verwendet.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Die CREATE DATABASE-Anweisung ist in einer expliziten Transaktion nicht zulässig. Weitere Informationen finden Sie unter [Transact-SQL-Anweisungen](../../t-sql/statements/statements.md).  
  
 Informationen zu minimalen und maximalen Einschränkungen für Datenbanken finden Sie unter „Minimum and Maximum Values“ (Minimale und maximale Werte) in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Bei der Erstellung der Datenbank muss genügend freier Speicherplatz *auf jedem Computeknoten* verfügbar sein, um den kombinierten Gesamtspeicherplatz der folgenden Größen zuzuweisen:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank mit Tabellen mit einer Größe von *replicated_table_size*.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank mit Tabellen mit einer Größe von (*distributed_table_size* / Anzahl von Computeknoten).  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Protokolle mit einer Größe von (*log_size* / Anzahl von Computeknoten).  
  
## <a name="locking"></a>Sperren  
 Führt eine gemeinsame Sperre für das DATABASE-Objekt durch.  
  
## <a name="metadata"></a>Metadaten  
 Nachdem dieser Vorgang erfolgreich abgeschlossen wurde, erscheint ein Eintrag für diese Datenbank in den Metadatensichten [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) und [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-basic-database-creation-examples"></a>A. Beispiele für die Erstellung einer grundlegenden Datenbank  
 Im folgenden Beispiel wird die Datenbank `mytest` mit einem zugewiesenen Speicherplatz von 100 GB pro Computeknoten für replizierte Tabellen, 500 GB pro Appliance für verteilte Tabellen und 100 GB pro Appliance für das Transaktionsprotokoll erstellt. In diesem Beispiel ist die Standardeinstellung für AUTOGROW auf OFF festgelegt.  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB );  
```  
  
 Im folgenden Beispiel wird die Datenbank `mytest` mit den gleichen Parametern wie oben erstellt, wobei AUTOGROW auf ON festgelegt ist. Dadurch kann sich die Datenbank über die angegebenen Größenparameter hinweg vergrößern.  
  
```  
CREATE DATABASE mytest  
   WITH   
   (AUTOGROW = ON,  
   REPLICATED_SIZE = 100 GB,  
   DISTRIBUTED_SIZE = 500 GB,  
   LOG_SIZE = 100 GB);  
```  
  
### <a name="b-creating-a-database-with-partial-gigabyte-sizes"></a>B. Erstellen einer Datenbank mit partiellen Gigabytegrößen  
 Im folgenden Beispiel wird die Datenbank `mytest`, für die AUTOGROW auf OFF festgelegt ist, mit einem zugewiesenen Speicherplatz von 1,5 GB pro Computeknoten für replizierte Tabellen, 5,25 GB pro Appliance für verteilte Tabellen und 10 GB pro Appliance für das Transaktionsprotokoll erstellt.  
  
```  
CREATE DATABASE mytest  
   WITH   
   (REPLICATED_SIZE = 1.5 GB,  
   DISTRIBUTED_SIZE = 5.25 GB,  
   LOG_SIZE = 10 GB);  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER DATABASE &#40;Parallel Data Warehouse&#41;](../../t-sql/statements/alter-database-parallel-data-warehouse.md)   
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)  
  
  
