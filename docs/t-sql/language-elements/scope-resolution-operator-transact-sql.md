---
title: ":: (Bereich Auflösung) (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
dev_langs:
- TSQL
ms.assetid: 764d8f91-957b-4037-997b-a9b6b533c504
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a08432ae682cea4156b2090837e2f7b4d85c42b3
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="-scope-resolution-transact-sql"></a>:: (Scope Resolution) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Der Bereichsauflösungsoperator **::** ermöglicht den Zugriff auf statische Elemente eines Verbunddatentyps. Ein verbunddatentyp ist enthält mehrere einfache Datentypen und Methoden, z. B. die integrierten CLR-Typen und benutzerdefinierte SQLCLR User-Defined Typen (UDTs).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Zugriff auf das `GetRoot()`-Element des `hierarchyid`-Typs mithilfe des Bereichsauflösungsoperators dargestellt.  
  
```  
DECLARE @hid hierarchyid;  
SELECT @hid = hierarchyid::GetRoot();  
PRINT @hid.ToString();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `/`  
  
## <a name="see-also"></a>Siehe auch  
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
