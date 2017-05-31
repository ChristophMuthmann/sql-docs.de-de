---
title: Simulieren einer IF-WHILE EXISTS-Anweisung in einem nativ kompilierten Modul | Microsoft-Dokumentation
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c0e187c1-cbd9-463c-b417-8a734574f102
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d509d0d749591a134a0b87aa457bb53d28901a99
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="simulating-an-if-while-exists-statement-in-a-natively-compiled-module"></a>Simulieren einer IF-WHILE EXISTS-Anweisung in einem nativ kompilierten Modul
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Nativ kompilierte gespeicherte Prozeduren unterstützen in bedingten Anweisungen nicht die **EXISTS** -Klausel, z. B. IF und WHILE.  
  
 Das folgende Beispiel veranschaulicht eine Behelfslösung unter Verwendung einer BIT-Variablen mit einer SELECT-Anweisung zum Simulieren einer EXISTS-Klausel:  
  
```tsql  
DECLARE @exists BIT = 0  
SELECT TOP 1 @exists = 1 FROM MyTable WHERE …  
IF @exists = 1  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Migrationsprobleme bei nativ kompilierten gespeicherten Prozeduren](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [Von In-Memory OLTP nicht unterstützte Transact-SQL-Konstrukte](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
