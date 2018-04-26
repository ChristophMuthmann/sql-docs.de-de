---
title: FileStream und FileTable gespeicherte Systemprozeduren (Transact-SQL) | Microsoft Docs
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 19ee3e87d2878dcf56d0d8d26e79d1116f657fa6
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="filestream-and-filetable-system-stored-procedures-transact-sql"></a>FileStream- und FileTable gespeicherte Systemprozeduren (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Dieser Abschnitt beschreibt die gespeicherten Systemprozeduren zu der FileTable und Filestream-Funktion.  

## <a name="filestream-and-filetable-system-stored-procedures"></a>FileStream- und Filetable gespeicherten Systemprozeduren
  [Sp_filestream_force_garbage_collection (Transact-SQL)](filestream-and-filetable-sp-filestream-force-garbage-collection.md)

   Erzwingt die Ausführung des FILESTREAM-Garbage Collectors und löscht alle nicht benötigten FILESTREAM-Dateien.

  [Sp_kill_filestream_non_transacted_handles (Transact-SQL)](filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)

  Schließt nicht transaktionale Dateihandles für FileTable-Daten.


## <a name="see-also"></a>Siehe auch
[FileStream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetables](../../relational-databases/blob/filetables-sql-server.md)
<br>[FileStream und FileTable: dynamische Verwaltungssichten (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[FileStream und FileTable-Katalogsichten (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
  
  
