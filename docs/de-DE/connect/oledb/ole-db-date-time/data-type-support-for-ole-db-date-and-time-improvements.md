---
title: Datentypunterstützung für OLE DB-Datum und Uhrzeit-Verbesserungen | Microsoft Docs
description: Datentypunterstützung für OLE DB-Datum und Uhrzeit-Verbesserungen
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], data type support
- OLE DB, date/time improvements
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 73695c6149b48b957475b1b9f779c3226db87691
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="data-type-support-for-ole-db-date-and-time-improvements"></a>Datentypunterstützung für OLE DB-Datum und Uhrzeit-Verbesserungen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Dieser Artikel enthält Informationen zu OLE DB (OLE DB-Treiber für SQL Server) Datentypen, unterstützen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Datum/Uhrzeit-Datentypen.  
  
## <a name="data-type-mapping-in-rowsets-and-parameters"></a>Datentypzuordnung zu Rowsets und Parametern  
 OLE DB stellt zwei neue Datentypen bereit, um die neuen Servertypen zu unterstützen: DBTYPE_DBTIME2 und DBTYPE_DBTIMESTAMPOFFSET. Die folgende Tabelle zeigt die vollständige Servertypzuordnung:  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datentyp|OLE DB-Datentyp|Wert|  
|-----------------------------------------|----------------------|-----------|  
|datetime|DBTYPE_DBTIMESTAMP|135 (oledb.h)|  
|smalldatetime|DBTYPE_DBTIMESTAMP|135 (oledb.h)|  
|Datum|DBTYPE_DBDATE|133 ("OleDb.h")|  
|Uhrzeit|DBTYPE_DBTIME2|145 (msoledbsql.h)|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|146 (msoledbsql.h)|  
|datetime2|DBTYPE_DBTIMESTAMP|135 (oledb.h)|  
  
## <a name="data-formats-strings-and-literals"></a>Datenformate: Zeichenfolgen und Literale  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datentyp|OLE DB-Datentyp|Zeichenfolgenformat für Clientkonvertierungen|  
|-----------------------------------------|----------------------|------------------------------------------|  
|datetime|DBTYPE_DBTIMESTAMP|'yyyy-mm-dd hh:mm:ss[.999]'<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützt bis zu drei Sekundenbruchteilziffern für Datetime.|  
|smalldatetime|DBTYPE_DBTIMESTAMP|'yyyy-mm-dd hh:mm:ss'<br /><br /> Dieser Datentyp weist die Genauigkeit von einer Minute. Die zweite Komponente ist 0 (null) auf Ausgabe und wird auf Eingabe vom Server gerundet.|  
|Datum|DBTYPE_DBDATE|'yyyy-mm-dd'|  
|Uhrzeit|DBTYPE_DBTIME2|'hh:mm:ss[.9999999]'<br /><br /> Sekundenbruchteile können optional mit bis zu sieben Ziffern angegeben werden.|  
|datetime2|DBTYPE_DBTIMESTAMP|'yyyy-mm-dd hh:mm:ss[.fffffff]'<br /><br /> Sekundenbruchteile können optional mit bis zu sieben Ziffern angegeben werden.|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|'yyyy-mm-dd hh:mm:ss[.fffffff] +/-hh:mm'<br /><br /> Sekundenbruchteile können optional mit bis zu sieben Ziffern angegeben werden.|  
  
 Für Datums-/Uhrzeitliterale gibt es keine Änderungen der Escapesequenzen.  
  
 Sekundenbruchteile in Ergebnissen verwenden immer einen Punkt (.) anstelle eines Doppelpunkts (:).  
  
 An Anwendungen zurückgegebene Zeichenfolgenwerte haben immer die gleiche Länge für eine bestimmte Spalte. Die Komponenten Jahr, Monat, Tag, Stunde, Minute und Sekunde werden mit führenden Nullen bis zur maximalen Breite aufgefüllt. Zwischen Datum und Uhrzeit und zwischen Zeit und Zeitzonenoffset ist jeweils genau eine Leerstelle. Ein Zeitzonenoffset wird immer mit einem Zeichen eingeleitet. Dieses Zeichen ist ein Plus (+), wenn der Offset 0 (null) ist. Es gibt keine Leerstellen zwischen dem Zeichen und dem Offsetwert. Sekundenbruchteile werden bei Bedarf bis zur definierten Genauigkeit für die Spalte mit nachfolgenden Nullen aufgefüllt, jedoch nicht weiter. Für Datetime-Spalten werden drei Ziffern für Sekundenbruchteile. Für smalldatetime-Spalten gibt es, keine Ziffern für Sekundenbruchteile und die Sekunden sind immer 0 (null).  
  
 Konvertierungen aus Zeichenfolgenwerten, die von der Anwendung bereitgestellt werden, sind flexibler und erlauben Komponentenwerte, die unter der maximalen Breite liegen. Jahre können aus 1-4 Ziffern bestehen. Monate, Tage, Stunden, Minuten und Sekunden können 1 oder 2 Ziffern haben. Es kann beliebig viele Leerstellen zwischen Datum-/Uhrzeit und Zeit-/Zeitzonenoffsets geben. Das Zeichen eines Offsets mit 0 (null) Stunden und 0 (null) Minuten kann Plus oder Minus sein. Nachfolgende Nullen sind bis zu einem Maximum von 9 Ziffern für Sekundenbruchteile zugelassen. Eine Zeitkomponente kann mit einem Dezimaltrennzeichen und keinen Ziffern für Sekundenbruchteile enden.  
  
 Eine leere Zeichenfolge ist kein gültiges Datum-/Uhrzeitliteral und stellt keinen NULL-Wert dar. Der Versuch, eine leere Zeichenfolge in einen Datum-/Uhrzeitwert zu konvertieren, führt Fehlern mit SQLSTATE 22018 und der Meldung „Ungültiger Zeichenwert für Konvertierungsangabe“.  
  
## <a name="data-formats-data-structures"></a>Datenformate: Datenstrukturen  
 In der unten beschriebenen OLE DB-spezifischen Strukturen entspricht OLE DB die folgenden Einschränkungen. Diese werden vom gregorianischen Kalender genommen:  
  
-   Der Bereich für den Monat liegt zwischen 1 und 12.  
  
-   Der Bereich für das Tagfeld liegt zwischen 1 und der Anzahl Tage in dem Monat und muss mit den Feldern für Jahr und Monat konsistent sein unter Berücksichtigung von Schaltjahren.  
  
-   Der Bereich für die Stunden liegt zwischen 0 und 23.  
  
-   Der Bereich für die Minuten liegt zwischen 0 und 59.  
  
-   Der Bereich für die Sekunden liegt zwischen 0 und 59. Es sind bis zu zwei Schaltsekunden erlaubt, um die Synchronisierung mit der Sideralzeit zu gewährleisten.  
  
 Implementierungen für die folgenden bestehenden OLE DB-Strukturen wurden geändert, um die Unterstützung der neuen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datum-/Uhrzeitdatentypen sicherzustellen. Die Definitionen haben sich jedoch nicht geändert.  
  
-   DBTYPE_DATE (Dies ist ein Automatisierung-DATE-Typ. Wird intern als eine **doppelte**... Der ganzzahlige Teil gibt die Anzahl von Tagen seit dem 30. Dezember 1899 wieder und der Bruchteil den Teil eines Tages. Dieser Typ hat eine Genauigkeit von 1 Sekunde und hat daher eine effektive Dezimalstelle von 0.)  
  
-   DBTYPE_DBDATE  
  
-   DBTYPE_DBTIME  
  
-   DBTYPE_DBTIMESTAMP (das Bruchteilfeld wird von OLE DB als der milliardste Teil einer Sekunde (Nanosekunde) definiert, und der gültige Bereich liegt zwischen 0-999.999.999)  
  
-   DBTYPE_FILETIME  
  
### <a name="dbtypedbtime2"></a>DBTYPE_DBTIME2  
 Diese Struktur wird auf beiden Betriebssystemen (32 Bit und 64 Bit) bis 12 Byte aufgefüllt.  
  
```  
typedef struct tagDBTIME2 {  
    USHORT hour;  
    USHORT minute;  
    USHORT second;  
    ULONG fraction;  
    } DBTIME2;  
```  
  
### <a name="dbtype-dbtimestampoffset"></a>DBTYPE_ DBTIMESTAMPOFFSET  
  
```  
typedef struct tagDBTIMESTAMPOFFSET {  
    SHORT year;  
    USHORT month;  
    USHORT day;  
    USHORT hour;  
    USHORT minute;  
    USHORT second;  
    ULONG fraction;  
    SHORT timezone_hour;  
    SHORT timezone_minute;  
    } DBTIMESTAMPOFFSET;  
```  
  
 Wenn `timezone_hour` negativ ist, `timezone_minute` muss negativ oder 0 (null). Wenn `timezone_hour` positiv ist, `timezone minute` muss positiv sein oder 0 (null). Wenn `timezone_hour` 0 (null) ist, kann `timezone minute` einen Wert zwischen -59 und +59 haben.  
  
### <a name="ssvariant"></a>SSVARIANT  
 Dieses struct enthält jetzt die neuen Strukturen DBTYPE_DBTIME2 und DBTYPE_DBTIMESTAMPOFFSET und fügt Sekundenbruchteile für entsprechende Typen hinzu.  
  
```  
struct SSVARIANT {  
   SSVARTYPE vt;  
   DWORD dwReserved1;  
   DWORD dwReserved2;  
   union {  
// ...  
      DBTIMESTAMP tsDateTimeVal;  
      DBDATE dDateVal;  
      struct _Time2Val {  
         DBTIME2 tTime2Val;  
         BYTE bScale;  
      } Time2Val;  
      struct _DateTimeVal {  
         DBTIMESTAMP tsDateTimeVal;  
         BYTE bScale;  
      } DateTimeVal;  
      struct _DateTimeOffsetVal {   
         DBTIMESTAMPOFFSET tsoDateTimeOffsetVal;  
         BYTE bScale;  
      } DateTimeOffsetVal;  
// ...  
   };  
};  
```  
  
 Ferner wird die Enumeration, die dem SSVARIANT-Typ zugewiesen ist und den Enumerationstyp bestimmt, folgendermaßen erweitert:  
  
```  
enum SQLVARENUM {  
// ...  
   // Datetime  
   VT_SS_DATETIME      = DBTYPE_DBTIMESTAMP,  
   VT_SS_SMALLDATETIME = 206,  
  
   VT_SS_DATE = DBTYPE_DBDATE,  
   VT_SS_TIME2 = DBTYPE_DBTIME2,  
   VT_SS_DATETIME2 = 212  
   VT_SS_DATETIMEOFFSET = DBTYPE_DBTIMESTAMPOFFSET  
};  
```  
  
 Anwendungen, die Migration zu OLE DB-Treiber für SQL Server, mit denen **Sql_variant** und basieren auf der eingeschränkten Genauigkeit von **"DateTime"** müssen aktualisiert werden, wenn das zugrunde liegende Schema aktualisiert wird, um verwenden**datetime2** statt **"DateTime"**.  
  
 Die Zugriffsmakros für SSVARIANT wurden durch Hinzufügen von Folgendem ebenfalls erweitert:  
  
```  
#define V_SS_DATETIME2(X)       V_SS_UNION(X, DateTimeVal)  
#define V_SS_TIME2(X)           V_SS_UNION(X, Time2Val)  
#define V_SS_DATE(X)            V_SS_UNION(X, dDateVal)  
#define V_SS_DATETIMEOFFSET(X)  V_SS_UNION(X, DateTimeOffsetVal)  
```  
  
## <a name="data-type-mapping-in-itabledefinitioncreatetable"></a>Datentypzuordnung zu ITableDefinition::CreateTable  
 Die folgende Typzuordnung wird mit DBCOLUMNDESC-Strukturen, die von itabledefinition:: CreateTable verwendeten verwendet:  
  
|OLE DB-Datentyp (*wType*)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datentyp|Hinweise|  
|----------------------------------|-----------------------------------------|-----------|  
|DBTYPE_DBDATE|Datum||  
|DBTYPE_DBTIMESTAMP|**datetime2**(p)|Der OLE DB-Treiber für SQL Server überprüft das DBCOLUMDESC *bScale* Member, um die Genauigkeit in Sekundenbruchteilen zu bestimmen.|  
|DBTYPE_DBTIME2|**Zeit**(p)|Der OLE DB-Treiber für SQL Server überprüft das DBCOLUMDESC *bScale* Member, um die Genauigkeit in Sekundenbruchteilen zu bestimmen.|  
|DBTYPE_DBTIMESTAMPOFFSET|**datetimeoffset**(p)|Der OLE DB-Treiber für SQL Server überprüft das DBCOLUMDESC *bScale* Member, um die Genauigkeit in Sekundenbruchteilen zu bestimmen.|  
  
 Wenn eine Anwendung DBTYPE_DBTIMESTAMP in legt *wType*, kann die Zuordnung zu überschreiben **datetime2** durch Angabe eines Typs in *PwszTypeName*. Wenn **"DateTime"** angegeben wird, *bScale* muss 3 sein. Wenn **Smalldatetime** angegeben wird, *bScale* muss 0 sein. Wenn *bScale* ist nicht konsistent mit *wType* und *PwszTypeName*, wird DB_E_BADSCALE zurückgegeben.  
  
## <a name="see-also"></a>Siehe auch  
 [Datum und Uhrzeit-Verbesserungen & #40; OLE DB & #41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
