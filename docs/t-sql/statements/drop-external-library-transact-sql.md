---
title: "Löschen von EXTERNEN Bibliothek (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
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
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: ac2814f7c0b0d1bf6de60d52ea65e54caab0f72d
ms.contentlocale: de-de
ms.lasthandoff: 10/10/2017

---
# <a name="drop-external-library-transact-sql"></a>Löschen von EXTERNEN Bibliothek (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

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

Fügen Sie ein benutzerdefiniertes R-Paket, mit dem Namen `customPackage`, in einer Datenbank:

```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM 'C:\Users\Username\CustomPackages\customPackage.zip';
```

Löschen der `customPackage` Bibliothek.

```sql
DROP EXTERNAL LIBRARY customPackage <user_name>;
```

## <a name="see-also"></a>Siehe auch  
[Erstellen von EXTERNEN Bibliothek (Transact-SQL)](create-external-library-transact-sql.md)  
[ALTER externe Bibliothek (Transact-SQL)](alter-external-library-transact-sql.md)  
[Sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[Sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  


