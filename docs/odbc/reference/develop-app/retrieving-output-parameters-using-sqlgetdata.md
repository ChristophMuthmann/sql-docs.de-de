---
title: Abrufen von Ausgabeparametern mit SQLGetData | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLGetData function [ODBC], retrieving output parameters
- output parameters [ODBC]
- retrieving output parameters [ODBC]
ms.assetid: 7a8c298a-2160-491d-a300-d36f45568d9c
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c1c4c3a857436f9b66d5aed447a6d5b47d59915a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="retrieving-output-parameters-using-sqlgetdata"></a>Abrufen von Ausgabeparametern mit SQLGetData
Vor der ODBC 3.8 konnte eine Anwendung nur die Output-Parameter einer Abfrage mit einer gebundenen Ausgabepuffer abrufen. Allerdings ist es schwierig, einen sehr umfangreichen Puffer zuzuordnen, wenn die Größe des Parameterwerts sehr groß ist (z. B. ein großes Bild). ODBC 3.8 führt eine neue Methode zum Abrufen von Ausgabeparametern in Teilen. Eine Anwendung kann nun Aufrufen **SQLGetData** mit einem kleinen Puffer mehrere Male auf, um einen großen Parameterwert abzurufen. Dies ähnelt der welcher Spaltendaten abrufen.  
  
 So binden ein Output-Parameter oder ein Eingabe-/Ausgabeparameter in Teilen abgerufen werden sollen, rufen **SQLBindParameter** mit der *InputOutputType* Argument festgelegt wird, um SQL_PARAM_OUTPUT_STREAM oder SQL_PARAM_INPUT_OUTPUT an _STREAM. Eine Anwendung kann mit SQL_PARAM_INPUT_OUTPUT_STREAM, verwenden **SQLPutData** Eingabedaten in den Parameter, und klicken Sie dann verwenden **SQLGetData** Output-Parameters abgerufen. Die Eingabedaten müssen in der Data-at-Execution-(DAE) werden zu bilden, mit **SQLPutData** anstatt an ein vorab Puffer gebunden wird.  
  
 Diese Funktion kann von ODBC 3.8-Anwendungen verwendet werden oder neu kompiliert ODBC 3.x und ODBC 2.x-Anwendungen und diese Anwendungen benötigen einen ODBC 3.8-Treiber, der beim Abrufen von Ausgabeparametern mit unterstützt **SQLGetData** und ODBC 3.8-Treiber -Manager. Informationen zum Aktivieren von älteren Anwendung für die Verwendung der neuer ODBC-Funktionen finden Sie unter [Kompatibilitätsmatrix](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
## <a name="usage-example"></a>Verwendungsbeispiel  
 Betrachten Sie beispielsweise das Ausführen einer gespeicherten Prozedur **{AUFRUF sp_f(?,?)}** , wobei beide Parameter als SQL_PARAM_OUTPUT_STREAM gebunden sind, und die gespeicherte Prozedur kein Resultset zurückgegeben (weiter unten in diesem Thema finden Sie ein komplexeres Szenario):  
  
1.  Rufen Sie für jeden Parameter **SQLBindParameter** mit *InputOutputType* SQL_PARAM_OUTPUT_STREAM festgelegt und *ParameterValuePtr* auf ein Token, z. B. einen Parameter mit der Nummer festlegen , ein Zeiger auf Daten oder ein Zeiger auf eine Struktur, die die Anwendung verwendet, um Eingabeparameter zu binden. In diesem Beispiel wird die Ordnungszahl des Parameters als Token verwenden.  
  
2.  Führen Sie die Abfrage mit **SQLExecDirect** oder **SQLExecute**. SQL_PARAM_DATA_AVAILABLE wird zurückgegeben werden, der angibt, dass gestreamte Output-Parameter für den Abruf verfügbar sind.  
  
3.  Rufen Sie **SQLParamData** zum Abrufen des Parameters, der zum Abrufen verfügbar ist. **SQLParamData** zurück mit dem Token des den ersten verfügbaren Parameter, der festgelegt wird, in SQL_PARAM_DATA_AVAILABLE **SQLBindParameter** (Schritt 1). Das Token wird im Puffer zurückgegeben, die die *ValuePtrPtr* verweist auf.  
  
4.  Rufen Sie **SQLGetData** mit dem Argument *Col*_or\_*Param_Num* an den Parameter ordinal zum Abrufen der Daten von den ersten verfügbaren Parameter festlegen. Wenn **SQLGetData** gibt SQL_SUCCESS_WITH_INFO und SQLState 01004 (Daten abgeschnitten), und die Art ist variabler Länge auf dem Client und Server, gibt es weitere Daten aus dem ersten verfügbaren Parameter abgerufen werden sollen. Sie können weiterhin aufrufen **SQLGetData** bis durch ein anderes SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO zurückgegeben **SQLState**.  
  
5.  Wiederholen Sie Schritt 3 und 4 den aktuellen Parameter abgerufen werden.  
  
6.  Rufen Sie **SQLParamData** erneut aus. Wenn alles außer SQL_PARAM_DATA_AVAILABLE zurückgegeben werden, es ist keine weiteren Parameter Streamingdaten abgerufen, und der Rückgabecode werden den Rückgabecode, der die nächste Anweisung, die ausgeführt wird.  
  
7.  Rufen Sie **SQLMoreResults** um den nächsten Satz von Parametern zu verarbeiten, bis SQL_NO_DATA zurückgegeben. **SQLMoreResults** SQL_NO_DATA wird in diesem Beispiel zurückgegeben werden, wenn das Anweisungsattribut SQL_ATTR_PARAMSET_SIZE auf 1 festgelegt wurde. Andernfalls **SQLMoreResults** zurück SQL_PARAM_DATA_AVAILABLE, um anzugeben, dass gestreamte Output-Parameter für den nächsten Satz von Parametern zum Abrufen verfügbar sind.  
  
 Ähnlich wie bei einem Eingabeparameter DAE das Token im Argument verwendeten *ParameterValuePtr* in **SQLBindParameter** (Schritt 1) kann ein Zeiger, der auf eine Anwendung-Datenstruktur zeigt die enthält die Ordnungszahl des Parameters und weitere anwendungsspezifische Informationen bei Bedarf.  
  
 Die Reihenfolge der zurückgegebenen gestreamte Ausgabe oder Eingabe-/Ausgabeparameter treiberspezifisch ist und möglicherweise nicht immer identisch mit der Reihenfolge, in der Abfrage angegeben.  
  
 Wenn die Anwendung nicht aufruft **SQLGetData** in Schritt 4, wird der Wert des Parameters wird verworfen. Auf ähnliche Weise, wenn die Anwendung aufruft, **SQLParamData** vor allen eines Parameters für einen Wert von gelesen wurden **SQLGetData**, der Rest des Werts wird verworfen und die Anwendung kann die nächste verarbeiten Parameter.  
  
 Wenn die Anwendung aufruft, **SQLMoreResults** vor allen gestreamte Ausgabe Parameter verarbeitet werden (**SQLParamData** SQL_PARAM_DATA_AVAILABLE gibt weiterhin zurück), alle verbleibenden Parameter werden verworfen. Auf ähnliche Weise, wenn die Anwendung aufruft, **SQLMoreResults** vor allen eines Parameters für einen Wert von gelesen wurden **SQLGetData**, der Rest der Werte und alle verbleibenden Parameter werden verworfen, und die Anwendung kann weiter Parametersatz Verarbeitung fort.  
  
 Beachten Sie, dass eine Anwendung die C-Datentyp in beide angeben kann **SQLBindParameter** und **SQLGetData**. Die C-Datentyp mit angegebenen **SQLGetData** überschreibt die C-Datentyp, der im angegebenen **SQLBindParameter**, es sei denn, in der C-Datentyp angegeben **SQLGetData** SQL_APD_TYPE ist.  
  
 Obwohl eine gestreamte Ausgabeparameter mehr nützlich ist, wenn der Datentyp des Output-Parameters vom Typ BLOB ist, kann diese Funktionalität auch mit einem beliebigen Datentyp verwendet werden. Die Datentypen von gestreamte Output-Parameter unterstützt, werden im Treiber angegeben.  
  
 Wenn SQL_PARAM_INPUT_OUTPUT_STREAM-Parameter verarbeitet werden, sind **SQLExecute** oder **SQLExecDirect** werden zuerst SQL_NEED_DATA zurückgegeben. Eine Anwendung kann Aufrufen **SQLParamData** und **SQLPutData** DAE Parameterdaten zu senden. Wenn alle DAE Eingabeparameter verarbeitet werden, **SQLParamData** gibt SQL_PARAM_DATA_AVAILABLE, um anzugeben, gestreamte Output-Parameter sind verfügbar.  
  
 Wenn es Output-Parameter und gebundene Output-Parameter zu verarbeitenden gestreamt werden, bestimmt der Treiber die Reihenfolge für die Verarbeitung von Output-Parameter. Wenn ein Output-Parameter in einen Puffer gebunden ist (die **SQLBindParameter** Parameter *InputOutputType* auf SQL_PARAM_INPUT_OUTPUT oder SQL_PARAM_OUTPUT festgelegt ist), der Puffer kann nicht aufgefüllt werden, bis  **SQLParamData** gibt SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO zurück. Eine Anwendung eine Grenze lesen sollten erst nach Puffern **SQLParamData** gibt SQL_SUCCESS oder SQL_SUCCESS_WITH_INFO, die nach allen Ausgabeparameter gestreamt wird verarbeitet werden.  
  
 Die Datenquelle kann zurück, dass eine Warnung und das Ergebnis, darüber hinaus auf gestreamte Output-Parameters festgelegt. Im Allgemeinen Warnungen und Resultsets werden getrennt verarbeitet aus einem Stream befindlichen Output-Parameter durch den Aufruf **SQLMoreResults**. Prozess Warnungen und das Resultset vor der Verarbeitung der gestreamte Output-Parameter.  
  
 Die folgende Tabelle beschreibt die verschiedene Szenarien eines einzelnen Befehls auf dem Server und die Funktionsweise der Anwendung gesendet.  
  
|Szenario|Rückgabewert von SQLExecute oder SQLExecDirect|Was Sie als Nächstes tun|  
|--------------|---------------------------------------------------|---------------------|  
|Daten nur enthalten gestreamte Output-Parameter.|SQL_PARAM_DATA_AVAILABLE|Verwendung **SQLParamData** und **SQLGetData** abzurufenden gestreamte Output-Parameter.|  
|Enthält das Resultset und Ausgabeparameter|SQL_SUCCESS|Rufen Sie das Resultset mit **SQLBindCol** und **SQLGetData**.<br /><br /> Rufen Sie **SQLMoreResults** Verarbeitung gestreamte Output-Parameter beginnen. Es sollte SQL_PARAM_DATA_AVAILABLE zurückgegeben werden.<br /><br /> Verwendung **SQLParamData** und **SQLGetData** abzurufenden gestreamte Output-Parameter.|  
|Enthält eine Warnmeldung und Ausgabeparameter|SQL_SUCCESS_WITH_INFO|Verwendung **SQLGetDiagRec** und **SQLGetDiagField** zum Verarbeiten von Nachrichten Warnung.<br /><br /> Rufen Sie **SQLMoreResults** Verarbeitung gestreamte Output-Parameter beginnen. Es sollte SQL_PARAM_DATA_AVAILABLE zurückgegeben werden.<br /><br /> Verwendung **SQLParamData** und **SQLGetData** abzurufenden gestreamte Output-Parameter.|  
|Enthält eine Warnmeldung, Resultsets und Ausgabeparameter|SQL_SUCCESS_WITH_INFO|Verwendung **SQLGetDiagRec** und **SQLGetDiagField** zum Verarbeiten von Nachrichten Warnung. Rufen Sie anschließend **SQLMoreResults** legen Sie zum Starten der Verarbeitung des Ergebnisses.<br /><br /> Rufen Sie ein Resultset mit **SQLBindCol** und **SQLGetData**.<br /><br /> Rufen Sie **SQLMoreResults** Verarbeitung gestreamte Output-Parameter beginnen. **SQLMoreResults** SQL_PARAM_DATA_AVAILABLE zurückgeben soll.<br /><br /> Verwendung **SQLParamData** und **SQLGetData** abzurufenden gestreamte Output-Parameter.|  
|Abfrageparameter mit DAE Eingabeparametern, z. B. eine gestreamte Eingabe/Ausgabe (DAE)|SQL-NEED_DATA|Rufen Sie **SQLParamData** und **SQLPutData** DAE senden Eingabe Parameterdaten.<br /><br /> Nachdem alle DAE Eingabeparameter verarbeitet werden, **SQLParamData** zurückgeben kann, einem Rückgabecode, der **SQLExecute** und **SQLExecDirect** zurückgeben kann. Die Fälle in dieser Tabelle können dann angewendet werden.<br /><br /> Wenn der Rückgabecode SQL_PARAM_DATA_AVAILABLE ist, stehen gestreamte Output-Parameter. Muss eine Anwendung aufrufen **SQLParamData** erneut aus, um das Token für die gestreamte Ausgabeparameter abzurufen, wie in der ersten Zeile dieser Tabelle beschrieben.<br /><br /> Wenn der Rückgabecode SQL_SUCCESS lautet, ist es ein Resultset verarbeitet oder die Verarbeitung abgeschlossen ist.<br /><br /> Ist der Rückgabecode SQL_SUCCESS_WITH_INFO, sollten Sie die Warnung Nachrichten zum Verarbeiten vorhanden sind.|  
  
 Nach dem **SQLExecute**, **SQLExecDirect**, oder **SQLMoreResults** gibt SQL_PARAM_DATA_AVAILABLE ein Sequenzfehler Funktion führt, wenn eine Anwendung ruft eine eine Funktion, die nicht in der folgenden Liste ist:  
  
-   **SQLAllocHandle** / **SQLAllocHandleStd**  
  
-   **SQLDataSources** / **SQLDrivers**  
  
-   **SQLGetInfo** / **SQLGetFunctions**  
  
-   **SQLGetConnectAttr** / **SQLGetEnvAttr** / **SQLGetDescField** / **SQLGetDescRec**  
  
-   **SQLNumParams**  
  
-   **SQLDescribeParam**  
  
-   **SQLNativeSql**  
  
-   **SQLParamData**  
  
-   **SQLMoreResults**  
  
-   **SQLGetDiagField** / **SQLGetDiagRec**  
  
-   **SQLCancel**  
  
-   **SQLCancelHandle** (mit Anweisungshandle)  
  
-   **SQLFreeStmt** (klicken Sie mit der Option = SQL_CLOSE, SQL_DROP oder SQL_UNBIND)  
  
-   **SQLCloseCursor**  
  
-   **SQLDisconnect**  
  
-   **SQLFreeHandle** (mit HandleType = SQL_HANDLE_STMT auf)  
  
-   **SQLGetStmtAttr**  
  
 Anwendungen können weiterhin **SQLSetDescField** oder **SQLSetDescRec** Bindungsinformationen über die festgelegt. Feld Zuordnung wird nicht geändert werden. Allerdings können Felder in den Deskriptor neue Werte zurückgeben. Beispielsweise könnte SQL_DESC_PARAMETER_TYPE SQL_PARAM_INPUT_OUTPUT_STREAM oder SQL_PARAM_OUTPUT_STREAM zurückgeben.  
  
## <a name="usage-scenario-retrieve-an-image-in-parts-from-a-result-set"></a>Verwendungsszenario: Abrufen eines Bilds in Teilen aus einem Resultset  
 **SQLGetData** können verwendet werden, um Daten in Teilen abrufen, wenn eine gespeicherte Prozedur gibt ein Resultset, das eine Zeile aus Metadaten zu einem Bild enthält, und das Bild wird in einem großen Output-Parameter zurückgegeben.  
  
```  
// CREATE PROCEDURE SP_TestOutputPara  
//      @ID_of_picture   as int,  
//      @Picture         as varbinary(max) out  
// AS  
//     output the image data through streamed output parameter  
// GO  
BOOL displayPicture(SQLUINTEGER idOfPicture, SQLHSTMT hstmt) {  
   SQLLEN      lengthOfPicture;    // The actual length of the picture.  
   BYTE        smallBuffer[100];   // A very small buffer.  
   SQLRETURN   retcode, retcode2;  
  
   // Bind the first parameter (input parameter)  
   SQLBindParameter(  
         hstmt,  
         1,                         // The first parameter.   
         SQL_PARAM_INPUT,           // Input parameter: The ID_of_picture.  
         SQL_C_ULONG,               // The C Data Type.  
         SQL_INTEGER,               // The SQL Data Type.  
         0,                         // ColumnSize is ignored for integer.  
         0,                         // DecimalDigits is ignored for integer.  
         &idOfPicture,              // The Address of the buffer for the input parameter.  
         0,                         // BufferLength is ignored for integer.  
         NULL);                     // This is ignored for integer.  
  
   // Bind the streamed output parameter.  
   SQLBindParameter(  
         hstmt,   
         2,                         // The second parameter.  
         SQL_PARAM_OUTPUT_STREAM,   // A streamed output parameter.   
         SQL_C_BINARY,              // The C Data Type.    
         SQL_VARBINARY,             // The SQL Data Type.  
         0,                         // ColumnSize: The maximum size of varbinary(max).  
         0,                         // DecimalDigits is ignored for binary type.  
         (SQLPOINTER)2,             // ParameterValuePtr: An application-defined  
                                    // token (this will be returned from SQLParamData).  
                                    // In this example, we used the ordinal   
                                    // of the parameter.  
         0,                         // BufferLength is ignored for streamed output parameters.  
         &lengthOfPicture);         // StrLen_or_IndPtr: The status variable returned.   
  
   retcode = SQLPrepare(hstmt, L"{call SP_TestOutputPara(?, ?)}", SQL_NTS);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   retcode = SQLExecute(hstmt);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   // Assume that the retrieved picture exists.  Use SQLBindCol or SQLGetData to retrieve the result-set.  
  
   // Process the result set and move to the streamed output parameters.  
   retcode = SQLMoreResults( hstmt );  
  
   // SQLGetData retrieves and displays the picture in parts.  
   // The streamed output parameter is available.  
   while (retcode == SQL_PARAM_DATA_AVAILABLE) {  
      SQLPOINTER token;   // Output by SQLParamData.  
      SQLLEN cbLeft;      // #bytes remained  
      retcode = SQLParamData(hstmt, &token);   // returned token is 2 (according to the binding)  
      if ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
         // A do-while loop retrieves the picture in parts.  
         do {  
            retcode2 = SQLGetData(   
               hstmt,   
               (UWORD) token,          // the value of the token is the ordinal.   
               SQL_C_BINARY,           // The C-type.  
               smallBuffer,            // A small buffer.   
               sizeof(smallBuffer),    // The size of the buffer.  
               &cbLeft);               // How much data we can get.  
         }  
         while ( retcode2 == SQL_SUCCESS_WITH_INFO );  
      }  
   }  
  
   return TRUE;  
}  
```  
  
## <a name="usage-scenario-send-and-receive-a-large-object-as-a-streamed-inputoutput-parameter"></a>Verwendungsszenario: Senden und Empfangen von ein großes Objekt als eine gestreamte Eingabe-/Ausgabeparameter  
 **SQLGetData** abrufen und Senden von Daten in Teilen, wenn eine gespeicherte Prozedur übergeben wird, ein großes Objekt als Eingabe/Ausgabe-Parameter, den Wert in und aus der Datenbank streaming verwendet werden können. Sie müssen nicht alle Daten im Arbeitsspeicher speichern.  
  
```  
// CREATE PROCEDURE SP_TestInOut  
//       @picture as varbinary(max) out  
// AS  
//    output the image data through output parameter   
// go  
  
BOOL displaySimilarPicture(BYTE* image, ULONG lengthOfImage, SQLHSTMT hstmt) {  
   BYTE smallBuffer[100];   // A very small buffer.  
   SQLRETURN retcode, retcode2;  
   SQLLEN statusOfPicture;  
  
   // First bind the parameters, before preparing the statement that binds the output streamed parameter.  
   SQLBindParameter(  
      hstmt,   
      1,                                 // The first parameter.  
      SQL_PARAM_INPUT_OUTPUT_STREAM,     // I/O-streamed parameter: The Picture.  
      SQL_C_BINARY,                      // The C Data Type.  
      SQL_VARBINARY,                     // The SQL Data Type.  
      0,                                 // ColumnSize: The maximum size of varbinary(max).  
      0,                                 // DecimalDigits is ignored.   
      (SQLPOINTER)1,                     // An application defined token.   
      0,                                 // BufferLength is ignored for streamed I/O parameters.  
      &statusOfPicture);                 // The status variable.  
  
   statusOfPicture = SQL_DATA_AT_EXEC;   // Input data in parts (DAE parameter at input).  
  
   retcode = SQLPrepare(hstmt, L"{call SP_TestInOut(?) }", SQL_NTS);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   // Execute the statement.  
   retcode = SQLExecute(hstmt);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   if ( retcode == SQL_NEED_DATA ) {  
      // Use SQLParamData to loop through DAE input parameters.  For  
      // each, use SQLPutData to send the data to database in parts.  
  
      // This example uses an I/O parameter with streamed output.  
      // Therefore, the last call to SQLParamData should return  
      // SQL_PARAM_DATA_AVAILABLE to indicate the end of the input phrase   
      // and report that a streamed output parameter is available.  
  
      // Assume retcode is set to the return value of the last call to  
      // SQLParamData, which is equal to SQL_PARAM_DATA_AVAILABLE.  
   }  
  
   // Start processing the streamed output parameters.  
   while ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
      SQLPOINTER token;   // Output by SQLParamData.  
      SQLLEN cbLeft;     // #bytes remained  
      retcode = SQLParamData(hstmt, &token);  
      if ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
         do {  
            retcode2 = SQLGetData(   
               hstmt,   
               (UWORD) token,          // the value of the token is the ordinal.   
               SQL_C_BINARY,           // The C-type.  
               smallBuffer,            // A small buffer.   
               sizeof(smallBuffer),    // The size of the buffer.  
               &cbLeft);               // How much data we can get.  
         }  
         while ( retcode2 == SQL_SUCCESS_WITH_INFO );  
      }  
   }   
  
   return TRUE;  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Anweisungsparametern](../../../odbc/reference/develop-app/statement-parameters.md)

