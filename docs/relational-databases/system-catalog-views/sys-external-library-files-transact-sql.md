---
title: Sys.external_library_files (Transact-SQL) | Microsoft Docs
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
- external_library_files
- external_library_files_TSQL
- sys.external_library_files
- sys.external_library_files_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.external_library_files catalog view
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: a3196218bbb886544a77c2fd1184c806591b16e6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysexternallibraryfiles-transact-sql"></a>Sys.external_library_files (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Enthält eine Zeile für jede Datei, die aus einer externen Bibliothek besteht.

|Spaltenname |Datentyp |Description|
|------|------|-----|
|external_library_id | int |Die ID des Objekts, externe Bibliothek. |
|content |varbinary(max) |Inhalt des Dateielements externe Bibliothek. |
|Plattform |tinyint |ID der die Hostplattform, auf der SQL Server installiert ist. |
|platform_desc | nvarchar(60) |Name des Host-Plattform. Gültige Werte sind "WINDOWS", "LINUX". |

### <a name="see-also"></a>Siehe auch  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[EXTERNE BIBLIOTHEK ERSTELLEN](../../t-sql/statements/create-external-library-transact-sql.md)  
[Paketverwaltung für SQL Server-Machine Learning-Dienst](../../advanced-analytics/r/installing-and-managing-r-packages.md)  
