---
title: CREATE AGGREGATE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
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
f1_keywords:
- CREATE_AGGREGATE_TSQL
- CREATE AGGREGATE
- AGGREGATE_TSQL
- AGGREGATE
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE AGGREGATE statement
- aggregate functions [SQL Server], user-defined
- user-defined functions [CLR integration]
ms.assetid: 62eebc19-9f15-4245-94fa-b3fcd64a9d42
caps.latest.revision: 50
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e5fb189cbb6e2dda34b8b1012e73e5e1c4b780d3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-aggregate-transact-sql"></a>CREATE AGGREGATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt eine benutzerdefinierte Aggregatfunktion, deren Implementierung in einer Klasse einer Assembly in [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] definiert ist. Damit [!INCLUDE[ssDE](../../includes/ssde-md.md)] die Aggregatfunktion an die Implementierung bindet, muss zunächst die [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Assembly, die die Implementierung enthält, mithilfe einer CREATE ASSEMBLY-Anweisung in eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hochgeladen werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE AGGREGATE [ schema_name . ] aggregate_name  
        (@param_name <input_sqltype>   
        [ ,...n ] )  
RETURNS <return_sqltype>  
EXTERNAL NAME assembly_name [ .class_name ]  
  
<input_sqltype> ::=  
        system_scalar_type | { [ udt_schema_name. ] udt_type_name }  
  
<return_sqltype> ::=  
        system_scalar_type | { [ udt_schema_name. ] udt_type_name }  
  
```  
  
## <a name="arguments"></a>Argumente  
 *schema_name*  
 Der Name des Schemas, zu dem die benutzerdefinierte Aggregatfunktion gehört.  
  
 *aggregate_name*  
 Der Name der Aggregatfunktion, die Sie erstellen möchten.  
  
 **@** *param_name*  
 Ein oder mehrere Parameter im benutzerdefinierten Aggregat. Der Wert eines Parameters muss vom Benutzer angegeben werden, wenn die Aggregatfunktion ausgeführt wird. Geben Sie einen Parameternamen an, der mit dem Zeichen **@** beginnt. Der Parametername muss den Regeln für [Bezeichner](../../relational-databases/databases/database-identifiers.md) entsprechen. Parameter gelten lokal in der jeweiligen Funktion.  
  
 *system_scalar_type*  
 Einer der skalaren Systemdatentypen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um den Wert des Eingabeparameters oder Rückgabewerts zu speichern. Alle skalaren Datentypen, außer **text**, **ntext** und **image**, können als Parameter für ein benutzerdefiniertes Aggregat verwendet werden. Nicht skalare Typen, wie beispielsweise **cursor** und **table**, können nicht angegeben werden.  
  
 *udt_schema_name*  
 Der Name des Schemas, zu dem der CLR-benutzerdefinierte Typ gehört. Wenn der Name des Schemas nicht angegeben ist, verweist [!INCLUDE[ssDE](../../includes/ssde-md.md)] auf *udt_type_name* in der folgenden Reihenfolge:  
  
-   Der systemeigene SQL-Namespace.  
  
-   Das Standardschema des aktuellen Benutzers in der aktuellen Datenbank  
  
-   Das **dbo** -Schema in der aktuellen Datenbank  
  
 *udt_type_name*  
 Der Name eines CLR-benutzerdefinierten Typs, der bereits in der aktuellen Datenbank erstellt wurde. Falls *udt_schema_name* nicht angegeben wird, wird in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] davon ausgegangen, dass der Typ zum Schema des aktuellen Benutzers gehört.  
  
 *assembly_name* [ **.***class_name* ]  
 Die Assembly, die an die benutzerdefinierte Aggregatfunktion gebunden werden soll, und optional der Name des Schemas, zu dem die Assembly gehört, sowie der Name der Klasse innerhalb der Assembly, die das benutzerdefinierte Aggregat implementiert. Die Assembly muss bereits mit einer CREATE ASSEMBLY-Anweisung in der Datenbank erstellt worden sein. *class_name* muss ein gültiger [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Bezeichner sein und mit dem Namen einer Klasse übereinstimmen, die in der Assembly vorhanden ist. *class_name* kann ein mit dem Namespace qualifizierter Name sein, falls die zum Erstellen der Klasse verwendete Programmiersprache Namespaces verwendet, z.B. C#. Wenn *class_name* nicht angegeben ist, geht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] davon aus, dass der Wert mit *aggregate_name* identisch ist.  
  
## <a name="remarks"></a>Remarks  
 Standardmäßig ist die Möglichkeit, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR-Code ausführt, deaktiviert. Sie können Datenbankobjekte erstellen, ändern und löschen, die auf Module für verwalteten Code verweisen. Der Code in diesen Modulen wird jedoch nur in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt, wenn die Option [clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) mithilfe von [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) aktiviert wird.  
  
 Die in *assembly_name* angegebene Assemblyklasse und die zugehörigen Methoden sollten alle Anforderungen zum Implementieren einer benutzerdefinierten Aggregatfunktion in einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erfüllen. Weitere Informationen finden Sie unter [Benutzerdefinierte CLR-Aggregate](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CREATE AGGREGATE-Berechtigungen sowie die REFERENCES-Berechtigung für die Assembly, die in der EXTERNAL NAME-Klausel angegeben ist.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird davon ausgegangen, dass eine StringUtilities.csproj-Beispielanwendung kompiliert wird. Weitere Informationen finden Sie unter [Beispiel für Zeichenfolgenhilfsprogramm-Funktionen](http://msdn.microsoft.com/library/9623013f-15f1-4614-8dac-1155e57c880c).  
  
 In diesem Beispiel wird das `Concatenate`-Aggregat erstellt. Bevor das Aggregat erstellt wird, wird die `StringUtilities.dll`-Assembly in der lokalen Datenbank registriert.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @SamplesPath nvarchar(1024)  
-- You may have to modify the value of the this variable if you have  
--installed the sample some location other than the default location.  
  
SELECT @SamplesPath = REPLACE(physical_name, 'Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\master.mdf', 'Microsoft SQL Server\130\Samples\Engine\Programmability\CLR\')   
     FROM master.sys.database_files   
     WHERE name = 'master';  
  
CREATE ASSEMBLY StringUtilities FROM @SamplesPath + 'StringUtilities\CS\StringUtilities\bin\debug\StringUtilities.dll'  
WITH PERMISSION_SET=SAFE;  
GO  
  
CREATE AGGREGATE Concatenate(@input nvarchar(4000))  
RETURNS nvarchar(4000)  
EXTERNAL NAME [StringUtilities].[Microsoft.Samples.SqlServer.Concatenate];  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [DROP AGGREGATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-aggregate-transact-sql.md)  
  
  
