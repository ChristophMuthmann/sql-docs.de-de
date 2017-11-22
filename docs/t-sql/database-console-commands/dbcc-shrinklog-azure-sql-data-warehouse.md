---
title: DBCC SHRINKLOG (Azure SQL Datawarehouse) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
caps.latest.revision: "11"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e2561b5658e87e2d33f4ccd7649ede7d7fa2857d
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="dbcc-shrinklog-azure-sql-data-warehouse"></a>DBCC SHRINKLOG (Azure SQL Datawarehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Reduziert die Größe des Transaktionsprotokolls *über die Appliance* für den aktuellen [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Datenbank. Die Daten werden zum Verkleinern des Transaktionsprotokolls defragmentiert. Im Laufe der Zeit kann das Transaktionsprotokoll der Datenbank ineffizienten werden. Verwenden Sie DBCC SHRINKLOG Fragmentierung und Verringern der Protokollgröße.
  
![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Syntax  
  
```sql
DBCC SHRINKLOG   
    [ ( SIZE = { target_size [ MB | GB | TB ]  } | DEFAULT ) ]   
    [ WITH NO_INFOMSGS ]   
[;]  
```  
  
## <a name="arguments"></a>Argumente  
Größe = { *Target_size* [MB | **GB** | TB]} | **Standard**.  
*Target_size* wird die gewünschte Größe für das Transaktionsprotokoll in allen Compute-Knoten, wenn DBCC SHRINKLOG abgeschlossen sind. Es ist eine ganze Zahl größer als 0.  
Die Größe wird in Megabyte (MB), Gigabyte (GB) oder Terabyte (TB) gemessen. Es ist die Gesamtgröße des Transaktionsprotokolls auf allen der Serverknoten.  
Standardmäßig reduziert DBCC SHRINKLOG das Transaktionsprotokoll auf die Protokollgröße in den Metadaten für die Datenbank gespeichert. Die Protokollgröße in den Metadaten richtet sich nach den LOG_SIZE-Parameter im [CREATE DATABASE &#40; Azure SQL Datawarehouse &#41; ](../../t-sql/statements/create-database-azure-sql-data-warehouse.md) oder [ALTER DATABASE &#40; Azure SQL Datawarehouse &#41; ](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md). DBCC SHRINKLOG reduziert die Größe des Transaktionsprotokolls auf den Standardwert bei Größe `SIZE=DEFAULT` angegeben wird, oder wenn die `SIZE` -Klausel weggelassen.
  
WITH NO_INFOMSGS  
Informationsmeldungen sind nicht in den Ergebnissen DBCC SHRINKLOG angezeigt.  
  
## <a name="permissions"></a>Berechtigungen  
Erfordert die ALTER SERVER STATE-Berechtigung.
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
DBCC SHRINKLOG ändert nicht die Protokollgröße in den Metadaten für die Datenbank gespeichert. Die Metadaten wird weiterhin der LOG_SIZE-Parameter enthalten, der in der CREATE DATABASE- oder ALTER DATABASE-Anweisung angegeben wurde.
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Beispiele: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] und[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-shrink-the-transaction-log-to-the-original-size-specified-by-create-database"></a>A. Verkleinern des Transaktionsprotokolls auf die ursprüngliche Dateigröße, die durch CREATE DATABASE angegeben.  
Nehmen Sie an, dass das Transaktionsprotokoll für die Adressen Datenbank auf 100 MB festgelegt wurde, während der Erstellung der Datenbank Adressen. Die CREATE DATABASE-Anweisung für Adressen hatte, also LOG_SIZE = 100 MB. Nehmen Sie nun an das Protokoll 150 MB erreicht hat und er wieder auf 100 MB verkleinert werden soll.
  
Jede der folgenden Anweisungen wird versucht, das Transaktionsprotokoll für die Datenbank Adressen auf die Standardgröße von 100 MB zu verkleinern. Wenn Verkleinerung des Protokolls auf 100 MB Datenverlust verursacht wird, wird DBCC SHRINKLOG das Protokoll ohne Verlust von Daten an die kleinste Größe möglichen, der größer als 100 MB verkleinert.
  
```sql
USE Addresses;  
DBCC SHRINKLOG ( SIZE = 100 MB );  
DBCC SHRINKLOG ( SIZE = DEFAULT );  
DBCC SHRINKLOG;  
```  
  
  
