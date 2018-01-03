---
title: Arbeiten mit SSMA-Projekten (MySQLToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Working with SSMA projects, create new project
- Working with SSMA projects, customize settings
- Working with SSMA projects, Open project
- Working with SSMA projects, Save project
ms.assetid: 9e4394e9-f177-41d9-839e-5d53a9c9b840
caps.latest.revision: "20"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b7fd7677d8194938fdc11dc364de8ceea9fe1414
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="working-with-ssma-projects-mysqltosql"></a>Arbeiten mit SSMA-Projekten (MySQLToSQL)
Um MySQL-Datenbanken zu SQL Server oder SQL Azure zu migrieren, müssen Sie zuerst eine SSMA-Projekt erstellen. Das Projekt ist eine Datei mit den folgenden Informationen an:  
  
-   Metadaten über die MySQL-Datenbanken, die Sie in SQL Server oder SQL Azure migrieren möchten.  
  
-   Metadaten zu der Zielinstanz von SQL Server- oder SQL Azure, die die migrierten Objekte und Daten erhalten.  
  
-   SQL Server- bzw. SQL Azure-Verbindungsinformationen.  
  
-   Einstellungen für Projektdateien.  
  
Wenn Sie ein Projekt öffnen, wird er von MySQL und SQL Server oder SQL Azure getrennt. Mit der Sie offline arbeiten. Weitere Informationen zum Wiederherstellen der Verbindung mit SQL Server finden Sie unter [Herstellen einer Verbindung mit SQL Server &#40; MySQLToSQL &#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="reviewing-default-project-settings"></a>Überprüfen die standardmäßigen Projekteinstellungen  
SSMA enthält verschiedene Einstellungen für konvertieren und laden die Datenbank, Migrieren von Daten und beim Synchronisieren von SSMA mit MySQL und SQL Server oder SQL Azure. Die Standardeinstellungen eignen sich für viele Benutzer. Bevor Sie ein neues SSMA-Projekt erstellen, sollten Sie die Einstellungen überprüfen. Falls erforderlich, können Sie die Standardeinstellungen ändern, die für alle neuen Projekte verwendet werden.  
  
##### <a name="to-review-default-project-settings"></a>Um standardprojekteinstellungen zu überprüfen.  
  
1.  Wählen Sie **Projekt Standardeinstellungen** aus der **Tools** Menü.  
  
2.  Wählen Sie den Projekttyp in **Migration Zielversion** Dropdownmenü für die Einstellungen angezeigt bzw. geändert werden, und klicken Sie dann auf **allgemeine** Registerkarte.  
  
3.  Klicken Sie im linken Bereich auf **Konvertierung**.  
  
4.  Überprüfen Sie im rechten Bereich, und ändern Sie die Einstellungen nach Bedarf. Weitere Informationen zu diesen Einstellungen finden Sie unter [Projekteinstellungen &#40; Konvertierung &#41; &#40; MySQLToSQL &#41; ](../../ssma/mysql/project-settings-conversion-mysqltosql.md) .  
  
5.  Wiederholen Sie die Schritte 1 bis 3 für die Migration, Synchronisierung, SQL Azure, GUI und Type Mapping-Seiten.  
  
-   Informationen zur von migrationseinstellungen finden Sie unter [Projekteinstellungen &#40; Migration &#41; &#40; MySQLToSQL &#41; ](../../ssma/mysql/project-settings-migration-mysqltosql.md).  
  
-   Weitere Informationen zu den Einstellungen für die Synchronisierung mit SQL Server finden Sie unter [Projekteinstellungen &#40; Synchronisierung &#41; &#40; MySQLToSQL &#41; ](../../ssma/mysql/project-settings-synchronization-mysqltosql.md).  
  
-   Informationen zu den GUI-Einstellungen finden Sie unter [Projekt Einstellungen (GUI) (SSMA häufigen Spalten)](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693).  
  
-   Informationen zu den datentypzuordnung Einstellungen finden Sie unter [Projekteinstellungen &#40; Typzuordnung &#41; &#40; MySQLToSQL &#41; ](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md).  
  
-   Weitere Informationen zu SQL Azure-Einstellungen finden Sie unter [Projekteinstellungen &#40; Azure SQL-Datenbank &#41; &#40; MySQLToSQL &#41; ](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md).  
  
> [!NOTE]  
> Die SQL Azure-Einstellungen werden angezeigt, bei der Auswahl **Migration zu SQL Azure** beim Erstellen eines Projekts.  
  
## <a name="creating-new-projects"></a>Erstellen neuer Projekte  
Um Daten aus MySQL-Datenbanken zu SQL Server oder SQL Azure zu migrieren, müssen Sie ein Projekt erstellen.  
  
##### <a name="to-create-a-new-project"></a>Zum Erstellen eines neuen Projekts  
  
1.  Wählen Sie **neues Projekt** aus der **Datei** Menü. Das Dialogfeld **Neues Projekt** wird angezeigt. Wählen Sie im Menü **Datei** die Option **Neues Projekt** aus. Das Dialogfeld **Neues Projekt** wird angezeigt.  
  
2.  In der **Namen** Geben Sie einen Namen für das Projekt.  
  
3.  In der **Speicherort** Feld, geben Sie ein oder wählen Sie einen Ordner für das Projekt.  
  
4.  In der **Migration auf** Dropdown-Liste, wählen Sie die Version des Ziels [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] verwendet für die Migration. Die verfügbaren Optionen sind:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014  
  
    -   Azure SQL-Datenbank  
  
Und klicken Sie dann auf **OK**  
  
SSMA wird die Projektdatei erstellt.  
  
## <a name="customizing-project-settings"></a>Anpassen von Projekteinstellungen  
Projekteinstellungen, die für alle neuen SSMA-Projekte, die Sie anwenden können auch die Einstellungen für jedes Projekt anpassen, zusätzlich zum Definieren des Standardwerts. Weitere Informationen finden Sie unter [Einstellung Projektoptionen &#40; MySQLToSQL &#41; ](../../ssma/mysql/setting-project-options-mysqltosql.md).  
  
Wenn Sie datentypzuordnungen zwischen den Quell- und Zieldatenbanken anpassen, können Sie Zuordnungen auf das Projekt, Datenbank oder Objektebene definieren. Weitere Informationen finden Sie unter [Zuordnung MySQL und SQL Server-Datentypen &#40; MySQLToSQL &#41; ](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md).  
  
## <a name="saving-projects"></a>Speichern von Projekten  
Das Speichern von Projekten-Feature ermöglicht den Benutzer, speichern die Einstellungen für Projektdateien und optional den Datenbankmetadaten im Wesentlichen der SSMA-Projektdatei.  
  
##### <a name="to-save-a-project"></a>Um ein Projekt zu speichern.  
  
-   Auf der **Datei** klicken Sie im Menü **speichern** Projekt.  
  
Wenn Datenbanken innerhalb des Projekts sich verändert haben oder nicht konvertiert wurde, fordert SSMA laden und Speichern von Metadaten. Laden und Speichern von Metadaten können Sie offline arbeiten. Außerdem können Sie eine vollständige Projektdatei an andere Personen, z. B. der technische Support in Verbindung zu senden. Wenn Sie aufgefordert werden, um Metadaten zu speichern, führen Sie folgende Schritte aus:  
  
1.  Für jede Datenbank, die den Status anzeigt **fehlenden Metadaten**, wählen Sie das Kontrollkästchen neben dem Datenbanknamen. Speichern von Metadaten kann einige Minuten dauern. Wenn Sie nicht, um Metadaten zu diesem Zeitpunkt zu speichern möchten, wählen Sie alle Kontrollkästchen nicht.  
  
2.  Klicken Sie auf **Speichern**.  
  
SSMA analysiert die MySQL-Schemas und speichern Sie die Metadaten in die Projektdatei.  
  
## <a name="opening-projects"></a>Öffnen von Projekten  
Wenn Sie ein Projekt öffnen, wird er von MySQL und SQL Server oder SQL Azure getrennt. Dadurch können Sie offline arbeiten. Um Metadaten zu aktualisieren, laden Sie Datenbankobjekte in SQL Server oder SQL Azure. Zum Migrieren von Daten müssen Sie eine Verbindung mit SQL Server- bzw. SQL Azure wiederherstellen.  
  
##### <a name="to-open-a-project"></a>Öffnen eines Projekts  
  
1.  Verwenden Sie eine der folgenden Verfahren aus:  
  
    1.  Auf der **Datei** Sie im Menü **zuletzt geöffnete Projekte**.  
  
    2.  Wählen Sie das Projekt, das Sie öffnen möchten.  
  
    3.  Auf der **Datei** klicken Sie im Menü **Projekt öffnen**, suchen Sie die Projektdatei .m2ssproj, wählen Sie die Datei, und klicken Sie dann auf **öffnen**.  
  
2.  Verbindung mit MySQL, auf die **Datei** klicken Sie im Menü **eine erneute Verbindung mit MySQL**.  
  
3.  Verbindung zu SQL Server, auf die **Datei** klicken Sie im Menü **eine erneute Verbindung mit SQL Server**.  
  
4.  Verbindung zu SQL Azure, auf die **Datei** klicken Sie im Menü **das erneute Verbinden mit SQL Azure.**  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt des Migrationsvorgangs besteht [Herstellen einer Verbindung mit MySQL &#40; MySQLToSQL &#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Herstellen einer Verbindung mit MySQL &#40; MySQLToSQL &#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
[Migrieren von MySQL-Datenbanken zu SQLServer – Azure SQL-Datenbank &#40; MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[Herstellen einer Verbindung mit SQLServer &#40; MySQLToSQL &#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
[Herstellen einer Verbindung mit Azure SQL-Datenbank &#40; MySQLToSQL &#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
