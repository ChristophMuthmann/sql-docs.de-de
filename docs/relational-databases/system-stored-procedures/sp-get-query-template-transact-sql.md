---
title: Sp_get_query_template (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_get_query_template
- sp_get_query_template_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_get_query_template
ms.assetid: 85e9bef7-2417-41a8-befa-fe75507d9bf2
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 17fa74789d172177747ed398c43ae5ac9f1f1db5
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spgetquerytemplate-transact-sql"></a>sp_get_query_template (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt das parametrisierte Format einer Abfrage zurück. Die zurückgegebenen Ergebnisse imitieren das parametrisierte Format einer Abfrage, das aus der Verwendung von erzwungener Parametrisierung resultiert. Sp_get_query_template dient hauptsächlich beim Erstellen von TEMPLATE-Planhinweislisten.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_get_query_template  
   [ @querytext = ] N'query_text'  
   , @templatetext OUTPUT   
   , @parameters OUTPUT   
```  
  
## <a name="arguments"></a>Argumente  
 "*Query_text*"  
 Die Abfrage, für die die parametrisierte Version erzeugt werden soll. "*Query_text*" muss in einfache Anführungszeichen eingeschlossen werden und die Unicode-Bezeichner N vorangestellt werden. N'*Query_text*"ist der Wert, der @querytext Parameter. Dies ist vom Typ **nvarchar(max)**.  
  
 @templatetext  
 Ist ein Ausgabeparameter vom Typ **nvarchar(max)**, wie angegeben, die parametrisierte Form der empfangen, bereitgestellt *Query_text* als Zeichenfolgenliteral.  
  
 @parameters  
 Ist ein Ausgabeparameter vom Typ **nvarchar(max)**, wie ein Zeichenfolgenliteral der Parameternamen und Datentypen zu empfangen, die in parametrisiert wurden angegeben, bereitgestellt @templatetext.  
  
## <a name="remarks"></a>Hinweise  
 Der Parameter sp_get_query_template gibt in folgenden Situationen einen Fehler zurück:  
  
-   Es ist nicht parametrisiert werden eventuell vorhandener Literalwerte in *Query_text*.  
  
-   *Query_text* NULL ist, keine Unicode-Zeichenfolge, syntaktisch ungültig ist oder nicht kompiliert werden.  
  
 Wenn Sp_get_query_template einen Fehler zurückgibt, es ändert nicht die Werte der @templatetext und @parameters Ausgabeparameter enthalten.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der public-Datenbankrolle.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt das parametrisierte Format einer Abfrage zurück, die zwei konstante literale Werte enthält.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @my_templatetext nvarchar(max)  
DECLARE @my_parameters nvarchar(max)  
EXEC sp_get_query_template   
    N'SELECT pi.ProductID, SUM(pi.Quantity) AS Total  
        FROM Production.ProductModel pm   
        INNER JOIN Production.ProductInventory pi  
        ON pm.ProductModelID = pi.ProductID  
        WHERE pi.ProductID = 2  
        GROUP BY pi.ProductID, pi.Quantity  
        HAVING SUM(pi.Quantity) > 400',  
@my_templatetext OUTPUT,  
@my_parameters OUTPUT;  
SELECT @my_templatetext;  
SELECT @my_parameters;  
```  
  
 Im Folgenden sehen Sie die parametrisierten Werte des `@my_templatetext``OUTPUT`-Parameters:  
  
 `select pi . ProductID , SUM ( pi . Quantity ) as Total`  
  
 `from Production . ProductModel pm`  
  
 `inner join Production . ProductInventory pi`  
  
 `on pm . ProductModelID = pi . ProductID`  
  
 `where pi . ProductID = @0`  
  
 `group by pi . ProductID , pi . Quantity`  
  
 `having SUM ( pi . Quantity ) > 400`  
  
 Beachten Sie, dass das erste konstante Literal, `2`, in einen Parameter konvertiert wird. Das zweite Literal, `400`, wird nicht konvertiert, da es sich in einer `HAVING`-Klausel befindet. Die von sp_get_query_template zurückgegebenen Ergebnisse imitieren das parametrisierte Format einer Abfrage, wenn die PARAMETERIZATION-Option von ALTER DATABASE auf FORCED festgelegt wird.  
  
 Im Folgenden sehen Sie die parametrisierten Werte des `@my_parameters OUTPUT`-Parameters:  
  
```  
@0 int  
```  
  
> [!NOTE]  
>  Die Reihenfolge und Benennung von Parametern in der Ausgabe von sp_get_query_template kann sich von einem zum nächsten Quick Fix Engineering, Service Pack und Versionsupgrade für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ändern. Upgrades können auch bewirken, dass eine andere Gruppe mit konstanten Literalen für dieselbe Abfrage parametrisiert und unterschiedliche Abstände auf die Ergebnisse beider Ausgabeparameter angewendet werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Datenbankmodul gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Angeben des Abfrageparametrisierungsverhaltens mithilfe von Planhinweislisten](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)  
  
  
