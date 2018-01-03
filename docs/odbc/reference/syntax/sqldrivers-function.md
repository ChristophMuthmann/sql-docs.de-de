---
title: SQLDrivers-Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLDrivers
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLDrivers
helpviewer_keywords: SQLDrivers function [ODBC]
ms.assetid: 6b5b7514-e9cb-4cfd-8b7a-ab51dfab9efa
caps.latest.revision: "23"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ad4afa4a54b63b759b03774f77ed7ec0371ff931
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqldrivers-function"></a>SQLDrivers-Funktion
**Konformität**  
 Version eingeführt: ODBC 2.0 Standardkonformität: ODBC  
  
 **Zusammenfassung**  
 **SQLDrivers** sind Beschreibungen der Treiber und Treiber Attribut Schlüsselwörter aufgeführt. Diese Funktion wird nur vom Treiber-Manager implementiert.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLDrivers(  
     SQLHENV         EnvironmentHandle,  
     SQLUSMALLINT    Direction,  
     SQLCHAR *       DriverDescription,  
     SQLSMALLINT     BufferLength1,  
     SQLSMALLINT *   DescriptionLengthPtr,  
     SQLCHAR *       DriverAttributes,  
     SQLSMALLINT     BufferLength2,  
     SQLSMALLINT *   AttributesLengthPtr);  
```  
  
## <a name="arguments"></a>Argumente  
 *EnvironmentHandle*  
 [Eingabe] Umgebungshandles.  
  
 *Richtung*  
 [Eingabe] Bestimmt, ob der Treiber-Manager abruft, um die nächste treiberbeschreibung in der Liste (SQL_FETCH_NEXT) oder gibt an, ob die Suche vom Anfang der Liste (SQL_FETCH_FIRST) beginnt.  
  
 *DriverDescription*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die treiberbeschreibung zurückgegeben.  
  
 Wenn *DriverDescription* NULL ist, *DescriptionLengthPtr* weiterhin die Gesamtzahl der Zeichen (mit Ausnahme der Null-Terminierung Zeichen für Zeichendaten) zurück zur Rückgabe in der Puffer verweist *DriverDescription*.  
  
 *BufferLength1*  
 [Eingabe] Länge der **DriverDescription* Puffers in Zeichen.  
  
 *DescriptionLengthPtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Gesamtzahl der Zeichen (mit Ausnahme von Null-Abschlusszeichen) zurückgegeben verfügbar im zurückzugebenden \* *DriverDescription*. Wenn die Anzahl der zurückzugebenden verfügbaren Zeichen ist größer als oder gleich ist *BufferLength1*, um die treiberbeschreibung in \* *DriverDescription* auf abgeschnitten  *BufferLength1* abzüglich der Länge des ein Null-Abschlusszeichen.  
  
 *DriverAttributes*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Liste der Treiber-Attribut-Wert-Paaren zurück (siehe "Kommentare").  
  
 Wenn *DriverAttributes* NULL ist, *AttributesLengthPtr* gibt weiterhin zurück, die Gesamtanzahl der Bytes (ausgenommen die Null-Terminierung Zeichen für Zeichendaten) verfügbar, die in den Puffer zurückgegeben verweist *DriverAttributes*.  
  
 *BufferLength2*  
 [Eingabe] Länge der \* *DriverAttributes* Puffers in Zeichen. Wenn die  *\*DriverDescription* Wert ist eine Unicode-Zeichenfolge (beim Aufrufen von **SQLDriversW**), wird die *Pufferlänge* Argument muss eine gerade Zahl sein.  
  
 *AttributesLengthPtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Gesamtanzahl der Bytes (ausgenommen die Null-Terminierung Byte) zurückgegeben verfügbar im zurückzugebenden \* *DriverAttributes*. Wenn die Anzahl der Bytes, die für die Rückgabe verfügbar, größer als oder gleich ist *BufferLength2*, die Liste der Attribut-Wert-Paare im \* *DriverAttributes* auf abgeschnitten  *BufferLength2* abzüglich der Länge des Null-Abschlusszeichen.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLDrivers** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, ein zugeordneten SQLSTATE-Wert abgerufen werden kann, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_HANDLE_ENV und ein *behandeln* von *EnvironmentHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die in der Regel zurückgegebenes **SQLDrivers** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|(DM) Treibermanager-spezifische informationsmeldung. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|(DM) Puffer \* *DriverDescription* war nicht groß genug, um die vollständige treiberbeschreibung zurückzugeben. Aus diesem Grund wurden die Beschreibung abgeschnitten. Die Länge der treiberbeschreibung des vollständigen wird zurückgegeben, \* *DescriptionLengthPtr*. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)<br /><br /> (DM) Puffer \* *DriverAttributes* war nicht groß genug für die vollständige Liste der Attribut-Wert-Paaren zurück. Deshalb wurde die Liste abgeschnitten. Die Länge der ungekürzte Liste mit Attribut-Wert-Paare im zurückgegeben **AttributesLengthPtr*. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber-Manager (DM) konnte nicht belegt werden, die zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich ist.|  
|HY010|Fehler bei Funktionssequenz|(DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) für Argument angegebene Wert *BufferLength1* war kleiner als 0.<br /><br /> (DM) für Argument angegebene Wert *BufferLength2* war kleiner als 0 oder gleich 1.|  
|HY103|Ungültiger Abrufcode|(DM) der Wert für das Argument angegebene *Richtung* war nicht gleich SQL_FETCH_FIRST oder SQL_FETCH_NEXT.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
  
## <a name="comments"></a>Kommentare  
 **SQLDrivers** gibt zurück, um die treiberbeschreibung in der \* *DriverDescription* Puffer. Es gibt zusätzliche Informationen über den Treiber in den \* *DriverAttributes* Puffer als Liste von Paaren aus Schlüsselwort-Wert. Alle Schlüsselwörter aufgeführt in die Systeminformationen für die Treiber für alle Treiber, mit Ausnahme von zurückgegeben werden **CreateDSN**, die verwendet, um die Erstellung von Datenquellen aufzufordern, und daher ist optional. Jedes Paar wird durch ein Nullbyte beendet, und die vollständige Liste mit null Byte beendet wird (d. h. zwei null-Bytes markieren Sie am Ende der Liste). Beispielsweise gibt möglicherweise ein dateibasierten Treiber mithilfe der C#-Syntax die folgenden Liste der Attribute zurück ("\0" steht für ein Null-Zeichen):  
  
```  
FileUsage=1\0FileExtns=*.dbf\0\0  
```  
  
 Wenn \* *DriverAttributes* ist nicht groß genug für die gesamte Liste, die Liste wird abgeschnitten, **SQLDrivers** SQLSTATE 01004 (Daten abgeschnitten) und die Länge der Liste zurückgegeben (mit Ausnahme der Im abschließenden Null-Terminierung Byte) zurückgegeben **AttributesLengthPtr*.  
  
 Treiber-Attribut Schlüsselwörter werden aus der Systeminformationen hinzugefügt, wenn der Treiber installiert ist. Weitere Informationen finden Sie unter [ODBC-Komponenten installieren](../../../odbc/reference/install/installing-odbc-components.md).  
  
 Eine Anwendung kann Aufrufen **SQLDrivers** mehrere Male auf, um Beschreibungen für alle Treiber abzurufen. Der Treiber-Manager ruft diese Informationen aus der Systeminformationen ab. Wenn es keine weitere Treiber Beschreibungen sind **SQLDrivers** gibt SQL_NO_DATA zurück. Wenn **SQLDrivers** mit SQL_FETCH_NEXT aufgerufen wird, sofort nach dem SQL_NO_DATA zurückgegeben wird, wird die erste treiberbeschreibung zurückgegeben. Informationen darüber, wie eine Anwendung zurückgegebene Informationen verwendet **SQLDrivers**, finden Sie unter [Auswählen der Datenquelle oder Treiber](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Wenn SQL_FETCH_NEXT, um übergeben wird **SQLDrivers** das erste Mal aufgerufen wird, **SQLDrivers** gibt der erste Name der Datenquelle zurück.  
  
 Da **SQLDrivers** implementiert ist der Treiber-Manager wird für alle Treiber unabhängig davon, einen bestimmten Treiber Einhaltung von Standards unterstützt.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Ermitteln und Auflisten von Werten, die für die Verbindung mit einer Datenquelle|[SQLBrowseConnect-Funktion](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Herstellen einer Verbindung mit einer Datenquelle|[SQLConnect-Funktion](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Datenquellennamen zurückgeben|[SQLDataSources-Funktion](../../../odbc/reference/syntax/sqldatasources-function.md)|  
|Herstellen einer Verbindung mit einer Datenquelle mit einer Zeichenfolge oder ein Dialogfeld Verbindungsdialogfeld|[SQLDriverConnect-Funktion](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
