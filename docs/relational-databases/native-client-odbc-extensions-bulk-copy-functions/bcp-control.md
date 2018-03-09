---
title: Bcp_control | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- bcp_control
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_control function
ms.assetid: 32187282-1385-4c52-9134-09f061eb44f5
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 41d583812419f62ab7e9822fefaaac1a8b82a1f7
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/24/2018
---
# <a name="bcpcontrol"></a>bcp_control
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Ändert die Standardeinstellungen für verschiedene Steuerelementparameter für einen Massenkopiervorgang zwischen einer Datei und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Syntax  
  
```  
  
RETCODE bcp_control (  
        HDBC hdbc,  
        INT eOption,  
        void* iValue);  
```  
  
## <a name="arguments"></a>Argumente  
 *HDBC*  
 Das für den Massenkopiervorgang aktivierte ODBC-Verbindungshandle.  
  
 *eOption*  
 Ist einer der folgenden Werte:  
  
 BCPABORT  
 Beendet einen Massenkopiervorgang, der bereits ausgeführt wird. Rufen Sie **Bcp_control** mit einem *eOption* -Wert bcpabort von einem anderen Thread zum Beenden einer laufenden Massenkopiervorgang. Die *iValue* Parameter wird ignoriert.  
  
 BCPBATCH  
 Die Anzahl von Zeilen pro Batch. Der Standardwert ist 0, womit beim Extrahieren von Daten alle Zeilen in einer Tabelle oder beim Kopieren von Daten nach [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alle Zeilen in der Benutzerdatendatei angegeben werden. Ein Wert kleiner als 1 setzt BCPBATCH auf den Standardwert zurück.  
  
 BCPDELAYREADFMT  
 Ein boolescher Wert, wenn auf True festgelegt, führt dazu, dass [Bcp_readfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md) , bei der Ausführung zu lesen. Wenn "false" (Standard), Bcp_readfmt sofort wird die Formatdatei zu lesen. Ein Sequenzfehler tritt auf, wenn BCPDELAYREADFMT "true ist", und Sie Bcp_columns oder Bcp_setcolfmt rufen.  
  
 Ein Sequenzfehler tritt auch beim Aufrufen `bcp_control(hdbc,` BCPDELAYREADFMT`, (void *)FALSE)` nach dem Aufruf `bcp_control(hdbc,` BCPDELAYREADFMT`, (void *)TRUE)` und Bcp_writefmt.  
  
 Weitere Informationen finden Sie unter [Metadatenermittlung](../../relational-databases/native-client/features/metadata-discovery.md).  
  
 BCPFILECP  
 *iValue* enthält die Nummer der Codepage für die Datendatei an. Sie können die Nummer der Codepage angeben, z. B. 1252 oder 850 bzw. einen der folgenden Werte  
  
 BCPFILE_ACP: Daten in der Datei befinden sich auf der Microsoft Windows® Codepage des Clients.  
  
 BCPFILE_OEMCP: Daten in der Datei befinden sich auf der OEM-Codepage des Clients (Standard).  
  
 BCPFILE_RAW: Daten in der Datei befinden sich auf der Codepage von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 BCPFILEFMT  
 Die Versionsnummer des Datendateiformats. Dies kann 80 ([!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]), 90 ([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]), 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] oder [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]), 110 ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]), oder 120 ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]). Der Standardwert ist 120. Dies ist beim Exportieren und Importieren von Daten in Formate nützlich, die in früheren Versionen des Servers unterstützt wurden. Z. B. zum Importieren von Daten, die aus einer Textspalte abgerufen wurde eine [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Server in einer **varchar(max)** Spalte in einer [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Server oder höher, sollten Sie 80 angeben. Auf ähnliche Weise, wenn Sie beim Exportieren von Daten von 80 angeben eine **varchar(max)** Spalte wird gespeichert wie Textspalten im gespeichert werden die [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] formatieren und können in einer Textspalte importiert werden eine [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Server.  
  
 BCPFIRST  
 Dies ist die erste Datenzeile der zu kopierenden Datei oder Tabelle. Der Standard ist 1; ein Wert kleiner als 1 setzt diese Option auf den Standardwert zurück.  
  
 BCPFIRSTEX  
 Gibt für BCP-OUT-Vorgänge die erste Zeile der Datenbanktabelle an, die in die Datendatei kopiert werden soll.  
  
 Gibt für BCP-IN-Vorgänge die erste Zeile der Datendatei an, die in die Datenbanktabelle kopiert werden soll.  
  
 Die *iValue* Parameter muss die Adresse einer 64-Bit-Ganzzahl mit Vorzeichen, die den Wert sein. Der maximale Wert, der an BCPFIRSTEX übergeben werden kann, beträgt 2 ^ 63-1.  
  
 BCPFMTXML  
 Gibt an, dass die generierte Formatdatei im XML-Format sein soll. Es ist standardmäßig deaktiviert.  
  
 XML-Formatdateien bieten größere Flexibilität, sind jedoch mit einigen Einschränkungen verbunden. Beispielsweise können Sie nicht das Präfix und das Abschlusszeichen für ein Feld gleichzeitig angeben in älteren Formatdateien möglich war.  
  
> [!NOTE]  
>  XML-Formatdateien werden nur unterstützt, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zusammen mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client installiert wird.  
  
 BCPHINTS  
 *iValue* enthält einen SQLTCHAR-Zeichenfolgenzeiger. Die adressierte Zeichenfolge gibt entweder Verarbeitungshinweise für das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Massenkopieren oder eine Transact-SQL-Anweisung an, die ein Resultset zurückgibt. Wenn eine Transact-SQL-Anweisung angegeben ist, die mehr als ein Resultset zurückgibt, werden alle auf das erste Resultset folgenden Resultsets nicht berücksichtigt. Weitere Informationen zum Massenkopieren Verarbeitungshinweise, finden Sie unter [Bcp (Hilfsprogramm)](../../tools/bcp-utility.md).  
  
 BCPKEEPIDENTITY  
 Wenn *iValue* ist "true", gibt an, dass Massenkopierfunktionen Datenwerte, die für einen bereitgestellten einfügen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Spalten mit einer Identity-Einschränkung definiert. Die Eingabedatei muss Werte für die IDENTITY-Spalten angeben. Wenn dies nicht festgelegt ist, werden neue Identitätswerte für die eingefügten Zeilen generiert. Alle in der Datei für die IDENTITY-Spalten vorhandenen Daten werden ignoriert.  
  
 BCPKEEPNULLS  
 Bestimmt, ob leere Datenwerte in der Datei in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle in NULL-Werte konvertiert werden. Wenn *iValue* ist "true", werden leere Werte konvertiert werden, auf NULL in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelle. In der Standardeinstellung werden leere Werte in einen Standardwert für die Spalte in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle konvertiert, sofern ein Standardwert angegeben ist.  
  
 BCPLAST  
 Entspricht der letzten zu kopierenden Zeile. In der Standardeinstellung werden alle Zeilen kopiert. Ein Wert kleiner als 1 setzt diese Option auf den Standardwert zurück.  
  
 BCPLASTEX  
 Gibt für BCP-OUT-Vorgänge die letzte Zeile der Datenbanktabelle an, die in die Datendatei kopiert werden soll.  
  
 Gibt für BCP-IN-Vorgänge die letzte Zeile der Datendatei an, die in die Datenbanktabelle kopiert werden soll.  
  
 Die *iValue* Parameter muss die Adresse einer 64-Bit-Ganzzahl mit Vorzeichen, die den Wert sein. Der maximale Wert, der an BCPLASTEX übergeben werden kann, ist 2^63-1.  
  
 BCPMAXERRS  
 Gibt die Anzahl von Fehlern an, die zulässig sind, bevor der Massenkopiervorgang fehlschlägt. Der Standardwert ist 10. ein Wert kleiner als 1 setzt diese Option auf den Standardwert zurück. Beim Massenkopieren sind maximal 65.535 Fehler zulässig. Wenn für diese Option größere Werte als 65.535 festgelegt werden, wird diese Option auf 65.535 festgelegt.  
  
 BCPODBC  
 Bei "true", gibt an, dass **"DateTime"** und **Smalldatetime** ODBC-Zeitstempel Escape-Sequenz-Präfix und Suffix im Zeichenformat gespeicherten Werte verwendet. Die BCPODBC-Option gilt nur für DB_OUT.  
  
 Bei "false", ein **"DateTime"** Wert, der 1. Januar 1997 darstellt, wird in der Zeichenfolge konvertiert: 1997-01-01-00:00:00.000. Wenn "true", die gleiche **"DateTime"** -Wert wie folgt dargestellt: {ts ' 1997-01-01 00:00:00.000 "}.  
  
 BCPROWCOUNT  
 Gibt die Anzahl von Zeilen zurück, auf die sich der aktuelle (oder letzte) BCP-Vorgang auswirkt.  
  
 BCPTEXTFILE  
 Wenn der Wert TRUE ist, wird angegeben, dass die Datendatei eine Textdatei und keine Binärdatei ist. Bei einer Textdatei bestimmt BCP, ob es sich um Unicode handelt, indem der Unicode-Bytemarker in den ersten beiden Bytes der Datendatei überprüft wird.  
  
 BCPUNICODEFILE  
 Wenn der Wert TRUE ist, wird angegeben, dass die Eingabedatei eine Unicode-Datei ist.  
  
 *iValue*  
 Ist der Wert für den angegebenen *eOption*. *iValue* für zukünftige Erweiterungen auf 64-Bit-Werte zulassen einen void-Zeiger ist ein Ganzzahlwert (LONGLONG) umgewandelt.  
  
## <a name="returns"></a>Rückgabewert  
 SUCCEED oder FAIL.  
  
## <a name="remarks"></a>Hinweise  
 Mit dieser Funktion werden verschiedene Steuerelementparameter für Massenkopiervorgänge festgelegt, einschließlich der Anzahl von Fehlern, die vor dem Abbrechen eines Massenkopiervorgangs zulässig sind, der Nummern der ersten und letzten Zeilen, die aus einer Datendatei kopiert werden sollen, und der Batchgröße.  
  
 Außerdem wird diese Funktion dazu verwendet, die SELECT-Anweisung beim Massenkopieren des Resultsets einer SELECT-Anweisung aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anzugeben. Legen Sie *eOption* auf BCPHINTS und *iValue* haben einen Zeiger auf eine SQLTCHAR-Zeichenfolge, die die SELECT-Anweisung enthält.  
  
 Diese Steuerelementparameter sind nur beim Kopieren zwischen einer Benutzerdatei und einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Tabelle sinnvoll. Steuerelementparameter-Einstellungen haben keine Auswirkungen auf Zeilen in kopiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit [Bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md).  
  
## <a name="example"></a>Beispiel  
  
```  
// Variables like henv not specified.  
SQLHDBC      hdbc;  
DBINT      nRowsProcessed;  
  
// Application initiation, get an ODBC environment handle, allocate the  
// hdbc, and so on.  
...   
  
// Enable bulk copy prior to connecting on allocated hdbc.  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP, (SQLPOINTER) SQL_BCP_ON,  
   SQL_IS_INTEGER);  
  
// Connect to the data source, return on error.  
if (!SQL_SUCCEEDED(SQLConnect(hdbc, _T("myDSN"), SQL_NTS,  
   _T("myUser"), SQL_NTS, _T("myPwd"), SQL_NTS)))  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Initialize bulk copy.   
if (bcp_init(hdbc, _T("address"), _T("address.add"), _T("addr.err"),  
   DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Set the number of rows per batch.   
if (bcp_control(hdbc, BCPBATCH, (void*) 1000) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Set file column count.   
if (bcp_columns(hdbc, 1) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Set the file format.   
if (bcp_colfmt(hdbc, 1, 0, 0, SQL_VARLEN_DATA, '\n', 1, 1)  
   == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Execute the bulk copy.   
if (bcp_exec(hdbc, &nRowsProcessed) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
printf_s("%ld rows processed by bulk copy.", nRowsProcessed);  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Funktionen zum Massenkopieren](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
