---
title: Sys.external_libraries (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- external_libraries
- external_libraries_TSQL
- sys.external_libraries
- sys.external_libraries_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.external_libraries catalog view
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: bb229022bcccfb9cdc8c419844d30335337575d4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysexternallibraries-transact-sql"></a>Sys.external_libraries (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]


Unterstützt die Verwaltung von Paket-Bibliotheken, die im Zusammenhang mit der externen Laufzeiten z. B. R oder Python.

## <a name="sysexternallibraries"></a>Sys.external_libraries

Der Katalog Ansicht sys.external_libraries enthält eine Zeile für jede externe Bibliothek, die in die Datenbank hochgeladen wurde.

|Spaltenname |Datentyp | Description|
|------|------|------|
|external_library_id |int | Die ID des Objekts, externe Bibliothek. |
|name |sysname |Der Name der externen Bibliothek. Ist eindeutig innerhalb der Datenbank pro Besitzer.|
|principal_id |int |ID des Prinzipals, der dieser externen Bibliothek besitzt. |
|Sprache | sysname | Der Name der Sprache oder Common Language Runtime, die die externe Bibliothek unterstützt. Gültige Werte sind "R". Zusätzliche Laufzeiten möglicherweise in Zukunft verfügbar sein.|
|Bereich |int |0 für Öffentliche Bereich; 1 für private scope |  
|scope_desc |vom Datentyp varchar(7) |Gibt an, ob das Paket öffentlich oder privat ist.|


## <a name="see-also"></a>Siehe auch  
[sys.external_library_files](sys-external-library-files-transact-sql.md)  
[EXTERNE BIBLIOTHEK ERSTELLEN](../../t-sql/statements/create-external-library-transact-sql.md)  
[Paketverwaltung für SQL Server R Services](../../advanced-analytics/r/installing-and-managing-r-packages.md)  
