---
title: IsNull (geometry-Datentyp) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|spatial-geography
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- IsNull (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- IsNull (geometry Data Type)
ms.assetid: f95813a5-26c0-48aa-bfb8-56d2a0980788
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6f9b97eaa73b70beea9e56b2e4a07e99ea9e9e83
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="isnull-geometry-data-type"></a>IsNull (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Der Typ einer **geometry**-Instanz ist NULL. Gibt 0 zurück, wenn die Instanz nicht NULL ist.
  
## <a name="syntax"></a>Syntax  
  
```  
.IsNull  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Typ: **bit**  
  
 CLR-Typ: **SqlBoolean**  
  
## <a name="remarks"></a>Remarks  
 `IsNull` kann verwendet werden, um zu überprüfen, ob eine **geometry**-Instanz NULL ist. Dies kann zu möglicherweise verwirrenden Ergebnissen führen, da 0 zurückgegeben wird, wenn die Instanz nicht NULL ist, aber NULL zurückgegeben wird, wenn die Instanz NULL ist.  
  
 Diese Methode wird in erster Linie von der .SQL Server-Infrastruktur verwendet. Es wird nicht empfohlen, mit `IsNull` zu prüfen, ob eine Instanz NULL ist.  
  

## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erweiterte Methoden für geometry-Instanzen](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

