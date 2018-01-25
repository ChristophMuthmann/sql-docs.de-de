---
title: Bcp_bind | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: bcp_bind
apilocation: sqlncli11.dll
apitype: DLLExport
helpviewer_keywords: bcp_bind function
ms.assetid: 6e335a5c-64b2-4bcf-a88f-35dc9393f329
caps.latest.revision: "47"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9efa0570e0ffe698fccb7decb6eafbf5877842db
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/24/2018
---
# <a name="bcpbind"></a>bcp_bind
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Bindet Daten einer Programmvariablen an eine Tabellenspalte im Hinblick auf einen Massenkopiervorgang in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RETCODE bcp_bind (  
        HDBC hdbc,   
        LPCBYTE pData,  
        INT cbIndicator,  
        DBINT cbData,  
        LPCBYTE pTerm,  
        INT cbTerm,  
        INT eDataType,  
        INT idxServerCol);  
```  
  
## <a name="arguments"></a>Argumente  
 *HDBC*  
 Das für den Massenkopiervorgang aktivierte ODBC-Verbindungshandle.  
  
 *pData*  
 Ein Zeiger auf die kopierten Daten. Wenn *eDataType* SQLTEXT, SQLNTEXT, SQLXML, SQLUDT, SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SQLBINARY, SQLNCHAR oder SQLIMAGE ist, wird *pData* kann NULL sein. Ein NULL-Wert *pData* gibt an, dass lange Datenwerte zu sendende [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Segmenten mit [Bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md). Der Benutzer sollte nur festgelegt *pData* auf NULL, wenn der Benutzer-gebundenen Feld entsprechende Spalte eine BLOB-Spalte, andernfalls ist **Bcp_bind** schlägt fehl.  
  
 Falls Indikatoren in den Daten vorhanden sind, stehen sie im Speicher direkt vor den Daten. Die *pData* Parameter verweist auf die Indikatorvariable in diesem Fall und die Breite des Indikators, den *CbIndicator* Parameter durch Massenkopieren, um die Benutzerdaten ordnungsgemäß verwendet wird.  
  
 *cbIndicator*  
 Die Länge eines Längen- oder NULL-Indikators für die Spaltendaten in Byte. Gültige Indikatorlängenwerte sind 0 (wenn kein Indikator verwendet wird), 1, 2, 4 oder 8. Indikatoren stehen im Speicher direkt vor allen Daten. Beispielsweise könnte die folgende Strukturtypdefinition verwendet werden, um für einen Massenkopiervorgang Ganzzahlwerte in eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle einzufügen:  
  
```  
typedef struct tagBCPBOUNDINT  
    {  
    int iIndicator;  
    int Value;  
    } BCPBOUNDINT;  
```  
  
 In diesem Beispiel das *pData* Parametersatz würde an die Adresse einer deklarierten Instanz der Struktur, die die Adresse des dem IINDICATOR *iIndicator* Strukturmember. Die *CbIndicator* Parametersatz würde auf die Größe einer ganzen Zahl ((sizeof(int)), und die *CbData* Parameter würde erneut festgelegt werden, um die Größe einer ganzen Zahl ((sizeof(int)). Zum Massenkopieren eine Zeile mit dem Server, die eine NULL-Wert für die gebundene Spalte den Wert der Instanz *iIndicator* Element sollte auf SQL_NULL_DATA festgelegt werden.  
  
 *cbData*  
 Die Anzahl der Datenbytes in der Programmvariablen ohne die Länge eventuell vorhandener Längenindikatoren, NULL-Indikatoren oder Abschlusszeichen.  
  
 Festlegen von *CbData* auf SQL_NULL_DATA gibt an, dass alle an den Server kopierten Zeilen einen NULL-Wert für die Spalte enthalten.  
  
 Festlegen von *CbData* auf SQL_VARLEN_DATA an, dass das System ein zeichenfolgenabschlusszeichen verwenden die andere Methode, um zu bestimmen, die Länge der Daten kopiert.  
  
 Bei Datentypen mit fester Länge wie ganzen Zahlen gibt der Datentyp dem System die Länge der Daten an. Aus diesem Grund für Datentypen mit fester Länge *CbData* kann problemlos auf sql_varlen_data festgelegt ist oder die Länge der Daten.  
  
 Für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zeichen und Binärdatentypen *CbData* kann SQL_VARLEN_DATA, SQL_NULL_DATA, ein positiver Wert oder 0 sein. Wenn *CbData* auf sql_varlen_data festgelegt, verwendet das System ein Längen-/Null-Indikator (falls vorhanden) oder eine abschlusszeichensequenz, um die Länge der Daten zu bestimmen. Wenn beide Indikatoren bereitgestellt werden, verwendet das System beim Massenkopieren den Wert, der zu der kleineren zu kopierenden Datenmenge führt. Wenn *CbData* auf sql_varlen_data festgelegt, der Datentyp der Spalte ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zeichen- oder Binärdatentyp ist und weder ein Längenindikator noch eine abschlusszeichensequenz angegeben ist, gibt das System eine Fehlermeldung zurück.  
  
 Wenn *CbData* 0 oder ein positiver Wert sein, das System verwendet *CbData* als Datenlänge. Allerdings If, zusätzlich zu einem positiven *CbData* Wert, eine Länge Längenindikator oder eine abschlusszeichensequenz angegeben ist, bestimmt das System die Datenlänge mithilfe der Methode, führt die geringste Menge an Daten, die kopiert werden.  
  
 Die *CbData* Parameterwert stellt die Anzahl der Datenbytes dar. Zeichendaten durch Unicode-Zeichen, und klicken Sie dann auf einen positiven dargestellt *CbData* Parameterwert darstellt, die Anzahl der Zeichen multipliziert mit der Größe in Byte der einzelnen Zeichen.  
  
 *pTerm*  
 Ein Zeiger auf das Bytemuster, falls vorhanden, das das Ende dieser Programmvariablen markiert. Beispielsweise weisen ANSI- und MBCS-C-Zeichenfolgen normalerweise ein 1-Byte-Abschlusszeichen (\0) auf.  
  
 Wenn kein Abschlusszeichen für die Variable vorhanden ist, legen Sie *pTerm* auf NULL.  
  
 Sie können eine leere Zeichenfolge ("") verwenden, um das C-NULL-Abschlusszeichen als Programmvariablen-Abschlusszeichen festzulegen. Da die Null-terminierte leere Zeichenfolge ein einzelnes Byte (das abschlusszeichenbyte selbst) ausmachen, legen Sie *CbTerm* auf 1. Beispielsweise, um anzugeben, dass die Zeichenfolge in *SzName* Null-terminiert ist und dass das Abschlusszeichen verwendet werden soll, um die Länge anzugeben:  
  
```  
bcp_bind(hdbc, szName, 0,  
   SQL_VARLEN_DATA, "", 1,  
   SQLCHARACTER, 2)  
```  
  
 In einer abgewandelten Form dieses Beispiels kann hinweisen, dass 15 Zeichen kopiert werden die *SzName* Variable auf der zweiten Spalte der gebundenen Tabelle:  
  
```  
bcp_bind(hdbc, szName, 0, 15,   
   NULL, 0, SQLCHARACTER, 2)  
```  
  
 Die API für das Massenkopieren führt nach Bedarf eine Zeichenkonvertierung von Unicode in MBCS aus. Stellen Sie sicher, dass sowohl die Bytezeichenfolge des Abschlusszeichens als auch die Länge der Bytezeichenfolge richtig festgelegt sind. Angenommen, um anzugeben, dass die Zeichenfolge in *SzName* ist eine Unicode-Doppelbyte-Zeichenfolge von Unicode-null-abschlusszeichenwert beendet:  
  
```  
bcp_bind(hdbc, szName, 0,   
   SQL_VARLEN_DATA, L"",  
   sizeof(WCHAR), SQLNCHAR, 2)  
```  
  
 Wenn die Grenze [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Spalte Breitzeichen ist, erfolgt keine Konvertierung auf [Bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md). Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Spalte vom Typ MBCS-Zeichen ist, wird eine Konvertierung von Doppelbytezeichen in Multibytezeichen durchgeführt, wenn die Daten an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gesendet werden.  
  
 *cbTerm*  
 Anzahl von Bytes im Abschlusszeichen für die Programmvariable, falls vorhanden. Wenn kein Abschlusszeichen für die Variable vorhanden ist, legen Sie *CbTerm* auf 0.  
  
 *eDataType*  
 Der C-Datentyp der Programmvariablen. Die Daten in der Programmvariablen werden in den Typ der Datenbankspalte konvertiert. Wenn dieser Parameter 0 ist, wird keine Konvertierung ausgeführt.  
  
 Die *eDataType* Parameter aufgelistet, indem die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datentyptoken in sqlncli.h, nicht die ODBC C-datentypenumeratoren. Beispielsweise können Sie eine 2-Byte-Ganzzahl, ODBC-Typ SQL_C_SHORT, angeben, indem Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-spezifischen Typ SQLINT2 verwenden.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]führte die Unterstützung für SQLXML und SQLUDT Datentyptoken in der ***eDataType*** Sie diesen Parameter verwenden.  
  
 *idxServerCol*  
 Die Ordnungsposition der Spalte in der Datenbanktabelle, in die die Daten kopiert werden. Die erste Spalte einer Tabelle ist die Spalte 1. Die Ordnungsposition einer Spalte wird von [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md)ausgegeben.  
  
## <a name="returns"></a>Rückgabewert  
 SUCCEED oder FAIL.  
  
## <a name="remarks"></a>Hinweise  
 Verwendung **Bcp_bind** für eine schnelle und effiziente Möglichkeit zum Kopieren von Daten aus einer Programmvariablen in eine Tabelle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Rufen Sie [Bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) bevor dies oder jede andere Funktion zum Massenkopieren aufrufen. Aufrufen von **Bcp_init** legt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Zieltabelle für das Massenkopieren. Beim Aufrufen von **Bcp_init** für die Verwendung mit **Bcp_bind** und [Bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md), **Bcp_init** *SzDataFile*-Parameter, der angibt, der Datendatei wird auf NULL; festgelegt. die **Bcp_init *** eDirection* -Parameter auf DB_IN festgelegt ist.  
  
 Führen Sie einen separaten **Bcp_bind** rufen Sie für jede Spalte in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle in die Sie kopieren möchten. Wenn alle erforderlichen **Bcp_bind** Aufrufe vorgenommen wurden, und rufen dann **Bcp_sendrow** , senden eine Zeile mit Daten von Ihren Programmvariablen an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Das erneute Binden einer Spalte wird nicht unterstützt.  
  
 Bei Bedarf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aufrufen, um die bereits empfangenen Zeilen zu speichern, [Bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md). Rufen Sie z. B. **Bcp_batch** einmal nach jeweils 1000 Zeilen eingefügt oder beliebiges anderes Intervall.  
  
 Wenn es keine weiteren Zeilen mehr sind eingefügt werden, rufen Sie [Bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md). Andernfalls wird ein Fehler ausgelöst.  
  
 Steuerparametereinstellungen, die mit angegebenen [Bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md), wirken sich nicht auf **Bcp_bind** zeilenübertragungen.  
  
 Wenn *pData* für eine Spalte auf NULL festgelegt wird, da sein Wert durch Aufrufe von bereitgestellt werden, [Bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md), alle nachfolgenden Spalten mit *eDataType* SQLText, SQLNTEXT, festlegen SQLXML, SQLUDT, SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SQLBINARY, SQLNCHAR oder SQLIMAGE muss auch mit gebunden *pData* auf NULL festgelegt, und ihre Werte müssen auch angegeben werden, durch Aufrufe von **Bcp_moretext**.  
  
 Für neue große Werttypen wie z. B. **varchar(max)**, **varbinary(max)**, oder **nvarchar(max)**, können Sie SQLCHARACTER, SQLVARCHAR, SQLVARBINARY, SQLBINARY und SQLNCHAR als typindikatoren im die *eDataType* Parameter.  
  
 Wenn *CbTerm* ist nicht 0 ist, einen beliebigen Wert (1, 2, 4 oder 8) ist ungültig für das Präfix (*CbIndicator*). In diesem Fall [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client wird das Abschlusszeichen suchen, berechnet die Datenlänge in Bezug auf das Abschlusszeichen (*ich*), und legen Sie die *CbData* auf den kleineren Wert von i und den Wert des Präfix.  
  
 Wenn *CbTerm* ist 0 und *CbIndicator* (Präfix) ist nicht 0 (null) *CbIndicator* muss 8 sein. Das 8-Byte-Präfix kann die folgenden Werte annehmen:  
  
-   0xFFFFFFFFFFFFFFFF bedeutet einen NULL-Wert für das Feld.  
  
-   0xFFFFFFFFFFFFFFFE wird als spezieller Präfixwert behandelt und wird für die effiziente Übertragung von Datensegmenten an den Server verwendet. Die Daten mit diesem speziellen Präfix weisen das folgende Format auf:  
  
-   < SPECIAL_PREFIX > \<0 oder mehr DATA CHUNKS >< ZERO_CHUNK >, in denen:  
  
-   SPECIAL_PREFIX 0xFFFFFFFFFFFFFFFE entspricht.  
  
-   DATA_CHUNK ist ein 4-Byte-Präfix, das die Länge des Segments enthält, gefolgt von den Daten selbst, deren Länge in dem 4-Byte-Präfix angegeben ist.  
  
-   ZERO_CHUNK ist ein 4-Byte-Wert, der alle Nullen (00000000) enthält, die das Ende der Daten angeben.  
  
-   Jede andere gültige 8 Byte-Länge wird als reguläre Datenlänge behandelt.  
  
 Aufrufen von [Bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) Verwendung **Bcp_bind** führt zu einem Fehler.  
  
## <a name="bcpbind-support-for-enhanced-date-and-time-features"></a>bcp_bind-Unterstützung für erweiterte Funktionen für Datum und Uhrzeit  
 Informationen zu den Arten der Verwendung der *eDataType* -Parameter für Datum/Uhrzeit-Typen finden Sie unter [Massenkopieränderungen für erweiterte Datums- und Uhrzeittypen &#40; OLE DB und ODBC &#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
 Weitere Informationen finden Sie unter [Datum und Uhrzeit-Verbesserungen &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="example"></a>Beispiel  
  
```  
#include sql.h  
#include sqlext.h  
#include odbcss.h  
// Variables like henv not specified.  
HDBC      hdbc;  
char         szCompanyName[MAXNAME];  
DBINT      idCompany;  
DBINT      nRowsProcessed;  
DBBOOL      bMoreData;  
char*      pTerm = "\t\t";  
  
// Application initiation, get an ODBC environment handle, allocate the  
// hdbc, and so on.  
...   
  
// Enable bulk copy prior to connecting on allocated hdbc.  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP, (SQLPOINTER) SQL_BCP_ON,  
   SQL_IS_INTEGER);  
  
// Connect to the data source; return on error.  
if (!SQL_SUCCEEDED(SQLConnect(hdbc, _T("myDSN"), SQL_NTS,  
   _T("myUser"), SQL_NTS, _T("myPwd"), SQL_NTS)))  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Initialize bcp.   
if (bcp_init(hdbc, "comdb..accounts_info", NULL, NULL  
   DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Bind program variables to table columns.   
if (bcp_bind(hdbc, (LPCBYTE) &idCompany, 0, sizeof(DBINT), NULL, 0,  
   SQLINT4, 1)    == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_bind(hdbc, (LPCBYTE) szCompanyName, 0, SQL_VARLEN_DATA,  
   (LPCBYTE) pTerm, strnlen(pTerm, sizeof(pTerm)), SQLCHARACTER, 2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
while (TRUE)  
   {  
   // Retrieve and process program data.   
   if ((bMoreData = getdata(&idCompany, szCompanyName)) == TRUE)  
      {  
      // Send the data.   
      if (bcp_sendrow(hdbc) == FAIL)  
         {  
         // Raise error and return.  
         return;  
         }  
      }  
   else  
      {  
      // Break out of loop.  
      break;  
      }  
   }  
  
// Terminate the bulk copy operation.  
if ((nRowsProcessed = bcp_done(hdbc)) == -1)  
   {  
   printf_s("Bulk-copy unsuccessful.\n");  
   return;  
   }  
  
printf_s("%ld rows copied.\n", nRowsProcessed);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen zum Massenkopieren](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
