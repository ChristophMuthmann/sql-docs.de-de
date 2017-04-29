---
title: Arbeiten mit Verzeichnissen und Pfaden in FileTables | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FileTables [SQL Server], directories
ms.assetid: f1e45900-bea0-4f6f-924e-c11e1f98ab62
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d41410b3da1f823a29da0c5b7bd706dff4ce4584
ms.lasthandoff: 04/11/2017

---
# <a name="work-with-directories-and-paths-in-filetables"></a>Arbeiten mit Verzeichnissen und Pfaden in FileTables
  Beschreibt die Verzeichnisstruktur, mit der die Dateien in FileTables gespeichert werden.  
  
##  <a name="HowToDirectories"></a> Vorgehensweise: Arbeiten mit Verzeichnissen und Pfaden in FileTables  
 Sie können die folgenden drei Funktionen verwenden, um mit FileTable-Verzeichnissen in [!INCLUDE[tsql](../../includes/tsql-md.md)]zu arbeiten:  
  
|Für dieses Ergebnis|Verwenden Sie diese Funktion|  
|------------------------|-----------------------|  
|Ermitteln des UNC-Pfades auf der Stammebene für eine bestimmte FileTable oder die aktuelle Datenbank.|[FileTableRootPath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filetablerootpath-transact-sql.md)|  
|Ermitteln eines absoluten oder relativen UNC-Pfades für eine Datei oder ein Verzeichnis in einer FileTable.|[GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md)|  
|Ermitteln des ID-Wertes "path_locator" für die angegebene Datei bzw. das angegebene Verzeichnis in einer FileTable unter Angabe des Pfades.|[GetPathLocator &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md)|  
  
##  <a name="BestPracticeRelativePaths"></a> Vorgehensweise: Relative Pfade für portablen Code verwenden  
 Um Code und Anwendungen vom aktuellen Computer und von der Datenbank unabhängig zu halten, sollten Sie keinen Code schreiben, der auf absoluten Dateipfaden basiert. Rufen Sie stattdessen den vollständigen Pfad für eine Datei mit der Funktion [FileTableRootPath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filetablerootpath-transact-sql.md) und der Funktion [GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md)zur Laufzeit ab, wie im folgenden Beispiel gezeigt. Die **GetFileNamespacePath** -Funktion gibt standardmäßig den relativen Pfad der Datei unter dem Stammpfad der Datenbank zurück.  
  
```tsql  
USE database_name;  
DECLARE @root nvarchar(100);  
DECLARE @fullpath nvarchar(1000);  
  
SELECT @root = FileTableRootPath();  
SELECT @fullpath = @root + file_stream.GetFileNamespacePath()  
    FROM filetable_name  
    WHERE name = N'document_name';  
  
PRINT @fullpath;  
GO  
```  
  
##  <a name="restrictions"></a> Wichtige Einschränkungen  
  
###  <a name="nesting"></a> Schachtelungsebene  
  
> **WICHTIG!** Es ist nicht möglich, mehr als 15 Ebenen von Unterverzeichnissen im FileTable-Verzeichnis zu speichern. Wenn Sie 15 Unterverzeichnisebenen speichern, kann die niedrigste Ebene keine Dateien enthalten, da diese Dateien eine zusätzliche Ebene darstellen würden.  
  
###  <a name="fqnlength"></a> Länge des vollständigen Pfadnamens  
  
> **WICHTIG!** Das NTFS-Dateisystem unterstützt Pfadnamen, die viel länger als die 260-Zeichen-Grenze der Windows-Shell und der meisten Windows-APIs sind. Daher ist es möglich, Dateien in der Dateihierarchie einer FileTable mit Transact-SQL zu erstellen. Diese können Sie mit dem Windows-Explorer oder vielen anderen Windows-Anwendungen weder anzeigen noch öffnen, da der vollständige Pfadname 260 Zeichen überschreitet. Sie können jedoch weiterhin mit Transact-SQL auf diese Dateien zugreifen.  
  
##  <a name="fullpath"></a> Der vollständige Pfad zu einem in einer FileTable gespeicherten Element  
 Der vollständige Pfad zu einer Datei oder einem Verzeichnis, der in einer FileTable gespeichert wurde, beginnt mit den folgenden Elementen:  
  
1.  Die für den FILESTREAM-Datei-E/A-Zugriff auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzebene aktivierte Freigabe.  
  
2.  Der auf Datenbankebene angegebene **DIRECTORY_NAME** .  
  
3.  Das auf FileTable-Ebene angegebene **FILETABLE_DIRECTORY** .  
  
 Die resultierende Hierarchie sieht etwa folgendermaßen aus:  
  
 `\\<machine>\<instance-level FILESTREAM share>\<database-level directory>\<FileTable directory>\`  
  
 Diese Verzeichnishierarchie bildet den Stamm des FileTable-Namespace. Unter dieser Verzeichnishierarchie werden die FILESTREAM-Daten für die FileTable als Dateien wie auch als Unterverzeichnisse gespeichert, die auch Dateien und Unterverzeichnisse enthalten können.  
  
 Bitte denken Sie daran, dass die unter der FILESTREAM-Freigabe auf Instanzebene erstellte Verzeichnishierarchie eine virtuelle Verzeichnishierarchie ist. Diese Hierarchie wird in der Datenbank [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeichert und nicht physisch im NTFS-Dateisystem dargestellt. Alle Vorgänge, die unter der FILESTREAM-Freigabe und in den enthaltenen FileTables auf Dateien und Verzeichnisse zugreifen, werden durch eine im Dateisystem eingebettete [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponente abgefangen und behandelt.  
  
##  <a name="roots"></a> Die Semantik der Stammverzeichnisse auf der Instanz-, Datenbank- und FileTable-Ebene  
 Diese Verzeichnishierarchie achtet auf die folgende Semantik:  
  
-   Die FILESTREAM-Freigabe auf Instanzebene wird von einem Administrator konfiguriert und als Eigenschaft des Servers gespeichert. Sie können diese Freigabe mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager umbenennen. Ein Umbenennungsvorgang wird erst wirksam, wenn der Server neu gestartet wird.  
  
-   Der **DIRECTORY_NAME** auf Datenbankebene ist standardmäßig NULL, wenn Sie eine neue Datenbank erstellen. Ein Administrator kann diesen Namen festlegen oder mit der Anweisung **ALTER DATABASE** ändern. Der Name muss in dieser Instanz eindeutig sein, wobei nicht zwischen Groß- und Kleinschreibung unterschieden wird.  
  
-   In der Regel geben Sie den **FILETABLE_DIRECTORY** -Namen als Teil der Anweisung **CREATE TABLE** beim Erstellen einer FileTable an. Sie können diesen Namen mit dem Befehl **ALTER TABLE** ändern.  
  
-   Es ist nicht möglich, diese Stammverzeichnisse kann durch Datei-E/A-Vorgänge umzubenennen.  
  
-   Es ist nicht möglich, diese Stammverzeichnisse mit exklusiven Dateihandles zu öffnen.  
  
##  <a name="is_directory"></a> Die is_directory-Spalte im FileTable-Schema  
 In der folgenden Tabelle wird die Interaktion zwischen der Spalte **is_directory** und der Spalte **file_stream** beschrieben, die die FILESTREAM-Daten in einer FileTable enthält.  
  
||||  
|-|-|-|  
|*is_directory* **value**|*file_stream* **value**|**Verhalten**|  
|FALSE|NULL|Dies ist eine ungültige Kombination, die von einer systemdefinierten Einschränkung abgefangen wird.|  
|FALSE|\<Wert >|Das Element stellt eine Datei dar.|  
|TRUE|NULL|Das Element stellt ein Verzeichnis dar.|  
|TRUE|\<Wert >|Dies ist eine ungültige Kombination, die von einer systemdefinierten Einschränkung abgefangen wird.|  
  
##  <a name="alwayson"></a> Verwenden von virtuellen Netzwerknamen mit (VNNs) AlwaysOn-Verfügbarkeitsgruppen  
 Wenn die Datenbank, die FILESTREAM- oder FileTable-Daten enthält, zu einer AlwaysOn-Verfügbarkeitsgruppe gehört:  
  
-   Die FILESTREAM-Funktion und die FileTable-Funktion akzeptieren oder geben virtuelle Netzwerknamen (VNNs) statt Computernamen zurück. Weitere Informationen zu diesen Funktionen finden Sie unter [Filestream- und FileTable-Funktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filestream-and-filetable-functions-transact-sql.md).  
  
-   Bei allen Zugriffen auf FILESTREAM- oder FileTable-Daten über Dateisystem-APIs sollten VNNs statt der Computernamen verwendet werden. Weitere Informationen finden Sie unter [FILESTREAM und FileTable bei AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Aktivieren der erforderlichen Komponenten für FileTable](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)   
 [Erstellen, Ändern und Löschen von FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)   
 [Zugreifen auf FileTables mit Transact-SQL](../../relational-databases/blob/access-filetables-with-transact-sql.md)   
 [Zugreifen auf FileTables mit Datei-E/A-APIs](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)  
  
  

