---
title: Massenimport von LOB-Daten (Large Objects) mit dem OPENROWSET-Massenrowsetanbieter | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: import-export
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SINGLE_NCLOB option
- bulk rowset providers [SQL Server]
- bulk importing [SQL Server], data formats
- OPENROWSET function, bulk importing large data
- SINGLE_CLOB option
- data formats [SQL Server], large-object data
- large data, bulk imports
- SINGLE_BLOB option
ms.assetid: 171cdd5c-1e47-4bd7-b99a-4f0fd4e10526
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4e309875d56367c83a638fd8cea76b579125f607
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="bulk-import-large-object-data-with-openrowset-bulk-rowset-provider"></a>Massenimport von LOB-Daten (Large Objects) mithilfe des OPENROWSET-Massenrowsetanbieters
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OPENROWSET-Bulkrowsetanbieter ermöglicht den Massenimport einer Datendatei als LOB-Daten.  
  
 Vom OPENROWSET-Bulkrowsetanbieter unterstützte LOB-Datentypen: **varbinary(max)**oder **image**, **varchar(max)**oder **text**und **nvarchar(max)**oder **ntext**.  
  
> [!NOTE]  
>  Die Datentypen **image**, **text** und **ntext** sind als veraltet markiert.  
  
 Die OPENROWSET BULK-Klausel unterstützt drei Optionen zum Importieren vom Inhalt einer Datendatei als einzeiliges, einspaltiges Rowset. Statt eine Formatdatei zu verwenden, können Sie eine dieser LOB-Optionen angeben. Folgende Optionen stehen zur Verfügung:  
  
 SINGLE_BLOB  
 Liest die Inhalte von *data_file* als einzelne Zeile und gibt die Inhalte als einspaltiges Rowset des **varbinary(max)**-Datentyps zurück.  
  
 SINGLE_CLOB  
 Liest die Inhalte der angegebenen Datendatei als Zeichen, und gibt die Inhalte als einzeiliges, einspaltiges Rowset im **varchar(max)**-Datentyp zurück, wobei die Sortierung der aktuellen Datenbank verwendet wird, z.B. Text oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word-Dokument.  
  
 SINGLE_NCLOB  
 Liest die Inhalte der angegebenen Datendatei als Unicode, und gibt die Inhalte als einzeiliges, einspaltiges Rowset im **nvarchar(max)**-Datentyp zurück, wobei die Sortierung der aktuellen Datenbank verwendet wird.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Importieren von Massendaten mithilfe von BULK INSERT oder OPENROWSET(BULK...) &#40;BULK...&#41; &#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Beibehalten von NULL-Werten oder Verwenden von Standardwerten während des Massenimports &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)   
 [bcp (Hilfsprogramm)](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)  
  
  
