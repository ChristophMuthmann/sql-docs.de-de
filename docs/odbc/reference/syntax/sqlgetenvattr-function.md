---
title: SQLGetEnvAttr Funktion | Microsoft Docs
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
- SQLGetEnvAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetEnvAttr
helpviewer_keywords:
- SQLGetEnvAttr function [ODBC]
ms.assetid: 01f4590f-427a-4280-a1c3-18de9f7d86c1
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 11c2b83057291f04e7476abddc63c0ccb9954b85
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgetenvattr-function"></a>SQLGetEnvAttr-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLGetEnvAttr** gibt die aktuelle Einstellung eines Attributs Umgebung zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLGetEnvAttr(  
     SQLHENV        EnvironmentHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumente  
 *EnvironmentHandle*  
 [Eingabe] Umgebungshandles.  
  
 *Attribut*  
 [Eingabe] Abzurufenden Attributs.  
  
 *ValuePtr*  
 [Ausgabe] Zeiger auf einen Puffer, in dem den aktuellen Wert des Attributs gemäß zurückgegeben *Attribut*.  
  
 Wenn *ValuePtr* NULL ist, *StringLengthPtr* weiterhin die Gesamtanzahl der Bytes (ausgenommen die Null-Terminierung Zeichen für Zeichendaten) zurück in den Puffer verweist zurückzugebendenverfügbar *ValuePtr*.  
  
 *Pufferlänge*  
 [Eingabe] Wenn *ValuePtr* zeigt auf eine Zeichenfolge, in dieses Argument muss die Länge des \* *ValuePtr*. Wenn \* *ValuePtr* ist eine ganze Zahl *Pufferlänge* wird ignoriert. Wenn  *\*ValuePtr* eine Unicode-Zeichenfolge (beim Aufrufen von **SQLGetEnvAttrW**), wird die *Pufferlänge* Argument muss eine gerade Zahl sein. Wenn der Wert des Attributs nicht auf eine Zeichenfolge ist *Pufferlänge* wird nicht verwendet.  
  
 *StringLengthPtr*  
 [Ausgabe] Ein Zeiger auf einen Puffer, in dem die Gesamtanzahl der Bytes (ausgenommen die Null-Abschlusszeichen) zurückgegeben verfügbar im zurückzugebenden  *\*ValuePtr*. Wenn *ValuePtr* ist ein null-Zeiger, keine Länge zurückgegeben. Wenn der Wert des Attributs ist eine Zeichenfolge, und die Anzahl der Bytes, die für die Rückgabe verfügbar ist, größer als oder gleich *Pufferlänge*, die Daten in \* *ValuePtr* auf abgeschnitten  *Pufferlänge* abzüglich der Länge des ein Null-Abschlusszeichen und wird vom Treiber Null-terminiert.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLGetEnvAttr** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_ HANDLE_ENV und ein *behandeln* von *EnvironmentHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die häufig zurückgegebenes **SQLGetEnvAttr** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01004|Zeichenfolgedaten wurden rechts abgeschnitten|Die Daten in \* *ValuePtr* wurde abgeschnitten, um werden *Pufferlänge* minus der Null-Abschlusszeichen. Die Länge des Wertes ungekürzten Zeichenfolge wird zurückgegeben, **StringLengthPtr*. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY010|Fehler bei Funktionssequenz|(DM) **SQL_ATTR_ODBC_VERSION** noch nicht über festgelegt **SQLSetEnvAttr**. Sie müssen nicht festzulegende **SQL_ATTR_ODBC_VERSION** explizit bei Verwendung von **SQLAllocHandleStd**.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY092|Ungültiger Attribut-/Optionsbezeichner|Der Wert für das Argument angegebene *Attribut* war für die vom Treiber unterstützten ODBC-Version ungültig.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Der Wert für das Argument angegebene *Attribut* war gültiges Attribut für ODBC-Umgebung für die ODBC-Version vom Treiber unterstützt, jedoch wurde vom Treiber nicht unterstützt.|  
|IM001|Diese Funktion wird im Treiber nicht unterstützt.|(DM) der Treiber entspricht der *EnvironmentHandle* der Funktion nicht unterstützt.|  
  
## <a name="comments"></a>Kommentare  
 Eine Liste der Attribute, finden Sie unter [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). Keine Umgebung treiberspezifischen Attribute sind vorhanden. Wenn *Attribut* ein Attribut, das eine Zeichenfolge zurückgibt, gibt *ValuePtr* muss ein Zeiger auf einen Puffer, in dem die Zeichenfolge zurückgegeben. Die maximale Länge der Zeichenfolge, die Null-Terminierung Byte, einschließlich werden *Pufferlänge* Bytes.  
  
 **SQLGetEnvAttr** kann zu einem beliebigen Zeitpunkt zwischen der Zuordnung und die Freigabe ein Umgebungshandle aufgerufen werden. Alle Umgebung Attribute, die von der Anwendung für die Umgebung erfolgreich festgelegt bleiben, bis **SQLFreeHandle** aufgerufen wird, auf die *EnvironmentHandle* mit einem *HandleType*SQL_HANDLE_ENV auf. Mehr als ein Umgebungshandle zugewiesen werden kann, gleichzeitig in ODBC 3.*.x*. Ein Attribut Umgebung auf eine Umgebung ist nicht betroffen, wenn eine andere Umgebung zugeordnet wurde.  
  
> [!NOTE]  
>  Das SQL_ATTR_OUTPUT_NTS Umgebung-Attribut wird von Standards kompatiblen Anwendungen unterstützt. Wenn **SQLGetEnvAttr** aufgerufen wird, wird die ODBC 3.*.x* -Treiber-Manager gibt SQL_TRUE immer für dieses Attribut zurück. SQL_ATTR_OUTPUT_NTS auf SQL_TRUE festgelegt werden können, nur durch einen Aufruf von **SQLSetEnvAttr**.  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Die Einstellung der Verbindungsattribut zurückgeben|[SQLGetConnectAttr-Funktion](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Die Einstellung eines Attributs Anweisung zurückgeben|[SQLGetStmtAttr-Funktion](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|Ein Verbindungsattribut festlegen|[SQLSetConnectAttr-Funktion](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Wenn eine Umgebung-Attribut|[SQLSetEnvAttr-Funktion](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Wenn eine Anweisungsattribut|[SQLSetStmtAttr-Funktion](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)
