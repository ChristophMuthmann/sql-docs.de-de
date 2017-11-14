---
title: ADO--Enumerationskonstanten | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- enumerated constants [ADO]
ms.assetid: c97ed131-1a93-463c-9e61-22f029b0c474
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 93011b8b30d552e5bf3852c9e4d483161d90fc55
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="ado-enumerated-constants"></a>ADO--Enumerationskonstanten
Um das Debuggen zu erleichtern, Liste der ADO-Enumerationen einen Wert für jede Konstante. Dieser Wert ist nur eine Empfehlung und kann von einer Version von ADO auf einen anderen ändern. Der Code sollte nur auf den Namen, die nicht den tatsächlichen Wert, der jede Enumerationskonstante abhängig sein.  
  
|||  
|-|-|  
|[ADCPROP_ASYNCTHREADPRIORITY_ENUM](../../../ado/reference/ado-api/adcprop-asyncthreadpriority-enum.md)|Für eine RDS **Recordset** Objekt, gibt die Ausführungspriorität des asynchronen Threads, die Daten abruft.|  
|[ADCPROP_AUTORECALC_ENUM](../../../ado/reference/ado-api/adcprop-autorecalc-enum.md)|Gibt an, wann die **MSDataShape** Anbieter neu berechnet, aggregierte und berechnete Spalten in einer hierarchischen **Recordset**.|  
|[ADCPROP_UPDATECRITERIA_ENUM](../../../ado/reference/ado-api/adcprop-updatecriteria-enum.md)|Gibt an, welche Felder verwendet werden können, zum Erkennen von Konflikten während einer optimistischen Aktualisierung einer Zeile der Datenquelle mit einem **Recordset** Objekt.|  
|[ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md)|Gibt an, ob die **UpdateBatch** Methode einen impliziten gefolgt **Resync** Methodenvorgangs und wenn dies der Fall ist, den Bereich dieses Vorgangs.|  
|[AffectEnum](../../../ado/reference/ado-api/affectenum.md)|Gibt an, welche Datensätze von einem Vorgang betroffen sind.|  
|[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)|Gibt ein Lesezeichen, der angibt, in dem der Vorgang beginnen soll.|  
|[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)|Gibt an, wie ein Befehlsargument interpretiert werden sollen.|  
|[CompareEnum](../../../ado/reference/ado-api/compareenum.md)|Gibt die relative Position von zwei Datensätzen, die durch ihre Lesezeichen dargestellt.|  
|[ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md)|Gibt die verfügbaren Berechtigungen zum Ändern von Daten in eine **Verbindung**, öffnen eine **Datensatz**, oder das Angeben von Werten für die **Modus** Eigenschaft von der  **Datensatz** und **Stream** Objekte.|  
|[ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md)|Gibt an, ob die **öffnen** Methode von einer **Verbindung** Objekt sollte nach dem zurückgeben (synchron) oder bevor (asynchron) die Verbindung hergestellt wird.|  
|[ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md)|Gibt an, ob ein Dialogfeld angezeigt werden soll, um fehlende Parameter beim Öffnen einer Verbindung mit einer ODBC-Datenquelle anzufordern.|  
|[CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md)|Gibt das Verhalten der **CopyRecord** Methode.|  
|[CursorLocationEnum](../../../ado/reference/ado-api/cursorlocationenum.md)|Gibt den Speicherort des Cursormoduls.|  
|[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)|Gibt an, welche Funktionen die **unterstützt** Methode sollte für testen.|  
|[CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)|Gibt den Typ der Cursor, mit dem einem **Recordset** Objekt.|  
|[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)|Gibt den Datentyp, der eine **Feld**, **Parameter**, oder **Eigenschaft**.|  
|[EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)|Gibt den Bearbeitungsstatus eines Datensatzes.|  
|[ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)|Gibt den Typ des ADO-Laufzeitfehler.|  
|[EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)|Gibt den Grund an, der ein Ereignis ausgelöst hat.|  
|[EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)|Gibt den aktuellen Status der Ausführung eines Ereignisses an.|  
|[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)|Gibt an, wie ein Anbieter einen Befehl ausgeführt werden soll.|  
|[FieldEnum](../../../ado/reference/ado-api/fieldenum.md)|Gibt an, die spezielle Felder verwiesen wird, der **Felder** Auflistung von einem **Datensatz** Objekt.|  
|[FieldAttributeEnum](../../../ado/reference/ado-api/fieldattributeenum.md)|Gibt einen oder mehrere Attribute eines eine **Feld** Objekt.|  
|[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)|Gibt den Status einer **Feld** Objekt.|  
|[FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)|Gibt die Gruppe von Datensätzen aus gefiltert werden sollen eine **Recordset**.|  
|[GetRowsOptionEnum](../../../ado/reference/ado-api/getrowsoptionenum.md)|Gibt an, wie viele Datensätze zum Abrufen von aus einer **Recordset**.|  
|[IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md)|Gibt die Ebene der Isolation jeder Transaktion für eine **Verbindung** Objekt.|  
|[LineSeparatorsEnum](../../../ado/reference/ado-api/lineseparatorsenum.md)|Gibt an, das als Zeilentrennzeichen in Text verwendete Zeichen **Stream** Objekte.|  
|[LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)|Gibt den Typ der Sperre, die auf Datensätze, die während der Bearbeitung platziert werden.|  
|[MarshalOptionsEnum](../../../ado/reference/ado-api/marshaloptionsenum.md)|Gibt an, welche Datensätze mit dem Server zurückgegeben werden sollen.|  
|[MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md)|Gibt das Verhalten der **Datensatz** Objekt **MoveRecord** Methode.|  
|[ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md)|Gibt an, ob ein Objekt offen oder geschlossen, Herstellen einer Verbindung mit einer Datenquelle, die Ausführung eines Befehls oder Abrufen von Daten.|  
|[ParameterAttributesEnum](../../../ado/reference/ado-api/parameterattributesenum.md)|Gibt die Attribute einer **Parameter** Objekt.|  
|[ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md)|Gibt an, ob die **Parameter** Eingabeparameter, Ausgabeparameter oder beides darstellt, oder wenn der Parameter der Rückgabewert einer gespeicherten Prozedur ist.|  
|[PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md)|Gibt das Format zum Speichern einer **Recordset**.|  
|[PositionEnum](../../../ado/reference/ado-api/positionenum.md)|Gibt die aktuelle Position des Datensatzzeigers innerhalb einer **Recordset**.|  
|[PropertyAttributesEnum](../../../ado/reference/ado-api/propertyattributesenum.md)|Gibt die Attribute einer **Eigenschaft** Objekt.|  
|[RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md)|Gibt an, für die **Datensatz** Objekt **öffnen** Methode, ob ein vorhandenes **Datensatz** sollte bereits geöffnet ist, oder ein neues **Datensatz** erstellt werden soll.|  
|[RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md)|Gibt Optionen zum Öffnen einer **Datensatz**. Diese Werte können mithilfe eines OR-Operators kombiniert werden.|  
|[RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md)|Gibt den Status eines Datensatzes in Bezug auf BatchUpdates und andere Massenvorgänge.|  
|[RecordTypeEnum](../../../ado/reference/ado-api/recordtypeenum.md)|Gibt den Typ des **Datensatz** Objekt.|  
|[ResyncEnum](../../../ado/reference/ado-api/resyncenum.md)|Gibt an, ob die zugrunde liegenden Werte überschrieben werden, durch den Aufruf von **Resync**.|  
|[SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md)|Gibt an, ob eine Datei erstellt oder werden, beim Speichern überschrieben von werden eine **Stream** Objekt. Die Werte können mit einem AND-Operator kombiniert werden.|  
|[SchemaEnum](../../../ado/reference/ado-api/schemaenum.md)|Gibt den Typ des Schemas **Recordset** , die die **OpenSchema** Methode abgerufen. Gibt die Richtung einer Datensatz Suche innerhalb einer **Recordset**.|  
|[SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md)|Gibt die Richtung einer Datensatz Suche innerhalb einer **Recordset**. Gibt den Typ des **Seek** ausgeführt.|  
|[SeekEnum](../../../ado/reference/ado-api/seekenum.md)|Gibt den Typ des **Seek** ausgeführt. Gibt Optionen zum Öffnen einer **Stream** Objekt. Die Werte können mit einem AND-Operator kombiniert werden.|  
|[StreamOpenOptionsEnum](../../../ado/reference/ado-api/streamopenoptionsenum.md)|Gibt Optionen zum Öffnen einer **Stream** Objekt. Die Werte können mit einem AND-Operator kombiniert werden. Gibt an, ob der gesamte Datenstrom oder die nächste Zeile aus gelesen werden soll eine **Stream** Objekt.|  
|[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)|Gibt an, ob der gesamte Datenstrom oder die nächste Zeile aus gelesen werden soll eine **Stream** Objekt. Gibt den Typ der Daten in einem **Stream** Objekt.|  
|[StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md)|Gibt den Typ der Daten in einem **Stream** Objekt. Gibt an, ob eine Linie wird als Trennzeichen an die Zeichenfolge angefügt wird eine **Stream** Objekt.|  
|[StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md)|Gibt an, ob eine Linie wird als Trennzeichen an die Zeichenfolge angefügt wird eine **Stream** Objekt. Gibt das Format an, wenn das Abrufen einer **Recordset** als Zeichenfolge.|  
|[StringFormatEnum](../../../ado/reference/ado-api/stringformatenum.md)|Gibt das Format an, wenn das Abrufen einer **Recordset** als Zeichenfolge. Gibt die Transaktionsattribute von einem **Verbindung** Objekt.|  
|[XactAttributeEnum](../../../ado/reference/ado-api/xactattributeenum.md)|Gibt die Transaktionsattribute von einem **Verbindung** Objekt.|  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-API-Referenz](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO-Auflistungen](../../../ado/reference/ado-api/ado-collections.md)   
 [Dynamische Eigenschaften von ADO.NET](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [Anhang B: ADO-Fehler](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO-Ereignisse](../../../ado/reference/ado-api/ado-events.md)   
 [ADO-Methoden](../../../ado/reference/ado-api/ado-methods.md)   
 [ADO-Objektmodell](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO-Objekte und Schnittstellen](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [Eigenschaften von ADO.NET](../../../ado/reference/ado-api/ado-properties.md)

