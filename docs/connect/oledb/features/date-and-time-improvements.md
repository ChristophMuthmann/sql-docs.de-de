---
title: Datum und Uhrzeit-Verbesserungen | Microsoft Docs
description: Datum und Uhrzeit-Verbesserungen in OLE DB-Treiber für SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2d6b287b7cf96ec91ce776dd65bcec01e8c777a1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="date-and-time-improvements"></a>Datum und Uhrzeit-Verbesserungen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  In diesem Thema wird beschrieben, die OLE DB-Treiber für SQL Server-Unterstützung für das Datum und Uhrzeit-Datentypen, die in hinzugefügt wurden [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  
  
 Weitere Informationen zu den Datum/Uhrzeit-Verbesserungen finden Sie unter [Datum und Uhrzeit-Verbesserungen &#40;OLE DB-&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md).  
  
 Informationen zu Beispielanwendungen, die diese Funktion veranschaulichen, finden Sie unter [Programmierbeispiele für SQL Server-Daten](http://msftdpprodsamples.codeplex.com/).  
  
## <a name="usage"></a>Verwendung  
 In den folgenden Abschnitten werden verschiedene Methoden zur Verwendung der neuen Datums- und Uhrzeittypen beschrieben.  
  
### <a name="use-date-as-a-distinct-data-type"></a>Verwenden von 'Date' als eindeutigen Datentyp  
 Beginnend mit [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], verbesserte Unterstützung für Datum/Uhrzeit-Typen ist es effizienter, die DBTYPE_DBDATE OLE DB-Typ zu verwenden.  
  
### <a name="use-time-as-a-distinct-data-type"></a>Verwenden von 'Time' als eindeutigen Datentyp  
 OLE DB verfügt bereits über einen Datentyp, der nur die Zeit enthält: DBTYPE_DBTIME, der die Zeit mit einer Genauigkeit von 1 Sekunde angibt.
  
 Die neue [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Zeitdatentyp verfügt über Dezimalstellen Genauigkeit von bis zu 100 Nanosekunden. Dies erfordert einen neuen Typ in OLE DB-Treiber für SQL Server: DBTYPE_DBTIME2. Vorhandene Anwendungen, in denen Zeitdaten nicht in Sekundenbruchteilen angegeben werden, können time(0)-Spalten verwenden. Die vorhandenen OLE DB DBTYPE_TIME-Typ und die entsprechenden Strukturen sollten richtig funktionieren, es sei denn, die Anwendungen von den in den Metadaten zurückgegebenen Typ abhängig sind.  
  
### <a name="use-time-as-a-distinct-data-type-with-extended-fractional-seconds-precision"></a>Verwenden von 'Time' als eindeutigen Datentyp mit einer Genauigkeit in Sekundenbruchteilen  
 Einige Anwendungen, z. B. in der Fertigung und Prozesssteuerung, erfordern die Fähigkeit, Zeitdaten mit einer Genauigkeit von bis zu 100 Nanosekunden zu verarbeiten. Neuer Typ zu diesem Zweck in der OLE DB ist DBTYPE_DBTIME2.  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision"></a>Verwenden von 'Datetime' mit einer Genauigkeit in Sekundenbruchteilen  
 OLE DB definiert bereits einen Typ mit einer Genauigkeit von bis zu 1 Nanosekunde. Dieser Typ wird jedoch bereits verwendet, von vorhandenen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] und solche Anwendungen erwarten von nur 1/300 einer zweiten Genauigkeit. Der neue **datetime2(3)** -Typ ist nicht direkt kompatibel mit dem vorhandenen datetime-Typ. Wenn das Risiko besteht, dass sich dies auf das Verhalten der Anwendung auswirkt, müssen Anwendungen das neue DBCOLUMN-Flag zur Bestimmung des tatsächlichen Servertyps verwenden.    
  
### <a name="use-datetime-with-extended-fractional-seconds-precision-and-timezone"></a>Verwenden von 'Datetime' mit einer Genauigkeit in Sekundenbruchteilen und Zeitzoneninformationen  
 Einige Anwendungen erfordern datetime-Werte mit Zeitzoneninformationen. Dies wird durch den neuen DBTYPE_DBTIMESTAMPOFFSET Typ unterstützt.
  
### <a name="use-datetimedatetimedatetimeoffset-data-with-client-side-conversions-consistent-with-existing-conversions"></a>Verwenden von 'Date'-/'Time'-/'Datetime'-/'Datetimeoffset'-Daten mit clientseitigen Konvertierungen in Übereinstimmung mit vorhandenen Konvertierungen  
 Die Konvertierungen werden erweitert, konsistent, Konvertierungen zwischen allen Datums- und Uhrzeittypen in eingeführt einzuschließen [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Siehe auch  
 [OLE DB-Treiber für SQL Server-Features](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
