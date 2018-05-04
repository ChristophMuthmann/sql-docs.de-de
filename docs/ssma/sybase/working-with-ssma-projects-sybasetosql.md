---
title: Arbeiten mit SSMA-Projekten (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 11091d95-c488-48c3-891a-743cac94ac93
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 4cf7525599256dce04617bd63e5de0239deabb7b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-ssma-projects-sybasetosql"></a>Arbeiten mit SSMA-Projekten (SybaseToSQL)
Zum Migrieren von Datenbanken von Sybase Adaptive Server Enterprise (ASE) zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, Sie zuerst ein SSMA Projekt erstellen. Das Projekt ist eine Datei, die Metadaten zu den Datenbanken ASE enthält, die Sie zum migrieren möchten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder Metadaten zu der Zielinstanz von SQL Azure [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, die die migrierten Objekte und Daten, erhalten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Verbindungsinformationen und Einstellungen für Projektdateien.  
  
Wenn Sie ein Projekt öffnen, wird getrennt von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Dadurch können Sie offline arbeiten. Sie können die Verbindung mit wiederherstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md) / [Herstellen einer Verbindung mit Azure SQL-Datenbank &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md).  
  
## <a name="reviewing-default-project-settings"></a>Überprüfen die standardmäßigen Projekteinstellungen  
SSMA enthält mehrere Optionen zum Umrechnen und Laden von Datenbankobjekten, Migrieren von Daten und beim Synchronisieren von SSMA mit ASE und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Die Standardeinstellungen für diese Optionen eignen sich für viele Benutzer. Jedoch bevor Sie ein neues SSMA-Projekt erstellen, sollten Sie überprüfen Sie die Optionen und, wenn Sie möchten, ändern die Standardwerte, die für alle neuen Projekte verwendet werden.  
  
**Um standardprojekteinstellungen zu überprüfen.**  
  
1.  Auf der **Tools** klicken Sie im Menü **Projekt Standardeinstellungen**.  
  
2.  Wählen Sie den Projekttyp in **Migration Zielversion** Dropdownmenü für die Einstellungen sind erforderlich, angezeigt oder geändert werden soll, und klicken Sie dann auf **allgemeine** Registerkarte.  
  
3.  Klicken Sie im linken Bereich auf **Konvertierung**.  
  
4.  Überprüfen Sie im rechten Bereich die Optionen, die Optionen nach Bedarf ändern. Weitere Informationen zu diesen Optionen finden Sie unter [Projekteinstellungen &#40;Konvertierung&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md).  
  
5.  Wiederholen Sie die Schritte 1 bis 3 für die Migration, SQL Azure, Laden von Objekten, GUI und Type Mapping-Seiten.  
  
    -   Informationen zu Migrationsoptionen finden Sie unter [Projekteinstellungen &#40;Migration&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md).  
  
    -   Weitere Informationen zu Optionen zum Laden von Objekten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], finden Sie unter [Projekteinstellungen &#40;Synchronisierung&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md).  
  
    -   Weitere Informationen über die GUI-Optionen finden Sie unter [Projekteinstellungen &#40;GUI&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md).  
  
    -   Weitere Informationen zu datentypzuordnung-Einstellungen, klicken Sie auf [Projekteinstellungen &#40;Typzuordnung&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md).  
  
    -   Weitere Informationen zu SQL Azure-Optionen finden Sie unter [Projekteinstellungen &#40;Azure SQL-Datenbank &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md).  
  
    > [!NOTE]  
    > Die SQL Azure-Einstellungen werden angezeigt, bei der Auswahl **Migration zu SQL Azure** beim Erstellen eines Projekts.  
  
## <a name="creating-new-projects"></a>Erstellen neuer Projekte  
Zum Migrieren von Daten aus Datenbanken ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, müssen Sie zunächst ein Projekt erstellen.  
  
**Zum Erstellen eines Projekts**  
  
1.  Wählen Sie im Menü **Datei** die Option **Neues Projekt** aus.  
  
    Das Dialogfeld **Neues Projekt** wird angezeigt.  
  
2.  In der **Namen** Geben Sie einen Namen für das Projekt.  
  
3.  In der **Speicherort** Feld, geben Sie ein oder wählen Sie einen Ordner für das Projekt.  
  
4.  In der **Migration auf** Dropdown-Liste, wählen Sie die Version des Ziels [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] verwendet für die Migration. Die verfügbaren Optionen sind:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016  
  
    -   Azure SQL-Datenbank  
  
Und klicken Sie dann auf **OK**.  
  
## <a name="customizing-project-settings"></a>Anpassen von Projekteinstellungen  
Zusätzlich zum Definieren von Standard-projekteinstellungen, die für alle neuen SSMA-Projekte gelten, können Sie die Einstellungen für jedes Projekt anpassen. Weitere Informationen finden Sie unter [Einstellung Projektoptionen &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md).  
  
Wenn Sie datentypzuordnungen zwischen Quell-und Zieldatenbanken anpassen, können Sie Zuordnungen auf das Projekt, Datenbank oder Objektebene definieren. Weitere Informationen zur Zuordnung finden Sie unter [Zuordnung Sybase ASE und SQL Server-Datentypen &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
## <a name="saving-projects"></a>Speichern von Projekten  
Wenn Sie ein Projekt speichern, behält SSMA den projekteinstellungen und optional die Datenbank-Metadaten in die Projektdatei.  
  
**Um ein Projekt zu speichern.**  
  
-   Auf der **Datei** klicken Sie im Menü **Projekt speichern**.  
  
    Wenn Datenbanken innerhalb des Projekts sich verändert haben oder nicht konvertiert wurde, fordert SSMA Sie Metadaten in das Projekt zu speichern. Metadaten zu speichern, können Sie die offline arbeiten und senden eine vollständige Projektdatei an andere Personen, einschließlich der technischen Support in Verbindung. Wenn Sie aufgefordert werden, um Metadaten zu speichern, führen Sie folgende Schritte aus:  
  
    1.  Für jede Datenbank, die den Status anzeigt **fehlenden Metadaten**, wählen Sie das Kontrollkästchen neben dem Datenbanknamen.  
  
        Speichern von Metadaten kann einige Minuten dauern. Wenn Sie nicht, um Metadaten zu diesem Zeitpunkt zu speichern möchten, wählen Sie alle Kontrollkästchen nicht.  
  
    2.  Klicken Sie auf die **speichern** Schaltfläche.  
  
        SSMA analysiert die Sybase ASE Schemas und speichern Sie die Metadaten in die Projektdatei.  
  
## <a name="opening-projects"></a>Öffnen von Projekten  
Wenn Sie ein Projekt öffnen, wird getrennt von ASE und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Dadurch können Sie offline arbeiten. Um Metadaten zu aktualisieren, laden Sie die Datenbankobjekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Um Daten zu migrieren, müssen die Verbindung mit ASE und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure.  
  
**Öffnen eines Projekts**  
  
1.  Verwenden Sie eine der folgenden Verfahren aus:  
  
    -   Auf der **Datei** Sie im Menü **zuletzt geöffnete Projekte**, und wählen Sie dann das Projekt, das Sie öffnen möchten.  
  
    -   Auf der **Datei** klicken Sie im Menü **Projekt öffnen**, suchen Sie die Projektdatei .s2ssproj, wählen Sie die Datei, und klicken Sie dann auf **öffnen**.  
  
2.  Verbindung zum ASE, auf die **Datei** klicken Sie im Menü **eine erneute Verbindung zu Sybase**.  
  
3.  Eine Verbindung mit herstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, auf die **Datei** klicken Sie im Menü **eine erneute Verbindung mit SQL Server** / **eine erneute Verbindung mit SQL Azure**.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt des Migrationsvorgangs besteht darin [Herstellen einer Verbindung mit der Sybase ASE](http://msdn.microsoft.com/en-us/a45a2330-9175-4c9e-af38-ef920e350614).  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Sybase ASE-Datenbanken zu SQLServer – Azure SQL-Datenbank &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[Herstellen einer Verbindung mit der Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)  
[Herstellen einer Verbindung mit SQLServer &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)  
[Herstellen einer Verbindung mit Azure SQL-Datenbank &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
