---
title: Importieren von Daten aus früheren SQL Server-Versionen im nativen Format oder im Zeichenformat | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: import-export
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- earlier versions [SQL Server], import and export data formats
- -V switch
- data formats [SQL Server], earlier versions
- previous versions [SQL Server], import and export data formats
ms.assetid: e644696f-9017-428e-a5b3-d445d1c630b3
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e37b412b3cbb435c6e037472b6286ac3261039b1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="import-native-and-character-format-data-from-earlier-versions-of-sql-server"></a>Importieren von Daten aus früheren SQL Server-Versionen im systemeigenen Format oder im Zeichenformat
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Sie können [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]bcp **in** verwenden, um Daten im nativen Format oder im Zeichenformat mithilfe des Schalters [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]-V [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]aus [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , **oder** zu importieren. Der Schalter **-V** veranlasst [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , Datentypen aus der angegebenen früheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zu verwenden. Zudem entspricht das Datendateiformat dem Format dieser früheren Version.  
  
 Um eine frühere Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für eine Datendatei anzugeben, verwenden Sie den Schalter **-V** mit einem der folgenden Qualifizierer:  
  
|SQL Server-Version|Qualifizierer|  
|------------------------|---------------|  
|[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]|**-V80**|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|**-V90**|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|**-V100**|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|**-V 110**|  
  
## <a name="interpretation-of-data-types"></a>Interpretation von Datentypen  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höhere Versionen bieten Unterstützung für einige neue Typen. Beim Importieren eines neuen Datentyps aus einer früheren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , muss der Dateityp in einem Format gespeichert sein, das von den älteren **bcp** -Clients gelesen werden kann. In der folgenden Tabelle finden Sie eine Übersicht, wie die neuen Datentypen konvertiert werden, damit sie mit den früheren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]kompatibel sind.  
  
|Neue Datentypen in SQL Server 2005|Kompatible Datentypen in Version 6*x*|Kompatible Datentypen in Version 70|Kompatible Datentypen in Version 80|  
|---------------------------------------|-------------------------------------------|-----------------------------------------|-----------------------------------------|  
|**bigint**|**decimal**|**decimal**|*|  
|**sql_variant**|**text**|**nvarchar(4000)**|*|  
|**varchar(max)**|**text**|**text**|**text**|  
|**nvarchar(max)**|**ntext**|**ntext**|**ntext**|  
|**varbinary(max)**|**image**|**image**|**image**|  
|XML|**ntext**|**ntext**|**ntext**|  
|UDT**|**image**|**image**|**image**|  
  
 *Dieser Typ wird nativ unterstützt.  
  
 **UDT gibt einen benutzerdefinierten Typ an.  
  
## <a name="exporting-using-v-80"></a>Exportieren mit –V 80  
 Bei einem Massenexport von Daten mithilfe des **–V80** -Schalters werden Daten vom Typ **nvarchar(max)**, **varchar(max)**, **varbinary(max)**, XML und UDT – wie Daten vom Typ **text**, **image**und **ntext** – anstatt mit einem 8-Byte-Präfix mit einem 4-Byte-Präfix im einheitlichen Modus gespeichert. Dies ist der Standardwert für [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höhere Versionen.  
  
## <a name="copying-date-values"></a>Kopieren von Datumswerten  
 Von**bcp** wird die ODBC-API für das Massenkopieren verwendet. Deshalb verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]bcp **zum Importieren von Datumswerten in** das ODBC-Datumsformat (*jjjj-mm-tt hh:mm:ss*[*.f...*]).  
  
 Der Befehl **bcp** exportiert Datendateien im Zeichenformat immer mithilfe des ODBC-Standardformats für **datetime** - und **smalldatetime** -Werte. So wird beispielsweise eine **datetime** -Spalte mit dem Datum `12 Aug 1998` beim Massenkopieren in eine Datendatei als Zeichenfolge `1998-08-12 00:00:00.000`übertragen.  
  
> [!IMPORTANT]  
>  Achten Sie beim Importieren von Daten mit **bcp** in ein **smalldatetime**-Feld darauf, dass der Wert für Sekunden 00.000 ist; andernfalls ruft der Vorgang einen Fehler hervor. Der **smalldatetime** -Datentyp kann nur Werte beinhalten, die auf die volle Minute gerundet sind. BULK INSERT und INSERT ... SELECT * FROM OPENROWSET(BULK...) schlagen in diesem Fall nicht fehl, schneiden jedoch den Sekundenwert ab.  
  
##  <a name="RelatedTasks"></a> Verwandte Aufgaben  
 **So verwenden Sie Datenformate für Massenimport oder Massenexport**  
  
-   [Verwenden des Zeichenformats zum Importieren und Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Verwenden des nativen Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Verwenden des Unicode-Zeichenformats zum Importieren und Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Verwenden des nativen Unicode-Formats zum Importieren oder Exportieren von Daten &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Abwärtskompatibilität des SQL Server-Datenbankmoduls](../../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
