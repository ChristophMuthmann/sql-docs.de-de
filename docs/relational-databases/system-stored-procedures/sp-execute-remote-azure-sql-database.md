---
title: Sp_execute_remote (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sp_execute_remote
- sp_execute_remote_TSQL
helpviewer_keywords:
- remote execution
- queries, remote execution
ms.assetid: ca89aa4c-c4c1-4c46-8515-a6754667b3e5
caps.latest.revision: 17
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: d681bdeafa6fc39a01a41f067bf9cec7a809add6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="spexecuteremote-azure-sql-database"></a>Sp_execute_remote (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Führt eine [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung auf einem einzelnen Azure SQL-Remotedatenbank oder eine Gruppe von Datenbanken, die als Shards in einem horizontalen Partitionierungsschema dienen.  
  
 Die gespeicherte Prozedur ist Teil des Features flexible Abfrage.  Finden Sie unter [Übersicht zu Azure SQL-Datenbank elastischen Datenbank Abfragen](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/) und [elastische Datenbankabfragen für Sharding (horizontales partitionieren)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-horizontal-partitioning/).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
sp_execute_remote [ @data_source_name = ] datasourcename  
[ , @stmt = ] statement  
[   
  { , [ @params = ] N'@parameter_name data_type [,...n ]' }   
     { , [ @param1 = ] 'value1' [ ,...n ] }  
]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @data_source_name =] *Datasourcename*  
 Identifiziert die externe Datenquelle, in dem die Anweisung ausgeführt wird. Finden Sie unter [externe Datenquelle erstellen &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md). Die externe Datenquelle kann vom Typ "RDBMS" oder "SHARD_MAP_MANAGER" sein.  
  
 [ @stmt= ] *statement*  
 Ist eine Unicode-Zeichenfolge, enthält eine [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung oder eines Batches. @stmt eine Unicode-Konstante oder eine Unicode-Variable muss sein. Komplexere Unicodeausdrücke, wie z. B. die Verkettung von zwei Zeichenfolgen mit dem +-Operator, sind nicht zulässig. Zeichenkonstanten sind nicht zulässig. Wenn eine Unicode-Konstante angegeben wird, muss er mit vorangestellt ein **N**. Beispielsweise die Unicode-Konstante **N 'Sp_who'** gültig ist, aber die Zeichenkonstante **'Sp_who'** nicht. Die Länge der Zeichenfolge wird nur durch den verfügbaren Arbeitsspeicher des Datenbankservers begrenzt. Auf 64-Bit-Servern, die Größe der Zeichenfolge ist auf 2 GB sind, die maximale Größe des beschränkt **nvarchar(max)**.  
  
> [!NOTE]  
>  @stmt kann Parameter aufweisen, z. B. das gleiche Format wie ein Variablenname enthalten: `N'SELECT * FROM HumanResources.Employee WHERE EmployeeID = @IDParameter'`  
  
 Für jeden Parameter in @stmt ist ein entsprechender Eintrag in der @params-Parameterdefinitionsliste und in der Parameterwerteliste erforderlich.  
  
 [ @params=] N'@*Parameter_name ** Data_type* [,... *n* ] "  
 Eine Zeichenfolge, die die Definitionen aller Parameter enthält, die in @stmt eingebettet wurden. Die Zeichenfolge muss eine Unicode-Konstante oder eine Unicode-Variable sein. Jede Parameterdefinition besteht aus einem Parameternamen und einem Datentyp. *n* ist ein Platzhalter, der zusätzliche Parameterdefinitionen. Jeder Parameter im angegebenen @stmtmust definiert werden, @params. Wenn die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung bzw. ein solcher Batch in @stmt keine Parameter enthält, ist @params nicht erforderlich. Der Standardwert für diesen Parameter ist NULL.  
  
 [ @param1= ] '*value1*'  
 Der Wert für den ersten Parameter, der in der Parameterzeichenfolge definiert ist. Bei diesem Wert kann es sich um eine Unicode-Konstante oder eine Unicode-Variable handeln. Für jeden Parameter in @stmt muss ein Parameterwert angegeben werden. Die Werte sind nicht erforderlich, wenn die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung oder der -Batch in @stmt keine Parameter aufweist.  
  
 *n*  
 Ein Platzhalter für die Werte zusätzlicher Parameter. Werte können nur Konstanten oder Variablen sein. Werte können keine komplexeren Ausdrücke sein, wie z. B. Funktionen oder Ausdrücke, die mithilfe von Operatoren erstellt werden.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder ungleich 0 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Gibt das Resultset der ersten SQL-Anweisung zurück.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die `ALTER ANY EXTERNAL DATA SOURCE`-Berechtigung.  
  
## <a name="remarks"></a>Hinweise  
 `sp_execute_remote` Parameter müssen in der Reihenfolge eingegeben werden, wie im obigen Syntaxabschnitt beschrieben. Wenn die Parameter nicht in der vorgegebenen Reihenfolge eingegeben werden, wird eine Fehlermeldung ausgegeben.  
  
 `sp_execute_remote` weist das gleiche Verhalten wie [EXECUTE &#40;Transact-SQL&#41; ](../../t-sql/language-elements/execute-transact-sql.md) im Hinblick auf Batches und der Gültigkeitsbereich von Namen. Die Transact-SQL-Anweisung oder der Batch in die Sp_execute_remote *@stmt* Parameter wird nicht kompiliert werden, bis die Sp_execute_remote-Anweisung ausgeführt wird.  
  
 `sp_execute_remote` das Resultset mit dem Namen "$ShardName", die den Namen der Remotedatenbank enthält, die die Zeile erstellt hinzugefügt eine zusätzliche Spalte.  
  
 `sp_execute_remote` kann verwendet werden, ähnlich wie [Sp_executesql &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
### <a name="simple-example"></a>Einfaches Beispiel  
 Das folgende Beispiel erstellt und führt eine einfache SELECT-Anweisung in einer Remotedatenbank.  
  
```sql  
EXEC sp_execute_remote  
    N'MyExtSrc',  
    N'SELECT COUNT(w_id) AS Count_id FROM warehouse'   
```  
  
### <a name="example-with-multiple-parameters"></a>Beispiel mit mehreren Parametern  
Erstellen Sie eine datenbankbezogenen Anmeldeinformationen in einer Benutzerdatenbank Administratoranmeldeinformationen für die master-Datenbank angeben. Erstellen einer externen Datenquelle zeigen die master-Datenbank und die datenbankbezogenen Anmeldeinformationen angeben. Dann Folgendes Beispiel in der Benutzerdatenbank und führt die `sp_set_firewall_rule` Prozedur in der master-Datenbank. Die `sp_set_firewall_rule` Prozedur erfordert 3 Parameter, und erfordert die `@name` Parameter Unicode sein.

```
EXEC sp_execute_remote @data_source_name  = N'PointToMaster', 
@stmt = N'sp_set_firewall_rule @name, @start_ip_address, @end_ip_address', 
@params = N'@name nvarchar(128), @start_ip_address varchar(50), @end_ip_address varchar(50)',
@name = N'TempFWRule', @start_ip_address = '0.0.0.2', @end_ip_address = '0.0.0.2';
```

## <a name="see-also"></a>Siehe auch:

[ERSTELLEN VON DATENBANKWEITE ANMELDEINFORMATIONEN](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
[Erstellen der EXTERNEN Datenquelle (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)  
    
