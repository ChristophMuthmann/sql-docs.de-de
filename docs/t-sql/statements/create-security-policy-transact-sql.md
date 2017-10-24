---
title: CREATE SECURITY POLICY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SECURITY_POLICY_TSQL
- CREATE SECURITY
- SECURITY
- CREATE_SECURITY_POLICY_TSQL
- CREATE_SECURITY_TSQL
- SECURITY POLICY
- SECURITY_TSQL
- CREATE SECURITY POLICY
dev_langs:
- TSQL
helpviewer_keywords:
- RLS
- CREATE SECURITY POLICY statement
- Row-Level Security
ms.assetid: d6ab70ee-0fa2-469c-96f6-a3c16d673bc8
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 53292dc3f9f5cbd36913276496084d4648f13520
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-security-policy-transact-sql"></a>CREATE SECURITY POLICY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Erstellt eine Sicherheitsrichtlinie für die Sicherheit auf Zeilenebene.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```     
CREATE SECURITY POLICY [schema_name. ] security_policy_name    
    { ADD [ FILTER | BLOCK ] } PREDICATE tvf_schema_name.security_predicate_function_name   
      ( { column_name | arguments } [ , …n] ) ON table_schema_name. table_name    
      [ <block_dml_operation> ] , [ , …n] 
    [ WITH ( STATE = { ON | OFF }  [,] [ SCHEMABINDING = { ON | OFF } ] ) ]  
    [ NOT FOR REPLICATION ] 
[;]  
  
<block_dml_operation>  
    [ { AFTER { INSERT | UPDATE } }   
    | { BEFORE { UPDATE | DELETE } } ]  
```  
  
## <a name="arguments"></a>Argumente  
 *security_policy_name*  
 Der Name der Sicherheitsrichtlinie. Namen von Sicherheitsrichtlinien müssen den Regeln für Bezeichner entsprechen und innerhalb der Datenbank und für jedes Schema eindeutig sein.  
  
 *schema_name*  
 Der Name des Schemas, zu dem die Sicherheitsrichtlinie gehört. *Schema_name* aufgrund der schemabindung erforderlich ist.  
  
 [FILTER | BLOCK]  
 Der Typ des sicherheitsprädikat für die Funktion, die an die Zieltabelle gebunden wird. FILTER-Prädikate Filtern automatisch die Zeilen, die für Lesevorgänge verfügbar sind. BLOCK-Prädikate explizit Block-Schreibvorgänge, die die Prädikatfunktion verletzen.  
  
 *tvf_schema_name.security_predicate_function_name*  
 Die Inline-Tabellenwertfunktion, die als Prädikat verwendet wird und bei Abfragen für eine Zieltabelle erzwungen wird. Für einen bestimmten DML-Vorgang für eine bestimmte Tabelle kann höchstens ein Sicherheitsprädikat definiert werden. Die Inline-Tabellenwertfunktion muss mit der SCHEMABINDING-Option erstellt worden sein.  
  
 { *Column_name* | *Argumente* }  
 Der Spaltenname oder Ausdruck, der als Parameter für die Sicherheitsprädikatfunktion verwendet wird. Alle Spalten in der Zieltabelle können als Argumente für die Prädikatfunktion verwendet werden. Ausdrücke, die Literale, vordefinierte Elemente und arithmetische Operatoren enthalten, können verwendet werden.  
  
 *table_schema_name.table_name*  
 Die Zieltabelle, auf die das Sicherheitsprädikat angewendet wird. Mehrere deaktivierte Sicherheitsrichtlinien können für einen bestimmten DML-Vorgang eine einzelne Tabelle abzielen, aber zu jedem Zeitpunkt kann nur eine aktiviert werden.  
  
 *\<Block_dml_operation >* der bestimmten DML-Vorgang für die Block-Prädikat angewendet werden. Nach dem gibt an, dass das Prädikat für die Werte der Zeilen ausgewertet werden soll, nachdem der DML-Vorgang durchgeführt (INSERT- oder UPDATE) wurde. Vor dem gibt an, dass das Prädikat auf die Werte der Zeilen ausgewertet wird vor der DML-Vorgang durchgeführt (Update- oder DELETE). Wenn kein Vorgang angegeben ist, gilt das Prädikat für alle Vorgänge.  
  
 [STATE = {ON | **OFF** }]  
 Aktiviert oder deaktiviert das Erzwingen der Sicherheitsprädikate der Sicherheitsrichtlinie für die Zieltabellen. Wenn nichts angegeben ist, wird die erstellte Sicherheitsrichtlinie aktiviert.  
  
 [SCHEMABINDING = {ON | OFF}]  
 Gibt an, ob alle prädikatfunktionen in der Richtlinie mit der Option SCHEMABINDING erstellt werden müssen. Standardmäßig müssen alle Funktionen mit SCHEMABINDING erstellt werden.  
  
 NOT FOR REPLICATION  
 Gibt an, dass die Sicherheitsrichtlinie nicht ausgeführt werden soll, wenn ein Replikations-Agent das Zielobjekt ändert. Weitere Informationen finden Sie unter [Kontrollieren des Verhaltens von Triggern und Einschränkungen während der Synchronisierung &#40;Replikationsprogrammierung mit Transact-SQL&#41;](../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md).  
  
 [*Table_schema_name*.] *Table_name*  
 Die Zieltabelle, auf die das Sicherheitsprädikat angewendet wird. Mehrere deaktivierte Sicherheitsrichtlinien können auf eine einzelne Tabelle abzielen, aber zu jedem Zeitpunkt kann nur eine aktiviert werden.  
  
## <a name="remarks"></a>Hinweise  
 Wenn prädikatfunktionen mit speicheroptimierten Tabellen verwenden, müssen Sie nehmen **SCHEMABINDING** und Verwenden der **WITH NATIVE_COMPILATION** Kompilierung-Hinweis.  
  
 Block-Prädikate werden ausgewertet, nachdem der entsprechende DML-Vorgang ausgeführt wird. Aus diesem Grund kann eine READ UNCOMMITTED Abfrage vorübergehender Werte anzuzeigen, die ein Rollback.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER ANY SECURITY POLICY-Berechtigung und die ALTER-Berechtigung für das Schema.  
  
 Darüber hinaus sind die folgenden Berechtigungen für jedes hinzugefügte Prädikat erforderlich:  
  
-   SELECT- und REFERENCES-Berechtigungen für die Funktion, die als Prädikat verwendet wird.  
  
-   REFERENCES-Berechtigung für die Zieltabelle, die an die Richtlinie gebunden wird.  
  
-   REFERENCES-Berechtigung für jede Spalte in der Zieltabelle, die als Argument verwendet wird.  
  
## <a name="examples"></a>Beispiele  
 Die folgenden Beispiele veranschaulichen die Verwendung der **CREATE SECURITY POLICY** -Syntax. Ein Beispiel einer vollständigen Szenarios für Sicherheitsrichtlinien finden Sie unter [Sicherheit auf Zeilenebene](../../relational-databases/security/row-level-security.md).  
  
### <a name="a-creating-a-security-policy"></a>A. Erstellen einer Sicherheitsrichtlinie  
 Die folgende Syntax erstellt eine Sicherheitsrichtlinie mit einem Filterprädikat für die Customer-Tabelle und lässt die Sicherheitsrichtlinie deaktiviert.  
  
```  
CREATE SECURITY POLICY [FederatedSecurityPolicy]   
ADD FILTER PREDICATE [rls].[fn_securitypredicate]([CustomerId])   
ON [dbo].[Customer];  
```  
  
### <a name="b-creating-a-policy-that-affects-multiple-tables"></a>B. Erstellen einer Richtlinie mit Auswirkungen auf mehrere Tabellen  
 Die folgende Syntax erstellt eine Sicherheitsrichtlinie mit drei Filterprädikaten für drei verschiedenen Tabellen und aktiviert die Sicherheitsrichtlinie.  
  
```  
CREATE SECURITY POLICY [FederatedSecurityPolicy]   
ADD FILTER PREDICATE [rls].[fn_securitypredicate1]([CustomerId])   
    ON [dbo].[Customer],  
ADD FILTER PREDICATE [rls].[fn_securitypredicate1]([VendorId])   
    ON [dbo].[ Vendor],  
ADD FILTER PREDICATE [rls].[fn_securitypredicate2]([WingId])   
    ON [dbo].[Patient]  
WITH (STATE = ON);  
```  
  
### <a name="c-creating-a-policy-with-multiple-types-of-security-predicates"></a>C. Erstellen eine Richtlinie mit mehreren Arten von sicherheitsprädikaten  
 Hinzufügen von Filter-Prädikat und Block-Prädikat der Sales-Tabelle ein.  
  
```  
CREATE SECURITY POLICY rls.SecPol  
    ADD FILTER PREDICATE rls.tenantAccessPredicate(TenantId) ON dbo.Sales,  
    ADD BLOCK PREDICATE rls.tenantAccessPredicate(TenantId) ON dbo.Sales AFTER INSERT;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sicherheit auf Zeilenebene](../../relational-databases/security/row-level-security.md)   
 [ALTER SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-security-policy-transact-sql.md)   
 [DROP SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-security-policy-transact-sql.md)   
 [sys.security_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [Sys. security_predicates &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)  
  
  


