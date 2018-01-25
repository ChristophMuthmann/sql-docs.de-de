---
title: IsNull (Geography-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: IsNull (geography Data Type)
dev_langs: TSQL
helpviewer_keywords: IsNull method
ms.assetid: c031074f-bfda-4584-a3bf-4e7c324f237f
caps.latest.revision: "16"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c07ddb41209c507845da7e790035ab54ed1044f1
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="isnull-geography-data-type"></a>IsNull (geography-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Eine Eigenschaft, der angibt, wenn die **Geography** -Instanz null ist. Gibt TRUE zurück, wenn die Instanz NULL ist, und gibt 0 zurück, wenn die Instanz nicht NULL ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
.IsNull  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Typ: **Bit**  
  
 CLR-Typ: **SqlBoolean**  
  
## <a name="remarks"></a>Hinweise  
 `IsNull`kann verwendet werden, um zu testen, ob eine **Geography** -Instanz null ist. Dies kann zu möglicherweise verwirrenden Ergebnissen führen, da 0 zurückgegeben wird, wenn die Instanz nicht NULL ist, aber NULL zurückgegeben wird, wenn die Instanz NULL ist.  
  
 Diese Methode wird hauptsächlich von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Infrastruktur; es wird empfohlen, dass Sie das T-SQL-Prädikat IS NULL verwenden, um zu testen, ob eine **Geography** -Instanz null ist. Weitere Informationen zu den T-SQL-Prädikat IS NULL, finden Sie unter [IS NULL &#40; Transact-SQL &#41; ](../../t-sql/queries/is-null-transact-sql.md).  
  
## <a name="examples"></a>Beispiele  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Methoden für geography-Instanzen](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
