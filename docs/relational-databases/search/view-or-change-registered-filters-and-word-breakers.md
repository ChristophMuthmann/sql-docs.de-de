---
title: "Anzeigen oder &#196;ndern von registrierten Filtern und W&#246;rtertrennungen | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Volltextsuche [SQL Server], Wörtertrennung"
  - "Volltextsuche [SQL Server], Filter"
  - "Filter [Volltextsuche]"
  - "Wörtertrennungen [Volltextsuche]"
ms.assetid: f88c54df-b1aa-4701-807f-dc92c32363fd
caps.latest.revision: 22
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 22
---
# Anzeigen oder &#196;ndern von registrierten Filtern und W&#246;rtertrennungen
  Nach dem Installieren oder Deinstallieren von Wörtertrennungen oder Filtern werden die Änderungen nicht automatisch auf Serverinstanzen wirksam. In diesem Thema wird beschrieben, wie die zurzeit registrierte Wörtertrennung oder die Filter angezeigt werden und wie neu installierte Wörtertrennungen und Filter auf einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registriert werden.  
  
### So zeigen Sie eine Liste der Sprachen an, deren Wörtertrennungen derzeit registriert sind.  
  
1.  Verwenden Sie die [sys.fulltext_languages](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)-Katalogsicht wie folgt:  
  
    ```  
    SELECT * FROM sys.fulltext_languages;   
    ```  
  
### So zeigen Sie eine Liste der Filter an, die derzeit registriert sind  
  
1.  Verwenden Sie die gespeicherte Systemprozedur [sp_help_fulltext_system_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md) wie folgt:  
  
    ```  
    EXEC sp_help_fulltext_system_components 'filter';    
    ```  
  
### So registrieren Sie neu installierte Wörtertrennungen und Filter  
  
1.  Verwenden Sie zum Aktualisieren der Liste mit den Sprachen die gespeicherte Systemprozedur [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md) wie folgt:  
  
    ```  
    exec sp_fulltext_service 'update_languages';   
    ```  
  
### So heben Sie die Registrierung deinstallierter Wörtertrennungen und Filter auf  
  
1.  Verwenden Sie zum Aktualisieren der Liste mit den Sprachen **sp_fulltext_service** wie folgt:  
  
    ```  
    exec sp_fulltext_service 'update_languages'  
    ```  
  
2.  Verwenden Sie zum Neustarten der Filterdaemon-Hostprozesse (fdhost.exe) **sp_fulltext_service** wie folgt:  
  
    ```  
    exec sp_fulltext_service 'restart_all_fdhosts';  
    ```  
  
### So ersetzen Sie vorhandene Wörtertrennungen oder Filter beim Installieren neuer Wörtertrennungen und Filter  
  
1.  Vergewissern Sie sich bei der Vorbereitung zur Installation einer DLL-Datei, die neue Wörtertrennungen oder Filter enthält, dass diese nicht den gleichen Namen einer DLL-Datei hat, die bereits auf Ihrer Serverinstanz installiert ist.  
  
2.  Kopieren Sie die neue DLL-Datei in das Verzeichnis, das die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard-DLL-Dateien für die Serverinstanz enthält. Der Standardspeicherort ist:  
  
     C:\Programme\Microsoft SQL Server\MSSQL.*Instanzname*\MSSQL\Binn  
  
    > [!IMPORTANT]  
    >  Es wird dringend empfohlen, nur signierte und überprüfte Komponenten zu laden. Außerdem sollten Sie den FDHOST-Startprogrammdienst (MSSQLFDLauncher) mit den geringstmöglichen Privilegien ausführen.  
  
3.  Installieren Sie die neue Wörtertrennung oder die Filter.  
  
     **So installieren und laden Sie Microsoft Filter Pack IFilters**  
  
    -   [So registrieren Sie Microsoft Filter Pack IFilters bei SQL Server](http://go.microsoft.com/fwlink/?LinkId=130439)  
  
4.  Verwenden Sie zum Laden neu installierter Wörtertrennungen und Filter in die Serverinstanz **sp_fulltext_service** wie folgt:  
  
    ```  
    EXEC sp_fulltext_service @action='load_os_resources', @value=1;  
    ```  
  
5.  Verwenden Sie zum Aktualisieren der Liste mit den Sprachen **sp_fulltext_service** wie folgt:  
  
    ```  
    EXEC sp_fulltext_service 'update_languages';  
    ```  
  
6.  Verwenden Sie zum Neustarten der Filterdaemon-Hostprozesse (fdhost.exe) **sp_fulltext_service** wie folgt:  
  
    ```  
    EXEC sp_fulltext_service 'restart_all_fdhosts';   
    ```  
  
## Siehe auch  
 [Festlegen des Dienstkontos für das Startprogramm des Volltextfilterdaemon](../../relational-databases/search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)   
 [Konfigurieren und Verwalten von Filtern für die Suche](../../relational-databases/search/configure-and-manage-filters-for-search.md)   
 [Konfigurieren und Verwalten von Wörtertrennungen und Wortstammerkennungen für die Suche](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)  
  
  