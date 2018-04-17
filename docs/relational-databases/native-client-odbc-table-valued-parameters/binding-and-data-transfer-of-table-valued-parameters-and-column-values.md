---
title: Bindung und Datenübertragung von Tabellenwertparametern, Parametern und Spaltenwerte | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), binding and data transfer
ms.assetid: 0a2ea462-d613-42b6-870f-c7fa086a6b42
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: fe37d43513051134632215cc6b551d8ec471b736
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="binding-and-data-transfer-of-table-valued-parameters-and-column-values"></a>Bindung und Datenübertragung von Tabellenwertparametern und Spaltenwerten
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Tabellenwertparameter müssen ebenso wie andere Parameter gebunden werden, bevor sie an den Server übergeben werden. Die Anwendung bindet Tabellenwertparameter die gleiche Weise wie andere Parameter: mit SQLBindParameter oder entsprechende Aufrufe SQLSetDescField oder SQLSetDescRec. Tabellenwertparameter haben den Serverdatentyp SQL_SS_TABLE. Der C-Typ kann entweder als SQL_C_DEFAULT oder SQL_C_BINARY angegeben werden.  
  
 In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] oder höher werden nur Eingabe-Tabellenwertparameter unterstützt. Daher resultiert jeder Versuch, SQL_DESC_PARAMETER_TYPE auf einen anderen Wert als SQL_PARAM_INPUT festzulegen, in der Rückgabe von SQL_ERROR mit SQLSTATE = HY105 und der Meldung "Der Parametertyp ist ungültig".  
  
 Gesamten Tabellenwertparameter-Spalten können mit dem Attribut SQL_CA_SS_COL_HAS_DEFAULT_VALUE Standardwerte zugewiesen werden. Einzelne Tabellenwertparameter-Spaltenwerte, allerdings können keine Standardwerte zugewiesen werden von SQL_DEFAULT_PARAM in *StrLen_or_IndPtr* mit SQLBindParameter. Tabellenwertparameter als Ganzes können nicht auf einen Standardwert festgelegt werden, von SQL_DEFAULT_PARAM in *StrLen_or_IndPtr* mit SQLBindParameter. Wenn diese Regeln nicht eingehalten werden, gibt SQLExecute oder SQLExecDirect SQL_ERROR zurück. Generiert ein Diagnosedatensatz mit SQLSTATE = 07S01 und der Meldung "Verwendung des Standardparameters ungültig für Parameter \<p >", wobei \<p > die Ordnungszahl des Tabellenwertparameters in der abfrageanweisung.  
  
 Nachdem die Anwendung den Tabellenwertparameter gebunden hat, muss sie jede einzelne Tabellenwertparameter-Spalte binden. Hierzu ruft die Anwendung zuerst SQLSetStmtAttr auf, um SQL_SOPT_SS_PARAM_FOCUS auf die Ordnungszahl für einen Tabellenwertparameter festgelegt. Und dann die Anwendung die Spalten der Tabellenwertparameter von Aufrufen an die folgenden Routinen bindet: SQLBindParameter SQLSetDescRec und SQLSetDescField. Wenn SQL_SOPT_SS_PARAM_FOCUS auf 0 Wiederherstellungen das übliche Verhalten von SQLBindParameter SQLSetDescRec und SQLSetDescField auf reguläre Parameter der obersten Ebene.
 
 Hinweis: die Linux- und Macintosh-ODBC-Treiber beim UnixODBC-2.3.1 zu 2.3.4, der zum Einstellen der TVP-Name mit dem Deskriptorfeld SQL_CA_SS_TYPE_NAME über SQLSetDescField, UnixODBC nicht automatisch zwischen ANSI- und Unicode-Zeichenfolgen je nach den genauen konvertiert Funktion mit dem Namen (SQLSetDescFieldA / SQLSetDescFieldW). Es ist erforderlich, die entweder immer SQLBindParameter oder SQLSetDescFieldW mit einer Zeichenfolge Unicode (UTF-16) verwenden, um den TVP-Namen festgelegt.
  
 Für den Tabellenwertparameter an sich werden keine Daten gesendet oder empfangen, die Daten werden für die einzelnen Spalten, aus denen er sich zusammensetzt, gesendet und empfangen. Da der Tabellenwertparameter eine Pseudospalte ist, werden die Parameter für SQLBindParameter verwendet, um auf andere Attribute als andere Datentypen wie folgt zu verweisen:  
  
|Parameter|Verknüpftes Attribut für Parametertypen, die keine Tabellenwertparameter sind, einschließlich Spalten|Verknüpftes Attribut für Tabellenwertparameter|  
|---------------|--------------------------------------------------------------------------------|----------------------------------------------------|  
|*InputOutputType*|SQL_DESC_PARAMETER_TYPE in IPD<br /><br /> Für Tabellenwertparameter-Spalten muss diese Angabe der Angabe für den Tabellenwertparameter selbst entsprechen.|SQL_DESC_PARAMETER_TYPE in IPD<br /><br /> Hier muss SQL_PARAM_INPUT angegeben werden.|  
|*ValueType*|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE in APD|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE in APD<br /><br /> Hier muss SQL_C_DEFAULT oder SQL_C_BINARY angegeben werden.|  
|*ParameterType*|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE in IPD|SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE in IPD<br /><br /> Hier muss SQL_SS_TABLE angegeben werden.|  
|*ColumnSize*|SQL_DESC_LENGTH oder SQL_DESC_PRECISION in IPD<br /><br /> Dies hängt vom Wert der *ParameterType*.|SQL_DESC_ARRAY_SIZE<br /><br /> Kann auch mit SQL_ATTR_PARAM_SET_SIZE festgelegt werden, wenn der Parameterfokus auf den Tabellenwertparameter festgelegt wurde.<br /><br /> Bei einem Tabellenwertparameter ist dies die Anzahl von Zeilen in den Tabellenwertparameter-Spaltenpuffern.|  
|*DecimalDigits*|SQL_DESC_PRECISION oder SQL_DESC_SCALE in IPD|Nicht verwendet. Diese Angabe muss 0 sein.<br /><br /> Wenn dieser Parameter ist nicht 0, SQLBindParameter wird SQL_ERROR zurückgegeben, und ein Diagnosedatensatz mit SQLSTATE erzeugende = HY104 und der Meldung "Ungültige Genauigkeit oder Dezimalstellenanzahl".|  
|*ParameterValuePtr*|SQL_DESC_DATA_PTR in APD|SQL_CA_SS_TYPE_NAME<br /><br /> Dies ist ein optionales Attribut für gespeicherte Prozeduren, und NULL kann angegeben werden, wenn es nicht erforderlich ist. Es muss für SQL-Anweisungen angegeben werden, die keine Prozeduraufrufe sind.<br /><br /> Dieser Parameter dient als eindeutiger Wert, anhand dessen die Anwendung den betreffenden Tabellenwertparameter bei Verwendung einer variablen Zeilenbindung identifizieren kann. Weitere Informationen finden Sie im Abschnitt "Variable Tabellenwertparameter-Zeilenbindung" weiter unten in diesem Thema.<br /><br /> Wenn ein Tabellenwertparameter-Typnamen bei einem Aufruf von SQLBindParameter angegeben ist, muss es als Unicode-Wert, auch bei Anwendungen angegeben werden, die als ANSI-Anwendungen erstellt werden. Der Wert für den Parameter verwendet *StrLen_or_IndPtr* sollte entweder SQL_NTS oder die Länge der Zeichenfolge multipliziert mit sizeof(WCHAR) sein.|  
|*Pufferlänge*|SQL_DESC_OCTET_LENGTH in APD|Die Länge des Typnamens des Tabellenwertparameters in Byte<br /><br /> Kann SQL_NTS sein, wenn der Typname NULL-termininiert ist, oder 0, wenn der Typname des Tabellenwertparameters nicht erforderlich ist.|  
|*StrLen_or_IndPtr*|SQL_DESC_OCTET_LENGTH_PTR in APD|SQL_DESC_OCTET_LENGTH_PTR in APD<br /><br /> Für Tabellenwertparameter wird hier die Zeilenanzahl statt die Datenlänge angegeben.|  
  
 Zwei Datenübertragungsmodi werden für Tabellenwertparameter unterstützt: feste Zeilenbindung und variable Zeilenbindung.  
  
## <a name="fixed-table-valued-parameter-row-binding"></a>Feste Tabellenwertparameter-Zeilenbindung  
 Bei der festen Zeilenbindung ordnet die Anwendung Puffer (oder Pufferarrays) zu, die groß genug sind, um alle Eingabespaltenwerte aufnehmen zu können. Die Anwendung führt Folgendes aus:  
  
1.  Bindet alle Parameter über SQLBindParameter, SQLSetDescRec oder SQLSetDescField Aufrufe an.  
  
    1.  Sie legt SQL_DESC_ARRAY_SIZE auf die maximale Anzahl von Zeilen fest, die für jeden Tabellenwertparameter übertragen werden können. Dies kann in der SQLBindParameter-Aufruf.  
  
2.  Ruft die SQLSetStmtAttr auf, um SQL_SOPT_SS_PARAM_FOCUS auf die Ordnungszahl der einzelnen Tabellenwertparameter festzulegen.  
  
    1.  Für jeden Tabellenwertparameter werden Tabellenwertparameter-Spalten mithilfe von SQLBindParameter, SQLSetDescRec oder SQLSetDescField Aufrufe gebunden.  
  
    2.  Für jede Tabellenwertparameter-Spalte, die Standardwerte besitzen, ruft SQLSetDescField um SQL_CA_SS_COL_HAS_DEFAULT_VALUE auf 1 festgelegt.  
  
3.  Ruft die SQLSetStmtAttr auf, um SQL_SOPT_SS_PARAM_FOCUS auf 0 festgelegt. Dies muss erfolgen, bevor SQLExecute oder SQLExecDirect aufgerufen wird. Andernfalls wird SQL_ERROR zurückgegeben, und es wird ein Diagnosedatensatz mit SQLSTATE=HY024 und der Meldung "Ungültiger Attributwert, SQL_SOPT_SS_PARAM_FOCUS (muss zur Laufzeit Null sein)" generiert.  
  
4.  Legt *StrLen_or_IndPtr* oder SQL_DESC_OCTET_LENGTH_PTR auf SQL_DEFAULT_PARAM und für einen Tabellenwertparameter keine Zeilen oder die Anzahl der Zeilen, auf den nächsten Aufruf von SQLExecute oder SQLExecDirect übertragen werden sollen, wenn der Tabellenwertparameter Parameter weist Zeilen auf. *StrLen_or_IndPtr* oder SQL_DESC_OCTET_LENGTH_PTR kann nicht auf SQL_NULL_DATA festgelegt werden für einen Tabellenwertparameter als Tabellenwertparameter keine Nullwerte zulässig sind, (obwohl einzelnen Tabellenwertparameter-Spalten NULL sein können). Wenn dieser Wert auf einen ungültigen Wert festgelegt ist, SQLExecute oder SQLExecDirect SQL_ERROR zurück gibt und ein Diagnosedatensatz mit SQLSTATE generiert = HY090 und der Meldung "Ungültige Zeichenfolgen- oder Pufferlänge für Parameter \<p >", wobei "p die Parameternummer".  
  
5.  SQLExecute oder SQLExecDirect aufruft.  
  
 Eingabe-Tabellenwertparameter-Spaltenwerte können schrittweise übergeben werden, wenn *StrLen_or_IndPtr* auf SQL_LEN_DATA_AT_EXEC festgelegt ist (*Länge*) oder SQL_DATA_AT_EXEC für die Spalte. Dies gleicht der Übergabe einzelner Werte bei Verwendung von Parameterarrays. Wie alle Data-at-Execution-Parameter, welche Zeile des Arrays nicht von SQLParamData angegeben ist anfordert der Treiber Daten; die Anwendung muss dies erledigen. Die Anwendung kann keine Annahmen über die Reihenfolge treffen, in der der Treiber Werte anfordert.  
  
## <a name="variable-table-valued-parameter-row-binding"></a>Variable Tabellenwertparameter-Zeilenbindung  
 Bei einer variablen Zeilenbildung werden die Zeilen zur Laufzeit in Batches übertragen, und die Anwendung übergibt die Zeilen bei Bedarf dem Treiber. Dies ähnelt der Übergabe einzelner Werte für Data-at-Execution-Parameter zur Laufzeit. Bei einer variablen Zeilenbindung geht die Anwendung wie folgt vor:  
  
1.  Sie bindet Parameter und Tabellenwertparameter-Spalten wie in den Schritten 1 bis 3 im vorigen Abschnitt mit dem Titel "Feste Tabellenwertparameter-Zeilenbindung" beschrieben.  
  
2.  Legt *StrLen_or_IndPtr* oder SQL_DESC_OCTET_LENGTH_PTR für alle Tabellenwertparameter, die zum Zeitpunkt der Ausführung auf SQL_DATA_AT_EXEC übergeben werden sollen. Wenn keiner dieser beiden Zeiger festgelegt wird, wird der Parameter wie im vorherigen Abschnitt beschrieben verarbeitet.  
  
3.  SQLExecute oder SQLExecDirect aufruft. Dieser Aufruf gibt SQL_NEED_DATA zurück, falls SQL_PARAM_INPUT- oder SQL_PARAM_INPUT_OUTPUT-Parameter als Data-at-Execution-Parameter behandelt werden sollen. In diesem Fall geht die Anwendung wie folgt vor:  
  
    -   Ruft die SQLParamData. Dies gibt die *ParameterValuePtr* Wert für einen Data-at-Execution-Parameter und den Rückgabecode SQL_NEED_DATA zurück. Wenn alle Parameterdaten an den Treiber übergeben wurde, gibt SQLParamData SQL_SUCCESS, SQL_SUCCESS_WITH_INFO oder SQL_ERROR zurück. Bei Data-at-Execution-Parametern *ParameterValuePtr*, die identisch mit den Deskriptor Deskriptorfeld sql_desc_data_ptr entspricht, können Sie als ein Token für den Parameter eindeutig identifiziert, für die ist ein Wert erforderlich, betrachtet werden. Dieses "Token" wird beim Binden von der Anwendung an den Treiber übergeben und während der Ausführung dann wieder an die Anwendung übergeben.  
  
4.  Zum Senden von Zeilendaten für Tabellenwertparameter für null-Tabellenwertparameter, wenn der Tabellenwertparameter keine Zeilen enthält, ruft die Anwendung mit SQLPutData *StrLen_or_Ind* auf SQL_DEFAULT_PARAM festgelegt.  
  
     Bei Tabellenwertparametern, die nicht NULL sind, geht die Anwendung wie folgt vor:  
  
    -   Legt *Str_Len_or_Ind* für alle Tabellenwertparameter-Spalten auf die entsprechenden Werte und füllt die Datenpuffer für Tabellenwertparameter-Spalten, die keine Data-at-Execution-Parameter sein. Tabellenwertparameter-Spalten können Daten zur Laufzeit auf ähnliche Weise übergeben werden wie dem Treiber gewöhnliche Parameter schrittweise übergeben werden.  
  
    -   Ruft die SQLPutData mit *Str_Len_or_Ind* auf die Anzahl der Zeilen festgelegt, die an den Server gesendet werden. Werte, die nicht im Bereich von 0 bis SQL_DESC_ARRAY_SIZE oder SQL_DEFAULT_PARAM liegen, sind ungültig und bewirken die Rückgabe von SQLSTATE HY090 und der Meldung "Ungültige Zeichenfolgen- oder Pufferlänge". Mit 0 wird angegeben, dass alle Zeilen übermittelt wurden und dass keine weiteren Daten für einen Tabellenwertparameter vorliegen (wie im zweiten Aufzählungspunkt dieser Auflistung beschrieben). SQL_DEFAULT_PARAM kann nur verwendet werden, wenn der Treiber zum ersten Mal Daten für einen Tabellenwertparameter anfordert (wie im ersten Aufzählungspunkt dieser Auflistung beschrieben).  
  
5.  Wenn alle Zeilen gesendet wurden, ruft Sie SQLPutData, für den Tabellenwertparameter mit einem *Str_Len_or_Ind* Wert von 0 und fährt dann mit Schritt 3a oben.  
  
6.  Ruft SQLParamData erneut aus. Wenn Data-at-Execution-Parameter auf die Tabellenwertparameter-Spalten vorhanden sind, werden diese durch den Wert identifiziert *ValuePtrPtr* von SQLParamData zurückgegeben. Wenn alle Spaltenwerte verfügbar sind, wird erneut SQLParamData Zurückgeben der *ParameterValuePtr* Wert für den Tabellenwertparameter und die Anwendung beginnt erneut.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellenwertparameter &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
