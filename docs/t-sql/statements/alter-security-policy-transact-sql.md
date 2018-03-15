---
title: ALTER SECURITY POLICY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_SECURITY_POLICY_TSQL
- ALTER SECURITY POLICY
- ALTER_SECURITY_TSQL
- ALTER SECURITY
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER SECURITY POLICY statement
ms.assetid: a8efc37e-113d-489c-babc-b914fea2c316
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f5ce90660a43e5285735a74a01b560ec210ba3f0
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/02/2018
---
# <a name="alter-security-policy-transact-sql"></a>ALTER SECURITY POLICY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Ändert eine Sicherheitsrichtlinie.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```sql  
ALTER SECURITY POLICY schema_name.security_policy_name   
    (  
        { ADD { FILTER | BLOCK } PREDICATE tvf_schema_name.security_predicate_function_name   
           ( { column_name | arguments } [ , …n ] ) ON table_schema_name.table_name   
           [ <block_dml_operation> ]  }   
        | { ALTER { FILTER | BLOCK } PREDICATE tvf_schema_name.new_security_predicate_function_name   
             ( { column_name | arguments } [ , …n ] ) ON table_schema_name.table_name   
           [ <block_dml_operation> ] }  
        | { DROP { FILTER | BLOCK } PREDICATE ON table_schema_name.table_name }   
        | [ <additional_add_alter_drop_predicate_statements> [ , ...n ] ]  
    )    [ WITH ( STATE = { ON | OFF } ]  
    [ NOT FOR REPLICATION ]  
[;]  
  
<block_dml_operation>  
    [ { AFTER { INSERT | UPDATE } }   
    | { BEFORE { UPDATE | DELETE } } ]  
```  
  
## <a name="arguments"></a>Argumente  
 security_policy_name  
 Der Name der Sicherheitsrichtlinie. Namen von Sicherheitsrichtlinien müssen den Regeln für Bezeichner entsprechen und innerhalb der Datenbank und für jedes Schema eindeutig sein.  
  
 schema_name  
 Der Name des Schemas, zu dem die Sicherheitsrichtlinie gehört. *schema_name* ist aufgrund der Schemabindung erforderlich.  
  
 [ FILTER | BLOCK ]  
 Der Typ des Sicherheitsprädikats für die Funktion, die an die Zieltabelle gebunden wird. FILTER-Prädikate filtern automatisch die Zeilen, die für Lesevorgänge zur Verfügung stehen. BLOCK-Prädikate blockieren explizit Schreibvorgänge, die die Prädikatfunktion verletzen.  
  
 tvf_schema_name.security_predicate_function_name  
 Die Inline-Tabellenwertfunktion, die als Prädikat verwendet wird und bei Abfragen für eine Zieltabelle erzwungen wird. Für einen bestimmten DML-Vorgang für eine bestimmte Tabelle kann höchstens ein Sicherheitsprädikat definiert werden. Die Inline-Tabellenwertfunktion muss mit der SCHEMABINDING-Option erstellt worden sein.  
  
 { column_name | arguments }  
 Der Spaltenname oder Ausdruck, der als Parameter für die Sicherheitsprädikatfunktion verwendet wird. Alle Spalten in der Zieltabelle können als Argumente für die Prädikatfunktion verwendet werden. Ausdrücke, die Literale, vordefinierte Elemente und arithmetische Operatoren enthalten, können verwendet werden.  
  
 *table_schema_name.table_name*  
 Die Zieltabelle, auf die das Sicherheitsprädikat angewendet wird. Mehrere deaktivierte Sicherheitsrichtlinien können sich auf eine einzelne Tabelle für einen DML-Vorgang beziehen. Es kann allerdings immer nur eine Sicherheitsrichtlinie aktiv sein.  
  
 *\<block_dml_operation>*  
 Der DML-Vorgang, auf den das BLOCK-Prädikat angewendet werden soll. AFTER legt fest, dass das Prädikat für die Zeilenwerte ausgewertet werden soll, nachdem der DML-Vorgang (INSERT oder UPDATE) durchgeführt wurde. BEFORE legt fest, dass das Prädikat für die Zeilenwerte ausgewertet werden soll, bevor der DML-Vorgang (UPDATE oder DELETE) durchgeführt wird. Wenn kein Vorgang angegeben ist, gilt das Prädikat für alle Vorgänge.  
  
 Sie können mit ALTER den Vorgang, auf den ein BLOCK-Prädikat angewendet wird, nicht verändern, da dieser Vorgang zur eindeutigen Identifizierung des Prädikats verwendet wird. Stattdessen müssen Sie das Prädikat löschen und für den neuen Vorgang ein neues erstellen.  
  
 WITH ( STATE = { ON | OFF } )  
 Aktiviert oder deaktiviert das Erzwingen der Sicherheitsprädikate der Sicherheitsrichtlinie für die Zieltabellen. Wenn nichts angegeben ist, wird die erstellte Sicherheitsrichtlinie deaktiviert.  
  
 NOT FOR REPLICATION  
 Gibt an, dass die Sicherheitsrichtlinie nicht ausgeführt werden soll, wenn ein Replikations-Agent das Zielobjekt ändert. Weitere Informationen finden Sie unter [Kontrollieren des Verhaltens von Triggern und Einschränkungen während der Synchronisierung &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md).  
  
 table_schema_name.table_name  
 Die Zieltabelle, auf die das Sicherheitsprädikat angewendet wird. Mehrere deaktivierte Sicherheitsrichtlinien können auf eine einzelne Tabelle abzielen, aber zu jedem Zeitpunkt kann nur eine aktiviert werden.  
  
## <a name="remarks"></a>Remarks  
 Die ALTER SECURITY POLICY-Anweisung liegt im Bereich einer Transaktion. Wird ein Rollback für die Transaktion ausgeführt, so wird auch für die Anweisung ein Rollback durchgeführt.  
  
 Wenn Sie Prädikatfunktionen mit speicheroptimierten Tabellen verwenden, müssen die Sicherheitsrichtlinien **SCHEMABINDING** umfassen und den Kompilierungshinweis **WITH NATIVE_COMPILATION** verwenden. Das SCHEMABINDING-Argument kann nicht mit der ALTER-Anweisung geändert werden, da es auf alle Prädikate angewendet wird. Zum Ändern der Schemabindung müssen Sie die Sicherheitsrichtlinie löschen und neu erstellen.  
  
 BLOCK-Prädikate werden ausgewertet, nachdem der entsprechende DML-Vorgang ausgeführt wurde. Aus diesem Grund kann eine READ UNCOMMITTED-Abfrage vorübergehende Werte lesen, für die später ein Rollback ausgeführt wird.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER ANY SECURITY POLICY-Berechtigung.  
  
 Darüber hinaus sind die folgenden Berechtigungen für jedes hinzugefügte Prädikat erforderlich:  
  
-   SELECT- und REFERENCES-Berechtigungen für die Funktion, die als Prädikat verwendet wird.  
-   REFERENCES-Berechtigung für die Zieltabelle, die an die Richtlinie gebunden wird.  
-   REFERENCES-Berechtigung für jede Spalte in der Zieltabelle, die als Argument verwendet wird.  
  
## <a name="examples"></a>Beispiele  
 Die folgenden Beispiele veranschaulichen die Verwendung der **ALTER SECURITY POLICY**-Syntax. Ein Beispiel eines vollständigen Szenarios für Sicherheitsrichtlinien finden Sie unter [Sicherheit auf Zeilenebene](../../relational-databases/security/row-level-security.md).  
  
### <a name="a-adding-an-additional-predicate-to-a-policy"></a>A. Hinzufügen eines zusätzlichen Prädikats zu einer Richtlinie  
 Die folgende Syntax ändert eine Sicherheitsrichtlinie, indem ein Filterprädikat zur `mytable`-Tabelle hinzugefügt wird.  
  
```  
ALTER SECURITY POLICY pol1   
    ADD FILTER PREDICATE schema_preds.SecPredicate(column1)   
    ON myschema.mytable;  
```  
  
### <a name="b-enabling-an-existing-policy"></a>B. Aktivieren einer vorhandenen Richtlinie  
 Im folgenden Beispiel wird die ALTER-Syntax verwendet, um eine Sicherheitsrichtlinie zu aktivieren.  
  
```  
ALTER SECURITY POLICY pol1 WITH ( STATE = ON );  
```  
  
### <a name="c-adding-and-dropping-multiple-predicates"></a>C. Hinzufügen und Löschen mehrerer Prädikate  
 Die folgende Syntax ändert eine Sicherheitsrichtlinie, indem Filterprädikate für die Tabellen `mytable1` und `mytable3` hinzugefügt werden und das Filterprädikat von der `mytable2`-Tabelle entfernt wird.  
  
```  
ALTER SECURITY POLICY pol1  
ADD FILTER PREDICATE schema_preds.SecPredicate1(column1)   
    ON myschema.mytable1,  
DROP FILTER PREDICATE   
    ON myschema.mytable2,  
ADD FILTER PREDICATE schema_preds.SecPredicate2(column2, 1)   
    ON myschema.mytable3;  
```  
  
### <a name="d-changing-the-predicate-on-a-table"></a>D. Ändern des Prädikats zu einer Tabelle  
 Die folgende Syntax ändert das vorhandene Filterprädikat für die mytable-Tabelle in die SecPredicate2-Funktion.  
  
```  
ALTER SECURITY POLICY pol1  
    ALTER FILTER PREDICATE schema_preds.SecPredicate2(column1)  
        ON myschema.mytable;  
```  
  
### <a name="e-changing-a-block-predicate"></a>E. Ändern eines BLOCK-Prädikats  
 Im folgenden Beispiel wird die BLOCK-Prädikatfunktion für einen Tabellenvorgang geändert.  
  
```  
ALTER SECURITY POLICY rls.SecPol  
    ALTER BLOCK PREDICATE rls.tenantAccessPredicate_v2(TenantId) 
    ON dbo.Sales AFTER INSERT;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Sicherheit auf Zeilenebene](../../relational-databases/security/row-level-security.md)   
 [CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [DROP SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-security-policy-transact-sql.md)   
 [sys.security_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [sys.security_predicates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)  
  
  
