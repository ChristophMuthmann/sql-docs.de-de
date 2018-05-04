---
title: FileStream und FileTable-Katalogsichten (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- FileTables [SQL Server], catalog views
ms.assetid: 2c83a4a7-720b-4435-a3b5-788c29f56949
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3919000b2ac82a23d4569c3ea1d97d2ca75f517a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="filestream-and-filetable-catalog-views-transact-sql"></a>Filestream- und FileTable-Katalogsichten (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In diesem Abschnitt werden die mit der FileTable-Funktion zusammenhängenden Katalogsichten beschrieben.  
  
## <a name="filestream-and-filetable-catalog-views-transact-sql"></a>FileStream und filetable-Katalogsichten (Transact-SQL)
 [sys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md)  
 Zeigt Informationen zur Ebene des nicht transaktionalen Zugriffs auf die aktivierten FILESTREAM-Daten in FileTables an. Enthält eine Zeile für jede Datenbank in der SQL Server-Instanz.  
  
 [sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)  
 Zeigt eine Liste mit systemdefinierten Objekten an, die sich auf FileTables beziehen. Enthält eine Zeile für jedes systemdefinierte Objekt.  
  
 [sys.filetables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)  
 Gibt eine Zeile für jede FileTable zurück. Erbt von **sys.tables**.  

## <a name="see-also"></a>Siehe auch
[FileStream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetables](../../relational-databases/blob/filetables-sql-server.md)
<br>[Dynamische Verwaltungssichten für Filestream und FileTable (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Gespeicherte Systemprozeduren für Filestream und FileTable (Transact-SQL)](../system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)
  
  
