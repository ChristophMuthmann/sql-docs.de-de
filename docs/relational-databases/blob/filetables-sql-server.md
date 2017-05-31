---
title: FileTables (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 10/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FileTables [SQL Server], overview
- FileTables [SQL Server]
- FileTable [SQL Server], see FileTables [SQL Server]
- FileTable [SQL Server]
ms.assetid: a57b629c-e9ed-48fd-9a48-ed3787d80c8f
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 605875c9ed6e60861f899ec88e465c636a5976d6
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="filetables-sql-server"></a>FileTables (SQL Server)
  Die FileTable-Funktion bietet für die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeicherten Dateidaten Unterstützung für den Windows-Dateinamespace und die Kompatibilität mit Windows-Anwendungen. Mit FileTable können das Speichersystem und die Datenverwaltungskomponenten einer Anwendung integriert werden. Zudem werden integrierte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienste (z. B. Volltextsuche und semantische Suche) über unstrukturierte Daten und Metadaten bereitgestellt.  
  
 So können Sie Dateien und Dokumente in besonderen Tabellen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] speichern, die als FileTables bezeichnet werden, und auf diese über Windows-Anwendungen zugreifen, so als ob sie im Dateisystem gespeichert wären, ohne Clientanwendungen ändern zu müssen.  
  
 Die FileTable-Funktion basiert auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] FILESTREAM-Technologie. Weitere Informationen zu FILESTREAM finden Sie unter [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
##  <a name="Goals"></a> Vorteile der FileTable-Funktion  
 Die Ziele der FileTable-Funktion umfassen Folgendes:  
  
-   Windows-API-Kompatibilität für Dateidaten, die in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank gespeichert sind. Die Windows-API-Kompatibilität schließt Folgendes ein:  
  
    -   Nicht transaktionaler Streamingzugriff und direkte Updates an FILESTREAM-Daten.  
  
    -   Ein hierarchischer Namespace von Verzeichnissen und Dateien.  
  
    -   Speichern von Dateiattributen, z. B. Erstellungsdatum und Änderungsdatum.  
  
    -   Unterstützung von APIs für die Windows-Datei- und Verzeichnisverwaltung.  
  
-   Kompatibilität mit anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Funktionen, einschließlich Verwaltungstools, Diensten und relationalen Abfragefunktionen über FILESTREAM und Dateiattributdaten.  
  
 FileTables beseitigen ein großes Hindernis bei der Verwendung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Speichern und Verwalten unstrukturierter Daten, die zu aktuell als Dateien auf Dateiservern gespeichert sind. Unternehmen können diesen Daten von Dateiservern in FileTables verschieben, um die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]bereitgestellten integrierten Verwaltungsfunktionen und Dienste verwenden zu können. Gleichzeitig kann die Windows-Anwendungskompatibilität für vorhandene Windows-Anwendungen aufrechterhalten werden, die diese Daten als Dateien im Dateisystem betrachten.  
 
  
##  <a name="Description"></a> Was sind FileTables?  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bietet eine besondere **Dateitabelle**– auch als **FileTable**bezeichnet – für Anwendungen, für die ein Datei- und Verzeichnisspeicher in der Datenbank mit Windows-API-Kompatibilität und nicht transaktionsbasiertem Zugriff erforderlich ist. FileTables sind spezielle Benutzertabellen mit einem vordefinierten Schema. Darin können FILESTREAM-Daten, Informationen zur Datei- und Verzeichnishierarchie sowie Dateiattribute gespeichert werden.  
  
 Eine FileTable bietet die folgende Funktionalität:  
  
-   Eine FileTable stellt eine Hierarchie von Verzeichnissen und Dateien dar. Sie speichert Daten zu allen Knoten in dieser Hierarchie, sowohl für Verzeichnisse als auch für die Dateien, die sie enthält. Diese Hierarchie beginnt bei einem Stammverzeichnis, das Sie angeben, wenn Sie die FileTable erstellen.  
  
-   Jede Zeile in einer FileTable stellt eine Datei oder ein Verzeichnis dar.  
  
-   Jede Zeile enthält die im Folgenden aufgeführten Elemente. Weitere Informationen zum Schema einer FileTable finden Sie unter [FileTable Schema](../../relational-databases/blob/filetable-schema.md).  
  
    -   Eine**file_stream** -Spalte für Datenstromdaten und ein **stream_id** -Bezeichner (GUID). (Die **file_stream** -Spalte für ein Verzeichnis ist NULL.)  
  
    -   Sowohl die **path_locator** -Spalte als auch die **parent_path_locator** -Spalte zur Darstellung und Verwaltung der Datei- und Verzeichnishierarchie.  
  
    -   10 Dateiattribute, z. B. Erstellungsdatum und Änderungsdatum, die von Datei-E/A-APIs benötigt werden.  
  
    -   Eine Typspalte, die die Volltextsuche und die semantische Suche für Dateien und Dokumente unterstützt.  
  
-   Eine FileTable erzwingt bestimmte systemdefinierte Einschränkungen und Trigger, um die Dateinamespacesemantik beizubehalten.  
  
-   Wenn die Datenbank für nicht transaktionalen Zugriff konfiguriert ist, wird die in der FileTable dargestellte Datei- und Verzeichnishierarchie in der für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz konfigurierten FILESTREAM-Freigabe verfügbar gemacht. Dadurch wird der Dateisystemzugriff für Windows-Anwendungen bereitgestellt.  
  
 Einige zusätzliche Eigenschaften von FileTables umfassen Folgendes:  
  
-   Die Datei- und Verzeichnisdaten, die in einer FileTable gespeichert sind, werden durch eine Windows-Freigabe für nicht transaktionalen Dateizugriff für Windows-API-basierte Anwendungen verfügbar gemacht. Für eine Windows-Anwendung sieht dies wie eine normale Freigabe mit Dateien und Verzeichnissen aus. Anwendungen können die Dateien und die Verzeichnisse in dieser Freigabe mithilfe eines umfangreichen Satzes von Windows-APIs verwalten.  
  
-   Bei der Verzeichnishierarchie, die über die Freigabe angegeben wird, handelt es sich um eine rein logische Verzeichnisstruktur, die innerhalb der FileTable beibehalten wird.  
  
-   Aufrufe zum Erstellen oder Ändern einer Datei oder eines Verzeichnisses über die Windows-Freigabe werden von einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Komponente abgefangen und in der FileTable in den entsprechenden relationalen Daten wiedergegeben.  
  
-   Windows-API-Vorgänge sind von ihrem Wesen her nicht transaktional und sind nicht Benutzertransaktionen zugeordnet. Transaktionszugriff auf FILESTREAM-Daten, die in einer FileTable gespeichert sind, wird jedoch vollständig unterstützt, wie dies auch bei FILESTREAM-Spalten in einer regulären Tabelle der Fall ist.  
  
-   FileTables können auch über den normalen [!INCLUDE[tsql](../../includes/tsql-md.md)] -Zugriff abgefragt und aktualisiert werden. Sie werden auch in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verwaltungstools und -funktionen, z. B. die Sicherung, integriert.  
  
##  <a name="additional"></a> Weitere Überlegungen zum Verwenden von FileTables  
  
###  <a name="DBA"></a> Überlegungen zur Verwaltung  
 **Informationen zu FILESTREAM und FileTables**  
  
-   FileTables werden getrennt von FILESTREAM konfiguriert. Sie können daher weiterhin die FILESTREAM-Funktion verwenden, ohne den nicht transaktionalem Zugriff zu aktivieren oder FileTables zu erstellen.  
  
-   Es gibt keinen nicht transaktionalen Zugriff auf FILESTREAM-Daten außer durch FileTables. Wenn Sie daher den nicht transaktionalen Zugriff aktivieren, hat dies keine Auswirkungen auf das Verhalten vorhandener FILESTREAM-Spalten und Anwendungen.  
  
 **Informationen zu FileTables und nicht transaktionalem Zugriff**  
  
-   Sie können den nicht transaktionalen Zugriff auf Datenbankebene aktivieren bzw. deaktivieren.  
  
-   Der nicht transaktionale Zugriff kann auf Datenbankebene konfiguriert oder optimiert werden, indem Sie ihn ausschalten oder nur den Lesezugriff bzw. den vollständigen Lese-/Schreibzugriff aktivieren.  
   
###  <a name="memory"></a> FileTables unterstützen keine Speicherabbilddateien  
 FileTables unterstützen keine Speicherabbilddateien Editor und Paint sind zwei häufige Beispiele für Anwendungen, die Speicherabbilddateien verwenden. Sie können diese Anwendungen nicht auf dem gleichen Computer wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwenden, um in einer FileTable gespeicherte Dateien zu öffnen. Sie können diese Anwendungen jedoch auf einem Remotecomputer verwenden, um in einer FileTable gespeicherte Dateien zu öffnen, da die Speicherabbildfunktion unter diesen Umständen nicht verwendet wird.  
   
##  <a name="reltasks"></a> Verwandte Aufgaben  
 [Aktivieren der erforderlichen Komponenten für FileTable](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)  
 Beschreibt, wie die erforderlichen Komponenten zum Erstellen und Verwenden von FileTables aktiviert werden.  
  
 [Erstellen, Ändern und Löschen von FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)  
 Beschreibt, wie eine neue FileTable erstellt bzw. eine vorhandene FileTable geändert oder gelöscht wird.  
  
 [Laden von Dateien in FileTables](../../relational-databases/blob/load-files-into-filetables.md)  
 Beschreibt, wie Dateien in FileTables geladen und migriert werden.  
  
 [Arbeiten mit Verzeichnissen und Pfaden in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
 Beschreibt die Verzeichnisstruktur, mit der die Dateien in FileTables gespeichert werden.  
  
 [Zugreifen auf FileTables mit Transact-SQL](../../relational-databases/blob/access-filetables-with-transact-sql.md)  
 Beschreibt, wie die Befehle der Transact-SQL-Datenbearbeitungssprache (Data Manipulation Language, DML) mit FileTables verwendet werden.  
  
 [Zugreifen auf FileTables mit Datei-E/A-APIs](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)  
 Beschreibt, wie Dateisystem-E/A in einer FileTable funktioniert.  
  
 [Verwalten von FileTables](../../relational-databases/blob/manage-filetables.md)  
 Beschreibt allgemeine administrative Tasks zum Verwalten von FileTables.  
  
##  <a name="relcontent"></a> Verwandte Inhalte  
 [FileTable Schema](../../relational-databases/blob/filetable-schema.md)  
 Beschreibt das vordefinierte und feste Schema einer FileTable.  
  
 [FileTable-Kompatibilität mit anderen SQL Server-Funktionen](../../relational-databases/blob/filetable-compatibility-with-other-sql-server-features.md)  
 Beschreibt, wie FileTables mit anderen Funktionen von SQL Server funktionieren.  
  
 [FileTable-DDL, Funktionen, gespeicherte Prozeduren und Sichten](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
 Listet die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen und die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankobjekte auf, die zur Unterstützung der FileTable-Funktion hinzugefügt oder geändert wurden.  
  
  

