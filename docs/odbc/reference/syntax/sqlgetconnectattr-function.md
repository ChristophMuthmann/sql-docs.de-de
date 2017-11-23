---
title: SQLGetConnectAttr-Funktion | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLGetConnectOption
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLGetConnectAttr
helpviewer_keywords: SQLGetConnectAttr function [ODBC]
ms.assetid: 2cb4ffa8-19d3-4664-8c2f-6682cdcc3f33
caps.latest.revision: "32"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1162bf771e9a3d757986c0b6a94d1a36dd4892f4
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="sqlgetconnectattr-function"></a>SQLGetConnectAttr-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLGetConnectAttr** gibt die aktuelle Einstellung der Verbindungsattribut.  
  
> [!NOTE]  
>  Weitere Informationen, was der Treiber-Manager diese Funktion auf, wenn eine ODBC 3. ordnet*.x* Anwendung arbeitet mit einer ODBC 2.*.x* -Treiber verwenden, finden Sie unter [Ersatzfunktionen für rückwärts zuordnen Die Kompatibilität der Anwendungen](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLGetConnectAttr(  
     SQLHDBC        ConnectionHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumente  
 *Verbindungshandle*  
 [Eingabe] Verbindungshandle.  
  
 *Attribut*  
 [Eingabe] Abzurufenden Attributs.  
  
 *ValuePtr*  
 [Ausgabe] Ein Zeiger auf Speicher, in dem den aktuellen Wert des Attributs gemäß zurückgegeben *Attribut*. Integer-Datentyp-Attribute einige Treiber können nur die untere 32 Bit schreiben oder 16-Bit, der einen Puffer und lassen Sie das Bit höherer Ordnung unverändert. Aus diesem Grund sollten Anwendungen verwendet einen Puffer SQLULEN erstellt wurde, und initialisieren den Wert auf 0 vor dem Aufrufen dieser Funktion.  
  
 Wenn *ValuePtr* NULL ist, *StringLengthPtr* weiterhin die Gesamtanzahl der Bytes (ausgenommen die Null-Terminierung Zeichen für Zeichendaten) zurück in den Puffer verweist zurückzugebendenverfügbar *ValuePtr*.  
  
 *Pufferlänge*  
 [Eingabe] Wenn *Attribut* ist ein ODBC-definierten Attribut und *ValuePtr* zeigt auf eine Zeichenfolge oder einen binären Puffer, in dieses Argument muss die Länge des \* *ValuePtr*. Wenn *Attribut* ist ein ODBC-definierten Attribut und \* *ValuePtr* ist eine ganze Zahl *Pufferlänge* wird ignoriert. Wenn der Wert in  *\*ValuePtr* eine Unicode-Zeichenfolge (beim Aufrufen von **SQLGetConnectAttrW**), wird die *Pufferlänge* Argument muss eine gerade Zahl sein.  
  
 Wenn *Attribut* ist ein Attribut treiberdefinierten die Anwendung zeigt die Art des Attributs an den Treiber-Manager an, indem die *Pufferlänge* Argument. *Pufferlänge* können die folgenden Werte aufweisen:  
  
-   Wenn  *\*ValuePtr* ist ein Zeiger auf eine Zeichenfolge *Pufferlänge* ist die Länge der Zeichenfolge.  
  
-   Wenn  *\*ValuePtr* ist ein Zeiger auf einen binären Puffer, der Anwendung stellen das Ergebnis der SQL_LEN_BINARY_ATTR (*Länge*)-Makro im *Pufferlänge*. Dies setzt einen negativen Wert in *Pufferlänge*.  
  
-   Wenn  *\*ValuePtr* ist ein Zeiger auf einen anderen Wert als eine Zeichenfolge oder Binärzeichenfolge, *Pufferlänge* müssen den Wert SQL_IS_POINTER.  
  
-   Wenn  *\*ValuePtr* enthält einen Datentyp mit fester Länge *Pufferlänge* ist SQL_IS_INTEGER oder SQL_IS_UINTEGER, nach Bedarf.  
  
 *StringLengthPtr*  
 [Ausgabe] Ein Zeiger auf einen Puffer, in dem die Gesamtanzahl der Bytes (ausgenommen die Null-Abschlusszeichen) zurückgegeben verfügbar im zurückzugebenden \* *ValuePtr*. Wenn \* *ValuePtr* ist ein null-Zeiger, keine Länge zurückgegeben. Wenn der Wert des Attributs ist eine Zeichenfolge, und die Anzahl der zurückzugebenden verfügbaren Bytes ist größer als *Pufferlänge* abzüglich der Länge des Null-Terminierung Zeichens enthalten, die Daten in  *\*ValuePtr*auf abgeschnitten *Pufferlänge* abzüglich der Länge des Null-Abschlusszeichen und wird vom Treiber Null-terminiert.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLGetConnectAttr** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert aus der Struktur diagnostische Daten abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* SQL_HANDLE_DBC auf, und ein *behandeln* von *Verbindungshandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die in der Regel zurückgegebenes **SQLGetConnectAttr** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben . Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|Die Daten in \* *ValuePtr* wurde abgeschnitten, um werden *Pufferlänge* abzüglich der Länge des ein Null-Abschlusszeichen. Die Länge des Wertes ungekürzten Zeichenfolge wird zurückgegeben, **StringLengthPtr*. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|08003|Verbindung nicht geöffnet|(DM) eine *Attribut* Wert, der eine geöffnete Verbindung erforderlich, wurde angegeben.|  
|08S01|Kommunikations-Verbindungsfehler|Die Verbindung zwischen dem Treiber und die Datenquelle mit der der Treiber verbunden wurde aufgetreten ist, bevor die Verarbeitung für die Funktion abgeschlossen.|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung aus der Struktur Diagnosedaten durch das Argument *MessageText* in **SQLGetDiagField** beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden, die zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich ist.|  
|HY010|Fehler bei Funktionssequenz|(DM) **SQLBrowseConnect** wurde aufgerufen, die *Verbindungshandle* und SQL_NEED_DATA zurückgegeben. Diese Funktion aufgerufen wurde, bevor **SQLBrowseConnect** SQL_SUCCESS_WITH_INFO oder SQL_SUCCESS zurückgegeben.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** wurde aufgerufen, die *Verbindungshandle* und SQL_PARAM_DATA_ zurückgegeben VERFÜGBAR. Diese Funktion wurde aufgerufen, bevor Daten für alle gestreamte Parameter abgerufen wurde.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|(DM)  *\*ValuePtr* ist eine Zeichenfolge, und Pufferlänge war kleiner als 0 (null), aber nicht SQL_NTS gleich.|  
|HY092|Ungültiger Attribut-/Optionsbezeichner|Der Wert für das Argument angegebene *Attribut* war für die vom Treiber unterstützten ODBC-Version ungültig.|  
|HY114|Verbindungsebene asynchrone Ausführung unterstützt-Treiber nicht.|(DM) versucht eine Anwendung, die asynchrone Ausführung mit SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE für einen Treiber zu aktivieren, die asynchrone Verbindungsvorgänge nicht unterstützt.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Der Wert für das Argument angegebene *Attribut* wurde ein gültiger ODBC-Verbindungsattribut für den ODBC-Version vom Treiber unterstützt, jedoch wurde vom Treiber nicht unterstützt.|  
|HYT01|Verbindungstimeout abgelaufen|Das Verbindungstimeout ist abgelaufen, bevor die Datenquelle auf die Anforderung geantwortet hat. Das Verbindungstimeout wird über festgelegt **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber, die entspricht der *Verbindungshandle* der Funktion nicht unterstützt.|  
  
## <a name="comments"></a>Kommentare  
 Allgemeine Informationen zu Verbindungsattributen finden Sie unter [Verbindungsattribute](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Eine Liste der Attribute, die festgelegt werden können, finden Sie unter [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md). Beachten Sie, dass bei *Attribut* ein Attribut, das eine Zeichenfolge zurückgibt, gibt *ValuePtr* muss ein Zeiger auf einen Puffer für die Zeichenfolge sein. Die maximale Länge der zurückgegebenen Zeichenfolge, einschließlich des Zeichens Null-Terminierung werden *Pufferlänge* Bytes.  
  
 Je nach dem Attribut, eine Anwendung keinen zum Herstellen einer Verbindung vor dem Aufruf **SQLGetConnectAttr**. Jedoch wenn **SQLGetConnectAttr** aufgerufen wird und das angegebene Attribut hat keinen Standardwert und wurde nicht festgelegt wurde, durch einen vorherigen Aufruf von **SQLSetConnectAttr**, **SQLGetConnectAttr**SQL_NO_DATA zurückgegeben wird.  
  
 Wenn *Attribut* ist SQL_ATTR_ TRACE oder SQL_ATTR_ ABLAUFVERFOLGUNGSDATEI *Verbindungshandle* keine gültig, und **SQLGetConnectAttr** nicht gibt SQL_ERROR oder SQL_ Zurück Wenn *Verbindungshandle* ist ungültig. Diese Attribute gelten für alle Verbindungen. **SQLGetConnectAttr** SQL_ERROR oder SQL_INVALID_HANDLE zurück, wenn eines anderen Arguments ungültig ist.  
  
 Obwohl eine Anwendung Anweisungsattribute, indem festlegen kann **SQLSetConnectAttr**, eine Anwendung können keine **SQLGetConnectAttr** -Anweisungsattribut Abrufen von Werten; aufgerufen werden muss  **SQLGetStmtAttr** , die Einstellung der Anweisungsattribute abzurufen.  
  
 SQL_ATTR_AUTO_IPD und SQL_ATTR_CONNECTION_DEAD Verbindungsattribute zurückgegeben werden können, durch den Aufruf von **SQLGetConnectAttr** aber nicht festgelegt werden, durch den Aufruf von **SQLSetConnectAttr**.  
  
> [!NOTE]  
>  Es gibt keine asynchrone Unterstützung für **SQLGetConnectAttr**. Bei der Implementierung **SQLGetConnectAttr**, ein Treiber kann die Leistung verbessern, minimiert die Anzahl der Fälle, in denen Informationen gesendet bzw. vom Server angefordert.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Die Einstellung eines Attributs Anweisung zurückgeben|[SQLGetStmtAttr-Funktion](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|Ein Verbindungsattribut festlegen|[SQLSetConnectAttr-Funktion](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Wenn eine Umgebung-Attribut|[SQLSetEnvAttr-Funktion](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Wenn eine Anweisungsattribut|[SQLSetStmtAttr-Funktion](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
