---
title: Arbeiten mit SSMA-Projekten (DB2ToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-db2
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
ms.assetid: 07abef8a-28e8-4a66-927c-c9a5b8c938ef
caps.latest.revision: "7"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0ed20ad1986bd80694dc452876cdd72aba23af82
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="working-with-ssma-projects-db2tosql"></a>Arbeiten mit SSMA-Projekten (DB2ToSQL)
Zum Migrieren von DB2-Datenbanken zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], erstellen Sie zunächst ein SSMA-Projekt. Das Projekt ist eine Datei mit den folgenden Informationen an:  
  
-   Metadaten zu den DB2-Datenbanken, die Sie zum migrieren möchten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
-   Metadaten für die Zielinstanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] erhalten, die die migrierten Objekte und Daten.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Verbindungsinformationen.  
  
-   Einstellungen für Projektdateien.  
  
Wenn Sie ein Projekt öffnen, wird Sie vom DB2 getrennt und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Mit der Sie offline arbeiten. Informationen zum Wiederherstellen der Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], finden Sie unter [Herstellen einer Verbindung mit SQL Server &#40; DB2eToSQL &#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md).  
  
## <a name="reviewing-default-project-settings"></a>Überprüfen die standardmäßigen Projekteinstellungen  
SSMA enthält verschiedene Einstellungen für das Konvertieren und Laden von Datenbankobjekten, Migrieren von Daten und Synchronisieren von SSMA mit DB2 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Die Standardeinstellungen eignen sich für viele Benutzer. Bevor Sie ein neues SSMA-Projekt erstellen, sollten Sie die Einstellungen überprüfen. Wenn Sie möchten, können Sie die Standardeinstellungen ändern, die für alle neuen Projekte verwendet werden.  
  
**Um standardprojekteinstellungen zu überprüfen.**  
  
1.  Auf der **Tools** Menü klicken Sie auf **Projekt Standardeinstellungen**.  
  
2.  Wählen Sie den Projekttyp in **Migration Zielversion** Dropdownmenü für die Einstellungen sind erforderlich, angezeigt oder geändert werden soll, und klicken Sie dann auf **allgemeine** Registerkarte.  
  
3.  Klicken Sie im linken Bereich auf **Konvertierung**.  
  
4.  Überprüfen Sie im rechten Bereich, und ändern Sie die Einstellungen nach Bedarf. Weitere Informationen zu diesen Einstellungen finden Sie unter [Projekteinstellungen &#40; Konvertierung &#41; &#40; DB2ToSQL &#41; ](../../ssma/db2/project-settings-conversion-db2tosql.md).  
  
5.  Wiederholen Sie die Schritte 1 bis 3 für die Migration, Synchronisierung, Laden von Systemobjekten, GUI und Type Mapping-Seiten.  
  
    -   Informationen zur von migrationseinstellungen finden Sie unter [Projekteinstellungen &#40; Migration &#41; &#40; DB2ToSQL &#41; ](../../ssma/db2/project-settings-migration-db2tosql.md).  
  
    -   Informationen zum Objekt-Systemeinstellungen finden Sie unter [Projekteinstellungen &#40; Laden Systemobjekte &#41; &#40; DB2ToSQL &#41; ](../../ssma/db2/project-settings-loading-system-objects-db2tosql.md).  
  
    -   Weitere Informationen zu Einstellungen für die Synchronisierung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], finden Sie unter [Projekteinstellungen &#40; Synchronisierung &#41; &#40; DB2ToSQL &#41; ](../../ssma/db2/project-settings-synchronization-db2tosql.md).  
  
    -   Informationen zu den GUI-Einstellungen finden Sie unter [Projekteinstellungen &#40; GUI &#41; &#40; DB2ToSQL &#41; ](../../ssma/db2/project-settings-gui-db2tosql.md).  
  
    -   Informationen zu den datentypzuordnung Einstellungen finden Sie unter [Projekteinstellungen &#40; Typzuordnung &#41; &#40; DB2ToSQL &#41; ](../../ssma/db2/project-settings-type-mapping-db2tosql.md).  
  
## <a name="creating-new-projects"></a>Erstellen neuer Projekte  
Zum Migrieren von Daten aus DB2-Datenbanken auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], müssen Sie zunächst ein Projekt erstellen.  
  
**Zum Erstellen eines Projekts**  
  
1.  Auf der **Datei** Menü klicken Sie auf **neues Projekt**.  
  
    Das Dialogfeld **Neues Projekt** wird angezeigt.  
  
2.  In der **Namen** Geben Sie einen Namen für das Projekt.  
  
3.  In der **Speicherort** Feld eingeben oder wählen Sie einen Ordner für das Projekt, und klicken Sie dann auf **OK**.  
  
4.  In der **Migration auf** Dropdown-Liste, wählen Sie die Version des Ziels [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] verwendet für die Migration. Die verfügbaren Optionen sind:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016  
  
    -   Azure SQL-Datenbank  
  
## <a name="customizing-project-settings"></a>Anpassen von Projekteinstellungen  
Zusätzlich zum Definieren von Standard-projekteinstellungen, die für alle neuen SSMA-Projekte gelten, können Sie die Einstellungen für jedes Projekt anpassen. Weitere Informationen finden Sie unter [Einstellung Projektoptionen &#40; OracleToSQL &#41;](../../ssma/oracle/setting-project-options-oracletosql.md) und Verwandte Abschnitte.  
  
Wenn Sie datentypzuordnungen zwischen Quell-und Zieldatenbanken anpassen, können Sie Zuordnungen auf das Projekt, Datenbank oder Objektebene definieren. Weitere Informationen finden Sie unter [DB2 zuordnen und SQL Server-Datentypen &#40; DB2ToSQL &#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md).  
  
## <a name="saving-projects"></a>Speichern von Projekten  
Wenn Sie ein Projekt speichern, behält SSMA den projekteinstellungen und optional die Datenbank-Metadaten in die Projektdatei.  
  
**Um ein Projekt zu speichern.**  
  
-   Auf der **Datei** Menü klicken Sie auf **Projekt speichern**.  
  
    Wenn die Schemas im Projekt haben sich verändert oder nicht konvertiert wurden, SSMA aufgefordert, zu laden und Speichern von Metadaten. Laden und Speichern von Metadaten können Sie offline arbeiten. Außerdem können Sie eine vollständige Projektdatei an andere Personen, z. B. der technische Support in Verbindung zu senden. Wenn Sie aufgefordert werden, um Metadaten zu speichern, führen Sie folgende Schritte aus:  
  
    1.  Für jedes Schema, das den Status anzeigt **fehlenden Metadaten**, wählen Sie das Kontrollkästchen neben dem Datenbanknamen.  
  
        Speichern von Metadaten kann einige Minuten dauern. Wenn Sie noch keine Metadaten speichern möchten, Sie keine Kontrollkästchen aktivieren.  
  
    2.  Klicken Sie auf die **speichern** Schaltfläche.  
  
        SSMA analysiert die DB2-Schemas und speichern Sie die Metadaten in die Projektdatei.  
  
## <a name="opening-projects"></a>Öffnen von Projekten  
Wenn Sie ein Projekt öffnen, wird getrennt von DB2 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Mit der Sie offline arbeiten. Um Metadaten zu aktualisieren, laden Sie die Datenbankobjekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Um Daten zu migrieren, müssen die Verbindung mit DB2 und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**Öffnen eines Projekts**  
  
1.  Verwenden Sie eine der folgenden Verfahren aus:  
  
    -   Auf der **Datei** Sie im Menü **zuletzt geöffnete Projekte**, und klicken Sie dann auf das Projekt, das Sie öffnen möchten.  
  
    -   Auf der **Datei** klicken Sie im Menü **Projekt öffnen**, suchen Sie die Projektdatei .o2ssproj, wählen Sie die Datei, und klicken Sie dann auf **öffnen**.  
  
2.  Verbindung mit DB2, auf die **Datei** Menü klicken Sie auf **eine erneute Verbindung mit DB2**.  
  
3.  Eine Verbindung mit herstellen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]auf die **Datei** Menü klicken Sie auf **eine erneute Verbindung mit SQL Server**.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt des Migrationsvorgangs besteht darin [Herstellen einer Verbindung mit DB2-Datenbank](http://msdn.microsoft.com/en-us/5eb5801d-f0c3-4127-97c0-0b1ef49f4844).  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von DB2-Datenbanken zu SQLServer &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
[Herstellen einer Verbindung mit DB2-Datenbank &#40; DB2ToSQL &#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)  
[Herstellen einer Verbindung mit SQLServer &#40; DB2eToSQL &#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)  
  
