---
title: "Vermeiden von Konflikten mit Datenbankvorgängen in FILESTREAM-Anwendungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FILESTREAM [SQL Server], Win32 and Transact-SQL Conflicts
ms.assetid: 8b1ee196-69af-4f9b-9bf5-63d8ac2bc39b
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 663627abeb04c63073b43337bfe795ba9bc9cd4d
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="avoid-conflicts-with-database-operations-in-filestream-applications"></a>Vermeiden von Konflikten mit Datenbankvorgängen in FILESTREAM-Anwendungen
  Bei Anwendungen, die SqlOpenFilestream() zum Öffnen von Win32-Dateihandles zum Lesen oder Schreiben von FILESTREAM-BLOB-Daten verwenden, können Konfliktfehler mit [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen auftreten, die in einer gemeinsamen Transaktion verwaltet werden. Dies gilt auch für [!INCLUDE[tsql](../../includes/tsql-md.md)] - oder MARS-Abfragen, bei denen das Beenden der Ausführung viel Zeit in Anspruch nimmt. Anwendungen müssen sorgfältig entworfen werden, wenn diese Art von Konflikten vermieden werden soll.  
  
 Wenn die [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] oder Anwendungen versuchen, FILESTREAM-BLOBs zu öffnen, überprüft die [!INCLUDE[ssDE](../../includes/ssde-md.md)] den zugeordneten Transaktionskontext. Die [!INCLUDE[ssDE](../../includes/ssde-md.md)] lässt die Anforderung zu bzw. verweigert sie in Abhängigkeit davon, ob der geöffnete Vorgang mit DDL-Anweisungen oder DML-Anweisungen arbeitet, Daten abruft oder Transaktionen verwaltet. Die folgende Tabelle zeigt, wie die [!INCLUDE[ssDE](../../includes/ssde-md.md)] ermittelt, ob eine [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung basierend auf dem Typ der Dateien, die in der Transaktion geöffnet sind, zugelassen oder verweigert wird.  
  
|Transact-SQL-Anweisungen|Geöffnet zum Lesen|Geöffnet zum Schreiben|  
|------------------------------|---------------------|----------------------|  
|DDL-Anweisungen, die mit Datenbankmetadaten arbeiten, z. B. CREATE TABLE, CREATE INDEX, DROP TABLE und ALTER TABLE.|Zulässig|Werden blockiert und schlagen mit einem Timeout fehl.|  
|DML-Anweisungen, die mit den Daten arbeiten, die in der Datenbank gespeichert sind, z. B. UPDATE, DELETE und INSERT.|Zulässig|Verweigert|  
|SELECT|Zulässig|Zulässig|  
|COMMIT TRANSACTION|Verweigert*|Verweigert*|  
|SAVE TRANSACTION|Verweigert*|Verweigert*|  
|ROLLBACK|Zulässig*|Zulässig*|  
  
 \* Die Transaktion wird abgebrochen, und geöffnete Handles für den Transaktionskontext werden für ungültig erklärt. Die Anwendung muss alle geöffneten Handles schließen.  
  
## <a name="examples"></a>Beispiele  
 In den folgenden Beispielen wird gezeigt, wie [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen und der FILESTREAM-Win32-Zugriff Konflikte verursachen können.  
  
### <a name="a-opening-a-filestream-blob-for-write-access"></a>A. Öffnen eines FILESTREAM-BLOB für Schreibzugriff  
 Das folgende Beispiel zeigt die Auswirkung des Öffnens einer Datei nur für den Schreibzugriff.  
  
```  
dstHandle =  OpenSqlFilestream(dstFilePath, Write, 0,  
    transactionToken, cbTransactionToken, 0);  
  
//Write some date to the FILESTREAM BLOB.  
WriteFile(dstHandle, updateData, …);  
  
//DDL statements will be denied.  
//DML statements will be denied.  
//SELECT statements will be allowed. The FILESTREAM BLOB is  
//returned without the modifications that are made by  
//WriteFile(dstHandle, updateData, …).  
CloseHandle(dstHandle);  
  
//DDL statements will be allowed.  
//DML statements will be allowed.  
//SELECT statements will be allowed. The FILESTREAM BLOB  
//is returned with the updateData applied.  
```  
  
### <a name="b-opening-a-filestream-blob-for-read-access"></a>B. Öffnen eines FILESTREAM-BLOB für Lesezugriff  
 Das folgende Beispiel zeigt die Auswirkung des Öffnens einer Datei nur für den Lesezugriff.  
  
```  
dstHandle =  OpenSqlFilestream(dstFilePath, Read, 0,  
    transactionToken, cbTransactionToken, 0);  
//DDL statements will be denied.  
//DML statements will be allowed. Any changes that are  
//made to the FILESTREAM BLOB will not be returned until  
//the dstHandle is closed.  
//SELECT statements will be allowed.  
CloseHandle(dstHandle);  
  
//DDL statements will be allowed.  
//DML statements will be allowed.  
//SELECT statements will be allowed.  
```  
  
### <a name="c-opening-and-closing-multiple-filestream-blob-files"></a>C. Öffnen und Schließen von mehreren FILESTREAM-BLOB-Dateien  
 Wenn mehrere Dateien geöffnet sind, wird die restriktivste Regel verwendet. Im folgenden Beispiel werden zwei Dateien geöffnet. Die erste Datei wird für den Lesezugriff geöffnet, die zweite für den Schreibzugriff. DML-Anweisungen werden verweigert, bis die zweite Datei geöffnet wird.  
  
```  
dstHandle =  OpenSqlFilestream(dstFilePath, Read, 0,  
    transactionToken, cbTransactionToken, 0);  
//DDL statements will be denied.  
//DML statements will be allowed.  
//SELECT statements will be allowed.  
  
dstHandle1 =  OpenSqlFilestream(dstFilePath1, Write, 0,  
    transactionToken, cbTransactionToken, 0);  
  
//DDL statements will be denied.  
//DML statements will be denied.  
//SELECT statements will be allowed.  
  
//Close the read handle. The write handle is still open.  
CloseHandle(dstHandle);  
//DML statements are still denied because the write handle is open.  
  
//DDL statements will be denied.  
//DML statements will be denied.  
//SELECT statements will be allowed.  
  
CloseHandle(dstHandle1);  
//DDL statements will be allowed.  
//DML statements will be allowed.  
//SELECT statements will be allowed.  
```  
  
### <a name="d-failing-to-close-a-cursor"></a>D. Fehler beim Schließen eines Cursors  
 Das folgende Beispiel zeigt, wie ein nicht geschlossener Anweisungscursor verhindern kann, dass `OpenSqlFilestream()` den BLOB für den Schreibzugriff öffnen kann.  
  
```  
TCHAR *sqlDBQuery =  
TEXT("SELECT GET_FILESTREAM_TRANSACTION_CONTEXT(),")  
TEXT("Chart.PathName() FROM Archive.dbo.Records");  
  
//Execute a long-running Transact-SQL statement. Do not allow  
//the statement to complete before trying to  
//open the file.  
  
SQLExecDirect(hstmt, sqlDBQuery, SQL_NTS);  
  
//Before you call OpenSqlFilestream() any open files  
//that the Cursor the Transact-SQL statement is using  
// must be closed. In this example,  
//SQLCloseCursor(hstmt) is not called so that  
//the transaction will indicate that there is a file  
//open for reading. This will cause the call to  
//OpenSqlFilestream() to fail because the file is  
//still open.  
  
HANDLE srcHandle =  OpenSqlFilestream(srcFilePath,  
     Write, 0,  transactionToken,  cbTransactionToken,  0);  
  
//srcHandle will == INVALID_HANDLE_VALUE because the  
//cursor is still open.  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ZUgreifen auf FILESTREAM-Daten mit OpenSqlFilestream](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)   
 [Verwenden von Multiple Active Result Sets &#40;MARS&#41;](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)  
  
  
