---
title: Rangfolge der Datentypen (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- precedence [SQL Server]
- data types [SQL Server], converting
- data types [SQL Server], precedence
- converting data types [SQL Server], precedence
- precedence [SQL Server], data types
ms.assetid: f4c804ab-ed3f-43b1-a024-c9ac6944b66b
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e61ec1dec12552219279370f01fe0dd494a22cbe
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="data-type-precedence-transact-sql"></a>Rangfolge der Datentypen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Wenn durch einen Operator zwei Ausdrücke verschiedener Datentypen kombiniert werden, geben die Rangfolgeregeln für Datentypen an, dass der Datentyp mit der niedrigeren Rangfolge in den Datentyp mit der höheren Rangfolge konvertiert wird. Wenn es sich bei der Konvertierung nicht um eine unterstützte implizite Konvertierung handelt, gibt das System einen Fehler zurück. Wenn beide Operandenausdrücke vom gleichen Datentyp sind, hat das Ergebnis der Operation diesen Datentyp.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet die folgende Rangfolge für Datentypen:
  
1.  benutzerdefinierte Datentypen (höchster)  
1.  **sql_variant**  
1.  **xml**  
1.  **datetimeoffset**  
1.  **datetime2**  
1.  **datetime**  
1.  **smalldatetime**  
1.  **Datum**  
1. **Uhrzeit**  
1. **float**  
1. **real**  
1. **decimal**  
1. **money**  
1. **smallmoney**  
1. **bigint**  
1. **int**  
1. **smallint**  
1. **tinyint**  
1. **bit**  
1. **ntext**  
1. **text**  
1. **image**  
1. **timestamp**  
1. **uniqueidentifier**  
1. **Nvarchar** (einschließlich **nvarchar(max)** )  
1. **nchar**  
1. **Varchar** (einschließlich **varchar(max)** )  
1. **char**  
1. **Varbinary** (einschließlich **varbinary(max)** )  
1. **binäre** (niedrigste Priorität)  
  
## <a name="see-also"></a>Siehe auch
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  
