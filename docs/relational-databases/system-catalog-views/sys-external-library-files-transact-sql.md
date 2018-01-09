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
ms.technology: 
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
ms.openlocfilehash: a03a50bdeda18d027fbad56e2cd4b86a261052b7
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="sysexternallibraryfiles-transact-sql"></a>Sys.external_library_files (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Enthält eine Zeile für jede Datei, die aus einer externen Bibliothek besteht.

|Spaltenname |Datentyp |Description|
|------|------|-----|
|external_library_id | ssNoversion |Die ID des Objekts, externe Bibliothek. |
|content |varbinary(max) |Inhalt des Dateielements externe Bibliothek. |
|Plattform |TINYINT |ID der die Hostplattform, auf der SQL Server installiert ist. |
|platform_desc | nvarchar(60) |Name des Host-Plattform. Gültige Werte sind "WINDOWS", "LINUX". |

### <a name="see-also"></a>Siehe auch  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[EXTERNE BIBLIOTHEK ERSTELLEN](../../t-sql/statements/create-external-library-transact-sql.md)  
[Paketverwaltung für SQL Server-Machine Learning-Dienst](../../advanced-analytics/r/installing-and-managing-r-packages.md)  
