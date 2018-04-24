---
title: ORIGINAL_DB_NAME (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ORIGINAL_DB_NAME
- ORIGINAL_DB_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ORIGINAL_DB_NAME function
ms.assetid: 7dadc40a-1287-4f31-8487-434ee477144d
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0dac5232750954d888e56509994dd81d49b95351
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="originaldbname-transact-sql"></a>ORIGINAL_DB_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den Datenbanknamen zurück, der vom Benutzer in der Datenbankverbindungszeichenfolge angegeben wird. Hierbei handelt es sich um die Datenbank, die mit der **sqlcmd-d**-Option (USE *Datenbank*) oder dem ODBC-Datenquellenausdruck (Anfangskatalog =*Datenbankname*) angegeben wird.  
  
 Diese Datenbank ist nicht mit der standardmäßigen Benutzerdatenbank identisch.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ORIGINAL_DB_NAME ()  
```  
  
## <a name="remarks"></a>Remarks  
 Wenn die ursprüngliche Datenbank nicht angegeben wird, gibt die Funktion eine leere Zeichenfolge zurück.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sqlcmd (Hilfsprogramm)](../../tools/sqlcmd-utility.md)   
 [Hilfsprogramm „osql“](../../tools/osql-utility.md)   
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
