---
title: ORIGINAL_DB_NAME (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b14df393efb9fb2ab6543e66eba763f50b1f00ff
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="originaldbname-transact-sql"></a>ORIGINAL_DB_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den Datenbanknamen zurück, der vom Benutzer in der Datenbankverbindungszeichenfolge angegeben wird. Dies ist die Datenbank, die mithilfe des Parameters der **Sqlcmd-d** Option (Verwendung *Datenbank*) oder dem ODBC-Datenquellenausdruck (Anfangskatalog =*Databasename*).  
  
 Diese Datenbank ist nicht mit der standardmäßigen Benutzerdatenbank identisch.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ORIGINAL_DB_NAME ()  
```  
  
## <a name="remarks"></a>Hinweise  
 Wenn die ursprüngliche Datenbank nicht angegeben wird, gibt die Funktion eine leere Zeichenfolge zurück.  
  
## <a name="see-also"></a>Siehe auch  
 [sqlcmd (Hilfsprogramm)](../../tools/sqlcmd-utility.md)   
 [Osql (Hilfsprogramm)](../../tools/osql-utility.md)   
 [SQL Server Native Client &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
