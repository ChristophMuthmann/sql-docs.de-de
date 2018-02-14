---
title: Zugreifen auf FILESTREAM-Daten mit OpenSqlFilestream | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: blob
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- OpenSqlFilestream
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- OpenSqlFilestream
ms.assetid: d8205653-93dd-4599-8cdf-f9199074025f
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3959deb132236ba93119e42f320970733fb0e01c
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="access-filestream-data-with-opensqlfilestream"></a>ZUgreifen auf FILESTREAM-Daten mit OpenSqlFilestream
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Die OpenSqlFilestream-API ruft ein Win32-kompatibles Dateihandle für ein im Dateisystem gespeichertes FILESTREAM-Blob (Binary Large Object) ab. Das Handle kann an eine der folgenden Windows32-APIs übergeben werden: [ReadFile](http://go.microsoft.com/fwlink/?LinkId=86422), [WriteFile](http://go.microsoft.com/fwlink/?LinkId=86423), [TransmitFile](http://go.microsoft.com/fwlink/?LinkId=86424), [SetFilePointer](http://go.microsoft.com/fwlink/?LinkId=86425), [SetEndOfFile](http://go.microsoft.com/fwlink/?LinkId=86426)oder [FlushFileBuffers](http://go.microsoft.com/fwlink/?LinkId=86427). Wenn Sie dieses Handle an eine andere Win32-API übergeben, wird der Fehler ERROR_ACCESS_DENIED zurückgegeben. Sie müssen das Handle schließen, indem Sie es an die Win32- [CloseHandle](http://go.microsoft.com/fwlink/?LinkId=86428) -API übergeben, bevor für die Transaktion ein Commit oder ein Rollback ausgeführt wird. Wenn das Handle nicht geschlossen wird, treten serverseitige Ressourcenverluste auf.  
  
 ALLE Zugriffe auf FILESTREAM-Datencontainer müssen in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Transaktion erfolgen. [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen können ebenfalls in der gleichen Transaktion ausgeführt werden. Damit wird die Konsistenz zwischen SQL-Daten und FILESTREAM-BLOB gewahrt.  
  
 Um mit Win32 auf FILESTREAM BLOB-Daten zuzugreifen, muss die [Windows-Autorisierung](../../relational-databases/security/choose-an-authentication-mode.md) aktiviert sein.  
  
> [!IMPORTANT]  
>  Wenn die Datei für Schreibzugriff geöffnet wird, ist der FILESTREAM-Agent der Besitzer der Transaktion. Es sind nur Win32-Datei-E/A-Vorgänge zulässig, bis die Transaktion freigegeben wird. Um die Transaktion freigeben zu können, muss das Schreibhandle geschlossen werden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
HANDLE OpenSqlFilestream (  
    LPCWSTR FilestreamPath,  
    SQL_FILESTREAM_DESIRED_ACCESS DesiredAccess,  
    ULONG OpenOptions,  
    LPBYTE FilestreamTransactionContext,  
    SIZE_T FilestreamTransactionContextLength,  
    PLARGE_INTEGER AllocationSize);  
```  
  
#### <a name="parameters"></a>Parameter  
 *FilestreamPath*  
 [in] Ist der **nvarchar(max)** -Pfad, der von der Funktion [PathName](../../relational-databases/system-functions/pathname-transact-sql.md) zurückgegeben wird. Der Aufruf von PathName muss von einem Konto erfolgen, das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SELECT- oder UPDATE-Berechtigungen für die FILESTREAM-Tabelle und -Spalte hat.  
  
 *DesiredAccess*  
 [in] Legt den verwenden Modus so fest, dass ein Zugriff auf FILESTREAM-BLOB-Daten erfolgt. Dieser Wert wird an die Funktion [DeviceIoControl](http://go.microsoft.com/fwlink/?LinkId=105527)übergeben.  
  
|Name|value|Bedeutung|  
|----------|-----------|-------------|  
|SQL_FILESTREAM_READ|0|Aus der Datei können Daten gelesen werden.|  
|SQL_FILESTREAM_WRITE|1|In die Datei können Daten geschrieben werden.|  
|SQL_FILESTREAM_READWRITE|2|Daten können aus der Datei gelesen und in diese geschrieben werden.|  
  
> [!NOTE]  
>  Diese Werte werden in der SQL_FILESTREAM_DESIRED_ACCESS-Enumeration in sqlncli.h definiert.  
  
 *OpenOptions*  
 [in] Die Dateiattribute und Flags. Dieser Parameter kann auch jede Kombination der folgenden Flags umfassen.  
  
|Flag|value|Bedeutung|  
|----------|-----------|-------------|  
|SQL_FILESTREAM_OPEN_NONE|0x00000000:|Die Datei wird geöffnet oder ohne besondere Optionen erstellt.|  
|SQL_FILESTREAM_OPEN_FLAG_ASYNC|0x00000001L|Die Datei wird geöffnet oder für asynchrone E/A erstellt.|  
|SQL_FILESTREAM_OPEN_FLAG_NO_BUFFERING|0x00000002L|Das System öffnet die Datei ohne Systemzwischenspeicherung.|  
|SQL_FILESTREAM_OPEN_FLAG_NO_WRITE_THROUGH|0x00000004L|Das System schreibt nicht durch einen Zwischencache. Die Schreibvorgänge erfolgen direkt auf den Datenträger.|  
|SQL_FILESTREAM_OPEN_FLAG_SEQUENTIAL_SCAN|0x00000008L|Auf eine Datei wird sequenziell (vom Anfang zum Ende) zugegriffen. Das System kann dies als Hinweis zur Optimierung der Zwischenspeicherung von Dateien verwenden. Wenn eine Anwendung den Dateizeiger für zufälligen Zugriff verschiebt, wird die Zwischenspeicherung möglicherweise nicht optimal durchgeführt.|  
|SQL_FILESTREAM_OPEN_FLAG_RANDOM_ACCESS|0x00000010L|Auf eine Datei wird nach dem Zufallsprinzip zugegriffen. Das System kann dies als Hinweis zur Optimierung der Zwischenspeicherung von Dateien verwenden.|  
  
 *FilestreamTransactionContext*  
 [in] Der Wert, der von der Funktion [GET_FILESTREAM_TRANSACTION_CONTEXT](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md) zurückgegeben wird.  
  
 *FilestreamTransactionContextLength*  
 [in] Anzahl von Bytes in den **varbinary(max)** -Daten, die von der Funktion GET_FILESTREAM_TRANSACTION_CONTEXT zurückgegeben werden. Die Funktion gibt ein Array von n Bytes zurück. n wird von der Funktion bestimmt und ist eine Eigenschaft des Bytearrays, das zurückgegeben wird.  
  
 *AllocationSize*  
 [in] Bestimmt die anfängliche Zuweisungsgröße der Datendatei in Bytes. Wird im Lesemodus ignoriert. Dieser Parameter kann NULL sein; in diesem Fall wird das Standarddateisystemverhalten verwendet.  
  
## <a name="return-value"></a>Rückgabewert  
 Wenn die Funktion erfolgreich ausgeführt wurde, ist der Rückgabewert ein offenes Handle zu einer angegebenen Datei. Wenn die Funktion fehlschlägt, ist der Rückgabewert INVALID_HANDLE_VALUE. Rufen Sie für erweiterte Fehlerinformationen GetLastError() auf.  
  
## <a name="examples"></a>Beispiele  
 Die folgenden Beispiele zeigen, wie Sie die `OpenSqlFilestream` -API verwenden, um ein Win32-Handle abzurufen.  
  
 [!code-cs[FILESTREAM#FS_CS_ReadAndWriteBLOB](../../relational-databases/blob/codesnippet/csharp/access-filestream-data-w_0_1.cs)]  
  
 [!code-vb[FILESTREAM#FS_VB_ReadAndWriteBLOB](../../relational-databases/blob/codesnippet/visualbasic/access-filestream-data-w_0_2.vb)]  
  
 [!code-cpp[FILESTREAM#FS_CPP_WriteBLOB](../../relational-databases/blob/codesnippet/cpp/access-filestream-data-w_0_3.cpp)]  
  
## <a name="remarks"></a>Remarks  
 Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client muss installiert sein, um diese API zu verwenden. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client wird mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Clienttools installiert. Weitere Informationen finden Sie unter [Installing SQL Server Native Client](../../relational-databases/native-client/applications/installing-sql-server-native-client.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Binary Large Object &#40;Blob&#41; Daten &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)   
 [Vornehmen von Teilupdates an FILESTREAM-Daten](../../relational-databases/blob/make-partial-updates-to-filestream-data.md)   
 [Vermeiden von Konflikten mit Datenbankvorgängen in FILESTREAM-Anwendungen](../../relational-databases/blob/avoid-conflicts-with-database-operations-in-filestream-applications.md)  
  
  
