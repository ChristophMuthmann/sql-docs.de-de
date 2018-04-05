---
title: Migrieren von lokalen SQLServer (Data Migration Assistant) | Microsoft Docs
ms.custom: ''
ms.date: 09/01/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: article
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, on-premises SQL Server
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 666236842318cfba0cee38f71ac694eef86cdbf5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="migrate-on-premises-sql-server-using-data-migration-assistant"></a>Migrieren von lokalen SQL Server mit dem Daten Migrations-Assistenten

Dieser Artikel enthält schrittweise Anleitungen zum Migrieren von SQLServer Data-Migrations-Assistenten verwenden.

Daten-Migrations-Assistent bietet nahtlose Bewertungen und Migrationen zu modernen lokalen SQL Server- und SQL Azure-VM-Daten-Plattformen.  

Führen Sie die folgenden Aufgaben aus, um die Migration auszuführen.

- [Erstellen eines neuen Migrationsprojekts](#create-a-new-migration-project)
- [Geben Sie den Quell- und Zielservern](#specify-source-and-target)
- [Hinzufügen von Datenbanken](#add-databases)
- [Wählen Sie Anmeldenamen](#select-logins)

## <a name="create-a-new-migration-project"></a>Erstellen eines neuen Migrationsprojekts

1. Klicken Sie auf **neu** (+) auf den linken Bereich, und wählen die **Migration** Projekttyp.

1. Legen Sie auf den Quell- und Ziel-Servertyp **SQL Server** , wenn Sie ein Upgrade einer lokalen SQL Server zum Ausführen einer modernen einer lokalen SQL Server.

1. Klicken Sie auf **Erstellen**.

   ![Erstellen des Migrationsprojekts](../dma/media/NewCreate.png)

## <a name="specify-the-source-and-target"></a>Geben Sie den Quell- und Zielservern

1. Für die Quelle, geben Sie den Namen der SQL Server-Instanz in der **Servernamen** -Feld in der **Datenquelle Serverdetails** Abschnitt. 

1. Wählen Sie die **Authentifizierungstyp** von der SQL Server-Quellinstanz unterstützt.

1. Für das Ziel, geben Sie den Namen der SQL Server-Instanz in der **Servernamen** -Feld in der **Server Zieldetails** Abschnitt. 

1. Wählen Sie die **Authentifizierungstyp** von SQL Server-Zielinstanz unterstützt.

1. Es wird empfohlen, dass Sie dazu die Verbindung verschlüsseln **Verschlüsselungsverbindung** in der **Verbindungseigenschaften** Abschnitt.

1. Klicken Sie auf **Weiter**.

   ![Geben Sie die Seite "Quelle und Ziel"](../dma/media/SourceTarget.png)

## <a name="add-databases"></a>Hinzufügen von Datenbanken

1. Wählen Sie die jeweiligen Datenbanken, die Sie migrieren, indem Sie Ihre Auswahl nur diese Datenbanken im linken Bereich des möchten die **Datenbanken hinzufügen** Seite.

   Standardmäßig werden alle Benutzerdatenbanken auf der SQL Server-Quellinstanz für die Migration ausgewählt.

1. Verwenden Sie die migrationseinstellungen auf der rechten Seite der Seite, um die Migrationsoptionen festgelegt, die auf die Datenbanken angewendet werden, wie folgt.

   > [!NOTE]
   > Sie können alle Datenbanken, die Sie migrieren, indem Sie den Server im linken Bereich auswählen, die migrationseinstellungen zuweisen. Sie können auch eine einzelne Datenbank mit spezifischen Einstellungen konfigurieren, indem Sie die Datenbank im linken Bereich auswählen.


 1. Geben Sie die **verfügbaren Speicherort von Quell- und Ziel-SQL-Server für den Sicherungsvorgang gemeinsam**. Stellen Sie sicher, dass das Dienstkonto, das die Quelle mit SQL Server-Instanz verfügt über Schreibberechtigungen auf den freigegebenen Speicherort, und das Ziel-Dienstkonto verfügt über für den freigegebenen Speicherort Leserechte.

 1. Geben Sie den Speicherort zum Wiederherstellen der Daten und transaktionale Protokolldateien auf dem Zielserver.

    ![Hinzufügen von Datenbanken](../dma/media/AddDatabases.png)

1. Geben Sie einen freigegebenen Speicherort an, dass die Quell- und SQL Server-Instanzen können, in zugreifen der **freigeben Standortoptionen** Feld.

1. Wenn Sie einen freigegebenen Speicherort bereitstellen, können aber, sowohl die Quell-als auch SQL Server auf, wählen Sie **kopieren Sie die Sicherungskopien der Datenbank an einen anderen Speicherort, die der Zielserver kann gelesen und Wiederherstellen von**. Geben Sie dann einen Wert für die **Speicherort für Sicherungen für Wiederherstellungsoption** Feld. 

   Stellen Sie sicher, dass das Benutzerkonto ausgeführt Data Migration Assistant Berechtigungen, um den Sicherungsspeicherort gelesen hat, und über Schreibberechtigungen für den Speicherort, von dem der Zielserver wird wiederhergestellt.

   ![Option zum Kopieren von datenbanksicherungen in anderen Speicherort](../dma/media/CopyDatabaseDifferentLocation.png)

1. Klicken Sie auf **Weiter**.

Daten-Migrations-Assistent führt Überprüfungen auf den Sicherungsordner Daten- und Protokolldateien Speicherorte-Datei. Wenn Fehler zurückgegeben wird, korrigieren Sie die Optionen und klicken Sie auf **Weiter**.

## <a name="select-logins"></a>Wählen Sie Anmeldenamen

1. Wählen Sie die spezifische Anmeldungen für die Migration.

   > [!IMPORTANT]
   > Stellen Sie sicher, dass die Anmeldungen aktivieren, die einen oder mehrere Benutzer in den Datenbanken, die für die Migration ausgewählt zugeordnet sind.   

   Standardmäßig werden alle SQL Server und Windows-Anmeldungen, die für die Migration qualifizieren für die Migration ausgewählt.

1. Klicken Sie auf **Starten der Migration**.

   ![Wählen Sie Anmeldenamen und das Starten der migration](../dma/media/SelectLogins.png)

## <a name="view-results"></a>Anzeigen der Ergebnisse

Sie können den Migrationsfortschritt überwachen, auf die **Ergebnisse anzeigen** Seite.

![Seite "Ergebnisse" anzeigen](../dma/media/ViewResults.png)

## <a name="export-migration-results"></a>Exportieren Sie die Ergebnisse der migration

1. Klicken Sie auf **Exportbericht** am unteren Rand der **Ergebnisse anzeigen** Seite, um die Ergebnisse der Migration in eine CSV-Datei zu speichern.

1. Überprüfen Sie die gespeicherte Datei ausführliche Informationen über die Migration für die Anmeldung, und überprüfen Sie dann die Änderungen.

## <a name="see-also"></a>Siehe auch

[Daten-Migrations-Assistenten (DMA)](../dma/dma-overview.md)

[Assistent für die Migration von Daten: Konfigurationseinstellungen](../dma/dma-configurationsettings.md)

[Assistent für die Migration von Daten: Bewährte Methoden](../dma/dma-bestpractices.md)
