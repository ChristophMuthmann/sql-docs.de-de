---
title: SQLSetEnvAttr-Funktion | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
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
- SQLSetEnvAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetEnvAttr
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC]
ms.assetid: 0343241c-4b15-4d4b-aa2b-2e8ab5215cd2
caps.latest.revision: 38
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c8a70e7d7de19f4f69a79db56742938ca0d61344
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetenvattr-function"></a>SQLSetEnvAttr-Funktion
**Konformität**  
 Version eingeführt: ODBC 3.0 Standardkonformität: ISO-92  
  
 **Zusammenfassung**  
 **SQLSetEnvAttr** Legt Attribute, die Aspekte der Umgebung zu steuern.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SQLRETURN SQLSetEnvAttr(  
     SQLHENV      EnvironmentHandle,  
     SQLINTEGER   Attribute,  
     SQLPOINTER   ValuePtr,  
     SQLINTEGER   StringLength);  
```  
  
## <a name="arguments"></a>Argumente  
 *EnvironmentHandle*  
 [Eingabe] Umgebungshandles.  
  
 *Attribut*  
 [Eingabe] Attribut, das festgelegt wird, aufgelistet in "Kommentare".  
  
 *ValuePtr*  
 [Eingabe] Zeiger auf den Wert zugeordnet werden *Attribut*. Abhängig vom Wert der *Attribut*, *ValuePtr* wird ein ganze 32-Bit-Wert sein, und zeigen Sie auf eine Null-terminierte Zeichenfolge.  
  
 *StringLength*  
 [Eingabe] Wenn *ValuePtr* zeigt auf eine Zeichenfolge oder einen binären Puffer, in dieses Argument muss die Länge des **ValuePtr*. Für Zeichenfolgendaten sollte dieses Argument die Anzahl der Bytes in der Zeichenfolge enthalten.  
  
 Wenn *ValuePtr* ist eine ganze Zahl *StringLength* wird ignoriert.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Wenn **SQLSetEnvAttr** gibt SQL_ERROR oder SQL_SUCCESS_WITH_INFO, einen zugeordneten SQLSTATE-Wert abgerufen werden können, durch den Aufruf **SQLGetDiagRec** mit einem *HandleType* von SQL_ HANDLE_ENV und ein *behandeln* von *EnvironmentHandle*. Die folgende Tabelle enthält die SQLSTATE-Werten, die in der Regel zurückgegebenes **SQLSetEnvAttr** und erläutert, jeweils im Kontext dieser Funktion; die Notation "(DM)" vorangestellt ist, die Beschreibungen der SQLSTATEs, die vom Treiber-Manager zurückgegeben. Der Rückgabecode, der jeden SQLSTATE-Wert zugeordnet wird SQL_ERROR zurückgegeben, sofern nicht anders angegeben. Wenn ein Treiber ein Attributs Umgebung nicht unterstützt, kann der Fehler nur während der Zeitpunkt des Verbindungsaufbaus zurückgegeben werden.  
  
|SQLSTATE|Fehler|Description|  
|--------------|-----------|-----------------|  
|01000|Allgemeine Warnung|Treiberspezifische Meldung dient zu Informationszwecken. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|01 S 02|Der Optionswert wurde geändert|Der Treiber nicht den Wert im angegebenen *ValuePtr* und einen ähnlichen Wert ersetzt. (Funktion gibt SQL_SUCCESS_WITH_INFO zurück.)|  
|HY000|Allgemeiner Fehler|Für die es keine spezifischen SQLSTATE wurde und für die keine implementierungsabhängige SQLSTATE definiert wurde, ist ein Fehler aufgetreten. Die zurückgegebene Fehlermeldung **SQLGetDiagRec** in der  *\*MessageText* Puffer beschreibt den Fehler und seiner Ursache.|  
|HY001|Fehler bei der speicherbelegung|Der Treiber konnte nicht belegt werden zur Unterstützung der Ausführung oder den Abschluss der Funktion erforderlich.|  
|HY009|Ungültige Verwendung des null-Zeiger|Das Attributargument identifiziert ein Umgebung-Attribut, das einen Zeichenfolgenwert erforderlich sind und die *ValuePtr* Argument wurde ein null-Zeiger.|  
|HY010|Fehler bei Funktionssequenz|(DM) für ein Verbindungshandle zugewiesen wurde *EnvironmentHandle*.<br /><br /> (DM) **SQL_ATTR_ODBC_VERSION** wurde nicht festgelegt wurde, mit **SQLSetEnvAttr** und *Attribut* stimmt nicht mit **SQL_ATTR_ODBC_VERSION**. Sie müssen nicht festzulegende **SQL_ATTR_ODBC_VERSION** explizit bei Verwendung von **SQLAllocHandleStd**.|  
|HY013|Speicherverwaltungsfehler|Der Funktionsaufruf konnte nicht verarbeitet werden, da die zugrunde liegenden Speicherobjekte, möglicherweise aufgrund von unzureichendem Speicher konnte nicht zugegriffen werden.|  
|HY024|Ungültiger Attributwert|Berücksichtigung des angegebenen *Attribut* Wert, ein ungültiger Wert wurde angegeben, *ValuePtr*.|  
|HY090|Ungültige Zeichenfolgen- oder Pufferlänge.|Die *StringLength* Argument war kleiner als 0 jedoch war nicht SQL_NTS.|  
|HY092|Ungültiger Attribut-/Optionsbezeichner|(DM) der Wert für das Argument angegebene *Attribut* war für die vom Treiber unterstützten ODBC-Version ungültig.|  
|HY117|Verbindung wird aufgrund eines unbekannten Transaktionsstatus angehalten. Nur trennen, und nur-Lese Funktionen sind zulässig.|(DM) finden Sie weitere Informationen zum Zustand "angehalten" [SQLEndTran-Funktion](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Optionales Feature nicht implementiert|Der Wert für das Argument angegebene *Attribut* war gültiges Attribut für ODBC-Umgebung für die ODBC-Version vom Treiber unterstützt, jedoch wurde vom Treiber nicht unterstützt.<br /><br /> (DM) die *Attribut* Argument war SQL_ATTR_OUTPUT_NTS, und *ValuePtr* SQL_FALSE wurde.|  
  
## <a name="comments"></a>Kommentare  
 Eine Anwendung kann Aufrufen **SQLSetEnvAttr** nur, wenn keine Verbindungshandle in der Umgebung zugeordnet ist. Alle Umgebung Attribute, die von der Anwendung für die Umgebung erfolgreich festgelegt bleiben, bis **SQLFreeHandle** für die Umgebung aufgerufen wird. Mehr als ein Umgebungshandle zugewiesen werden kann, gleichzeitig in ODBC 3.*.x*.  
  
 Legen Sie das Format der Informationen über *ValuePtr* richtet sich nach dem angegebenen *Attribut*. **SQLSetEnvAttr** Attributinformationen in einem von zwei verschiedenen Formaten akzeptiert: einen Null-terminierte Zeichenfolge oder eine ganze 32-Bit-Wert. Das Format der einzelnen wird in das Attribut Beschreibung aufgeführt.  
  
 Keine Umgebung treiberspezifischen Attribute sind vorhanden.  
  
 Verbindungsattribute können nicht festgelegt werden, durch den Aufruf von **SQLSetEnvAttr**. Dies dennoch versuchen SQLSTATE HY092 zurück (Ungültiger Attribut-/Optionsbezeichner).  
  
|*Attribut*|*ValuePtr* Inhalt|  
|-----------------|-------------------------|  
|SQL_ATTR_CONNECTION_POOLING (ODBC 3.8)|Eine 32-Bit-SQLUINTEGER-Wert, der aktiviert oder deaktiviert die Verbindungspooling auf der Ebene der Umgebung. Die folgenden Werte werden verwendet:<br /><br /> SQL_CP_OFF = Verbindung zum Verbindungspooling deaktiviert ist. Dies ist die Standardeinstellung.<br /><br /> SQL_CP_ONE_PER_DRIVER = eine einzelne Verbindungspools wird für jeden Treiber unterstützt. Jede Verbindung in einem Pool bezieht sich auf einen Treiber zur Verfügung.<br /><br /> SQL_CP_ONE_PER_HENV = eine einzelne Verbindungspools für jede Umgebung unterstützt wird. Jede Verbindung in einem Pool bezieht sich auf eine Umgebung zur Verfügung.<br /><br /> SQL_CP_DRIVER_AWARE = verwendet den Verbindungspool Awareness-Funktion des Treibers, sofern dieser verfügbar ist. Wenn der Treiber Verbindungspool Erkennung nicht unterstützt, SQL_CP_DRIVER_AWARE wird ignoriert, und SQL_CP_ONE_PER_HENV dient. Weitere Informationen finden Sie unter [Treiberfähiges Verbindungspooling](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md). In einer Umgebung, in denen einige Treibern unterstützt wird und einige Treiber unterstützen keine Verbindungspool Awareness, SQL_CP_DRIVER_AWARE können der Verbindungspool Awareness-Funktion auf die Treiber unterstützt allerdings handelt es sich entspricht einem festlegen, um SQL_CP_ONE_PER_HENV auf Treiber, die Verbindungspool Awareness-Funktion nicht unterstützen.<br /><br /> Verbindungspooling aktiviert ist, durch den Aufruf **SQLSetEnvAttr** SQL_CP_ONE_PER_DRIVER oder SQL_CP_ONE_PER_HENV das SQL_ATTR_CONNECTION_POOLING-Attribut festgelegt. Dieser Aufruf muss erfolgen, bevor die Anwendung die freigegebene Umgebung weist pooling ist für die Verbindung aktiviert werden. Das Umgebungshandle im Aufruf **SQLSetEnvAttr** ist auf Null gesetzt, wodurch SQL_ATTR_CONNECTION_POOLING ein Attribut auf Prozessebene. Wenn Verbindungspooling aktiviert ist, weist die Anwendung dann eine implizite freigegebene Umgebung durch Aufrufen von **SQLAllocHandle** mit der *InputHandle* -Argument auf SQL_HANDLE_ENV festgelegt.<br /><br /> Nachdem der Verbindungs-pooling aktiviert wurde, und eine freigegebene Umgebung für eine Anwendung ausgewählt wurde, SQL_ATTR_CONNECTION_POOLING kann nicht zurückgesetzt werden für die Umgebung, da **SQLSetEnvAttr** aufgerufen wird und eine null-Umgebung behandelt wird, wenn dieses Attribut festlegen. Wenn dieses Attribut festgelegt ist, während die Verbindung bereits auf einer freigegebenen Umgebung aktiviert ist, beeinflusst das Attribut nur freigegebene Umgebungen, die anschließend zugeordnet sind.<br /><br /> Es ist auch möglich, um Verbindungspooling in einer Umgebung zu aktivieren. Beachten Sie die folgenden Informationen zum Verbindungspooling Umgebung aus:<br /><br /> – Aktivieren Verbindungspooling auf ein NULL-Handle ist ein auf Prozessebene-Attribut. Anschließend zugeordnete Umgebungen werden einer freigegebenen Umgebung, und übernimmt die Einstellung Verbindungspooling auf Prozessebene.<br />: Nachdem eine Umgebung zugeordnet ist, kann eine Anwendung weiterhin die Pool-verbindungseinstellung ändern.<br />– Wenn die Umgebung Verbindungspooling aktiviert ist, und die Verbindung Treiber verwendet Treiber Verbindungspooling, nimmt die Umgebung pooling bevorzugt.<br /><br /> SQL_ATTR_CONNECTION_POOLING wird innerhalb der Treiber-Manager implementiert. Ein Treiber muss nicht SQL_ATTR_CONNECTION_POOLING implementieren. ODBC 2.0 und 3.0-Anwendungen können diese Umgebung Attribut festgelegt.<br /><br /> Weitere Informationen finden Sie unter [ODBC-Verbindungspooling](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md).|  
|SQL_ATTR_CP_MATCH (ODBC 3.0)|Ein 32-Bit-SQLUINTEGER-Wert, der bestimmt, wie eine Verbindung aus einem Verbindungspool ausgewählt wird. Wenn **SQLConnect** oder **SQLDriverConnect** wird aufgerufen, der Treiber-Manager bestimmt, welche Verbindung aus dem Pool wiederverwendet wird. Der Treiber-Manager versucht, entsprechen die Verbindungsoptionen in dem Aufruf und die Verbindungsattribute, die von der Anwendung für die Schlüsselwörter und Verbindungsattribute der Verbindungen im Pool festgelegt. Der Wert dieses Attributs bestimmt die Genauigkeit der übereinstimmenden Kriterien.<br /><br /> Die folgenden Werte werden verwendet, um den Wert dieses Attributs festzulegen:<br /><br /> SQL_CP_STRICT_MATCH = nur Verbindungen, die die Verbindungsoptionen im Aufruf exakt übereinstimmen und die Verbindung, die Attribute, die von der Anwendung festgelegtes wiederverwendet werden. Dies ist die Standardeinstellung.<br /><br /> SQL_CP_RELAXED_MATCH = Verbindungen mit übereinstimmenden Verbindungszeichenfolge-Schlüsselwörter verwendet werden können. Schlüsselwörtern übereinstimmen, aber nicht alle Verbindungsattribute müssen übereinstimmen.<br /><br /> Weitere Informationen dazu, wie der Treiber-Manager die Übereinstimmung ausführt, eine Verbindung mit einer poolverbindung, finden Sie unter [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md). Weitere Informationen zum Verbindungspooling finden Sie unter [ODBC-Verbindungspooling](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md).|  
|SQL_ATTR_ODBC_VERSION (ODBC 3.0)|Eine 32-Bit-Ganzzahl, die bestimmt, ob bestimmte Funktionen ODBC 2. weist*.x* Verhalten oder die ODBC 3.*.x* Verhalten. Die folgenden Werte werden verwendet, um den Wert dieses Attributs festzulegen:<br /><br /> SQL_OV_ODBC3_80 = der Treiber-Manager und Treiber Anlage die folgenden ODBC 3.8 Verhalten:<br /><br /> -Der Treiber gibt und ODBC 3. erwartet. *x* Codes für Date, Time und Timestamp.<br />– Der Treiber gibt ODBC 3. zurück. *x* SQLSTATE-codes Wenn **SQLError**, **SQLGetDiagField**, oder **SQLGetDiagRec** aufgerufen wird.<br />– Der *CatalogName* Argument in einem Aufruf von **SQLTables** akzeptiert ein Suchmuster entspricht.<br />-Der Treiber-Manager unterstützt die Erweiterbarkeit von C Daten. Weitere Informationen zur Erweiterbarkeit von C Daten finden Sie unter [C-Datentypen in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).<br /><br /> Weitere Informationen finden Sie unter [Neuigkeiten in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).<br /><br /> SQL_OV_ODBC3 = der Treiber-Manager und Treiber Anlage die folgenden ODBC 3.*.x* Verhalten:<br /><br /> -Der Treiber gibt und erwartet, dass ODBC 3.*.x* Codes für Date, Time und Timestamp.<br />-Der Treiber gibt ODBC 3.*.x* SQLSTATE-codes Wenn **SQLError**, **SQLGetDiagField**, oder **SQLGetDiagRec** aufgerufen wird.<br />– Der *CatalogName* Argument in einem Aufruf von **SQLTables** akzeptiert ein Suchmuster entspricht.<br />– Erweiterbarkeit von C Daten unterstützt der Treiber-Manager nicht.<br /><br /> SQL_OV_ODBC2 = der Treiber-Manager und Treiber Anlage die folgenden ODBC 2.*.x* Verhalten. Dies ist besonders nützlich für eine ODBC-2*.x* Anwendung arbeiten mit einem ODBC 3.*.x* Treiber.<br /><br /> -Der Treiber gibt und erwartet, dass ODBC 2.*.x* Codes für Date, Time und Timestamp.<br />-Der Treiber gibt ODBC 2.*.x* SQLSTATE-codes Wenn **SQLError**, **SQLGetDiagField**, oder **SQLGetDiagRec** aufgerufen wird.<br />– Der *CatalogName* Argument in einem Aufruf von **SQLTables** akzeptiert kein Suchmuster entspricht.<br />– Erweiterbarkeit von C Daten unterstützt der Treiber-Manager nicht.<br /><br /> Eine Anwendung muss dieses Attribut Umgebung festlegen, vor dem Aufrufen einer Funktion, die ein Argument SQLHENV verfügt oder der Aufruf SQLSTATE HY010 zurück (Sequenzfehler-Funktion). Es ist treiberspezifische, ob zusätzliches Verhalten für diese Umgebung Flags vorhanden ist.<br /><br /> -Weitere Informationen finden Sie unter [deklarieren Sie der Anwendungsverzeichnis ODBC-Version von](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) und [Verhaltensänderungen](../../../odbc/reference/develop-app/behavioral-changes.md).|  
|SQL_ATTR_OUTPUT_NTS (ODBC 3.0)|Eine 32-Bit-Ganzzahl, die bestimmt, wie der Treiber Zeichenfolgendaten zurückgegeben wird. Wenn SQL_TRUE, den Treiber Zeichenfolgendaten Null-terminierte zurückgibt. Wenn SQL_FALSE, den Treiber nicht Zeichenfolgendaten, die Null-terminierte zurückgibt.<br /><br /> Dieses Attribut standardmäßig auf SQL_TRUE. Ein Aufruf von **SQLSetEnvAttr** auf festgelegt ist, dass SQL_TRUE gibt SQL_SUCCESS zurück. Ein Aufruf von **SQLSetEnvAttr** auf SQL_FALSE gibt SQL_ERROR und SQLSTATE HYC00 festlegen (optionales Feature nicht implementiert).|  
  
## <a name="related-functions"></a>Verwandte Funktionen  
  
|Informationen zu|Finden Sie unter|  
|---------------------------|---------|  
|Ein Handle zuordnen|[SQLAllocHandle-Funktion](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Die Einstellung eines Attributs Umgebung zurückgeben|[SQLGetEnvAttr-Funktion](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [ODBC-API-Referenz](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC-Headerdateien](../../../odbc/reference/install/odbc-header-files.md)   
 [What's New in ODBC 3.8 (Neues in ODBX 3.8)](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
