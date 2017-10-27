---
title: "Erstellen, Ändern und Löschen von FileTables | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FileTables [SQL Server], altering
- FileTables [SQL Server], dropping
- FileTables [SQL Server], creating
ms.assetid: 47d69e37-8778-4630-809b-2261b5c41c2c
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0445d1e3f300031a0154e253009a516364cd4fc3
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="create-alter-and-drop-filetables"></a>Erstellen, Ändern und Löschen von FileTables
  Beschreibt, wie eine neue FileTable erstellt bzw. eine vorhandene FileTable geändert oder gelöscht wird.  
  
##  <a name="BasicsCreate"></a> Erstellen einer FileTable  
 Eine FileTable ist eine spezialisierte Benutzertabelle, die ein vordefiniertes und festes Schema aufweist. Dieses Schema speichert FILESTREAM-Daten, Datei- und Verzeichnisinformationen sowie Dateiattribute. Weitere Informationen zum FileTable-Beispielschema finden Sie unter [FileTable Schema](../../relational-databases/blob/filetable-schema.md).  
  
 Sie können mit Transact-SQL oder [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine neue FileTable erstellen. Da eine FileTable ein festes Schema hat, müssen Sie keine Liste von Spalten angeben. Mit der einfachen Syntax zum Erstellen einer FileTable können Sie Folgendes angeben:  
  
-   Einen Verzeichnisnamen. In der FileTable-Ordnerhierarchie wird dieses Verzeichnis auf Tabellenebene das untergeordnete Element des Datenbankverzeichnisses, das auf Datenbankebene angegeben wurde, und das übergeordnete Element der in der Tabelle gespeicherten Dateien oder Verzeichnisse.  
  
-   Den Namen der Sortierung, der in der Spalte **Name** der FileTable für Dateinamen verwendet werden soll.  
  
-   Die Namen, die für die 3 automatisch erstellten PRIMARY KEY- und UNIQUE-Einschränkungen verwendet werden sollen.  
  
###  <a name="HowToCreate"></a> Vorgehensweise: Erstellen einer FileTable  
 **Erstellen einer FileTable mit Transact-SQL**  
 Erstellen Sie eine FileTable, indem Sie die Option [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) mit der Option **AS FileTable** aufrufen. Da eine FileTable ein festes Schema hat, müssen Sie keine Liste von Spalten angeben. Sie können die folgenden beiden Einstellungen für die neue FileTable angeben:  
  
1.  **FILETABLE_DIRECTORY**. Gibt das Verzeichnis an, das als Stammverzeichnis für alle in der FileTable gespeicherten Dateien und Verzeichnisse verwendet wird. Dieser Name sollte für alle FileTable-Verzeichnisnamen in der Datenbank eindeutig sein. Bei Eindeutigkeitsvergleichen wird die Groß-/Kleinschreibung nicht beachtet, unabhängig von den aktuellen Sortiereinstellungen.  
  
    -   Dieser Wert hat weist den Datentyp **nvarchar(255)** auf und verwendet die feste Sortierung **Latin1_General_CI_AS_KS_WS**.  
  
    -   Der Verzeichnisname, den Sie angeben, muss den Anforderungen des Dateisystems im Hinblick auf einen gültigen Verzeichnisnamen entsprechen.  
  
    -   Dieser Name sollte für alle FileTable-Verzeichnisnamen in der Datenbank eindeutig sein. Bei Eindeutigkeitsvergleichen wird die Groß-/Kleinschreibung nicht beachtet, unabhängig von den aktuellen Sortiereinstellungen.  
  
    -   Wenn Sie beim Erstellen der FileTable keinen Verzeichnisnamen angeben, wird der Name der FileTable selbst als Verzeichnisname verwendet.  
  
2.  **FILETABLE_COLLATE_FILENAME**. Gibt den Namen der Sortierung an, die auf die **Name** -Spalte in der FileTable angewendet werden soll.  
  
    1.  Zur Einhaltung der Windows-Dateinamensemantik darf bei der angegebenen Sortierung die **Groß-/Kleinschreibung** nicht beachtet werden.  
  
    2.  Wenn Sie keinen Wert für **FILETABLE_COLLATE_FILENAME**oder **database_default**angeben, erbt die Spalte die Sortierung der aktuellen Datenbank. Wenn bei der aktuellen Datenbanksortierung die Groß-/Kleinschreibung beachtet wird, wird ein Fehler ausgelöst, und der **CREATE TABLE** -Vorgang schlägt fehl.  
  
3.  Sie können auch die Namen angeben, die für die 3 automatisch erstellten PRIMARY KEY- und UNIQUE-Einschränkungen verwendet werden sollen. Wenn Sie keine Namen angeben, dann werden diese vom System generiert, wie weiter unten in diesem Thema beschrieben.  
  
    -   **FILETABLE_PRIMARY_KEY_CONSTRAINT_NAME**  
  
    -   **FILETABLE_STREAMID_UNIQUE_CONSTRAINT_NAME**  
  
    -   **FILETABLE_FULLPATH_UNIQUE_CONSTRAINT_NAME**  
  
 **Beispiele**  
  
 Im folgenden Beispiel wird eine neue FileTable erstellt, und für **FILETABLE_DIRECTORY** und **FILETABLE_COLLATE_FILENAME**werden benutzerdefinierte Werte angegeben.  
  
```tsql  
CREATE TABLE DocumentStore AS FileTable  
    WITH (   
          FileTable_Directory = 'DocumentTable',  
          FileTable_Collate_Filename = database_default  
         );  
GO  
```  
  
 Im folgenden Beispiel wird zudem eine neue FileTable erstellt. Da keine benutzerdefinierten Werte angegeben werden, wird der Wert von **FILETABLE_DIRECTORY** zum Namen der FileTable, der Wert von **FILETABLE_COLLATE_FILENAME** wird zu database_default, und die PRIMARY KEY- und die UNIQUE-Einschränkung erhalten jeweils von System generierte Namen.  
  
```tsql  
CREATE TABLE DocumentStore AS FileTable;  
GO  
```  
  
 **Erstellen einer FileTable mithilfe von SQL Server Management Studio**  
 Erweitern Sie im Objekt-Explorer unter der ausgewählten Datenbank die Objekte, klicken Sie dann mit der rechten Maustaste auf den Ordner **Tabellen** , und wählen Sie dann **Neue FileTable**aus.  
  
 Mit dieser Option wird ein neues Skriptfenster geöffnet, das eine Transact-SQL-Skriptvorlage enthält, die Sie zum Erstellen einer FileTable anpassen und ausführen können. Passen Sie das Skript einfach mit der Option **Werte für Vorlagenparameter angeben** im Menü **Abfrage** an.  
  
###  <a name="ReqCreate"></a> Anforderungen und Einschränkungen beim Erstellen einer FileTable  
  
-   Sie können eine vorhandene Tabelle nicht ändern, um sie in eine FileTable zu konvertieren.  
  
-   Das zuvor auf der Datenbankebene angegebene übergeordnete Verzeichnis muss einen Wert ungleich NULL haben. Informationen zum Angeben des Verzeichnisses auf Datenbankebene finden Sie unter [Aktivieren der erforderlichen Komponenten für FileTable](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md).  
  
-   Da eine FileTable eine FILESTREAM-Spalte enthält, erfordert eine FileTable eine gültige FILESTREAM-Dateigruppe. Zum Erstellen einer FileTable können Sie optional eine gültige FILESTREAM-Dateigruppe als Teil des **CREATE TABLE** -Befehls angeben. Wenn Sie keine Dateigruppe angeben, verwendet die FileTable die Standard-FILESTREAM-Dateigruppe für die Datenbank. Wenn die Datenbank keine FILESTREAM-Dateigruppe aufweist, wird ein Fehler ausgelöst.  
  
-   Als Teil der **CREATE TABLE…AS FILETABLE** -Anweisung kann keine Tabelleneinschränkung erstellt werden. Sie können die Einschränkung jedoch später mit einer **ALTER TABLE** -Anweisung hinzufügen.  
  
-   Sie können keine FileTable in der **tempdb** -Datenbank oder in einer der anderen Systemdatenbanken erstellen.  
  
-   Eine FileTable kann nicht als temporäre Tabelle erstellt werden.  
  
##  <a name="BasicsAlter"></a> Ändern einer FileTable  
 Da eine FileTable ein vordefiniertes und festes Schema aufweist, können Sie keine Spalten hinzufügen oder ändern. Sie können einer FileTable jedoch benutzerdefinierte Indizes, Trigger, Einschränkungen und andere Optionen hinzufügen.  
  
 Informationen zum Aktivieren bzw. Deaktivieren des FileTable-Namespace (einschließlich der systemdefinierten Einschränkungen) mithilfe der ALTER TABLE-Anweisung finden Sie unter [Verwalten von FileTables](../../relational-databases/blob/manage-filetables.md).  
  
###  <a name="HowToChange"></a> Vorgehensweise: Ändern des Verzeichnisses für eine FileTable  
 **Ändern des Verzeichnisses für eine FileTable mit Transact-SQL**  
 Rufen Sie die ALTER TABLE-Anweisung auf, und geben Sie einen gültigen neuen Wert für die SET-Option von **FILETABLE_DIRECTORY** an.  
  
 **Beispiel**  
  
```tsql  
ALTER TABLE filetable_name  
    SET ( FILETABLE_DIRECTORY = N'directory_name' );  
GO  
```  
  
 **Ändern des Verzeichnisses für eine FileTable mit SQL Server Management Studio**  
 Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf eine FileTable, und wählen Sie **Eigenschaften** aus, um das Dialogfeld **Tabelleneigenschaften** zu öffnen. Geben Sie auf der Seite **FileTable** einen neuen Wert für **Name des FileTable-Verzeichnisses**ein.  
  
###  <a name="ReqAlter"></a> Anforderungen und Einschränkungen beim Ändern einer FileTable  
  
-   Sie können den Wert von **FILETABLE_COLLATE_FILENAME**nicht ändern.  
  
-   Die systemdefinierten Spalten einer FileTable können nicht geändert, gelöscht oder deaktiviert werden.  
  
-   Sie können einer FileTable keine neuen Benutzerspalten, berechnete Spalten oder persistente berechnete Spalten hinzufügen.  
  
##  <a name="BasicsDrop"></a> Löschen einer FileTable  
 Mithilfe der normalen Syntax für die [DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)-Anweisung können Sie eine FileTable löschen.  
  
 Beim Löschen einer FileTable werden auch die folgenden Objekte gelöscht:  
  
-   Alle Spalten der FileTable und alle der Tabelle zugeordneten Objekte, z. B. Indizes, Einschränkungen und Trigger, werden ebenfalls gelöscht.  
  
-   Das FileTable-Verzeichnis und die Unterverzeichnisse, die es enthielt, aus der FILESTREAM-Datei und der Verzeichnishierarchie der Datenbank.  
  
 Der DROP TABLE-Befehl schlägt fehl, wenn geöffnete Dateihandles im Dateinamespace der FileTable vorhanden sind. Informationen zum Schließen von geöffneten Handles finden Sie unter [Verwalten von FileTables](../../relational-databases/blob/manage-filetables.md).  
  
##  <a name="BasicsOtherObjects"></a> Beim Erstellen einer FileTable werden andere Datenbankobjekte erstellt  
 Wenn Sie eine neue FileTable erstellen, werden auch einige systemdefinierte Indizes und Einschränkungen erstellt. Sie können diese Objekte nicht ändern oder löschen; sie verschwinden nur, wenn die FileTable selbst gelöscht wird. Um eine Liste dieser Objekte anzuzeigen, fragen Sie die Katalogsicht [sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md) ab.  
  
```tsql  
--View all objects for all filetables, unsorted  
SELECT * FROM sys.filetable_system_defined_objects;  
GO  
  
--View sorted list with friendly names  
SELECT OBJECT_NAME(parent_object_id) AS 'FileTable', OBJECT_NAME(object_id) AS 'System-defined Object'  
    FROM sys.filetable_system_defined_objects  
    ORDER BY FileTable, 'System-defined Object';  
GO  
```  
  
 **Indizes, die erstellt werden, wenn Sie eine neue FileTable erstellen**  
 Wenn Sie eine neue FileTable erstellen, werden auch die folgenden systemdefinierten Indizes erstellt:  
  
|||  
|-|-|  
|**Spalten**|**Indextyp**|  
|[path_locator] ASC|Primärschlüssel, nicht gruppiert|  
|[parent_path_locator] ASC,<br /><br /> [name] ASC|Eindeutig, nicht gruppiert|  
|[stream_id] ASC|Eindeutig, nicht gruppiert|  
  
 **Einschränkungen, die erstellt werden, wenn Sie eine neue FileTable erstellen**  
 Wenn Sie eine neue FileTable erstellen, werden auch die folgenden systemdefinierten Einschränkungen erstellt:  
  
|Einschränkungen|Erzwingung|  
|-----------------|--------------|  
|Standardeinschränkungen in den folgenden Spalten:<br /><br /> creation_time<br /><br /> is_archive<br /><br /> is_directory<br /><br /> is_hidden<br /><br /> is_offline<br /><br /> is_readonly<br /><br /> is_system<br /><br /> is_temporary<br /><br /> last_access_time<br /><br /> last_write_time<br /><br /> path_locator<br /><br /> stream_id|Die systemdefinierten Standardeinschränkungen erzwingen Standardwerte für die angegebenen Spalten.|  
|Check-Einschränkungen|Die systemdefinierten CHECK-Einschränkungen erzwingen die folgenden Anforderungen:<br /><br /> Gültige Dateinamen<br /><br /> Gültige Dateiattribute<br /><br /> Übergeordnetes Objekt muss ein Verzeichnis sein.<br /><br /> Namespacehierarchie ist während der Dateibearbeitung gesperrt.|  
  
 **Benennungskonvention für die systemdefinierten Einschränkungen**  
 Die Namen der oben beschriebenen systemdefinierten Einschränkungen weisen das Format **\<constraintType>_\<tablename>[\_\<columnname>]\_\<uniquifier>** auf, wobei gilt:  
  
-   *<constraint_type>* ist CK (CHECK-Einschränkung), DF (Standardeinschränkung), FK (Fremdschlüssel), PK (Primärschlüssel) oder UQ (UNIQUE-Einschränkung).  
  
-   *\<uniquifier>* ist eine vom System generierte Zeichenfolge, die den Namen eindeutig macht. Diese Zeichenfolge kann den FileTable-Namen und einen eindeutigen Bezeichner enthalten.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von FileTables](../../relational-databases/blob/manage-filetables.md)  
  
  

