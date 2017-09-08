---
title: "Löschen von EXTERNEN Bibliothek (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP EXTERNAL LIBRARY
- DROP_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 143e9ac0dbe042ebbb034dff847cfc01ea5a5411
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="drop-external-library-transact-sql"></a>Löschen von EXTERNEN Bibliothek (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]  

Löscht eine vorhandenes Paket-Bibliothek.

## <a name="syntax"></a>Syntax  
```
DROP EXTERNAL LIBRARY library_name  
[ AUTHORIZATION owner_name ];  
```

### <a name="arguments"></a>Argumente

**library_name**

Gibt den Namen einer vorhandenen Paket-Bibliothek.

Bibliotheken beziehen sich auf den Benutzer. D. h. gelten Bibliotheksnamen innerhalb des Kontexts eines bestimmten Benutzers oder Besitzer eindeutig.

**owner_name**

Gibt den Namen des Benutzers oder der Rolle, der die externe Bibliothek besitzt.

Datenbankbesitzer können Bibliotheken, die von anderen Benutzern erstellt löschen.

### <a name="return-values"></a>Rückgabewerte

Eine informative Meldung wird zurückgegeben, wenn die Anweisung erfolgreich war.

## <a name="remarks"></a>Hinweise

Im Gegensatz zu anderen `DROP` Anweisungen in SQL Server, die diese Anweisung unterstützt eine optionale Authorization-Klausel angegeben. Dadurch können **Dbo** oder Benutzer in der **Db_owner** Rolle So löschen Sie eine Paket-Bibliothek hochgeladen werden, durch ein normaler Benutzer in der Datenbank.

## <a name="examples"></a>Beispiele

Hinzufügen einer Datenbank ggplot2:

```sql
CREATE EXTERNAL LIBRARY ggplot2 
FROM 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\ggplot2.zip';
```

Löschen Sie ggplot2 Bibliothek.

```sql
DROP EXTERNAL LIBRARY ggplot2 <user_name>;
```

## <a name="see-also"></a>Siehe auch  
[Erstellen von EXTERNEN Bibliothek (Transact-SQL)](create-external-library-transact-sql.md)  
[ALTER externe Bibliothek (Transact-SQL)](alter-external-library-transact-sql.md)  
[Sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[Sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  


