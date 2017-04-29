---
title: "Erstellen von Clientanwendungen für FILESTREAM-Daten | Microsoft Dokumentation"
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
- FILESTREAM [SQL Server], Win32
ms.assetid: 8a02aff6-e54c-40c6-a066-2083e9b090aa
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c8ae3ba00110ba3441ac5bfa6dc2e06979f59ee0
ms.lasthandoff: 04/11/2017

---
# <a name="create-client-applications-for-filestream-data"></a>Erstellen von Clientanwendungen für FILESTREAM-Daten
  Sie können Win32 zum Lesen und Schreiben von Daten in einem FILESTREAM BLOB verwenden. Hierfür sind die folgenden Schritte erforderlich:  
  
-   Lesen des FILESTREAM-Dateipfads.  
  
-   Lesen des aktuellen Transaktionskontexts.  
  
-   Abrufen eines Win32-Handles und Lesen und Schreiben von Daten im FILESTREAM BLOB mit diesem Handle.  
  
> [!NOTE]  
>  Für die Beispiele in diesem Thema sind die FILESTREAM-aktivierte Datenbank und die Tabelle erforderlich, die unter [Erstellen einer FILESTREAM-aktivierten Datenbank](../../relational-databases/blob/create-a-filestream-enabled-database.md) und [Erstellen einer Tabelle zum Speichern von FILESTREAM-Daten](../../relational-databases/blob/create-a-table-for-storing-filestream-data.md)erstellt werden.  
  
##  <a name="func"></a> Funktionen zum Arbeiten mit FILESTREAM-Daten  
 Wenn Sie FILESTREAM zum Speichern von Binary Large Object (BLOB)-Daten verwenden, können Sie die Dateien mit Win32-APIs bearbeiten. Zum Arbeiten mit FILESTREAM BLOB-Daten in Win32-Anwendungen stellt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die folgenden Funktionen und die folgende API bereit:  
  
-   [PathName](../../relational-databases/system-functions/pathname-transact-sql.md) gibt einen Pfad als Token an ein BLOB zurück. Eine Anwendung verwendet dieses Token, um ein Win32-Handle zu erhalten und mit BLOB-Daten zu arbeiten.  
  
     Wenn die Datenbank, die FILESTREAM-Daten enthält, zu einer AlwaysOn-Verfügbarkeitsgruppe gehört, dann gibt die PathName-Funktion den Namen eines virtuellen Netzwerks (VNN) statt eines Computernamens zurück.  
  
-   [GET_FILESTREAM_TRANSACTION_CONTEXT()](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md) gibt ein Token zurück, das die aktuelle Transaktion einer Sitzung darstellt. Anwendungen verwenden dieses Token, um FILESTREAM-Dateisystem-Streamingvorgänge an die Transaktion zu binden.  
  
-   Die [OpenSqlFilestream-API](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) bezieht ein Win32-Dateihandle. Die Anwendung verwendet dieses Handle, um die FILESTREAM-Daten zu streamen, und kann das Handle dann an die folgenden Win32-APIs weitergeben: [ReadFile](http://go.microsoft.com/fwlink/?LinkId=86422), [WriteFile](http://go.microsoft.com/fwlink/?LinkId=86423), [TransmitFile](http://go.microsoft.com/fwlink/?LinkId=86424), [SetFilePointer](http://go.microsoft.com/fwlink/?LinkId=86425), [SetEndOfFile](http://go.microsoft.com/fwlink/?LinkId=86426)oder [FlushFileBuffers](http://go.microsoft.com/fwlink/?LinkId=86427). Wenn die Anwendung mit dem Handle irgendeine andere API anruft, wird ein ERROR_ACCESS_DENIED-Fehler zurückgegeben. Die Anwendung sollte das Handle mit [CloseHandle](http://go.microsoft.com/fwlink/?LinkId=86428)schließen.  
  
 Alle Zugriffe auf FILESTREAM-Datencontainer müssen in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Transaktion erfolgen. [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen können auch in der gleichen Transaktion ausgeführt werden, damit die SQL-Daten mit den FILESTREAM-Daten konsistent bleiben.  
  
##  <a name="steps"></a> Schritte zum Zugreifen auf FILESTREAM-Daten  
  
###  <a name="path"></a> Lesen des FILESTREAM-Dateipfads  
 Jeder Zelle in einer FILESTREAM-Tabelle ist ein Dateipfad zugeordnet. Um den Pfad zu lesen, verwenden Sie die **PathName** -Eigenschaft einer **varbinary(max)** -Spalte in einer [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung. Das folgende Beispiel zeigt, wie der Dateipfad einer **varbinary(max)** -Spalte gelesen wird.  
  
 [!code-sql[FILESTREAM #FS_PathName](../../relational-databases/blob/codesnippet/tsql/create-client-applicatio_1.sql)]  
  
###  <a name="trx"></a> Lesen des Transaktionskontexts  
 Um den aktuellen Transaktionskontext abzurufen, verwenden Sie die [!INCLUDE[tsql](../../includes/tsql-md.md)] [GET_FILESTREAM_TRANSACTION_CONTEXT()](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md) function. Das folgende Beispiel zeigt, wie eine Transaktion gestartet und der aktuelle Transaktionskontext gelesen wird.  
  
 [!code-sql[FILESTREAM#FS_GET_TRANSACTION_CONTEXT](../../relational-databases/blob/codesnippet/tsql/create-client-applicatio_2.sql)]  
  
###  <a name="handle"></a> Abrufen eines Win32-Dateihandles  
 Um ein Win32-Dateihandle abzurufen, rufen Sie die OpenSqlFilestream-API auf. Diese API wird aus der Datei sqlncli.dll exportiert. Das zurückgegebene Handle kann an eine der folgenden Win32-APIs übergeben werden: [ReadFile](http://go.microsoft.com/fwlink/?LinkId=86422), [WriteFile](http://go.microsoft.com/fwlink/?LinkId=86423), [TransmitFile](http://go.microsoft.com/fwlink/?LinkId=86424), [SetFilePointer](http://go.microsoft.com/fwlink/?LinkId=86425), [SetEndOfFile](http://go.microsoft.com/fwlink/?LinkId=86426)oder [FlushFileBuffers](http://go.microsoft.com/fwlink/?LinkId=86427). Die folgenden Beispiele veranschaulichen, wie Sie ein Win32-Handle abrufen und zum Lesen und Schreiben von FILESTREAM BLOB-Daten verwenden.  
  
 [!code-cs[FILESTREAM#FS_CS_ReadAndWriteBLOB](../../relational-databases/blob/codesnippet/csharp/create-client-applicatio_3.cs)]  
  
 [!code-vb[FILESTREAM#FS_VB_ReadAndWriteBLOB](../../relational-databases/blob/codesnippet/visualbasic/create-client-applicatio_4.vb)]  
  
 [!code-cpp[FILESTREAM#FS_CPP_WriteBLOB](../../relational-databases/blob/codesnippet/cpp/create-client-applicatio_5.cpp)]  
  
##  <a name="best"></a> Bewährte Methoden für Anwendungsentwurf und Implementierung  
  
-   Wenn Sie Anwendungen entwerfen und implementieren, die FILESTREAM verwenden, beachten Sie die folgenden Richtlinien:  
  
-   Verwenden Sie NULL statt 0x, um eine nicht initialisierte FILESTREAM-Spalte darzustellen. Der 0x-Wert bewirkt, dass eine Datei erstellt wird. Bei NULL ist dies nicht der Fall.  
  
-   Vermeiden Sie Einfüge- und Löschvorgänge in Tabellen, die FILESTREAM-Spalten ungleich NULL enthalten. Bei Einfüge- und Löschvorgängen können die FILESTREAM-Tabellen geändert werden, die für Garbage Collection verwendet werden. Dies kann dazu führen, dass die Leistung einer Anwendung mit der Zeit nachlässt.  
  
-   Verwenden Sie in Anwendungen, die Replikation verwenden, NEWSEQUENTIALID() statt NEWID(). NEWSEQUENTIALID() erzielt in diesen Anwendungen bei der GUID-Generierung eine bessere Leistung als NEWID().  
  
-   Die FILESTREAM-API ist für Win32-Streamingzugriff auf Daten vorgesehen. Vermeiden Sie die Verwendung von [!INCLUDE[tsql](../../includes/tsql-md.md)] zum Lesen oder Schreiben von FILESTREAM-BLOBs (Binary Large Objects), die größer als 2 MB sind. Wenn Sie BLOB-Daten aus [!INCLUDE[tsql](../../includes/tsql-md.md)]lesen oder schreiben müssen, stellen Sie sicher, dass alle BLOB-Daten verarbeitet werden, bevor Sie versuchen, den FILESTREAM-BLOB über Win32 zu öffnen. Werden nicht alle [!INCLUDE[tsql](../../includes/tsql-md.md)] -Daten verarbeitet, schlagen möglicherweise alle folgenden FILESTREAM-Vorgänge zum Öffnen oder Schließen fehl.  
  
-   Vermeiden Sie [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen, die FILESTREAM-BLOBs aktualisieren oder diesen Daten anfügen bzw. voranstellen. Dies bewirkt, dass die BLOB-Daten in die Datenbank tempdb und anschließend zurück in eine neue physische Datei gespoolt werden.  
  
-   Vermeiden Sie, kleine BLOB-Updates an ein FILESTREAM-BLOB anzufügen. Jeder Anfügevorgang bewirkt, dass die zugrunde liegenden FILESTREAM-Dateien kopiert werden. Wenn eine Anwendung kleine BLOBs anfügen muss, schreiben Sie die BLOBs in eine **varbinary(max)** -Spalte, und führen Sie dann einen einzelnen Schreibvorgang für den FILESTREAM-BLOB durch, wenn die Anzahl der BLOBs eine vorher festgelegte Beschränkung erreicht.  
  
-   Vermeiden Sie, die Datenlänge von vielen BLOB-Dateien in einer Anwendung abzurufen. Dies ist ein zeitaufwendiger Vorgang, da die Größe nicht in [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]gespeichert wird. Wenn Sie die Länge einer BLOB-Datei festlegen müssen, verwenden Sie die [!INCLUDE[tsql](../../includes/tsql-md.md)] -DATALENGTH()-Funktion, um die Größe des BLOB zu bestimmen, wenn dieses geschlossen ist. DATALENGTH() öffnet die BLOB-Datei nicht, um deren Größe zu bestimmen.  
  
-   Wenn eine Anwendung das SMB (Server Message Block)-Protokoll verwendet, sollten FILESTREAM-BLOB-Daten in einem Vielfachen von 60 KB gelesen werden, um die Leistung zu optimieren.  
  
## <a name="see-also"></a>Siehe auch  
 [Vermeiden von Konflikten mit Datenbankvorgängen in FILESTREAM-Anwendungen](../../relational-databases/blob/avoid-conflicts-with-database-operations-in-filestream-applications.md)   
 [Zugreifen auf FILESTREAM-Daten mit OpenSqlFilestream](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)   
 [Binary Large Object &#40;BLOB&#41;-Daten &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)   
 [Vornehmen von Teilupdates an FILESTREAM-Daten](../../relational-databases/blob/make-partial-updates-to-filestream-data.md)  
  
  
