---
title: Bcp_gettypename | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: bcp_gettypename
apilocation: sqlncli11.dll
apitype: DLLExport
helpviewer_keywords: bcp_gettypename function
ms.assetid: 65f036d1-f60e-4b8a-97b3-76fccf0dfed4
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8f452b3c5e12b76ba2d1327b59f1cfa17f16bb46
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="bcpgettypename"></a>bcp_gettypename
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Gibt den SQL-Typnamen für ein angegebenes BCP-Typtoken zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RETCODE bcp_gettypename (  
        INT token,  
        DBBOOL fIsMaxType);  
```  
  
## <a name="arguments"></a>Argumente  
 *Token*  
 Ein Wert, der ein BCP-Typtoken angibt.  
  
 *Feld*  
 Gibt an, wenn ein angefordertes Token ein max-Typ ist.  
  
## <a name="returns"></a>Rückgabewert  
 Eine Zeichenfolge, die den SQL-Typnamen enthält, der dem BCP-Typ entspricht. Wenn ein ungültiger BCP-Typ angegeben wird, wird eine leere Zeichenfolge zurückgegeben.  
  
## <a name="remarks"></a>Hinweise  
 Die BCP-Typtoken werden in der sqlncli.h-Headerdatei und der sqlncli11.lib-Bibliothek definiert.  
  
 In der unten stehenden Tabelle werden die möglichen BCP-Typen aufgeführt, mit der Angabe, ob es sich um max-Typen handelt, sowie deren erwartete Ausgabe.  
  
|BCP-Typname|MaxType|Ausgabe|  
|-------------------|-------------|------------|  
|**SQLDECIMAL**|Sowohl als auch|**decimal**|  
|**SQLNUMERIC**|Sowohl als auch|**numeric**|  
|**SQLINT1**|Sowohl als auch|**tinyint**|  
|**SQLINT2 VERWENDEN**|Sowohl als auch|**smallint**|  
|**SQLINT4**|Sowohl als auch|**int**|  
|**SQLMONEY**|Sowohl als auch|**money**|  
|**SQLFLT8**|Sowohl als auch|**float**|  
|**SQLDATETIME**|Sowohl als auch|**datetime**|  
|**SQLBITN**|Sowohl als auch|**Bit-null**|  
|**SQLBIT**|Sowohl als auch|**bit**|  
|**SQLBIGCHAR**|Nein|**char**|  
|**SQLCHARACTER**|Nein|**char**|  
|**SQLBIGVARCHAR**|Nein|**varchar**|  
|**SQLVARCHAR**|Nein|**varchar**|  
|**SQLTEXT**|Sowohl als auch|**text**|  
|**SQLBIGBINARY**|Nein|**binary**|  
|**SQLBINARY**|Nein|**Binär (Binary)**|  
|**SQLBIGVARBINARY**|Nein|**Varbinary**|  
|**SQLVARBINARY**|Nein|**Varbinary**|  
|**SQLIMAGE**|Sowohl als auch|**Bild**|  
|**SQLINTN**|Sowohl als auch|**Int-null**|  
|**SQLDATETIMN**|Sowohl als auch|**"DateTime" null**|  
|**SQLMONEYN**|Sowohl als auch|**Money-null**|  
|**SQLFLTN**|Sowohl als auch|**Null, "float"**|  
|**SQLAOPSUM**|Sowohl als auch|**Sum**|  
|**SQLAOPAVG**|Sowohl als auch|**Avg**|  
|**SQLAOPCNT**|Sowohl als auch|**Count**|  
|**SQLAOPMIN**|Sowohl als auch|**Min**|  
|**SQLAOPMAX**|Sowohl als auch|**Max**|  
|**SQLDATETIM4**|Sowohl als auch|**smalldatetime**|  
|**SQLMONEY4**|Sowohl als auch|**Smallmoney**|  
|**SQLFLT4**|Sowohl als auch|**Echte**|  
|**SQLUNIQUEID**|Sowohl als auch|**uniqueidentifier**|  
|**SQLNCHAR**|Nein|**NCHAR**|  
|**SQLNVARCHAR**|Nein|**Nvarchar**|  
|**SQLNTEXT**|Sowohl als auch|**Ntext**|  
|**SQLVARIANT**|Sowohl als auch|**sql_variant**|  
|**SQLINT8**|Sowohl als auch|**Bigint**|  
|**SQLCHARACTER**|ja|**varchar(max)**|  
|**SQLBIGCHAR**|ja|**varchar(max)**|  
|**SQLBIGVARCHAR**|ja|**varchar(max)**|  
|**SQLVARCHAR**|ja|**varchar(max)**|  
|**SQLBINARY**|ja|**varbinary(max)**|  
|**SQLBIGBINARY**|ja|**varbinary(max)**|  
|**SQLBIGVARBINARY**|ja|**varbinary(max)**|  
|**SQLVARBINARY**|ja|**varbinary(max)**|  
|**SQLNCHAR**|ja|**nvarchar(max)**|  
|**SQLNVARCHAR**|ja|**nvarchar(max)**|  
|**SQLXML**|ja|**Xml**|  
|**SQLUDT**|Sowohl als auch|**UDT**|  
  
## <a name="bcpgettypename-support-for-enhanced-date-and-time-features"></a>bcp_gettypename-Unterstützung für erweiterte Funktionen für Datum und Uhrzeit  
 Die tokenparameterwerte für Datums-/Uhrzeittypen werden in der Spalte "Typ in sqlncli.h" der Tabelle in beschrieben [Massenkopieränderungen für erweiterte Datums- und Uhrzeittypen &#40; OLE DB und ODBC &#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md). Der zurückgegebene Wert ist in der entsprechenden Zeile der Spalte "Dateispeichertyp" angegeben.  
  
 Weitere Informationen finden Sie unter [Datum und Uhrzeit-Verbesserungen &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen zum Massenkopieren](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
