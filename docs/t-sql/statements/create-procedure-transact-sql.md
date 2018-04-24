---
title: CREATE PROCEDURE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 09/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PROC
- PROCEDURE
- CREATE PROCEDURE
- CREATE_PROC_TSQL
- PROCEDURE_TSQL
- CREATE PROC
- PROC_TSQL
- CREATE_PROCEDURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- parameters [SQL Server], stored procedures
- table-valued parameters
- SET statement, stored procedures
- stored procedures [SQL Server], creating
- wildcard parameters [SQL Server]
- maximum size of stored procedures
- WITH RECOMPILE clause
- common language runtime [SQL Server], stored procedures
- CREATE PROCEDURE statement
- local temporary procedures [SQL Server]
- WITH ENCRYPTION clause
- output parameters [SQL Server]
- nesting stored procedures
- user-defined stored procedures [SQL Server]
- system stored procedures [SQL Server], creating
- deferred name resolution, stored procedures
- referenced tables [SQL Server]
- global temporary procedures [SQL Server]
- cursor data type
- temporary stored procedures [SQL Server]
- size [SQL Server], stored procedures
- automatic stored procedure execution
- creating stored procedures
ms.assetid: afe3d86d-c9ab-44e4-b74d-4e3dbd9cc58c
caps.latest.revision: 180
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 252a6808352bd919129b483101fd9e2fbf396523
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-procedure-transact-sql"></a>CREATE PROCEDURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Erstellt eine gespeicherte [!INCLUDE[tsql](../../includes/tsql-md.md)]- oder CLR-Prozedur (Common Language Runtime) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], Azure SQL Data Warehouse und Parallel Data Warehouse. Gespeicherte Prozeduren gleichen den Prozeduren in anderen Programmiersprachen bezüglich der folgenden Merkmale und Fähigkeiten:  
  
-   Annehmen von Eingabeparametern und Zurückgeben mehrerer Werte in Form von Ausgabeparametern an die aufrufende Prozedur oder den aufrufenden Batch.  
  
-   Aufnehmen von Programmierungsanweisungen, die Operationen in der Datenbank ausführen, einschließlich des Aufrufens anderer Prozeduren.  
  
-   Zurückgeben eines Statuswertes an eine aufrufende Prozedur oder einen aufrufenden Batch, der Erfolg oder Fehlschlagen (sowie die Ursache für das Fehlschlagen) anzeigt.  
  
 Mithilfe dieser Anweisung können Sie eine dauerhafte Prozedur in der aktuellen Datenbank oder eine temporäre Prozedur in der **tempdb**-Datenbank erstellen.  
  
> [!NOTE]  
>  In diesem Thema wird die Integration der .NET Framework-CLR in SQL Server erläutert. Die CLR-Integration gilt nicht für Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)].

Wenn Sie die ausführlichen Informationen zur Syntax überspringen und ein Beispiel für eine einfache gespeicherte Prozedur möchten, fahren Sie einfach mit dem Abschnitt [Einfache Beispiele](#Simple) fort.
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```sql
-- Transact-SQL Syntax for Stored Procedures in SQL Server and Azure SQL Database  
  
CREATE [ OR ALTER ] { PROC | PROCEDURE } 
    [schema_name.] procedure_name [ ; number ]   
    [ { @parameter [ type_schema_name. ] data_type }  
        [ VARYING ] [ = default ] [ OUT | OUTPUT | [READONLY]  
    ] [ ,...n ]   
[ WITH <procedure_option> [ ,...n ] ]  
[ FOR REPLICATION ]   
AS { [ BEGIN ] sql_statement [;] [ ...n ] [ END ] }  
[;]  
  
<procedure_option> ::=   
    [ ENCRYPTION ]  
    [ RECOMPILE ]  
    [ EXECUTE AS Clause ]  
```  
  
```sql
-- Transact-SQL Syntax for CLR Stored Procedures  
  
CREATE [ OR ALTER ] { PROC | PROCEDURE } 
    [schema_name.] procedure_name [ ; number ]   
    [ { @parameter [ type_schema_name. ] data_type }   
        [ = default ] [ OUT | OUTPUT ] [READONLY]  
    ] [ ,...n ]   
[ WITH EXECUTE AS Clause ]  
AS { EXTERNAL NAME assembly_name.class_name.method_name }  
[;]  
```  
  
```sql
-- Transact-SQL Syntax for Natively Compiled Stored Procedures  
  
CREATE [ OR ALTER ] { PROC | PROCEDURE } [schema_name.] procedure_name  
    [ { @parameter data_type } [ NULL | NOT NULL ] [ = default ] 
        [ OUT | OUTPUT ] [READONLY] 
    ] [ ,... n ]  
  WITH NATIVE_COMPILATION, SCHEMABINDING [ , EXECUTE AS clause ]  
AS  
{  
  BEGIN ATOMIC WITH (set_option [ ,... n ] )  
sql_statement [;] [ ... n ]  
 [ END ]  
}  
 [;]  
  
<set_option> ::=  
    LANGUAGE =  [ N ] 'language'  
  | TRANSACTION ISOLATION LEVEL =  { SNAPSHOT | REPEATABLE READ | SERIALIZABLE }  
  | [ DATEFIRST = number ]  
  | [ DATEFORMAT = format ]  
  | [ DELAYED_DURABILITY = { OFF | ON } ]  
```  
  
```sql
-- Transact-SQL Syntax for Stored Procedures in Azure SQL Data Warehouse
-- and Parallel Data Warehouse  
  
-- Create a stored procedure   
CREATE { PROC | PROCEDURE } [ schema_name.] procedure_name  
    [ { @parameterdata_type } [ OUT | OUTPUT ] ] [ ,...n ]  
AS { [ BEGIN ] sql_statement [;][ ,...n ] [ END ] }  
[;]  
```  
  
## <a name="arguments"></a>Argumente
OR ALTER  
 **Gilt für:** Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1).  
  
 Ändert die Prozedur, wenn sie bereits vorhanden ist.
 
 *schema_name*  
 Der Name des Schemas, zu dem die Prozedur gehört. Prozeduren sind schemagebunden. Wird bei der Erstellung der Prozedur kein Schemaname angegeben, wird automatisch das Standardschema des die Prozedur erstellenden Benutzers zugewiesen.  
  
 *procedure_name*  
 Der Name der Prozedur. Prozedurnamen müssen den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) entsprechen und innerhalb des Schemas eindeutig sein.  
  
 Beim Benennen von Prozeduren sollten Sie das Präfix **_sp** vermeiden. Dieses Präfix wird von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet, um Systemprozeduren zu bestimmen. Das Verwenden des Präfixes kann zur Beschädigung von Anwendungscode führen, falls eine Systemprozedur mit dem gleichen Namen vorhanden ist.  
  
 Lokale oder globale temporäre Prozeduren können erstellt werden, indem *procedure_name* ein einzelnes Nummernzeichen (#) (*#procedure_name*) für lokale temporäre Prozeduren und ein doppeltes Nummernzeichen (*##procedure_name*) für globale temporäre Prozeduren vorangestellt wird. Eine lokale temporäre Prozedur ist nur für die Verbindung sichtbar, von der sie erstellt wurde. Die Prozedur wird automatisch gelöscht, wenn die Verbindung geschlossen wird. Eine globale temporäre Prozedur ist für alle Verbindungen verfügbar und wird am Ende der letzten Sitzung gelöscht, die die Prozedur verwendet. Für CLR-Prozeduren können keine temporären Namen angegeben werden.  
  
 Der vollständige Name einer Prozedur oder einer globalen temporären Prozedur, einschließlich ##, darf 128 Zeichen nicht überschreiten. Der vollständige Name einer lokalen temporären Prozedur, einschließlich #, darf 116 Zeichen nicht überschreiten.  
  
 **;** *number*  
 **Gilt für:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Eine optionale ganze Zahl zum Gruppieren von Prozeduren mit dem gleichen Namen. Diese gruppierten Prozeduren können alle mit einer DROP PROCEDURE-Anweisung gelöscht werden.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Nummerierte Prozeduren können nicht den **xml**-Typ oder benutzerdefinierte CLR-Typen verwenden und können nicht in einer Planhinweisliste verwendet werden.  
  
 **@** *parameter*  
 Ein in der Prozedur deklarierter Parameter. Geben Sie einen Parameternamen an, der mit dem „at“-Zeichen (**@**) beginnt. Der Parametername muss den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) entsprechen. Parameter gelten lokal in der jeweiligen Prozedur, d. h., dass Sie die gleichen Parameternamen in anderen Prozeduren verwenden können.  
  
 Mindestens ein Parameter (maximal 2.100) kann deklariert werden. Der Benutzer muss beim Aufrufen der Prozedur den Wert jedes deklarierten Parameters bereitstellen, sofern kein Standardwert für den Parameter definiert oder der Wert nicht auf den eines anderen Parameters festgelegt ist. Wenn eine Prozedur [Tabellenwertparameter](../../relational-databases/tables/use-table-valued-parameters-database-engine.md) enthält und der Parameter im Aufruf fehlt, wird eine leere Tabelle übergeben. Parameter können nur die Stelle von Konstantenausdrücken einnehmen. Sie können nicht anstelle von Tabellennamen, Spaltennamen oder Namen anderer Datenbankobjekte verwendet werden. Weitere Informationen finden Sie unter [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md).  
  
 Parameter können nicht deklariert werden, wenn FOR REPLICATION angegeben ist.  
  
 [ *type_schema_name***.** ] *data_type*  
 Der Datentyp des Parameters und das Schema, zu dem der Datenbanktyp gehört.  
  
**Richtlinien für [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozeduren:**  
  
-   Alle [!INCLUDE[tsql](../../includes/tsql-md.md)]-Datentypen können als Parameter verwendet werden.  
  
-   Verwenden Sie den benutzerdefinierten Tabellentyp, um Tabellenwertparameter zu erstellen. Tabellenwertparameter können nur INPUT-Parameter sein und müssen vom READONLY-Schlüsselwort begleitet werden. Weitere Informationen finden Sie unter [Verwenden von Tabellenwertparametern &#40;Databank-Engine&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
-   **cursor**-Datentypen können nur OUTPUT-Parameter sein und müssen vom VARYING-Schlüsselwort begleitet werden.  
  
**Richtlinien für CLR-Prozeduren:**  
  
-   Alle systemeignen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentypen, die über eine Entsprechung im verwalteten Code verfügen, können als Parameter verwendet werden. Weitere Informationen zu Entsprechungen zwischen CLR-Typen und zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatentypen finden Sie unter [Zuordnen von CLR-Parameterdaten](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md). Weitere Informationen zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Systemdatentypen und ihrer Syntax finden Sie unter [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).  
  
-   Tabellenwertdatentypen oder **cursor**-Datentypen können nicht als Parameter verwendet werden.  
  
-   Wenn es sich beim Datentyp des Parameters um einen CLR-benutzerdefinierten Typ handelt, müssen Sie über die EXECUTE-Berechtigung für diesen Typ verfügen.  
  
VARYING  
 Gibt das als Ausgabeparameter unterstützte Resultset an. Dieser Parameter wird dynamisch durch die Prozedur erstellt. Sein Inhalt kann variieren. Gilt nur für **cursor**-Parameter. Diese Option ist für CLR-Prozeduren nicht gültig.  
  
*default*  
 Ein Standardwert für einen Parameter. Wenn ein Standardwert für einen Parameter definiert ist, kann die Prozedur ausgeführt werden, ohne dass ein Wert für diesen Parameter angegeben wird. Der Standardwert muss eine Konstante oder NULL sein. Der konstante Wert kann ein Platzhalter sein, wodurch beim Weitergeben des Parameters an die Prozedur das LIKE-Schlüsselwort verwendet werden kann.   
  
 Standardwerte werden in der **sys.parameters.default**-Spalte nur für CLR-Prozeduren erfasst. Diese Spalte hat für [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedurparameter den Wert NULL.  
  
OUT | OUTPUT  
 Gibt an, dass es sich bei dem Parameter um einen Ausgabeparameter handelt. Verwenden Sie OUTPUT-Parameter, um Informationen an die aufrufende Prozedur zurückzugeben. **text**-, **ntext**- und **image**-Parameter können als OUTPUT-Parameter verwendet werden, es sei denn, es handelt sich bei der Prozedur um eine CLR-Prozedur. Ein Ausgabeparameter kann ein Cursorplatzhalter sein, sofern die Prozedur keine CLR-Prozedur ist. Ein Tabellenwert-Datentyp kann nicht als OUTPUT-Parameter einer Prozedur angegeben werden.  
  
READONLY  
 Gibt an, dass der Parameter nicht aktualisiert oder innerhalb des Texts der Prozedur geändert werden kann. Wenn der Parametertyp ein Tabellenwerttyp ist, muss READONLY angegeben werden.  
  
RECOMPILE  
 Gibt an, dass das [!INCLUDE[ssDE](../../includes/ssde-md.md)] keinen Abfrageplan für die Prozedur zwischenspeichert, wodurch diese bei jeder Ausführung kompiliert werden muss. Weitere Informationen zu den Gründen für eine erzwungene Neukompilierung finden Sie unter [Erneutes Kompilieren einer gespeicherten Prozedur](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md). Diese Option kann nicht für CLR-Prozeduren verwendet werden, wenn FOR REPLICATION angegeben ist.  
  
 Verwenden Sie den RECOMPILE-Abfragehinweis in der Abfragedefinition, damit das [!INCLUDE[ssDE](../../includes/ssde-md.md)] Abfragepläne für einzelne Abfragen innerhalb einer Prozedur verwirft. Weitere Informationen finden Sie unter [Abfragehinweise &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
ENCRYPTION  
 **Gilt für:** SQL Server ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt an, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] den Originaltext der CREATE PROCEDURE-Anweisung in ein verborgenes Format umwandelt. Die Ausgabe der Verbergung ist nicht direkt in den Katalogsichten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sichtbar. Benutzer, die keinen Zugriff auf Systemtabellen oder Datenbankdateien haben, können den verborgenen Text nicht abrufen. Der Text ist jedoch für berechtigte Benutzer verfügbar, die entweder auf die Systemtabellen über den [DAC-Port](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md) oder direkt auf die Datenbankdateien zugreifen. Des Weiteren können Benutzer, die einen Debugger an den Serverprozess anfügen können, die entschlüsselte Prozedur zur Laufzeit vom Arbeitsspeicher abrufen. Weitere Informationen zu Berechtigungen zum Zugreifen auf Systemmetadaten finden Sie unter [Konfigurieren der Sichtbarkeit von Metadaten](../../relational-databases/security/metadata-visibility-configuration.md).  
  
 Diese Option ist für CLR-Prozeduren nicht gültig.  
  
 Prozeduren, die mit dieser Option erstellt wurden, können nicht als Teil der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Replikation veröffentlicht werden.  
  
EXECUTE AS-*Klausel*  
 Gibt den Sicherheitskontext an, unter dem die Prozedur ausgeführt wird.  
  
 Für nativ kompilierte gespeicherte Prozeduren, die mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] beginnen, bestehen keine Einschränkungen für die EXECUTE AS-Klausel. In [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] werden die SELF-, OWNER- und *‘user_name’*-Klauseln bei nativ kompilierten gespeicherten Prozeduren unterstützt.  
  
 Weitere Informationen finden Sie unter [EXECUTE AS-Klausel &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
FOR REPLICATION  
 **Gilt für:** SQL Server ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt an, dass die Prozedur für die Replikation erstellt ist. Entsprechend kann sie nicht für den Abonnenten ausgeführt werden. Eine Prozedur, die mit der Option FOR REPLICATION erstellt wurde, wird als Filter für Prozeduren verwendet und nur während der Replikation ausgeführt. Parameter können nicht deklariert werden, wenn FOR REPLICATION angegeben ist. FOR REPLICATION kann nicht für CLR-Prozeduren angegeben werden. Die Option RECOMPILE wird bei Prozeduren ignoriert, die mit FOR REPLICATION erstellt wurden.  
  
 Eine `FOR REPLICATION`-Prozedur verfügt über einen **RF**-Objekttyp in **sys.objects** und in **sys.procedures**.  
  
 { [ BEGIN ] *sql_statement* [;] [ ...*n* ] [ END ] }  
 Eine oder mehrere [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, die den Textkörper der Prozedur umfassen. Sie können die optionalen BEGIN- und END-Schlüsselwörter zum Einschließen der Anweisungen verwenden. Informationen hierzu erhalten Sie in den folgenden Abschnitten zu bewährten Methoden, allgemeinen Hinweisen und Einschränkungen.  
  
EXTERNAL NAME *assembly_name ***.*** class_name ***.*** method_name*  
 **Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Gibt für eine CLR-Prozedur, auf die verwiesen wird, die Methode einer [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Assembly an. *class_name* muss ein gültiger [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Bezeichner und als Klasse in der Assembly vorhanden sein. Wenn die Klasse einen mit einem Namespace qualifizierten Namen hat, in dem ein Punkt (**.**) zur Trennung der Bestandteile des Namespace verwendet wird, muss der Klassenname mithilfe von Klammern (**[]**) oder mit Anführungszeichen (**""**) getrennt werden. Bei der angegebenen Methode muss es sich um eine statische Methode der Klasse handeln.  
  
 Standardmäßig kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] keinen CLR-Code ausführen. Sie können Datenbankobjekte, die auf CLR-Module (Common Language Runtime) verweisen, erstellen, ändern und löschen. Bevor Sie diese Verweise in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausführen können, müssen Sie jedoch die Option [clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) aktivieren. Verwenden Sie dazu [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
> [!NOTE]  
>  CLR-Prozeduren werden in einer enthaltenen Datenbank nicht unterstützt.  
  
ATOMIC WITH  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt die unteilbare Ausführung der gespeicherten Prozedur an. Änderungen werden entweder über ein Commit ausgeführt, oder ein Rollback aller Änderungen wird durch eine Ausnahme auslöst. Der ATOMIC WITH-Block ist für systemintern kompilierte gespeicherte Prozeduren erforderlich.  
  
 Wenn die Prozedur ein RETURN zurückgibt (explizit durch die RETURN-Anweisung oder implizit durch eine Ausführung), wird für von der Prozedur durchgeführte Arbeiten ein Commit ausgeführt. Wenn die Prozedur ein THROW zurückgibt, wird für von der Prozedur durchgeführte Arbeiten ein Rollback ausgeführt.  
  
 XACT_ABORT ist standardmäßig innerhalb eines ATOMIC-Blocks aktiviert und kann nicht geändert werden. XACT_ABORT gibt an, ob [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für die aktuelle Transaktion automatisch ein Rollback ausführt, wenn eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung einen Laufzeitfehler ausgibt.  
  
 Die folgenden SET-Optionen sind im ATOMIC-Block immer aktiviert; die Optionen können nicht geändert werden.  
-   CONCAT_NULL_YIELDS_NULL  
-   QUOTED_IDENTIFIER, ARITHABORT  
-   NOCOUNT  
-   ANSI_NULLS  
-   ANSI_WARNINGS  
  
SET-Optionen können innerhalb von ATOMIC-Blöcken nicht geändert werden. Die SET-Optionen in der Benutzersitzung werden nicht im Kontext der systemintern kompilierten gespeicherten Prozeduren verwendet. Diese Optionen werden zur Kompilierzeit korrigiert.  
  
BEGIN-, ROLLBACK- und COMMIT-Vorgänge können nicht innerhalb eines ATOMIC-Blocks verwendet werden.  
  
 Es gibt einen ATOMIC-Block für jede systemintern kompilierte gespeicherte Prozedur im äußeren Bereich der Prozedur. Die Blöcke können nicht geschachtelt werden. Weitere Informationen zu nativ kompilierten gespeicherten Prozeduren finden Sie unter [Nativ kompilierte gespeicherte Prozeduren](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
**NULL** | NOT NULL  
 Bestimmt, ob NULL-Werte in einem Parameter zulässig sind. NULL ist die Standardeinstellung.  
  
NATIVE_COMPILATION  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Gibt an, dass die Prozedur systemintern kompiliert wird. NATIVE_COMPILATION, SCHEMABINDING und EXECUTE AS können in beliebiger Reihenfolge angegeben werden. Weitere Informationen finden Sie unter [Nativ kompilierte gespeicherte Prozeduren](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
SCHEMABINDING  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Stellt sicher, dass Tabellen, auf die eine Prozedur verweist, nicht gelöscht oder geändert werden können. SCHEMABINDING ist in systemintern kompilierten gespeicherten Prozeduren erforderlich. Weitere Informationen finden Sie unter [Nativ kompilierte gespeicherte Prozeduren](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md). Es gelten dieselben SCHEMABINDING-Einschränkungen wie für benutzerdefinierte Funktionen. Weitere Informationen finden Sie im Abschnitt SCHEMABINDING in [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md).  
  
LANGUAGE = [N] 'language'  
 **Gilt für:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Entspricht der Sitzungsoption [SET LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/statements/set-language-transact-sql.md). LANGUAGE = [N] 'Sprache' ist erforderlich.  
  
TRANSACTION ISOLATION LEVEL  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Erforderlich für systemintern kompilierte gespeicherte Prozeduren. Gibt die Transaktionsisolationsstufe für die gespeicherte Prozedur an. Folgende Optionen stehen zur Verfügung:  
  
 Weitere Informationen zu diesen Optionen finden Sie unter [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
REPEATABLE READ  
 Gibt an, dass Anweisungen Daten nicht lesen können, die von anderen Transaktionen geändert wurden, für die jedoch noch kein Commit ausgeführt wurde. Wenn eine andere Transaktion Daten modifiziert, die von der aktuellen Transaktion gelesen wurden, schlägt die aktuelle Transaktion fehl.  
  
SERIALIZABLE  
 Gibt Folgendes an:  
-   Anweisungen können keine Daten lesen, die geändert wurden, für die jedoch noch kein Commit von anderen Transaktionen ausgeführt wurde.  
-   Wenn andere Transaktionen Daten modifizieren, die von der aktuellen Transaktion gelesen wurden, schlägt die aktuelle Transaktion fehl.  
-   Wenn eine andere Transaktion neue Zeilen mit Schlüsselwerten einfügt, die in den von Anweisungen in der aktuellen Transaktion gelesenen Schlüsselbereich fallen, schlägt die aktuelle Transaktion fehl.  
  
SNAPSHOT  
 Gibt an, dass von Anweisungen in einer Transaktion gelesene Daten der im Hinblick auf Transaktionen konsistenten Version der Daten entsprechen, die zu Beginn der Transaktion vorhanden waren.  
  
DATEFIRST = *number*  
 **Gilt für:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Legt den ersten Wochentag auf eine Zahl von 1 bis 7 fest. DATEFIRST ist optional. Wenn dies nicht angegeben ist, wird die Einstellung von der angegebenen Sprache abgeleitet.  
  
 Weitere Informationen finden Sie unter [SET DATEFIRST &#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md).  
  
DATEFORMAT = *format*  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Legt die Reihenfolge der Datumsteile für den Tag, den Monat und das Jahr fest, um die date-, smalldatetime-, datetime-, datetime2- und datetimeoffset-Zeichenfolgen zu interpretieren. DATEFORMAT ist optional. Wenn dies nicht angegeben ist, wird die Einstellung von der angegebenen Sprache abgeleitet.  
  
 Weitere Informationen finden Sie unter [SET DATEFORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md).  
  
DELAYED_DURABILITY = { OFF | ON }  
 **Gilt für**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] und [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Transaktionscommits können entweder vollständig dauerhaft (Standardeinstellung) oder verzögert dauerhaft sein.  
  
 Weitere Informationen finden Sie im Thema [Steuern der Transaktionsdauerhaftigkeit](../../relational-databases/logs/control-transaction-durability.md).  

## <a name="Simple"></a> Einfache Beispiele

Hier finden Sie zwei Beispiele, die Ihnen den Einstieg erleichtern:  
`SELECT DB_NAME() AS ThisDB;` gibt den Namen der aktuellen Datenbank zurück.  
Sie können diese Anweisung mit einer gespeicherten Prozedur umschließen wie z.B.:  
```sql  
CREATE PROC What_DB_is_this     
AS   
SELECT DB_NAME() AS ThisDB; 
```   
Diese gespeicherte Prozedur lässt sich mit der Anweisung `EXEC What_DB_is_this;` aufrufen.   

Sie ist etwas komplexer und dient dazu, einen Eingabeparameter bereitzustellen, um die Prozedur flexibler zu gestalten. Zum Beispiel:  
```sql   
CREATE PROC What_DB_is_that @ID int   
AS    
SELECT DB_NAME(@ID) AS ThatDB;   
```   
Geben Sie eine Datenbank-ID an, wenn Sie die Prozedur aufrufen. `EXEC What_DB_is_that 2;` gibt beispielsweise `tempdb` zurück.   

Weitere Beispiele finden Sie unter [Beispiele](#Examples) am Ende dieses Themas.     
    
## <a name="best-practices"></a>Bewährte Methoden  
 Im Folgenden werden zwar nicht alle bewährten Methoden aufgeführt, trotzdem können diese Vorschläge zur Verbesserung der Leistung beitragen.  
  
-   Verwenden Sie die SET NOCOUNT ON-Anweisung als erste Anweisung im Textkörper der Prozedur. Setzen Sie sie also direkt hinter das AS-Schlüsselwort. Hierdurch wird das Zurücksenden von Meldungen nach der Ausführung von SELECT-, INSERT-, UPDATE-, MERGE- und DELETE-Anweisungen durch [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] an den Client deaktiviert. Die Gesamtleistung der Datenbank und der Anwendung wird durch Vermeiden dieses unnötigen Netzwerkverarbeitungsaufwands verbessert. Weitere Informationen finden Sie unter [SET NOCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-nocount-transact-sql.md).  
  
-   Verwenden Sie beim Erstellen oder Verweisen auf Datenbankobjekte in der Prozedur Schemanamen. Die [!INCLUDE[ssDE](../../includes/ssde-md.md)] kann Objektnamen schneller auflösen, wenn nicht mehrere Schemas durchsucht werden müssen. Zudem werden Probleme hinsichtlich Berechtigung und Zugriff vermieden, die durch das Zuweisen eines Standardschemas eines Benutzers hervorgerufen werden, wenn Objekte ohne Angabe des Schemas erstellt werden.  
  
-   Verwenden Sie keine Wrapperfunktionen für Spalten, die in den WHERE- und JOIN-Klauseln angegeben sind. Hierdurch werden die Spalten nicht deterministisch, und der Abfrageprozessor kann keine Indizes verwenden.  
  
-   Vermeiden Sie das Verwenden skalarer Funktionen in SELECT-Anweisungen, die viele Datenzeilen zurückgeben. Da die skalare Funktion auf jede Zeile angewendet werden muss, entspricht das resultierende Verhalten zeilenbasierter Verarbeitung, und Leistungseinbußen treten auf.  
  
-   Vermeiden Sie die Verwendung von `SELECT *`. Geben Sie stattdessen die erforderlichen Spaltennamen an. Hierdurch können einige [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Fehler vermieden werden, die die Prozedurausführung beenden. Beispiel: Eine `SELECT *`-Anweisung, die Daten aus einer Tabelle mit 12 Spalten zurückgibt und anschließend die Daten in eine temporäre Tabelle mit 12 Spalten einfügt, wird nur so lange erfolgreich ausgeführt, bis die Anzahl oder die Reihenfolge der Spalten in einer der Tabellen geändert wird.  
  
-   Vermeiden Sie das Verarbeiten oder Zurückgeben übermäßig vieler Daten. Schränken Sie die Ergebnisse im Prozedurencode möglichst früh ein, damit alle nachfolgenden von der Prozedur durchgeführten Vorgänge mit dem kleinstmöglichen Dataset durchgeführt werden können. Senden Sie nur die notwendigen Daten an die Clientanwendung. Dies ist effizienter als das Senden zusätzlicher Daten im Netzwerk, wodurch die Clientanwendung unnötig große Resultsets verarbeiten muss.  
  
-   Verwenden Sie explizite Transaktionen durch Verwenden von BEGIN/COMMIT TRANSACTION, und halten Sie Transaktionen möglichst kurz. Längere Transaktionen führen dazu, dass Datensätze länger gesperrt sind und die Wahrscheinlichkeit von Deadlocks steigt.  
  
-   Verwenden Sie die [!INCLUDE[tsql](../../includes/tsql-md.md)] TRY…CATCH-Funktion zur Fehlerbehandlung innerhalb einer Prozedur. TRY…CATCH kann einen gesamten Block von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen kapseln. Hierdurch wird nicht nur weniger Verarbeitungsaufwand verursacht, sondern auch die Genauigkeit der Fehlerberichterstattung verbessert und der Programmierungsaufwand verringert.  
  
-   Verwenden Sie das DEFAULT-Schlüsselwort für alle Tabellenspalten, auf die durch CREATE TABLE- oder ALTER TABLE-[!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen im Textkörper der Prozedur verwiesen wird. Hierdurch wird NULL nicht an Spalten übergeben, von denen keine NULL-Werte zugelassen werden.  
  
-   Verwenden Sie für alle Spalten in einer temporären Tabelle NULL oder NOT NULL. Die Optionen ANSI_DFLT_ON und ANSI_DFLT_OFF steuern, wie [!INCLUDE[ssDE](../../includes/ssde-md.md)] den Spalten die Attribute NULL oder NOT NULL zuweist, wenn diese Attribute nicht in einer CREATE TABLE- oder ALTER TABLE-Anweisung angegeben sind. Wenn eine Verbindung eine Prozedur ausführt und für diese Optionen andere Einstellungen verwendet als die Verbindung, die die Prozedur erstellt hat, weisen die Spalten der für die zweite Verbindung erstellten Tabelle möglicherweise eine andere NULL-Zulässigkeit und ein anderes Verhalten auf. Wenn NULL oder NOT NULL explizit für jede Spalte angegeben ist, werden die temporären Tabellen für alle Verbindungen, die die Prozedur ausführen, mit derselben NULL-Zulässigkeit erstellt.  
  
-   Verwenden Sie Änderungsanweisungen, die NULL-Werte umwandeln, und schließen Sie Logik ein, von der Zeilen mit NULL-Werten aus Abfragen gelöscht werden. Beachten Sie, dass in [!INCLUDE[tsql](../../includes/tsql-md.md)] NULL keine leerer oder „Nichts“-Wert ist. Es handelt sich um einen Platzhalter für einen unbekannten Wert, weshalb unerwartetes Verhalten auftreten kann, besonders beim Abfragen von Resultsets oder Verwenden von AGGREGATE-Funktionen.  
  
-   Verwenden Sie den UNION ALL-Operator anstelle des UNION- oder OR-Operators, sofern nicht unbedingt unterschiedliche Werte erforderlich sind. Der UNION ALL-Operator erfordert weniger Verarbeitungsaufwand, da aus dem Resultset keine Duplikate herausgefiltert werden.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Für eine Prozedur gilt keine vordefinierte maximale Größe.  
  
 Innerhalb der Prozedur angegebene Variablen können benutzerdefinierte Variablen oder Systemvariablen (z.B. @@SPID) sein.  
  
 Wenn eine Prozedur zum ersten Mal ausgeführt wird, wird sie kompiliert, um einen optimalen Zugriffsplan für den Datenabruf zu bestimmen. Nachfolgende Ausführungen der Prozedur können den bereits generierten Plan erneut verwenden, wenn dieser weiterhin im Plancache des [!INCLUDE[ssDE](../../includes/ssde-md.md)]s vorhanden ist.  
  
 Mindestens eine Prozedur kann beim Start von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] automatisch ausgeführt werden. Die Prozeduren müssen vom Systemadministrator in der **Masterdatenbank** erstellt und unter der festen Serverrolle **sysadmin** als Hintergrundprozess ausgeführt werden. Die Prozeduren dürfen keine Eingabe- oder Ausgabeparameter besitzen. Weitere Informationen finden Sie unter [Ausführen einer gespeicherten Prozedur](../../relational-databases/stored-procedures/execute-a-stored-procedure.md).  
  
 Prozeduren sind geschachtelt, wenn eine Prozedur eine andere Prozedur aufruft oder verwalteten Code durch Verweisen auf eine CLR-Routine, einen -Typ oder ein -Aggregat ausführt. Sie können Prozeduren und Verweise auf verwalteten Code bis auf 32 Ebenen tief schachteln. Die Schachtelungsebene wird um eine Ebene erhöht, wenn die aufgerufene Prozedur oder der Verweis auf verwalteten Code die Ausführung beginnt, und um eine Ebene verringert, wenn die aufgerufene Prozedur oder der Verweis auf verwalteten Code die Ausführung beendet. Methoden, die innerhalb des verwalteten Codes aufgerufen wurden, werden nicht auf diese Grenze für Schachtelungsebenen angerechnet. Wenn jedoch eine gespeicherte CLR-Prozedur Datenzugriffsvorgänge über den von SQL Server verwalteten Anbieter ausführt, werden beim Übergang von verwaltetem Code zu SQL zusätzliche Schachtelungsebenen hinzugefügt.  
  
 Der Versuch, die Anzahl der maximalen Schachtelungsebenen zu überschreiten, führt dazu, dass die gesamte Aufrufkette fehlschlägt. Sie können die @@NESTLEVEL-Funktion verwenden, um die Schachtelungsebene für die zurzeit ausgeführte gespeicherte Prozedur zu speichern.  
  
## <a name="interoperability"></a>Interoperabilität  
 Das [!INCLUDE[ssDE](../../includes/ssde-md.md)] speichert die Einstellungen sowohl für SET QUOTED_IDENTIFIER als auch für SET ANSI_NULLS, wenn eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur erstellt oder geändert wird. Diese Originaleinstellungen werden verwendet, wenn die ausgeführt wird. Deshalb werden alle Clientsitzungseinstellungen für SET QUOTED_IDENTIFIER und SET ANSI_NULLS während der Ausführung der Prozedur ignoriert.  
  
 Andere SET-Optionen, wie z. B. SET ARITHABORT, SET ANSI_WARNINGS oder SET ANSI_PADDINGS, werden nicht gespeichert, wenn eine Prozedur erstellt oder geändert wird. Wenn die Logik der Prozedur von einer bestimmten Einstellung abhängig ist, schließen Sie eine SET-Anweisung am Anfang der Prozedur ein, um die richtige Einstellung sicherzustellen. Wenn eine SET-Anweisung aus einer Prozedur heraus ausgeführt wird, bleibt die betreffende Einstellung nur so lange in Kraft, bis die Ausführung der Prozedur abgeschlossen ist. Die Einstellung wird dann mit dem Wert wiederhergestellt, den sie hatte, als die Prozedur aufgerufen wurde. Dies gibt einzelnen Clients die Möglichkeit, die gewünschten Optionen festzulegen, ohne die Logik der Prozedur zu beeinflussen.  
  
 Beliebige SET-Anweisungen können in einer Prozedur angegeben werden, mit Ausnahme von SET SHOWPLAN_TEXT und SET SHOWPLAN_ALL. Diese müssen die einzigen Anweisungen im Batch sein. Die ausgewählte SET-Option bleibt während der Ausführung der Prozedur in Kraft und wird dann auf die vorherige Einstellung zurückgesetzt.  
  
> [!NOTE]  
>  SET ANSI_WARNINGS wird beim Übergeben von Parametern in einer Prozedur oder einer benutzerdefinierten Funktion oder beim Deklarieren und Festlegen von Variablen in einer Batchanweisung nicht berücksichtigt. Wird beispielsweise eine Variable als **char(3)** definiert und dann auf einen Wert festgelegt, der länger als drei Zeichen ist, werden die Daten auf die definierte Größe abgeschnitten, und die Anweisung INSERT oder UPDATE wird erfolgreich ausgeführt.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Die CREATE PROCEDURE-Anweisung kann nicht mit anderen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen in einem einzelnen Batch kombiniert werden.  
  
 Folgende Anweisungen können nicht an einer beliebigen Stelle im Textkörper einer gespeicherten Prozedur verwendet werden.  
  
||||  
|-|-|-|  
|CREATE AGGREGATE|CREATE SCHEMA|SET SHOWPLAN_TEXT|  
|CREATE DEFAULT|CREATE oder ALTER TRIGGER|Mit SET SHOWPLAN_XML|  
|CREATE oder ALTER FUNCTION|CREATE oder ALTER VIEW|USE *Name der Datenbank*|  
|CREATE oder ALTER PROCEDURE|SET PARSEONLY||  
|CREATE RULE|SET SHOWPLAN_ALL||  
  
 Eine Prozedur kann auf noch nicht vorhandene Tabellen verweisen. Zum Zeitpunkt der Erstellung wird nur die Syntaxüberprüfung ausgeführt. Die Prozedur wird erst dann kompiliert, wenn sie zum ersten Mal ausgeführt wird. Erst während des Kompilierens werden alle Objekte aufgelöst, auf die in der Prozedur verwiesen wird. Daher kann eine syntaktisch richtige Prozedur, die auf noch nicht vorhandene Tabellen verweist, erfolgreich erstellt werden. Die Prozedur schlägt jedoch zur Ausführungszeit fehl, wenn die Tabellen, auf die verwiesen wird, nicht vorhanden sind.  
  
 Sie können einen Funktionsnamen nicht als Parameterstandardwert oder den Wert angeben, der beim Ausführen einer Prozedur an einen Parameter weitergegeben wird. Sie können eine Funktion aber auch wie im folgenden Beispiel gezeigt als Variable übergeben.  
  
```sql
-- Passing the function value as a variable.  
DECLARE @CheckDate datetime = GETDATE();  
EXEC dbo.uspGetWhereUsedProductID 819, @CheckDate;   
GO  
```  
  
 Wenn die Prozedur Änderungen an einer Remoteinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vornimmt, kann für diese Änderungen kein Rollback ausgeführt werden. Remoteprozeduren nehmen nicht an Transaktionen teil.  
  
 Die in der EXTERNAL NAME-Klausel angegebene Methode muss die folgenden Merkmale aufweisen, damit das [!INCLUDE[ssDE](../../includes/ssde-md.md)] auf die richtige Methode verweisen kann, wenn sie in .NET Framework überladen wird.  
  
-   Sie muss als statische Methode deklariert sein.  
  
-   Sie muss dieselbe Anzahl von Parametern erhalten, wie in der Prozedur enthalten sind.  
  
-   Sie muss Parametertypen verwenden, die mit den Datentypen der jeweiligen Parameter der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozedur kompatibel sind. Weitere Informationen zur Übereinstimmung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentypen mit [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Datentypen finden Sie unter [Zuordnen von CLR-Parameterdaten](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).  
  
## <a name="metadata"></a>Metadaten  
 In der folgenden Tabelle sind die Katalogsichten und dynamischen Verwaltungssichten aufgeführt, die Sie verwenden können, um Informationen zu gespeicherten Prozeduren zurückzugeben.  
  
|Anzeigen|Description|  
|----------|-----------------|  
|[sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)|Gibt die Definition einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Prozedur zurück. Der Text einer mit der ENCRYPTION-Option erstellten Prozedur kann nicht mit der **sys.sql_modules**-Katalogsicht angezeigt werden.|  
|[sys.assembly_modules](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)|Gibt Informationen zu einer CLR-Prozedur zurück.|  
|[sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)|Gibt Informationen über die Parameter zurück, die in einer Prozedur definiert sind.|  
|[sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) [sys.dm_sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md) [sys.dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)|Gibt die Objekte zurück, auf die eine Prozedur verweist.|  
  
 Verwenden Sie die folgenden Leistungsindikatoren, um die Größe einer kompilierten Prozedur zu schätzen.  
  
|Name des Systemmonitorobjekts|Indikatorname des Systemmonitors|  
|-------------------------------------|--------------------------------------|  
|SQL Server: Plancache-Objekt|Cachetrefferquote|  
||Cacheseiten|  
||Cacheobjektzähler*|  
  
 * Diese Indikatoren sind für verschiedene Kategorien von Cacheobjekten verfügbar, einschließlich Ad-hoc-[!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, vorbereiteten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, Prozeduren, Triggern usw. Weitere Informationen finden Sie unter [SQL Server, Plancache-Objekt](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md).  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die **CREATE PROCEDURE**-Berechtigung für die Datenbank und die **ALTER**-Berechtigung für das Schema, in dem die Prozedur erstellt wird, oder die Mitgliedschaft in der festen Datenbankrolle **db_ddladmin**.  
  
 Bei gespeicherten CLR-Prozeduren müssen Sie der Besitzer der Assembly sein, auf die in der EXTERNAL NAME-Klausel verwiesen wird, oder über die **REFERENCES**-Berechtigung für diese Assembly verfügen.  
  
##  <a name="mot"></a> CREATE PROCEDURE und speicheroptimierte Tabellen  
 Auf speicheroptimierte Tabellen kann am effizientesten über traditionell und nativ kompilierte gespeicherte Prozeduren zugegriffen werden. Native Prozeduren sind in den meisten Fällen die effizientere Methode.
Weitere Informationen finden Sie unter [Nativ kompilierte gespeicherte Prozeduren](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
 Im folgenden Beispiel wird dargestellt, wie eine nativ kompilierte gespeicherte Prozedur erstellt wird, die auf die speicheroptimierte Tabelle `dbo.Departments` zugreift:  
  
```sql  
CREATE PROCEDURE dbo.usp_add_kitchen @dept_id int, @kitchen_count int NOT NULL  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
AS  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  
  UPDATE dbo.Departments  
  SET kitchen_count = ISNULL(kitchen_count, 0) + @kitchen_count  
  WHERE id = @dept_id  
END;  
GO  
```  
  
 Eine Prozedur, die ohne NATIVE_COMPILATION erstellt wurde, kann nicht in eine systemintern kompilierte gespeicherten Prozedur geändert werden. 
  
 Eine Besprechung der Programmierbarkeit von nativ kompilierten gespeicherten Prozeduren, dem unterstützten Abfragenoberflächenbereich und der Operatoren finden Sie unter [Unterstützte Features für nativ kompilierte T-SQL-Module](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).  
  
## <a name="Examples"></a> Beispiele  
  
|Kategorie|Funktionssyntaxelemente|  
|--------------|------------------------------|  
|[Grundlegende Syntax](#BasicSyntax)|CREATE PROCEDURE|  
|[Übergeben von Parametern](#Parameters)|@parameter <br> &nbsp;&nbsp;  • = default <br> &nbsp;&nbsp; • OUTPUT <br> &nbsp;&nbsp; • Tabellenwertparameter-Typ <br> &nbsp;&nbsp; • CURSOR VARYING|  
|[Ändern von Daten mithilfe einer gespeicherten Prozedur](#Modify)|UPDATE|  
|[Fehlerbehandlung](#Error)|TRY…CATCH|  
|[Verbergen der Prozedurdefinition](#Encrypt)|WITH ENCRYPTION|  
|[Erzwingen der erneuten Kompilierung der Prozedur](#Recompile)|WITH RECOMPILE|  
|[Festlegen des Sicherheitskontexts](#Security)|EXECUTE AS|  
  
###  <a name="BasicSyntax"></a> Grundlegende Syntax  
 Anhand von Beispielen in diesem Abschnitt wird die grundlegende Funktion der CREATE PROCEDURE-Anweisung mithilfe der mindestens erforderlichen Syntax veranschaulicht.  
  
#### <a name="a-creating-a-simple-transact-sql-procedure"></a>A. Erstellen einer einfachen Transact-SQL-Prozedur  
 Im folgenden Beispiel wird eine gespeicherte Prozedur erstellt, die alle Mitarbeiter (mit Vor- und Nachnamen), ihre Titel und ihre Abteilungsnamen aus einer Sicht in der [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]-Datenbank zurückgibt. Diese Prozedur verwendet keine Parameter. Das Beispiel zeigt dann die drei Methoden für das Ausführen der Prozedur.  
  
```sql  
CREATE PROCEDURE HumanResources.uspGetAllEmployees  
AS  
    SET NOCOUNT ON;  
    SELECT LastName, FirstName, JobTitle, Department  
    FROM HumanResources.vEmployeeDepartment;  
GO  
  
SELECT * FROM HumanResources.vEmployeeDepartment;  
```  
  
 Die `uspGetEmployees`-Prozedur kann auf folgende Arten ausgeführt werden:  
  
```sql  
EXECUTE HumanResources.uspGetAllEmployees;  
GO  
-- Or  
EXEC HumanResources.uspGetAllEmployees;  
GO  
-- Or, if this procedure is the first statement within a batch:  
HumanResources.uspGetAllEmployees;  
```  
  
#### <a name="b-returning-more-than-one-result-set"></a>B. Zurückgeben von mehreren Resultsets  
 Die folgende Prozedur gibt zwei Resultsets zurück.  
  
```sql  
CREATE PROCEDURE dbo.uspMultipleResults   
AS  
SELECT TOP(10) BusinessEntityID, Lastname, FirstName FROM Person.Person;  
SELECT TOP(10) CustomerID, AccountNumber FROM Sales.Customer;  
GO  
```  
  
#### <a name="c-creating-a-clr-stored-procedure"></a>C. Erstellen einer gespeicherten CLR-Prozedur  
 Im folgenden Beispiel wird die `GetPhotoFromDB`-Prozedur erstellt, die auf die `GetPhotoFromDB`-Methode der `LargeObjectBinary`-Klasse in der `HandlingLOBUsingCLR`-Assembly verweist. Bevor die Prozedur erstellt wird, wird die `HandlingLOBUsingCLR`-Assembly in der lokalen Datenbank registriert.  
  
**Gilt für:**  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] (wenn eine aus *assembly_bits* erstellte Assembly verwendet wird)  
  
```sql  
CREATE ASSEMBLY HandlingLOBUsingCLR  
FROM '\\MachineName\HandlingLOBUsingCLR\bin\Debug\HandlingLOBUsingCLR.dll';  
GO  
CREATE PROCEDURE dbo.GetPhotoFromDB  
(  
    @ProductPhotoID int,  
    @CurrentDirectory nvarchar(1024),  
    @FileName nvarchar(1024)  
)  
AS EXTERNAL NAME HandlingLOBUsingCLR.LargeObjectBinary.GetPhotoFromDB;  
GO  
```  
  
###  <a name="Parameters"></a> Übergeben von Parametern  
 Die Beispiele in diesem Abschnitt veranschaulichen, wie die Eingabe- und Ausgabeparameter zum Übergeben von Werten von und an eine gespeicherte Prozedur verwendet werden.  
  
#### <a name="d-creating-a-procedure-with-input-parameters"></a>D. Erstellen einer Prozedur mit Eingabeparametern  
 Im folgenden Beispiel wird eine gespeicherte Prozedur erstellt, die Informationen für einen bestimmten Mitarbeiter zurückgibt, indem Werte für den Vor- und Nachnamen des Mitarbeiters übergeben werden. Diese Prozedur akzeptiert nur genaue Übereinstimmungen für die übergebenen Parameter an.  
  
```sql  
IF OBJECT_ID ( 'HumanResources.uspGetEmployees', 'P' ) IS NOT NULL   
    DROP PROCEDURE HumanResources.uspGetEmployees;  
GO  
CREATE PROCEDURE HumanResources.uspGetEmployees   
    @LastName nvarchar(50),   
    @FirstName nvarchar(50)   
AS   
  
    SET NOCOUNT ON;  
    SELECT FirstName, LastName, JobTitle, Department  
    FROM HumanResources.vEmployeeDepartment  
    WHERE FirstName = @FirstName AND LastName = @LastName;  
GO  
  
```  
  
 Die `uspGetEmployees`-Prozedur kann auf folgende Arten ausgeführt werden:  
  
```sql
EXECUTE HumanResources.uspGetEmployees N'Ackerman', N'Pilar';  
-- Or  
EXEC HumanResources.uspGetEmployees @LastName = N'Ackerman', @FirstName = N'Pilar';  
GO  
-- Or  
EXECUTE HumanResources.uspGetEmployees @FirstName = N'Pilar', @LastName = N'Ackerman';  
GO  
-- Or, if this procedure is the first statement within a batch:  
HumanResources.uspGetEmployees N'Ackerman', N'Pilar';  
  
```  
  
#### <a name="e-using-a-procedure-with-wildcard-parameters"></a>E. Verwenden einer Prozedur mit Platzhalterparametern  
 Im folgenden Beispiel wird eine gespeicherte Prozedur erstellt, die Informationen für Mitarbeiter zurückgibt, indem vollständige oder Teilwerte für den Vor- und Nachnamen des Mitarbeiters übergeben werden. Diese Prozedur führt mit den übergebenen Parametern einen Mustervergleich aus oder verwendet die voreingestellten Standardwerte (Nachnamen, die mit dem Buchstaben `D` beginnen), wenn keine Parameter bereitgestellt sind.  
  
```sql  
IF OBJECT_ID ( 'HumanResources.uspGetEmployees2', 'P' ) IS NOT NULL   
    DROP PROCEDURE HumanResources.uspGetEmployees2;  
GO  
CREATE PROCEDURE HumanResources.uspGetEmployees2   
    @LastName nvarchar(50) = N'D%',   
    @FirstName nvarchar(50) = N'%'  
AS   
    SET NOCOUNT ON;  
    SELECT FirstName, LastName, JobTitle, Department  
    FROM HumanResources.vEmployeeDepartment  
    WHERE FirstName LIKE @FirstName AND LastName LIKE @LastName;  
```  
  
 Die `uspGetEmployees2`-Prozedur kann in verschiedenen Kombinationen ausgeführt werden. Hier werden nur einige mögliche Kombinationen gezeigt.  
  
```sql  
EXECUTE HumanResources.uspGetEmployees2;  
-- Or  
EXECUTE HumanResources.uspGetEmployees2 N'Wi%';  
-- Or  
EXECUTE HumanResources.uspGetEmployees2 @FirstName = N'%';  
-- Or  
EXECUTE HumanResources.uspGetEmployees2 N'[CK]ars[OE]n';  
-- Or  
EXECUTE HumanResources.uspGetEmployees2 N'Hesse', N'Stefen';  
-- Or  
EXECUTE HumanResources.uspGetEmployees2 N'H%', N'S%';  
```  
  
#### <a name="f-using-output-parameters"></a>F. Verwenden von OUTPUT-Parametern  
 Im folgenden Beispiel wird die `uspGetList`-Prozedur erstellt. Diese Prozedur gibt eine Liste der Produkte zurück, deren Preise einen angegebenen Betrag nicht überschreiten. Das Beispiel zeigt die Verwendung von mehreren `SELECT`- und mehreren `OUTPUT`-Parametern. OUTPUT-Parameter ermöglichen einer externen Prozedur, einem Batch oder mehreren [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen den Zugriff auf einen Satz von Werten während der Ausführung der Prozedur.  
  
```sql  
IF OBJECT_ID ( 'Production.uspGetList', 'P' ) IS NOT NULL   
    DROP PROCEDURE Production.uspGetList;  
GO  
CREATE PROCEDURE Production.uspGetList @Product varchar(40)   
    , @MaxPrice money   
    , @ComparePrice money OUTPUT  
    , @ListPrice money OUT  
AS  
    SET NOCOUNT ON;  
    SELECT p.[Name] AS Product, p.ListPrice AS 'List Price'  
    FROM Production.Product AS p  
    JOIN Production.ProductSubcategory AS s   
      ON p.ProductSubcategoryID = s.ProductSubcategoryID  
    WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice;  
-- Populate the output variable @ListPprice.  
SET @ListPrice = (SELECT MAX(p.ListPrice)  
        FROM Production.Product AS p  
        JOIN  Production.ProductSubcategory AS s   
          ON p.ProductSubcategoryID = s.ProductSubcategoryID  
        WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice);  
-- Populate the output variable @compareprice.  
SET @ComparePrice = @MaxPrice;  
GO  
```  
  
 Führen Sie `uspGetList` aus, um eine Liste der [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]-Produkte (Bikes) zurückzugeben, die weniger als `$700` kosten. Die `OUTPUT`-Parameter `@Cost` und `@ComparePrices` werden mit Sprachkonstrukten zur Ablaufsteuerung verwendet, um eine Meldung an das Fenster **Meldungen** zurückzugeben.  
  
> [!NOTE]  
>  Die OUTPUT-Variable muss definiert sein, wenn die Prozedur erstellt wird, und auch dann, wenn die Variable verwendet wird. Der Parametername und der Variablenname müssen nicht übereinstimmen. Jedoch müssen der Datentyp und die Position des Parameters übereinstimmen, es sei denn, es wird `@ListPrice` = *variable* verwendet.  
  
```sql  
DECLARE @ComparePrice money, @Cost money ;  
EXECUTE Production.uspGetList '%Bikes%', 700,   
    @ComparePrice OUT,   
    @Cost OUTPUT  
IF @Cost <= @ComparePrice   
BEGIN  
    PRINT 'These products can be purchased for less than   
    $'+RTRIM(CAST(@ComparePrice AS varchar(20)))+'.'  
END  
ELSE  
    PRINT 'The prices for all products in this category exceed   
    $'+ RTRIM(CAST(@ComparePrice AS varchar(20)))+'.';  
```  
  
 Im Folgenden wird ein Teil des Resultsets aufgeführt:  
  
 ```   
 Product                     List Price  
 --------------------------  ----------  
 Road-750 Black, 58          539.99  
 Mountain-500 Silver, 40     564.99  
 Mountain-500 Silver, 42     564.99  
 ...  
 Road-750 Black, 48          539.99  
 Road-750 Black, 52          539.99  
   
 (14 row(s) affected)   
  
 These items can be purchased for less than $700.00.
 ```  
  
#### <a name="g-using-a-table-valued-parameter"></a>G. Verwenden eines Tabellenwertparameters  
 Im folgenden Beispiel wird ein Tabellenwertparameter verwendet, um mehrere Zeilen in eine Tabelle einzufügen. Der Parametertyp wird erstellt und eine Tabellenvariable deklariert, die auf ihn verweist. Außerdem werden Daten in die Parameterliste eingefügt und die Werte dann an eine gespeicherte Prozedur übergeben. Die gespeicherte Prozedur verwendet die Werte, um mehrere Zeile in eine Tabelle einzufügen.  
  
```sql  
/* Create a table type. */  
CREATE TYPE LocationTableType AS TABLE   
( LocationName VARCHAR(50)  
, CostRate INT );  
GO  
  
/* Create a procedure to receive data for the table-valued parameter. */  
CREATE PROCEDURE usp_InsertProductionLocation  
    @TVP LocationTableType READONLY  
    AS   
    SET NOCOUNT ON  
    INSERT INTO [AdventureWorks2012].[Production].[Location]  
           ([Name]  
           ,[CostRate]  
           ,[Availability]  
           ,[ModifiedDate])  
        SELECT *, 0, GETDATE()  
        FROM  @TVP;  
GO  
  
/* Declare a variable that references the type. */  
DECLARE @LocationTVP   
AS LocationTableType;  
  
/* Add data to the table variable. */  
INSERT INTO @LocationTVP (LocationName, CostRate)  
    SELECT [Name], 0.00  
    FROM   
    [AdventureWorks2012].[Person].[StateProvince];  
  
/* Pass the table variable data to a stored procedure. */  
EXEC usp_InsertProductionLocation @LocationTVP;  
GO  
```  
  
##### <a name="h-using-an-output-cursor-parameter"></a>H. Verwenden eines OUTPUT-Cursorparameters  
 Im folgenden Beispiel wird der OUTPUT-Cursorparameter verwendet, um einen Cursor aus einer Prozedur an den aufrufenden Batch, die aufrufende Prozedur oder den aufrufenden Trigger zurückzugeben.  
  
 Zuerst wird die Prozedur erstellt, die einen Cursor für die `Currency`-Tabelle deklariert und dann öffnet:  
  
```sql  
CREATE PROCEDURE dbo.uspCurrencyCursor   
    @CurrencyCursor CURSOR VARYING OUTPUT  
AS  
    SET NOCOUNT ON;  
    SET @CurrencyCursor = CURSOR  
    FORWARD_ONLY STATIC FOR  
      SELECT CurrencyCode, Name  
      FROM Sales.Currency;  
    OPEN @CurrencyCursor;  
GO  
```  
  
 Als Nächstes wird ein Batch ausgeführt, der eine lokale Cursorvariable deklariert. Dann wird die Prozedur ausgeführt, um der lokalen Variablen den Cursor zuzuordnen, und zuletzt werden die Zeilen aus dem Cursor abgerufen.  
  
```sql  
DECLARE @MyCursor CURSOR;  
EXEC dbo.uspCurrencyCursor @CurrencyCursor = @MyCursor OUTPUT;  
WHILE (@@FETCH_STATUS = 0)  
BEGIN;  
     FETCH NEXT FROM @MyCursor;  
END;  
CLOSE @MyCursor;  
DEALLOCATE @MyCursor;  
GO  
```  
  
###  <a name="Modify"></a> Ändern von Daten mithilfe einer gespeicherten Prozedur  
 In den Beispielen in diesem Abschnitt wird gezeigt, wie Daten in Tabellen oder Sichten eingefügt oder geändert werden, indem eine DML-Anweisung (Data Manipulation Language, Datenbearbeitungssprache) in die Definition der Prozedur eingeschlossen wird.  
  
#### <a name="i-using-update-in-a-stored-procedure"></a>I. Verwenden von UPDATE in einer gespeicherten Prozedur  
 Im folgenden Beispiel wird eine UPDATE-Anweisung in einer gespeicherten Prozedur verwendet. Die Prozedur erfordert den Eingabeparameter `@NewHours` und den Ausgabeparameter `@RowCount`. Der `@NewHours`-Parameterwert wird in der UPDATE-Anweisung verwendet, um die Spalte `VacationHours` in der Tabelle `HumanResources.Employee` zu aktualisieren. Der Ausgabeparameter `@RowCount` wird verwendet, um die Anzahl betroffener Zeilen an eine lokale Variable zurückzugeben. Ein CASE-Ausdruck wird in der SET-Klausel verwendet, um den Wert, der für `VacationHours` festgelegt wird, bedingt zu bestimmen. Wenn der Mitarbeiter pro Stunde bezahlt wird (`SalariedFlag` = 0), ist `VacationHours` auf die aktuelle Anzahl der Stunden zuzüglich des Werts festgelegt, der unter `@NewHours` angegeben ist. Andernfalls ist `VacationHours` auf den Wert festgelegt, der unter `@NewHours` angegeben ist.  
  
```sql  
CREATE PROCEDURE HumanResources.Update_VacationHours  
@NewHours smallint  
AS   
SET NOCOUNT ON;  
UPDATE HumanResources.Employee  
SET VacationHours =   
    ( CASE  
         WHEN SalariedFlag = 0 THEN VacationHours + @NewHours  
         ELSE @NewHours  
       END  
    )  
WHERE CurrentFlag = 1;  
GO  
  
EXEC HumanResources.Update_VacationHours 40;  
```  
  
###  <a name="Error"></a> Fehlerbehandlung  
 Die Beispiele in diesem Abschnitt veranschaulichen Methoden zur Behandlung von Fehlern, die bei der Ausführung der gespeicherten Prozedur auftreten können.  
  
#### <a name="j-using-trycatch"></a>J. Verwenden von TRY…CATCH  
 Im folgenden Beispiel wird das TRY…CATCH-Konstrukt verwendet, um Fehlerinformationen zurückzugeben, die während der Ausführung einer gespeicherten Prozedur erfasst wurden.  
  
```sql  
CREATE PROCEDURE Production.uspDeleteWorkOrder ( @WorkOrderID int )  
AS  
SET NOCOUNT ON;  
BEGIN TRY  
   BEGIN TRANSACTION   
   -- Delete rows from the child table, WorkOrderRouting, for the specified work order.  
   DELETE FROM Production.WorkOrderRouting  
   WHERE WorkOrderID = @WorkOrderID;  
  
   -- Delete the rows from the parent table, WorkOrder, for the specified work order.  
   DELETE FROM Production.WorkOrder  
   WHERE WorkOrderID = @WorkOrderID;  
  
   COMMIT  
  
END TRY  
BEGIN CATCH  
  -- Determine if an error occurred.  
  IF @@TRANCOUNT > 0  
     ROLLBACK  
  
  -- Return the error information.  
  DECLARE @ErrorMessage nvarchar(4000),  @ErrorSeverity int;  
  SELECT @ErrorMessage = ERROR_MESSAGE(),@ErrorSeverity = ERROR_SEVERITY();  
  RAISERROR(@ErrorMessage, @ErrorSeverity, 1);  
END CATCH;  
  
GO  
EXEC Production.uspDeleteWorkOrder 13;  
  
/* Intentionally generate an error by reversing the order in which rows 
   are deleted from the parent and child tables. This change does not 
   cause an error when the procedure definition is altered, but produces 
   an error when the procedure is executed.  
*/  
ALTER PROCEDURE Production.uspDeleteWorkOrder ( @WorkOrderID int )  
AS  
  
BEGIN TRY  
   BEGIN TRANSACTION   
      -- Delete the rows from the parent table, WorkOrder, for the specified work order.  
   DELETE FROM Production.WorkOrder  
   WHERE WorkOrderID = @WorkOrderID;  
  
   -- Delete rows from the child table, WorkOrderRouting, for the specified work order.  
   DELETE FROM Production.WorkOrderRouting  
   WHERE WorkOrderID = @WorkOrderID;  
  
   COMMIT TRANSACTION  
  
END TRY  
BEGIN CATCH  
  -- Determine if an error occurred.  
  IF @@TRANCOUNT > 0  
     ROLLBACK TRANSACTION  
  
  -- Return the error information.  
  DECLARE @ErrorMessage nvarchar(4000),  @ErrorSeverity int;  
  SELECT @ErrorMessage = ERROR_MESSAGE(),@ErrorSeverity = ERROR_SEVERITY();  
  RAISERROR(@ErrorMessage, @ErrorSeverity, 1);  
END CATCH;  
GO  
-- Execute the altered procedure.  
EXEC Production.uspDeleteWorkOrder 15;  
  
DROP PROCEDURE Production.uspDeleteWorkOrder;  
```  
  
###  <a name="Encrypt"></a> Verbergen der Prozedurdefinition  
 In den Beispielen dieses Abschnitts wird gezeigt, wie die Definition der gespeicherten Prozedur verborgen wird.  
  
#### <a name="k-using-the-with-encryption-option"></a>K. Verwenden der WITH ENCRYPTION-Option  
 Im folgenden Beispiel wird die `HumanResources.uspEncryptThis`-Prozedur erstellt.  
  
**Gilt für:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], SQL Databse.  
  
```sql  
CREATE PROCEDURE HumanResources.uspEncryptThis  
WITH ENCRYPTION  
AS  
    SET NOCOUNT ON;  
    SELECT BusinessEntityID, JobTitle, NationalIDNumber, 
        VacationHours, SickLeaveHours   
    FROM HumanResources.Employee;  
GO  
```  
  
 Die Option `WITH ENCRYPTION` verbirgt die Definition der Prozedur bei Abfragen des Systemkatalogs oder bei Verwenden von Metadatenfunktionen, wie in den folgenden Beispielen gezeigt wird.  
  
 Führen Sie `sp_helptext` aus:  
  
```sql  
EXEC sp_helptext 'HumanResources.uspEncryptThis';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `The text for object 'HumanResources.uspEncryptThis' is encrypted.`  
  
 Fragen Sie die `sys.sql_modules`-Katalogsicht direkt ab:  
  
```sql  
SELECT definition FROM sys.sql_modules  
WHERE object_id = OBJECT_ID('HumanResources.uspEncryptThis');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 definition  
 --------------------------------  
 NULL  
 ```  
  
###  <a name="Recompile"></a> Erzwingen der erneuten Kompilierung der Prozedur  
 In den Beispielen dieses Abschnitts wird die WITH RECOMPILE-Klausel verwendet, um das erneute Kompilieren der Prozedur bei jeder Ausführung zu erzwingen.  
  
#### <a name="l-using-the-with-recompile-option"></a>L. Verwenden der WITH RECOMPILE-Option  
 Die `WITH RECOMPILE`-Klausel ist hilfreich, wenn die für die Prozedur bereitgestellten Parameter nicht typisch sind und wenn ein neuer Ausführungsplan nicht zwischengespeichert oder im Arbeitsspeicher abgelegt werden soll.  
  
```sql  
IF OBJECT_ID ( 'dbo.uspProductByVendor', 'P' ) IS NOT NULL   
    DROP PROCEDURE dbo.uspProductByVendor;  
GO  
CREATE PROCEDURE dbo.uspProductByVendor @Name varchar(30) = '%'  
WITH RECOMPILE  
AS  
    SET NOCOUNT ON;  
    SELECT v.Name AS 'Vendor name', p.Name AS 'Product name'  
    FROM Purchasing.Vendor AS v   
    JOIN Purchasing.ProductVendor AS pv   
      ON v.BusinessEntityID = pv.BusinessEntityID   
    JOIN Production.Product AS p   
      ON pv.ProductID = p.ProductID  
    WHERE v.Name LIKE @Name;  
```  
  
###  <a name="Security"></a> Festlegen des Sicherheitskontexts  
 Die Beispiele dieses Abschnitts verwenden die EXECUTE AS-Klausel zum Festlegen des Sicherheitskontexts, in dem die gespeicherte Prozedur ausgeführt wird.  
  
#### <a name="m-using-the-execute-as-clause"></a>M. Verwenden der EXECUTE AS-Klausel  
 Im folgenden Beispiel wird die Verwendung der [EXECUTE AS](../../t-sql/statements/execute-as-clause-transact-sql.md)-Klausel gezeigt, um den Sicherheitskontext anzugeben, in dem eine Prozedur ausgeführt werden kann. Im Beispiel gibt die Option `CALLER` an, dass die Prozedur im Kontext des Benutzers, der die Prozedur aufruft, ausgeführt werden kann.  
  
```sql  
CREATE PROCEDURE Purchasing.uspVendorAllInfo  
WITH EXECUTE AS CALLER  
AS  
    SET NOCOUNT ON;  
    SELECT v.Name AS Vendor, p.Name AS 'Product name',   
      v.CreditRating AS 'Rating',   
      v.ActiveFlag AS Availability  
    FROM Purchasing.Vendor v   
    INNER JOIN Purchasing.ProductVendor pv  
      ON v.BusinessEntityID = pv.BusinessEntityID   
    INNER JOIN Production.Product p  
      ON pv.ProductID = p.ProductID   
    ORDER BY v.Name ASC;  
GO  
```  
  
#### <a name="n-creating-custom-permission-sets"></a>N. Erstellen benutzerdefinierter Berechtigungssätze  
 Im folgenden Beispiel wird EXECUTE AS verwendet, um benutzerdefinierte Berechtigungen für einen Datenbankvorgang zu erstellen. Einige Vorgänge, z. B. TRUNCATE TABLE, besitzen keine Berechtigungen, die gewährt werden können. Indem Sie die TRUNCATE TABLE-Anweisung in eine gespeicherte Prozedur aufnehmen und festlegen, dass die Prozedur als Benutzer mit der Berechtigung zur Tabellenänderung ausgeführt wird, können Sie die Berechtigungen zum Abschneiden der Tabelle auf alle Benutzer ausdehnen, denen Sie die EXECUTE-Berechtigungen für die Prozedur erteilen.  
  
```sql  
CREATE PROCEDURE dbo.TruncateMyTable  
WITH EXECUTE AS SELF  
AS TRUNCATE TABLE MyDB..MyTable;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
### <a name="o-create-a-stored-procedure-that-runs-a-select-statement"></a>O. Erstellen einer gespeicherten Prozedur, die eine SELECT-Anweisung ausführt  
 In diesem Beispiel wird die grundlegende Syntax zum Erstellen und Ausführen einer Prozedur gezeigt. Beim Ausführen eines Batchs muss CREATE PROCEDURE in der ersten Anweisung enthalten sein. Um beispielsweise die folgende gespeicherte Prozedur in [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] zu erstellen, legen Sie zuerst den Datenbankkontext fest und führen dann die CREATE PROCEDURE-Anweisung aus.  
  
```sql  
-- Uses AdventureWorksDW database  
  
--Run CREATE PROCEDURE as the first statement in a batch.  
CREATE PROCEDURE Get10TopResellers   
AS   
BEGIN  
    SELECT TOP (10) r.ResellerName, r.AnnualSales  
    FROM DimReseller AS r  
    ORDER BY AnnualSales DESC, ResellerName ASC;  
END  
;  
  
--Show 10 Top Resellers  
EXEC Get10TopResellers;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [Control-of-Flow Language &#40;Transact-SQL&#41; (Sprachkonstrukte zur Ablaufsteuerung (Transact-SQL))](~/t-sql/language-elements/control-of-flow.md)   
 [Cursor](../../relational-databases/cursors.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DEKLARIEREN SIE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-procedure-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [Gespeicherte Prozeduren &#40;Datenbankmodul&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)   
 [sp_procoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md)   
 [sp_recompile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)   
 [sys.procedures &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-procedures-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [sys.numbered_procedures &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-numbered-procedures-transact-sql.md)   
 [sys.numbered_procedure_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-numbered-procedure-parameters-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [Erstellen einer gespeicherten Prozedur](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [Verwenden von Tabellenwertparametern &#40;Datenbank-Engine&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)   
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)  
  
  



