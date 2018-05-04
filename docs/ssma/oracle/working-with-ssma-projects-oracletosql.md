---
title: Arbeiten mit SSMA-Projekten (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Customizing Project Settings
ms.assetid: ee5d94c0-c7a6-4779-bd32-729bdaf61e1b
caps.latest.revision: 11
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 80f2581ac5212f7fe0b1c7684b4eb548c0fa8c2e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="working-with-ssma-projects-oracletosql"></a>Arbeiten mit SSMA-Projekten (OracleToSQL)
Zum Migrieren von Oracle-Datenbanken zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], erstellen Sie zunächst ein SSMA-Projekt. Das Projekt ist eine Datei mit den folgenden Informationen an:  
  
-   Metadaten für die Oracle-Datenbanken, die Sie zum migrieren möchten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Metadaten für die Zielinstanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] erhalten, die die migrierten Objekte und Daten.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Verbindungsinformationen.  
  
-   Einstellungen für Projektdateien.  
  
Wenn Sie ein Projekt öffnen, wird Sie aus Oracle-Datenbanken getrennt und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Mit der Sie offline arbeiten. Informationen zum Wiederherstellen der Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], finden Sie unter [Herstellen einer Verbindung mit SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md).  
  
## <a name="reviewing-default-project-settings"></a>Überprüfen die standardmäßigen Projekteinstellungen  
SSMA enthält mehrere Einstellungen zum Umrechnen und Laden von Datenbankobjekten, Migrieren von Daten und beim Synchronisieren von SSMA mit Oracle und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Die Standardeinstellungen eignen sich für viele Benutzer. Bevor Sie ein neues SSMA-Projekt erstellen, sollten Sie die Einstellungen überprüfen. Wenn Sie möchten, können Sie die Standardeinstellungen ändern, die für alle neuen Projekte verwendet werden.  
  
**Um standardprojekteinstellungen zu überprüfen.**  
  
1.  Auf der **Tools** Menü klicken Sie auf **Projekt Standardeinstellungen**.  
  
2.  Wählen Sie den Projekttyp in **Migration Zielversion** Dropdownmenü für die Einstellungen sind erforderlich, angezeigt oder geändert werden soll, und klicken Sie dann auf **allgemeine** Registerkarte.  
  
3.  Klicken Sie im linken Bereich auf **Konvertierung**.  
  
4.  Überprüfen Sie im rechten Bereich, und ändern Sie die Einstellungen nach Bedarf. Weitere Informationen zu diesen Einstellungen finden Sie unter [Projekteinstellungen &#40;Konvertierung&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md).  
  
5.  Wiederholen Sie die Schritte 1 bis 3 für die Migration, Synchronisierung, Laden von Systemobjekten, GUI und Type Mapping-Seiten.  
  
    -   Informationen zur von migrationseinstellungen finden Sie unter [Projekteinstellungen &#40;Migration&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-migration-oracletosql.md).  
  
    -   Informationen zum Objekt-Systemeinstellungen finden Sie unter [Projekteinstellungen&#40;laden Systemobjekte&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-loading-system-objects-oracletosql.md).  
  
    -   Weitere Informationen zu Einstellungen für die Synchronisierung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], finden Sie unter [Projekteinstellungen&#40;Synchronisierung&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md).  
  
    -   Informationen zu den GUI-Einstellungen finden Sie unter [Projekteinstellungen &#40;GUI&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-gui-oracletosql.md).  
  
    -   Informationen zu den datentypzuordnung Einstellungen finden Sie unter [Projekteinstellungen &#40;Typzuordnung&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md).  
  
## <a name="creating-new-projects"></a>Erstellen neuer Projekte  
Zum Migrieren von Daten aus Oracle-Datenbanken zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], müssen Sie zunächst ein Projekt erstellen.  
  
**Zum Erstellen eines Projekts**  
  
1.  Auf der **Datei** Menü klicken Sie auf **neues Projekt**.  
  
    Das Dialogfeld **Neues Projekt** wird angezeigt.  
  
2.  In der **Namen** Geben Sie einen Namen für das Projekt.  
  
3.  In der **Speicherort** Feld eingeben oder wählen Sie einen Ordner für das Projekt, und klicken Sie dann auf **OK**.  
  
4.  In der **Migration auf** Dropdown-Liste, wählen Sie die Version des Ziels [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] verwendet für die Migration. Die verfügbaren Optionen sind:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016  
  
    -   Azure SQL-Datenbank  
  
## <a name="customizing-project-settings"></a>Anpassen von Projekteinstellungen  
Zusätzlich zum Definieren von Standard-projekteinstellungen, die für alle neuen SSMA-Projekte gelten, können Sie die Einstellungen für jedes Projekt anpassen. Weitere Informationen finden Sie unter [Einstellung Projektoptionen &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md).  
  
Wenn Sie datentypzuordnungen zwischen Quell-und Zieldatenbanken anpassen, können Sie Zuordnungen auf das Projekt, Datenbank oder Objektebene definieren. Weitere Informationen finden Sie unter [Zuordnen von Oracle und SQL Server-Datentypen &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
## <a name="saving-projects"></a>Speichern von Projekten  
Wenn Sie ein Projekt speichern, behält SSMA den projekteinstellungen und optional die Datenbank-Metadaten in die Projektdatei.  
  
**Um ein Projekt zu speichern.**  
  
-   Auf der **Datei** Menü klicken Sie auf **Projekt speichern**.  
  
    Wenn die Schemas im Projekt haben sich verändert oder nicht konvertiert wurden, SSMA aufgefordert, zu laden und Speichern von Metadaten. Laden und Speichern von Metadaten können Sie offline arbeiten. Außerdem können Sie eine vollständige Projektdatei an andere Personen, z. B. der technische Support in Verbindung zu senden. Wenn Sie aufgefordert werden, um Metadaten zu speichern, führen Sie folgende Schritte aus:  
  
    1.  Für jedes Schema, das den Status anzeigt **fehlenden Metadaten**, wählen Sie das Kontrollkästchen neben dem Datenbanknamen.  
  
        Speichern von Metadaten kann einige Minuten dauern. Wenn Sie noch keine Metadaten speichern möchten, Sie keine Kontrollkästchen aktivieren.  
  
    2.  Klicken Sie auf die **speichern** Schaltfläche.  
  
        SSMA analysiert die Oracle-Schemas und speichern Sie die Metadaten in die Projektdatei.  
  
## <a name="opening-projects"></a>Öffnen von Projekten  
Wenn Sie ein Projekt öffnen, wird getrennt von Oracle und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Mit der Sie offline arbeiten. Um Metadaten zu aktualisieren, laden Sie die Datenbankobjekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Um Daten zu migrieren, müssen die Verbindung mit Oracle und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**Öffnen eines Projekts**  
  
1.  Verwenden Sie eine der folgenden Verfahren aus:  
  
    -   Auf der **Datei** Sie im Menü **zuletzt geöffnete Projekte**, und klicken Sie dann auf das Projekt, das Sie öffnen möchten.  
  
    -   Auf der **Datei** klicken Sie im Menü **Projekt öffnen**, suchen Sie die Projektdatei .o2ssproj, wählen Sie die Datei, und klicken Sie dann auf **öffnen**.  
  
2.  Verbindung mit Oracle, auf die **Datei** Menü klicken Sie auf **eine erneute Verbindung mit Oracle**.  
  
3.  Eine Verbindung mit herstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]auf die **Datei** Menü klicken Sie auf **eine erneute Verbindung mit SQL Server**.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt des Migrationsvorgangs besteht darin [Herstellen einer Verbindung mit Oracle-Datenbank (OracleToSQL)](http://msdn.microsoft.com/en-us/e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6).  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Oracle-Datenbanken zu SQLServer &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
[Herstellen einer Verbindung mit Oracle-Datenbank &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)  
[Herstellen einer Verbindung mit SQLServer &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
  
