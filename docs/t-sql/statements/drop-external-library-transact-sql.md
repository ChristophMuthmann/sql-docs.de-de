---
title: DROP EXTERNAL LIBRARY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: 
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
manager: craigg
ms.openlocfilehash: 8c45da28bf795fca50454fde21eb7d2c3c798296
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="drop-external-library-transact-sql"></a>DROP EXTERNAL LIBRARY (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Löscht eine vorhandene Paketbibliothek.

## <a name="syntax"></a>Syntax  

```
DROP EXTERNAL LIBRARY library_name  
[ AUTHORIZATION owner_name ];  
```

### <a name="arguments"></a>Argumente

**library_name**

Gibt den Namen einer vorhandenen Paketbibliothek an.

Bibliotheken umfassen nur den Benutzer. D.h., Bibliotheksnamen gelten innerhalb des Kontexts eines bestimmten Benutzers oder Besitzers als eindeutig.

**owner_name**

Gibt den Namen eines Benutzers oder einer Rolle an, der oder die die externe Bibliothek besitzt.

Datenbankbesitzer können Bibliotheken löschen, die von anderen Benutzern erstellt wurden.

### <a name="return-values"></a>Rückgabewerte

Eine Informationsmeldung wird zurückgegeben, wenn die Anweisung erfolgreich war.

## <a name="remarks"></a>Remarks

Im Gegensatz zu anderen `DROP`-Anweisungen in SQL Server unterstützt diese Anweisung das Angeben einer optionalen Autorisierungsklausel. Dies ermöglicht einem **dbo** oder Benutzer mit der Rolle **db_owner**, eine Paketbibliothek zu löschen, die von einem normalen Benutzer in die Datenbank hochgeladen wurde.

## <a name="examples"></a>Beispiele

Hinzufügen eines benutzerdefinierten R-Pakets namens `customPackage` in eine Datenbank:

```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM 'C:\Users\Username\CustomPackages\customPackage.zip';
```

Löschen der `customPackage`-Bibliothek:

```sql
DROP EXTERNAL LIBRARY customPackage <user_name>;
```

## <a name="see-also"></a>Siehe auch  
[CREATE EXTERNAL LIBRARY (Transact-SQL)](create-external-library-transact-sql.md)  
[ALTER EXTERNAL LIBRARY (Transact-SQL)](alter-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  

