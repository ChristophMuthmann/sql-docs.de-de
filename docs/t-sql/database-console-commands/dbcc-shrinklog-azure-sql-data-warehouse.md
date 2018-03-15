---
title: DBCC SHRINKLOG (Azure SQL Data Warehouse) | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d06917a784e507ab5568e28b4d34273f5fe71063
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-shrinklog-azure-sql-data-warehouse"></a>DBCC SHRINKLOG (Azure SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Reduziert die Größe des Transaktionsprotokolls *in der gesamten Anwendung* für die aktuelle [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]- oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]-Datenbank. Die Daten werden defragmentiert, um das Transaktionsprotokoll zu verkleinern. Mit der Zeit kann es sein, dass das Datenbanktransaktionsprotokoll zu viele Bestandteile hat und dadurch nicht effizient verwendet werden kann. Verwenden Sie DBCC SHRINKLOG, um diese Fragmentierung und damit auch die Protokollgröße zu verringern.
  
![Symbol zum Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions &#40;Transact-SQL&#41; (Transact-SQL-Syntaxkonventionen (Transact-SQL))](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DBCC SHRINKLOG   
    [ ( SIZE = { target_size [ MB | GB | TB ]  } | DEFAULT ) ]   
    [ WITH NO_INFOMSGS ]   
[;]  
```  
  
## <a name="arguments"></a>Argumente  
SIZE = { *target_size* [ MB | **GB** | TB ]  } | **DEFAULT**.  
*target_size* ist die gewünschte Größe des Transaktionsprotokolls auf sämtlichen Computeknoten, nachdem DBCC SHRINKLOG abgeschlossen wurde. Dabei handelt es sich um einen Integer größer als 0 (null).  
Die Protokollgröße wird in Megabyte (MB), Gigabyte (GB) oder Terabyte (TB) angegeben. Dabei handelt es sich um die Gesamtgröße aller Transaktionsprotokolle auf den Computeknoten.  
Standardmäßig reduziert DBCC SHRINKLOG das Transaktionsprotokoll auf die Protokollgröße, die in den Metadaten der Datenbank gespeichert ist. Die Protokollgröße in den Metadaten wird von dem LOG_SIZE-Parameter in [CREATE DATABASE &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/create-database-azure-sql-data-warehouse.md) oder [ALTER DATABASE &#40;Azure SQL Data Warehouse&#41;](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md) bestimmt. DBCC SHRINKLOG reduziert die Größe des Transaktionsprotokolls, wenn `SIZE=DEFAULT` angegeben oder die `SIZE`-Klausel weggelassen wird.
  
WITH NO_INFOMSGS  
Informationsmeldungen werden nicht in den DBCC SHRINKLOG-Ergebnissen angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
Erfordert die ALTER SERVER STATE-Berechtigung.
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
DBCC SHRINKLOG ändert nicht die Protokollgröße, die in den Metadaten der Datenbank gespeichert ist. Die Metadaten enthalten weiterhin den LOG_SIZE-Parameter, der in den Anweisungen CREATE DATABASE oder ALTER DATABASE angegeben wurde.
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
### <a name="a-shrink-the-transaction-log-to-the-original-size-specified-by-create-database"></a>A. Reduzieren Sie das Transaktionsprotokoll auf die ursprüngliche von CREATE DATABASE angegebene Größe.  
Angenommen, das Transaktionsprotokoll für die Adressdatenbank wurde bei der Erstellung der Adressdatenbank auf 100 MB festgelegt. D.h., die CREATE DATABASE-Anweisung für Adressen entspricht LOG_SIZE = 100 MB. Jetzt hat die Größe des Protokolls allerdings 150 MB erreicht und Sie möchten diese wieder auf 100 MB reduzieren.
  
Sie können eine der folgenden Anweisungen verwenden, um zu versuchen, das Transaktionsprotokoll der Adressdatenbank auf seine Standardgröße von 100 MB zu verkleinern. Wenn das Verkleinern des Protokolls auf 100 MB zu Datenverlusten führen würde, verkleinert DBCC SHRINKLOG es so weit wie möglich auf eine Größe von mehr als 100 MB, wobei jedoch keine Daten verloren gehen.
  
```sql
USE Addresses;  
DBCC SHRINKLOG ( SIZE = 100 MB );  
DBCC SHRINKLOG ( SIZE = DEFAULT );  
DBCC SHRINKLOG;  
```  
  
  
