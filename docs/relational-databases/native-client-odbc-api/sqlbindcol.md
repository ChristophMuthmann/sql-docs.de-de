---
title: SQLBindCol | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLBindCol function
ms.assetid: fbd7ba20-d917-4ca9-b018-018ac6af9f98
caps.latest.revision: 39
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3dce23669637b9fd39e9fa84d37600bae6e64f98
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlbindcol"></a>SQLBindCol
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  In der Regel sollten Sie die Auswirkungen der Verwendung von **SQLBindCol** zur Datenkonvertierung. Bindungskonvertierungen sind Clientprozesse. Wenn Sie beispielsweise einen Gleitkommawert, der an eine Zeichenspalte gebunden ist, abrufen, führt der Treiber die Gleitkomma-in-Zeichen-Konvertierung lokal durch, wenn eine Zeile abgerufen wird. Die [!INCLUDE[tsql](../../includes/tsql-md.md)] CONVERT-Funktion kann zum Übertragen der Kosten einer Datenkonvertierung auf den Server verwendet werden.  
  
 Eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann mehrere Sets an Ergebniszeilen bei einer einzelnen Anweisungsausführung zurückgeben. Jedes Resultset muss getrennt gebunden sein. Weitere Informationen zum Binden für mehrere Resultsets finden Sie unter [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md).  
  
 Der Entwickler kann Spalten binden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-spezifischen C-Datentypen mithilfe der *TargetType* Wert **SQL_C_BINARY**. An [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-spezifische Typen gebundene Spalten sind nicht übertragbar. Die definierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-spezifischen ODBC-C-Datentypen entsprechen den Typdefinitionen für DB-Library, und DB-Library-Entwickler, die Anwendungen übertragen, können diese Funktion nutzen.  
  
 Berichterstattung über die datenabschneidung ist ein kostengünstiger Prozess für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber. Sie können das Abschneiden vermeiden, indem Sie sicherstellen, dass alle gebundenen Datenpuffer weit genug sind, um Daten zurückzugeben. Bei Zeichendaten sollte die Breite ausreichend Platz für ein Zeichenfolgeabschlusszeichen bieten, wenn das Standardtreiberverhalten für den Zeichenfolgenabschluss verwendet wird. Binden Sie z. B. eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char(5)** Spalte in ein Array mit fünf Zeichen Abschneidung jedes abgerufenen Werts. Wenn Sie die gleiche Spalte an ein Array mit sechs Zeichen binden, wird die Abschneidung vermieden, indem ein Zeichenelement bereitgestellt wird, in dem das Null-Abschlusszeichen gespeichert werden soll. [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) können verwendet werden, um lange Zeichenfolgen und binäre Daten ohne Abschneidung effizient abzurufen.  
  
 Für große Datenwerttypen, wenn der Benutzer bereitgestellte Puffer nicht groß genug für den gesamten Wert der Spalte, ist **SQL_SUCCESS_WITH_INFO** wird zurückgegeben, und die "Zeichenfolgendaten; rechts abgeschnitten"Warnung wird ausgegeben. Die **StrLen_or_IndPtr** Argument wird die Anzahl der im Puffer gespeicherten Zeichen/Bytes enthalten.  
  
## <a name="sqlbindcol-support-for-enhanced-date-and-time-features"></a>SQLBindCol-Unterstützung für verbesserte Funktionen für Datum/Uhrzeit  
 Ergebnisspaltenwerte von Datum-/Uhrzeit-Typen werden konvertiert, wie in beschrieben [Konvertierungen von SQL-in C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md). Beachten Sie, dass zum Abrufen von Time und Datetimeoffset-Spalten als entsprechenden Strukturen (**SQL_SS_TIME2_STRUCT** und **sql_ss_timestampoffset_struct-Wert**), *TargetType*muss angegeben werden, als **SQL_C_DEFAULT** oder **SQL_C_BINARY**.  
  
 Weitere Informationen finden Sie unter [Datum und Uhrzeit-Verbesserungen & #40; ODBC & #41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlbindcol-support-for-large-clr-udts"></a>SQLBindCol-Unterstützung für große CLR-UDTs  
 **SQLBindCol** unterstützt große CLR-benutzerdefinierte Typen (UDTs). Weitere Informationen finden Sie unter [Large CLR User-Defined Datentypen & #40; ODBC & #41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLBindCol-Funktion](http://go.microsoft.com/fwlink/?LinkId=59327)   
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
