---
title: "Migrieren von Schemas für den Oracle HR zu SQLServer on Linux | Microsoft Docs"
description: Konvertieren von Oracle-Beispielschema in SQL Server on Linux
author: edmacauley
ms.author: edmacauley
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-oracle
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: 32ecce66caea01798b3c189108a5e196b04999d0
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="migrate-an-oracle-schema-to-sql-server-2017-on-linux-with-the-sql-server-migration-assistant"></a>Migrieren von einer Oracle-Schema zu SQL Server-2017 unter Linux mit SQL Server Migration Assistant

Dieses Lernprogramm verwendet SQL Server Migration Assistant (SSMA) für Oracle unter Windows verwendet, um die Oracle-Beispiel konvertieren **HR** Schema [2017 von SQL Server on Linux](../../linux/sql-server-linux-overview.md).

> [!div class="checklist"]
> * Herunterladen Sie und installieren Sie SSMA unter Windows
> * Erstellen Sie eine SSMA-Projekt, um die Migration zu verwalten
> * Herstellen einer Verbindung mit Oracle
> * Führen Sie einen Bericht
> * Konvertieren Sie das HR-Beispielschema
> * Migrieren von Daten

## <a name="prerequisites"></a>Erforderliche Komponenten

- Eine Instanz von Oracle 12c (12.2.0.1.0) mit der **HR** Schema installiert
- Eine funktionierende Instanz von SQL Server on Linux

> [!NOTE]
> Die gleichen Schritte können verwendet werden, um SQL-Zielserver unter Windows, jedoch müssen Sie Windows im Auswählen der **Migrieren zu** Projekt festlegen.

## <a name="download-and-install-ssma-for-oracle"></a>Herunterladen Sie und installieren Sie SSMA für Oracle

Es sind mehrere Editionen von SQL Server Migration Assistant verfügbar, abhängig von der Quelldatenbank.  Herunterladen der aktuellen Version der [SQL Server Migration Assistant für Oracle](http://aka.ms/ssmafororacle) und ihn mit den Anweisungen auf der Downloadseite installieren.

> [!NOTE]
> Zu diesem Zeitpunkt die **SSMA für die Oracle-Erweiterung Pack** wird unter Linux nicht unterstützt, aber es ist nicht für dieses Lernprogramm erforderlich.

## <a name="create-and-set-up-project"></a>Erstellen und Setup-Projekt

Verwenden Sie die folgenden Schritte aus, um ein neues SSMA-Projekt zu erstellen:

1. SSMA für die Oracle öffnen, und wählen Sie **neues Projekt** aus der **Datei** Menü.

1. Benennen Sie dem Projekt.

1. Wählen Sie "SQLServer 2017 (Linux) – Vorschau" in der **Migrieren zu** Feld.

SSMA für Oracle verwendet die Oracle-Beispielschemas nicht standardmäßig. Um das HR-Schema zu aktivieren, verwenden Sie die folgenden Schritte aus:

1. Wählen Sie in der SSMA das **Tools** Menü.

1. Wählen Sie **Projekt Standardeinstellungen**, und wählen Sie dann **Systemobjekte laden**.

1. Stellen Sie sicher, dass **HR** aktiviert ist, und wählen Sie **OK**.

## <a name="connect-to-oracle"></a>Herstellen einer Verbindung mit Oracle

Anschließend stellen Sie eine Verbindung SSMA zu Oracle.

1. Klicken Sie auf der Symbolleiste auf **Connect to Oracle**.

1. Geben Sie den Servernamen, Port, Oracle SID, Benutzername und Kennwort.

   ![Herstellen einer Verbindung mit Oracle](./media/sql-server-linux-convert-from-oracle/ConnectToOracle.png)

1. Klicken Sie dann auf **verbinden**. SSMA für die Oracle eine Verbindung mit Ihrer Datenbank her und liest die Metadaten, in einigen Minuten erneut.

## <a name="create-a-report"></a>Erstellen eines Berichts

Verwenden Sie die folgenden Schritte aus, um einen Bericht zu generieren.

1. In der **Oracle-Metadaten-Explorer**, erweitern Sie den Knoten des Servers.

1. Erweitern Sie **Schemas**, mit der rechten Maustaste **HR**, und wählen Sie **Bericht erstellen**.

   ![Oracle-Metadaten-Explorer erstellen Bericht](./media/sql-server-linux-convert-from-oracle/CreateReport.png)

1. Berichte, die alle Warnungen und Fehler im Zusammenhang mit der Konvertierung werden aufgelistet, wird ein neues Browserfenster geöffnet.

   > [!NOTE]
   > Sie müssen nicht mit der Liste für dieses Lernprogramm keine Wirkung. Wenn Sie diese Schritte für Oracle-Datenbank ausführen, lesen Sie den Bericht, für Ihre Datenbank wichtig Konvertierungsprobleme zu behandeln.

   ![Beispielbericht für die Migration](./media/sql-server-linux-convert-from-oracle/SSMAReport.png)

## <a name="connect-to-sql-server"></a>Verbindung mit SQL Server herstellen

Wählen Sie anschließend **Herstellen einer Verbindung mit SQL Server** und geben Sie die entsprechenden Verbindungsinformationen.  Wenn Sie einen Datenbanknamen verwenden, der noch nicht vorhanden ist, SSMA für Oracle wird für Sie erstellt wird.

![Verbindung mit SQL Server herstellen](./media/sql-server-linux-convert-from-oracle/ConnectToSQLServer.png)

## <a name="convert-schema"></a>Schema konvertieren

Mit der rechten Maustaste auf **HR** in **Oracle-Metadaten-Explorer**, und wählen Sie Schema konvertieren.

![Schema konvertieren](./media/sql-server-linux-convert-from-oracle/ConvertSchema.png)

## <a name="synchronize-database"></a>Synchronisieren der Datenbank

Als Nächstes Synchronisieren der Datenbank.

1. Nachdem die Konvertierung abgeschlossen ist, verwenden Sie die **Metadaten-Explorer von SQL Server** fahren Sie mit der Datenbank, die Sie im vorherigen Schritt erstellt.

1. Mit der rechten Maustaste auf die Datenbank aus, wählen **mit Datenbank synchronisieren**, und klicken Sie dann auf OK.

   ![Synchronisieren Sie mit der Datenbank](./media/sql-server-linux-convert-from-oracle/SynchronizeWithDatabase.png)

## <a name="migrate-data"></a>Migrieren von Daten

Der letzte Schritt besteht darin Ihre Daten migrieren.

1. In der **Oracle-Metadaten-Explorer**, mit der rechten Maustaste auf **HR**, und wählen Sie **Migrieren von Daten**.

1. Der Schritt beim Data Migration erfordert, dass Sie Ihre Anmeldeinformationen für Oracle und SQL Server erneut ein.

1. Überprüfen Sie nach Abschluss der Datenbericht für die Migration, die ähnlich wie im folgenden Bildschirmfoto aussehen sollte:

   ![Migrationsbericht Daten](./media/sql-server-linux-convert-from-oracle/DataMigrationReport.png)

## <a name="next-steps"></a>Nächste Schritte

Für eine komplexere Orcale Schema würde der Konvertierungsprozess mehr Zeit, testen und vor möglichen Änderungen an Clientanwendungen umfassen. Der Zweck dieses Lernprogramms ist zu zeigen, wie Sie SSMA für Oracle als Teil des gesamten Migrationsprozesses verwenden können.

In diesem Lernprogramm haben Sie gelernt, wie:
> [!div class="checklist"]
> * Installieren Sie SSMA unter Windows
> * Erstellen Sie ein neues SSMA-Projekt
> * Bewerten Sie und führen Sie eine Migration von Oracle

Untersuchen Sie anschließend andere Möglichkeiten zum Verwenden des SSMA:

> [!div class="nextstepaction"]
>[SQL Server Migration Assistant-Dokumentation](../sql-server-migration-assistant.md)
