---
title: Datum und Uhrzeit-Verbesserungen (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- date/time [ODBC]
- ODBC, date/time improvements
ms.assetid: e31d5ca5-2103-498f-954c-1ee93e217186
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 75eb2438dabb3d304158e524e7413df35ae9a8fc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="date-and-time-improvements-odbc"></a>Datum und Uhrzeit-Verbesserungen (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] wurden neue Datums- und Uhrzeitdatentypen eingeführt. In diesem Abschnitt wird beschrieben, wie diese neuen Typen als Erweiterungen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client verfügbar gemacht werden. Eine Übersicht über [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client unterstützten neuen Datums- und Uhrzeitdatentypen finden Sie unter [Datum und Uhrzeit-Verbesserungen](../../relational-databases/native-client/features/date-and-time-improvements.md). Ein Beispiel, ODBC-Datum/Uhrzeit-Unterstützung, finden Sie unter [Verwenden von Datums- und Uhrzeittypen](../../relational-databases/native-client-odbc-how-to/use-date-and-time-types.md).  
  
 Weitere allgemeine Informationen zu Datum und Uhrzeit-Datentypen finden Sie unter ["DateTime" &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Datentypunterstützung für ODBC-Verbesserungen bei Datum und Uhrzeit](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)  
 Liefert Informationen über ODBC-Typen, die Datums- und Uhrzeitdatentypen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützen.  
  
 [Metadaten &#40;ODBC&#41;](http://msdn.microsoft.com/library/99133efc-b1f2-46e9-8203-d90c324a8e4c)  
 Beschreibt, in der Implementierung Parameter (Descriptor, IPD) und Implementierung Zeile deskriptorfelder (IRD), sowie zurückgegebene Spaltenmetadaten zurückgegebenen Informationen **SQLColumns** und **SQLProcedureColumns**. Beschreibt außerdem zurückgegebene datentypmetadaten **SQLGetTypeInfo**.  
  
 [DateTime-Datentypkonvertierungen &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-odbc.md)  
 Beschreibt die Konvertierung zwischen datetime- und datetimeoffset-Werten.  
  
 [sql_variant-Unterstützung für Datum- und Uhrzeit-Typen](../../relational-databases/native-client-odbc-date-time/sql-variant-support-for-date-and-time-types.md)  
 Beschreibt die Unterstützung der SQL_VARIANT-Funktion für die verbesserte Datums- und Uhrzeitfunktionalität.  
  
 [Massenkopieren Kopie Änderungen für die verbesserte Datums- und Uhrzeittypen &#40;OLE DB- und ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 Beschreibt Datums-/Uhrzeitverbesserungen zur Unterstützung von Massenkopiervorgängen.  
  
 [Verbesserte Datums- und Uhrzeitangabe geben Verhalten bei früheren Versionen von SQL Server &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/enhanced-date-and-time-type-behavior-with-previous-sql-server-versions-odbc.md)  
 Beschreibt das erwartete Verhalten, bei der Kommunikation von einer Clientanwendung mithilfe der verbesserte Datums- und Uhrzeitfunktionen mit einer älteren Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und wenn ein Client mit einer älteren Version von kompiliert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client sendet Befehle an einen Server, die unterstützt erweiterte Funktionen für Datum und Uhrzeit.  
  
 [ODBC API-Unterstützung für verbesserte Funktionen für Datum und Uhrzeit](../../relational-databases/native-client-odbc-date-time/odbc-api-support-for-enhanced-date-and-time-features.md)  
 Listet die ODBC-Funktionen auf, die die verbesserte Datums- und Uhrzeitfunktionalität unterstützen.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Native Client & #40; ODBC & #41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
