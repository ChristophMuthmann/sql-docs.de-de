---
title: Zugreifen auf FileTables mit Datei-E/A-APIs | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/25/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FileTables [SQL Server], accessing files with file APIs
ms.assetid: fa504c5a-f131-4781-9a90-46e6c2de27bb
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fee941d70d60091034abfd77998616508fedd611
ms.lasthandoff: 04/11/2017

---
# <a name="access-filetables-with-file-input-output-apis"></a>Zugreifen auf FileTables mit Datei-E/A-APIs
  Beschreibt, wie Dateisystem-E/A in einer FileTable funktioniert.  
  
##  <a name="accessing"></a> Erste Schritte mit Datei-E/A-APIs mit FileTables  
 Die primäre Verwendung von FileTables wird durch das Windows-Dateisystem und Datei-E/A-APIs erwartet. FileTables unterstützt den nicht transaktionalen Zugriff durch den umfangreichen Satz verfügbarer Datei-E/A-APIs.  
  
1.  Datei-E/A-API-Zugriff beginnt in der Regel, indem er einen logischen UNC-Pfad für die Datei oder das Verzeichnis anfordert. Anwendungen können eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung mit der [GetFileNamespacePath](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md)-Funktion &#40;Transact-SQL&#41; verwenden, um den logischen Pfad für eine Datei oder ein Verzeichnis abzurufen. Weitere Informationen finden Sie unter [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md).  
  
2.  Von der Anwendung wird dieser logische Pfad anschließend verwendet, um ein Handle für die Datei oder das Verzeichnis abzurufen und etwas mit dem Objekt auszuführen. Der Pfad kann an jede unterstützte Dateisystem-API-Funktion, z. B. CreateFile() oder CreateDirectory(), übergeben werden, um eine Datei zu erstellen oder zu öffnen und ein Handle abzurufen. Das Handle kann verwendet werden, um dann Daten zu streamen, aufzuzählen oder Verzeichnisse zu organisieren oder um Dateiattribute zu erhalten bzw. festzulegen oder umd Dateien oder Verzeichnisse usw. zu löschen.  
  
##  <a name="create"></a> Erstellen von Dateien und Verzeichnissen in einer FileTable  
 Eine Datei oder ein Verzeichnis kann in einer FileTable mithilfe von Datei-E/A-APIs, beispielsweise CreateFile oder CreateDirectory, erstellt werden.  
  
-   Sämtliche CREATION_DISPOSITION-Flags, Freigabemodi und Zugriffsmodi werden unterstützt. Dies schließt die Erstellung, Löschung und direkte Änderung von Dateien ein. Aktualisierungen von Dateinamespaces (z. B. Erstellen und Löschen von Verzeichnissen, Umbenennungs- und Verschiebevorgänge) werden ebenfalls unterstützt.  
  
-   Das Erstellen einer neuen Datei oder eines neuen Verzeichnisses entspricht der Erstellung einer neuen Zeile in der zugrunde liegenden FileTable.  
  
-   Bei Dateien werden die Datenstromdaten in der **file_stream** -Spalte gespeichert, wohingegen diese Spalte bei Verzeichnissen NULL entspricht.  
  
-   Für Dateien enthält die **is_directory** -Spalte den Wert **false**. Für Verzeichnisse enthält diese Spalte den Wert **true**.  
  
-   Freigabe und Parallelität des Zugriffs werden erzwungen, wenn sich mehrere gleichzeitige Datei-E/A-Vorgänge oder [!INCLUDE[tsql](../../includes/tsql-md.md)] -Vorgänge in die Hierarchie auf die gleiche Datei oder das Verzeichnis auswirken.  
  
##  <a name="read"></a> Lesen von Dateien und Verzeichnissen in einer FileTable  
 Alle Datei-E/A-Zugriffsvorgänge (für Datenstrom- und Attributdaten) verfügen über eine Read Committed-Isolationssemantik für diese Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##  <a name="write"></a> Schreiben und Aktualisieren von Dateien und Verzeichnissen in einer FileTable  
  
-   Alle Datei-E/A-Schreib-/Updatevorgänge auf einer FileTable sind nicht transaktional. Das heißt, keine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Transaktion wird an diese Vorgänge gebunden, und es werden keine ACID-Garantien bereitgestellt.  
  
-   Alle Datei-E/A-Streaming- bzw. direkten Updates werden für die FileTable unterstützt.  
  
-   Updates der FILESTREAM-Daten oder -attribute über die Datei-E/A-APIs haben Updates der entsprechenden **file_stream** - und Dateiattributspalten in der FileTable zur Folge.  
  
##  <a name="delete"></a> Löschen von Dateien und Verzeichnissen in einer FileTable  
 Jede Windows-Datei-E/A-API-Semantik wird erzwungen, wenn Sie eine Datei oder ein Verzeichnis löschen.  
  
-   Beim Löschen eines Verzeichnisses tritt ein Fehler auf, wenn das Verzeichnis Unterverzeichnisse mit Dateien enthält.  
  
-   Durch Löschen einer Datei oder eines Verzeichnisses wird die entsprechende Zeile aus der FileTable entfernt. Dies entspricht dem Löschen dieser Zeile durch einen [!INCLUDE[tsql](../../includes/tsql-md.md)] -Vorgang.  
  
##  <a name="supported"></a> Unterstützte Dateisystemvorgänge  
 FileTables unterstützen die Dateisystem-APIs, die sich auf die folgenden Dateisystemvorgänge beziehen:  
  
-   Verzeichnisverwaltung  
  
-   Dateiverwaltung  
  
 FileTables unterstützen die folgenden Vorgänge nicht:  
  
-   Datenträgerverwaltung  
  
-   Volumeverwaltung  
  
-   Transaktions-NTFS  
  
##  <a name="considerations"></a> Weitere Überlegungen für Datei-E/A-Zugriff auf FileTables  
  
###  <a name="vnn"></a> Verwenden von virtuellen Netzwerknamen (VNNs) mit Always On-Verfügbarkeitsgruppen  
 Wenn die Datenbank, die FILESTREAM oder FileTable-Daten enthält, zu einer Always On-Verfügbarkeitsgruppe gehört, dann sollten bei allen Zugriffen auf FILESTREAM oder FileTable-Daten über die Dateisystem-APIs VNNs statt der Computernamen verwendet werden. Weitere Informationen finden Sie unter [FILESTREAM und FileTable bei AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md).  
  
###  <a name="partial"></a> Teilupdates  
 Ein überschreibbares Handle, das Daten in einer FileTable mit der [GetFileNamespacePath](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md)-Funktion &#40;Transact-SQL&#41; abruft, kann verwendet werden, um auf den FILESTREAM-Inhalt direkte Teilupdates auszuführen. Dies steht im Gegensatz zu dem transaktiven FILESTREAM-Zugriff über ein Handle, das durch den **OpenSQLFILESTREAM()** -Befehl und durch das Übergeben eines expliziten Transaktionskontexts abgerufen wurde.  
  
###  <a name="trans"></a> Transaktionssemantik  
 Wenn Sie mit Datei-E/A-APIs auf die Dateien in einer FileTable zugreifen, sind diese Vorgänge keinen Benutzertransaktionen zugeordnet und haben die folgenden zusätzlichen Eigenschaften:  
  
-   Nicht transaktiver Zugriff auf FILESTREAM-Daten in einer FileTable ist keinen Transaktionen zugeordnet und verfügt daher nicht über eine spezifische Isolationssemantik. Von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird jedoch möglicherweise Sperren- oder Parallelitätssemantik mithilfe von internen Transaktionen auf den FileTable-Daten erzwungen. Alle internen Transaktionen dieses Typs werden mit Read Committed-Isolation ausgeführt.  
  
-   Es gibt keine ACID-Garantien für diese nicht transaktiven Vorgänge hinsichtlich FILESTREAM-Daten. Die Konsistenzgarantien ähneln denen für Dateiupdates, die von Anwendungen im Dateisystem erstellt wurden.  
  
-   Für diese Änderungen ist kein Rollback möglich.  
  
 Auf die Spalte FILESTREAM in einer FileTable kann jedoch auch mit Transaktions-FILESTREAM-Zugriff zugegriffen werden, indem **OpenSqlFileStream()**aufgerufen wird. Diese Art von Zugriff kann vollständig transaktionsgebunden sein und berücksichtigt alle derzeit einheitlich unterstützten Transaktionen.  
  
###  <a name="concurrency"></a> Parallelitätssteuerung  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erzwingt die Parallelitätssteuerung für den FileTable-Zugriff unter Dateisystemanwendungen sowie zwischen Dateisystemanwendungen und [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anwendungen. Diese Parallelitätssteuerung wird durch entsprechende Sperren in den FileTable-Zeilen erreicht.  
  
###  <a name="triggers"></a> Trigger  
 Das Erstellen/Ändern/Löschen von Dateien/Verzeichnissen oder deren Attributen über das Dateisystem führt zu entsprechenden Einfüge-/Update-/Löschvorgängen in der FileTable. Alle zugeordneten [!INCLUDE[tsql](../../includes/tsql-md.md)] -DML-Trigger werden als Teil dieser Vorgänge ausgelöst.  
  
##  <a name="funclist"></a> In FileTables unterstützte Dateisystemfunktionalität  
  
|Funktion|Supported|Kommentare|  
|----------------|---------------|--------------|  
|**Oplocks**|ja|Ebene 2, Ebene 1, Batch- und Filter-Oplocks werden unterstützt.|  
|**Erweiterte Attribute**|Nein||  
|**Reparse Points**|Nein||  
|**Persistente ACLs**|Nein||  
|**Benannte Datenströme**|Nein||  
|**Dateien von geringer Dichte**|ja|Geringe Dichte kann nur für Dateien festgelegt werden und wirkt sich auf die Speicherung des Datenstroms aus. Da FILESTREAM-Daten auf NTFS-Volumes gespeichert werden, unterstützt die FileTable-Funktion Dateien mit geringer Dichte, indem er die Anforderungen an das NTFS-Dateisystem weiterleitet.|  
|**Komprimierung**|ja||  
|**Verschlüsselung**|ja||  
|**TxF**|Nein||  
|**Datei-IDs**|Nein||  
|**Objekt-IDs**|Nein||  
|**Symbolische Links**|Nein||  
|**Harte Links**|Nein||  
|**Kurze Namen**|Nein||  
|**Benachrichtigungen über Verzeichnisänderungen**|Nein||  
|**Bytebereichssperren**|ja|Anforderungen zur Bytebereichssperre werden an das NTFS-Dateisystem übergeben.|  
|**Im Speicher abgebildete Dateien**|Nein||  
|**Abbrechen von E/A**|ja||  
|**Sicherheit**|Nein|Sicherheit auf Windows-Freigabeebene und Sicherheit auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabellen-/Spaltenebene wird erzwungen.|  
|**USN-Journal**|Nein|Metadatenänderungen an Dateien und Verzeichnissen in einer FileTable sind DML-Vorgänge in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank. Daher werden sie in der entsprechenden Datenbankprotokolldatei protokolliert. Sie werden jedoch (abgesehen von Änderungen an der Größe) nicht im NTFS-USN-Journal protokolliert.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Änderungsnachverfolgung kann verwendet werden, um ähnliche Informationen zu erfassen.|  
  
## <a name="see-also"></a>Siehe auch  
 [Laden von Dateien in FileTables](../../relational-databases/blob/load-files-into-filetables.md)   
 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)   
 [Zugreifen auf FileTables mit Transact-SQL](../../relational-databases/blob/access-filetables-with-transact-sql.md)   
 [FileTable-DDL, Funktionen, gespeicherte Prozeduren und Sichten](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
  
  

