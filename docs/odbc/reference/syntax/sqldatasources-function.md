---
title: SQLDataSources Funktion | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLDataSources
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDataSources
helpviewer_keywords:
- SQLDataSources function [ODBC]
ms.assetid: 3f63b1b4-e70e-44cd-96c6-6878d50d0117
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c6de6bf96c05925e9044be5955036cd9c663501a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqldatasources-function"></a>SQLDataSources-Funktion
**Konformität**  
 Version eingeführt: ODBC 1.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLDataSources** gibt Informationen zu einer Datenquelle zurück. Diese Funktion wird nur vom Treiber-Manager implementiert.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLDataSources(  
     SQLHENV          EnvironmentHandle,  
     SQLUSMALLINT     Direction,  
     SQLCHAR *        ServerName,  
     SQLSMALLINT      BufferLength1,  
     SQLSMALLINT *    NameLength1Ptr,  
     SQLCHAR *        Description,  
     SQLSMALLINT      BufferLength2,  
     SQLSMALLINT *    NameLength2Ptr);  
```  
  
## <a name="arguments"></a>Argumente  
 *EnvironmentHandle*  
 [Eingabe] Umgebungshandles.  
  
 *Richtung*  
 [Eingabe] Bestimmt, welcher Datenquelle der Treiber-Manager Informationen zu zurückgibt. Mögliche Werte sind:  
  
 SQL_FETCH_NEXT (auf der nächsten Datenquellenname in der Liste abgerufen werden), SQL_FETCH_FIRST (abzurufenden vom Anfang der Liste), SQL_FETCH_FIRST_USER (zum Abruf der ersten Benutzer-DSN) oder SQL_FETCH_FIRST_SYSTEM (auf der ersten System-DSN fetch).  
  
 Wenn *Richtung* festgelegt ist, um SQL_FETCH_FIRST, nachfolgende Aufrufe **SQLDataSources** mit *Richtung* Satz an SQL_FETCH_NEXT zurückgeben, Benutzer und System-DSNs. Wenn *Richtung* auf SQL_FETCH_FIRST_USER, alle nachfolgenden Aufrufe festgelegt **SQLDataSources** mit *Richtung* zurück zum SQL_FETCH_NEXT nur Benutzer-DSNs. Wenn *Richtung* festgelegt ist, um SQL_FETCH_FIRST_SYSTEM, alle nachfolgenden Aufrufe **SQLDataSources** mit *Richtung* zurück zum SQL_FETCH_NEXT nur System-DSNs.  
  
 *ServerName*  
 [Ausgabe] Zeiger auf einen Puffer, in dem der Name der Datenquelle zurückgegeben.  
  
 Wenn *ServerName* NULL ist, *NameLength1Ptr* gibt weiterhin zurück, die Gesamtzahl der Zeichen (mit Ausnahme der Null-Terminierung Zeichen für Zeichendaten) verfügbaren zurückzugebenden im Puffer verweist *ServerName*.  
  
 *BufferLength1*  
 [Eingabe] Länge der **ServerName* Puffer, in Zeichen; Dies muss nicht länger sein als SQL_MAX_DSN_LENGTH plus Null-Abschlusszeichen.  
  
 *NameLength1Ptr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Gesamtzahl der Zeichen (mit Ausnahme von Null-Abschlusszeichen) zurückgegeben verfügbar im zurückzugebenden \* *ServerName*. Wenn die Anzahl der zurückzugebenden verfügbaren Zeichen ist größer als oder gleich ist *BufferLength1*, der Name der Datenquelle in \* *ServerName* auf abgeschnitten *BufferLength1* abzüglich der Länge des ein Null-Abschlusszeichen.  
  
 *Beschreibung*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Beschreibung des Treibers verknüpft sind mit der Datenquelle zurückgegeben. DBASE- oder SQL Server.  
  
 Wenn *Beschreibung* NULL ist, *NameLength2Ptr* gibt weiterhin zurück, die Gesamtzahl der Zeichen (mit Ausnahme der Null-Terminierung Zeichen für Zeichendaten) verfügbaren zurückzugebenden im Puffer verweist *Beschreibung*.  
  
 *BufferLength2*  
 [Eingabe] Länge in Zeichen von der **Beschreibung* Puffer.  
  
 *NameLength2Ptr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem die Gesamtzahl der Zeichen (mit Ausnahme von Null-Abschlusszeichen) zurückgegeben verfügbar im zurückzugebenden \* *Beschreibung*. Wenn die Anzahl der zurückzugebenden verfügbaren Zeichen ist größer als oder gleich ist *BufferLength2*, um die treiberbeschreibung in \* *Beschreibung* auf abgeschnitten *BufferLength2*  abzüglich der Länge des ein Null-Abschlusszeichen.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLDataSources** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, ein zugeordneten SQLSTATE-Wert abgerufen werden kann, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType*SQL_HANDLE_ENV auf, und ein *behandeln* von *EnvironmentHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die in der Regel zurückgegebenes **SQLDataSources** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|(DM) Treibermanager-spezifische informationsmeldung. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|(DM) Puffer \* *ServerName* war nicht groß genug ist, der vollständige Name der Datenquelle zurückgegeben. Deshalb wurde der Name abgeschnitten. Die Länge des gesamten Datenquellenname wird zurückgegeben, \* *NameLength1Ptr*. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)<br /><br /> (DM) Puffer \* *Beschreibung* war nicht groß genug, um die vollständige treiberbeschreibung zurückzugeben. Aus diesem Grund wurden die Beschreibung abgeschnitten. Die Länge des ungekürzte datenquellenbeschreibung wird zurückgegeben, **NameLength2Ptr*. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|HY000|Allgemeiner Fehler|(DM) Fehler für die keine spezifischen SQLSTATE vorhanden war, und für die keine implementierungsabhängige SQLSTATE definiert wurde. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber-Manager (DM) konnte nicht belegt werden, die zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich ist.|  
|HY010|Fehler bei Funktionssequenz|(DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *StatementHandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM) für Argument angegebene Wert *BufferLength1* war kleiner als 0.<br /><br /> (DM) für Argument angegebene Wert *BufferLength2* war kleiner als 0.|  
|HY103|Ungültiger Abrufcode|(DM) der Wert für das Argument angegebene *Richtung* war nicht SQL_FETCH_FIRST, SQL_FETCH_FIRST_USER, SQL_FETCH_FIRST_SYSTEM oder SQL_FETCH_NEXT gleich.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
  
## <a name="comments"></a>Kommentare  
 Da **SQLDataSources** implementiert ist der Treiber-Manager wird für alle Treiber unabhängig davon, einen bestimmten Treiber Einhaltung von Standards unterstützt.  
  
 Eine Anwendung kann Aufrufen **SQLDataSources** mehrere Male auf, um alle Datenquellennamen abzurufen. Der Treiber-Manager ruft diese Informationen aus der Systeminformationen ab. Der Treiber-Manager gibt SQL_NO_DATA zurück, wenn es keine weitere Datenquellennamen sind. Wenn **SQLDataSources** mit SQL_FETCH_NEXT aufgerufen wird, sofort nach dem SQL_NO_DATA zurückgegeben wird, wird der erste Name der Datenquelle zurückgegeben. Informationen darüber, wie eine Anwendung zurückgegebene Informationen verwendet **SQLDataSources**, finden Sie unter [Auswählen der Datenquelle oder Treiber](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Wenn SQL_FETCH_NEXT, um übergeben wird **SQLDataSources** das erste Mal aufgerufen wird, wird der erste Name der Datenquelle zurückgegeben.  
  
 Der Treiber wird bestimmt, wie Datenquellennamen tatsächliche Datenquellen zugeordnet sind.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Ermitteln und Auflisten von Werten, die für die Verbindung mit einer Datenquelle|[SQLBrowseConnect-Funktion](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Herstellen einer Verbindung mit einer Datenquelle|[SQLConnect-Funktion](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Herstellen einer Verbindung mit einer Datenquelle mit einer Zeichenfolge oder ein Dialogfeld Verbindungsdialogfeld|[SQLDriverConnect-Funktion](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Zurückgeben von Beschreibungen der Treiber-Attribute|[SQLDrivers-Funktion](../../../odbc/reference/syntax/sqldrivers-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
