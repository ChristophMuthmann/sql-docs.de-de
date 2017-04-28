---
title: "Aktivieren der erforderlichen Komponenten für FileTable | Microsoft-Dokumentation"
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
- FileTables [SQL Server], prerequisites
ms.assetid: 6286468c-9dc9-4eda-9961-071d2a36ebd6
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ed35c6e65d3c9670ddb59f352451adfde6c37e07
ms.lasthandoff: 04/11/2017

---
# <a name="enable-the-prerequisites-for-filetable"></a>Aktivieren der erforderlichen Komponenten für FileTable
  Beschreibt, wie die erforderlichen Komponenten zum Erstellen und Verwenden von FileTables aktiviert werden.  
  
##  <a name="EnablePrereq"></a> Aktivieren der erforderlichen Komponenten für FileTable  
 Aktivieren Sie zum Aktivieren der erforderlichen Komponenten zum Erstellen und Verwenden von FileTables die folgenden Elemente:  
  
-   **Auf Instanzebene:**  
  
    -   [Aktivieren von FILESTREAM auf Instanzebene](#BasicsFilestream)  
  
-   **Auf Datenbankebene:**  
  
    -   [Bereitstellen einer FILESTREAM-Dateigruppe auf der Datenbankebene](#filegroup)  
  
    -   [Aktivieren des nicht transaktionalen Zugriffs auf Datenbankebene](#BasicsNTAccess)  
  
    -   [Angeben eines Verzeichnisses für FileTables auf Datenbankebene](#BasicsDirectory)  
  
##  <a name="BasicsFilestream"></a> Aktivieren von FILESTREAM auf Instanzebene  
 FileTables erweitern die Funktionen der FILESTREAM-Funktion von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Daher muss FILESTREAM für Datei-E/A-Zugriff auf der Windows-Ebene und in der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktiviert werden, bevor Sie FileTables erstellen und verwenden können.  
  
###  <a name="HowToFilestream"></a> Vorgehensweise: Aktivieren von FILESTREAM auf Instanzebene  
 Informationen zum Aktivieren von FILESTREAM finden Sie unter [Aktivieren und Konfigurieren von FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md).  
  
 Wenn Sie **sp_configure** aufrufen, um FILESTREAM auf Instanzebene zu aktivieren, müssen Sie die Option „filestream_access_level“auf „2“ festlegen. Weitere Informationen finden Sie unter [Filestream-Zugriffsebene (Serverkonfigurationsoption)](../../database-engine/configure-windows/filestream-access-level-server-configuration-option.md).  
  
###  <a name="firewall"></a> Vorgehensweise: Zulassen von FILESTREAM durch die Firewall  
 Informationen zum Zulassen von FILESTREAM durch die Firewall finden Sie unter [Configure a Firewall for FILESTREAM Access](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md).  
  
##  <a name="filegroup"></a> Bereitstellen einer FILESTREAM-Dateigruppe auf der Datenbankebene  
 Bevor Sie FileTables in einer Datenbank erstellen können, muss die Datenbank eine FILESTREAM-Dateigruppe haben. Weitere Informationen zu dieser Voraussetzung finden Sie unter [Erstellen einer FILESTREAM-aktivierten Datenbank](../../relational-databases/blob/create-a-filestream-enabled-database.md).  
  
##  <a name="BasicsNTAccess"></a> Aktivieren des nicht transaktionalen Zugriffs auf Datenbankebene  
 Über FileTables können Windows-Anwendungen ein Windows-Dateihandle für FILESTREAM-Daten abrufen, ohne dass hierfür eine Transaktion erforderlich ist. Um diesen nicht transaktionalen Zugriff auf in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gespeicherte Dateien zuzulassen, müssen Sie die gewünschte Ebene des nicht transaktionalen Zugriffs auf Datenbankebene für jede Datenbank angeben, die FileTables enthält.  
  
###  <a name="HowToCheckAccess"></a> Vorgehensweise: Überprüfen, ob nicht transaktionaler Zugriff auf Datenbanken aktiviert ist  
 Fragen Sie die Katalogsicht [sys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md) ab, und überprüfen Sie die Spalten **non_transacted_access** und **non_transacted_access_desc**.  
  
```tsql  
SELECT DB_NAME(database_id), non_transacted_access, non_transacted_access_desc  
    FROM sys.database_filestream_options;  
GO  
```  
  
###  <a name="HowToNTAccess"></a> Vorgehensweise: Aktivieren von nicht transaktionalem Zugriff auf Datenbankebene  
 Die verfügbaren Stufen des nicht transaktionalen Zugriffs sind FULL, READ_ONLY und OFF.  
  
 **Angeben der Ebene des nicht transaktionalen Zugriffs mit Transact-SQL**  
 -   Wenn Sie **eine neue Datenbank erstellen**, rufen Sie die [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)-Anweisung mit der FILESTREAM-Option **NON_TRANSACTED_ACCESS** auf.  
  
    ```tsql  
    CREATE DATABASE database_name  
        WITH FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' )  
    ```  
  
-   Wenn Sie **eine vorhandene Datenbank ändern**, rufen Sie die [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)-Anweisung mit der FILESTREAM-Option **NON_TRANSACTED_ACCESS** auf.  
  
    ```tsql  
    ALTER DATABASE database_name  
        SET FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' )  
    ```  
  
 **Angeben der Ebene des nicht transaktionalen Zugriffs mithilfe von SQL Server Management Studio**  
 Sie können die Ebene des nicht transaktionalen Zugriffs im Feld **FILESTREAM Nicht durchgeführter Zugriff** der Seite **Optionen** des Dialogfelds **Datenbankeigenschaften** angeben. Weitere Informationen zu diesem Dialogfeld finden Sie unter [Datenbankeigenschaften &#40;Seite Optionen&#41;](../../relational-databases/databases/database-properties-options-page.md).  
  
##  <a name="BasicsDirectory"></a> Angeben eines Verzeichnisses für FileTables auf Datenbankebene  
 Wenn Sie nicht transaktionalen Zugriff auf Dateien auf Datenbankebene aktivieren, können Sie gleichzeitig optional einen Verzeichnisnamen mit der **DIRECTORY_NAME** -Option angeben. Wenn Sie keinen Verzeichnisnamen angeben, wenn Sie nicht transaktionalen Zugriff aktivieren, müssen Sie diesen später angeben, bevor Sie FileTables in der Datenbank erstellen können.  
  
 In der FileTable-Ordnerhierarchie wird dieses Verzeichnis auf Datenbankebene das untergeordnete Element des Freigabenamens, das für FILESTREAM auf Instanzebene angegeben wurde, und das übergeordnete Element von den in der Datenbank erstellten FileTables. Weitere Informationen finden Sie unter [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md).  
  
###  <a name="HowToDirectory"></a> Vorgehensweise: Angeben eines Verzeichnisses für FileTables auf Datenbankebene  
 Der angegebene Name muss in der Instanz für Verzeichnisse auf Datenbankebene eindeutig sein.  
  
 **Angeben eines Verzeichnisses für FileTables mit Transact-SQL**  
 -   Wenn Sie **eine neue Datenbank erstellen**, rufen Sie die [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)-Anweisung mit der FILESTREAM-Option **DIRECTORY_NAME** auf.  
  
    ```tsql  
    CREATE DATABASE database_name  
        WITH FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
-   Wenn Sie **eine vorhandene Datenbank ändern**, rufen Sie die [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)-Anweisung mit der FILESTREAM-Option **DIRECTORY_NAME** auf. Wenn Sie diese Optionen verwenden, um den Verzeichnisnamen zu ändern, muss die Datenbank exklusiv gesperrt sein und darf keine offenen Dateihandles aufweisen.  
  
    ```tsql  
    ALTER DATABASE database_name  
        SET FILESTREAM ( NON_TRANSACTED_ACCESS = FULL, DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
-   Wenn Sie **eine Datenbank anfügen**, rufen Sie die [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)-Anweisung mit der **FOR ATTACH**-Option und der FILESTREAM-Option **DIRECTORY_NAME** auf.  
  
    ```tsql  
    CREATE DATABASE database_name  
        FOR ATTACH WITH FILESTREAM ( DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
-   Wenn Sie **eine Datenbank wiederherstellen**, rufen Sie die [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)-Anweisung mit der FILESTREAM-Option **DIRECTORY_NAME** auf.  
  
    ```tsql  
    RESTORE DATABASE database_name  
        WITH FILESTREAM ( DIRECTORY_NAME = N'directory_name' );  
    GO  
    ```  
  
 **Angeben eines Verzeichnisses für FileTables mithilfe von SQL Server Management Studio**  
 Sie können im Feld **FILESTREAM Verzeichnisname** der Seite **Optionen** des Dialogfelds **Datenbankeigenschaften** einen Verzeichnisnamen angeben. Weitere Informationen zu diesem Dialogfeld finden Sie unter [Datenbankeigenschaften &#40;Seite Optionen&#41;](../../relational-databases/databases/database-properties-options-page.md).  
  
###  <a name="viewnames"></a> Vorgehensweise: Anzeigen vorhandener Verzeichnisnamen für die Instanz  
 Fragen Sie zum Anzeigen einer Liste vorhandener Verzeichnisnamen für die Instanz die [sys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md)-Katalogsicht ab, und überprüfen Sie die **filestream_database_directory_name**-Spalte.  
  
```tsql  
SELECT DB_NAME ( database_id ), directory_name  
    FROM sys.database_filestream_options;  
GO  
```  
  
###  <a name="ReqDirectory"></a> Anforderungen und Einschränkungen für das Verzeichnis auf Datenbankebene  
  
-   Das Festlegen von **DIRECTORY_NAME** ist beim Aufrufen von **CREATE DATABASE** oder **ALTER DATABASE**optional. Wenn Sie keinen Wert für **DIRECTORY_NAME**angeben, bleibt der Verzeichnisname NULL. Sie können jedoch erst FileTables in der Datenbank erstellen, wenn Sie einen Wert für **DIRECTORY_NAME** auf Datenbankebene angeben.  
  
-   Der Verzeichnisname, den Sie angeben, muss den Anforderungen des Dateisystems im Hinblick auf einen gültigen Verzeichnisnamen entsprechen.  
  
-   Wenn die Datenbank FileTables enthält, können Sie den **DIRECTORY_NAME** nicht auf einen NULL-Wert zurücksetzen.  
  
-   Wenn Sie eine Datenbank anfügen oder wiederherstellen, schlägt der Vorgang fehl, wenn die neue Datenbank über einen Wert für **DIRECTORY_NAME** verfügt, der bereits in der Zielinstanz vorhanden ist. Geben Sie einen eindeutigen Wert für **DIRECTORY_NAME** an, wenn Sie **CREATE DATABASE FOR ATTACH** oder **RESTORE DATABASE**aufrufen.  
  
-   Wenn Sie eine vorhandene Datenbank auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]aktualisieren, ist der Wert von **DIRECTORY_NAME** NULL.  
  
-   Wenn Sie nicht transaktionalen Zugriff auf Datenbankebene aktivieren oder deaktivieren, wird nicht überprüft, ob der Verzeichnisname angegeben wurde oder ob er eindeutig ist.  
  
-   Wenn Sie eine Datenbank löschen, die für FileTables aktiviert wurde, werden das Verzeichnis auf Datenbankebene und alle Verzeichnisstrukturen aller FileTables darunter entfernt.  
  
  
