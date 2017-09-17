---
title: SQLNativeSql-Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLNativeSql
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLNativeSql
helpviewer_keywords:
- SQLNativeSql function [ODBC]
ms.assetid: b8efc247-27ab-4a00-92b6-1400785783fe
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1672e4c1f21d223ed326c0e0649fc7cbb2376f74
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="sqlnativesql-function"></a>SQLNativeSql-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ODBC  
  
 **Zusammenfassung**  
 **SQLNativeSql** gibt die SQL-Zeichenfolge zurück, von der Treiber geändert wurde. **SQLNativeSql** die SQL-Anweisung wird nicht ausgeführt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLNativeSql(  
     SQLHDBC        ConnectionHandle,  
     SQLCHAR *      InStatementText,  
     SQLINTEGER     TextLength1,  
     SQLCHAR *      OutStatementText,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   TextLength2Ptr);  
```  
  
## <a name="arguments"></a>Argumente  
 *Verbindungshandle*  
 [Eingabe] Verbindungshandle.  
  
 *InStatementText*  
 [Eingabe] SQL-Text-Zeichenfolge übersetzt werden.  
  
 *TextLength1*  
 [Eingabe] Länge in Zeichen des **InStatementText* Textzeichenfolge.  
  
 *OutStatementText*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die übersetzte SQL-Zeichenfolge zurückgegeben.  
  
 Wenn *OutStatementText* NULL ist, *TextLength2Ptr* gibt weiterhin zurück, die Gesamtzahl der Zeichen (mit Ausnahme der Null-Terminierung Zeichen für Zeichendaten) verfügbar, die in den Puffer zurückgegeben verweist *OutStatementText*.  
  
 *Pufferlänge*  
 [Eingabe] Anzahl der Zeichen in der \* *OutStatementText* Puffer. Wenn der Rückgabewert in * \*InStatementText* eine Unicode-Zeichenfolge (beim Aufrufen von **SQLNativeSqlW**), wird die *Pufferlänge* Argument muss eine gerade Zahl sein.  
  
 *TextLength2Ptr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Gesamtanzahl der verfügbaren Zeichen ist (außer Null-Terminierung) im zurückzugebenden zurückgegeben \* *OutStatementText*. Ist die Anzahl der zurückzugebenden verfügbaren Zeichen ist größer als oder gleich *Pufferlänge*, die in SQL-Zeichenfolge übersetzt \* *OutStatementText* auf abgeschnitten * Pufferlänge* abzüglich der Länge des ein Null-Abschlusszeichen.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLNativeSql** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, ein zugeordneten SQLSTATE-Wert abgerufen werden kann, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* SQL_HANDLE_DBC auf, und ein *behandeln* von *Verbindungshandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLNativeSql** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|Der Puffer \* *OutStatementText* war nicht groß genug, um die gesamte SQL-Zeichenfolge zurückzugeben, damit die SQL-Zeichenfolge abgeschnitten wurden. Die Länge der ungekürzte SQL-Zeichenfolge wird zurückgegeben, **TextLength2Ptr*. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08003|Verbindung nicht geöffnet|Die *Verbindungshandle* war nicht verbunden.|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|22007|Ungültiges Datetime-format|**InStatementText* eine Escape-Klausel mit einem ungültigen Wert für Datum, Uhrzeit oder Zeitstempel enthalten.|  
|24000|Ungültiger Cursorstatus|Der Cursor, die in der Anweisung bezeichnet wurde vor dem Start des Resultsets oder nach dem Ende des Resultsets positioniert. Dieser Fehler kann durch einen Treiber, müssen eine systemeigene Implementierung des DBMS-Cursor nicht zurückgegeben werden.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der * \*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY009|Ungültige Verwendung des null-Zeiger|(DM) **InStatementText* wurde ein null-Zeiger.|  
|HY010|Fehler bei Funktionssequenz|(DM) eine asynchron ausgeführte Funktion wurde aufgerufen, für die *Verbindungshandle* und wurde noch ausgeführt werden, wenn diese Funktion aufgerufen wurde.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) das Argument *TextLength1* war kleiner als 0 ist, aber ungleich SQL_NTS.|  
|||(DM) das Argument *Pufferlänge* war kleiner als 0 und dem Argument *OutStatementText* war nicht null-Zeiger ist.|  
|HY109|Ungültige Cursorposition|Die aktuelle Zeile des Cursors wurde gelöscht oder nicht abgerufen wurde. Dieser Fehler kann durch einen Treiber, müssen eine systemeigene Implementierung des DBMS-Cursor nicht zurückgegeben werden.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber verknüpft sind, mit der *Verbindungshandle* der Funktion nicht unterstützt.|  
  
## <a name="comments"></a>Kommentare  
 Im folgenden sind Beispiele für was **SQLNativeSql** möglicherweise für die folgende Eingabe SQL-Zeichenfolge, die mit der skalaren Funktion CONVERT zurück. Angenommen Sie, dass die Spalte Empid vom Typ INTEGER, in der Datenquelle ist:  
  
```  
SELECT { fn CONVERT (empid, SQL_SMALLINT) } FROM employee  
```  
  
 Ein Treiber für Microsoft SQL Server möglicherweise die folgende übersetzte SQL-Zeichenfolge zurückzugeben:  
  
```  
SELECT convert (smallint, empid) FROM employee  
```  
  
 Ein Treiber für ORACLE-Server möglicherweise die folgende übersetzte SQL-Zeichenfolge zurück:  
  
```  
SELECT to_number (empid) FROM employee  
```  
  
 Ein Treiber für Ingres möglicherweise die folgende übersetzte SQL-Zeichenfolge zurück:  
  
```  
SELECT int2 (empid) FROM employee  
```  
  
 Weitere Informationen finden Sie unter [direkte Ausführung](../../../odbc/reference/develop-app/direct-execution-odbc.md) und [vorbereitete Ausführung](../../../odbc/reference/develop-app/prepared-execution-odbc.md).  
  
## <a name="related-functions"></a>Verwandte Funktionen  
 Keine.  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
