---
title: Installation und Konfiguration | Microsoft Docs
ms.prod: world-wide-importers
ms.prod_service: sql-non-specified
ms.service: samples
ms.component: 
ms.technology: samples
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d07ffb9a-ac4f-4295-9aeb-ecfb97600134
caps.latest.revision: "3"
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.workload: On Demand
ms.openlocfilehash: 64149cc79a4c2e4c19c2f93e02c97fcc42865712
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="wideworldimportersdw-installation-and-configuration"></a>WideWorldImportersDW Installation und Konfiguration
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Anweisungen zu Installation und Konfiguration für die WideWorldImportersDW-Datenbank.

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) (oder höher) oder [Azure SQL-Datenbank](https://azure.microsoft.com/services/sql-database/). Um die vollständige Version des Beispiels zu verwenden, verwenden Sie SQL Server-Evaluierung, Developer, Enterprise Edition.
- [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md). Für die besten Ergebnisse verwenden Sie das Release vom Juni 2016 oder höher.

## <a name="download"></a>Herunterladen

Die neueste Version des Beispiels:

[Wide World Importers-Version](http://go.microsoft.com/fwlink/?LinkID=800630)

Herunterladen Sie das Beispiel WideWorldImportersDW Datenbank Backup/bacpac-Datei, die entspricht auf Ihre Edition von SQL Server oder Azure SQL-Datenbank.

Quellcode und erstellen die Beispieldatenbank ist aus folgendem Ort verfügbar. Beachten Sie, dass das datenpopulation auf ETL aus der OLTP-Datenbank ("wideworldimporters"):

[Wide World Importers-Quelle](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-dw-database-scripts)

## <a name="install"></a>Install


### <a name="sql-server"></a>SQL Server

Um eine Sicherung einer SQL Server-Instanz wiederherzustellen, können Sie Management Studio verwenden.

1. Öffnen Sie SQL Server Management Studio, und Verbinden mit SQL Server-Zielinstanz.
2. Mit der rechten Maustaste auf die **Datenbanken** Knoten, und wählen **Restore Database**.
3. Wählen Sie **Gerät** , und klicken Sie auf die Schaltfläche mit den **...**
4. Klicken Sie im Dialogfeld **Sicherungsmedien auswählen**, klicken Sie auf **hinzufügen**, navigieren Sie zu der Sicherung in das Dateisystem des Servers, und wählen Sie die Sicherung. Klicken Sie auf **OK**.
5. Wenn erforderlich, ändern Sie den Zielspeicherort für die Daten und Protokolldateien, in der **Dateien** Bereich. Beachten Sie, dass es die bewährte Methode zum Hinzufügen von Daten und Protokolldateien auf verschiedenen Laufwerken handelt.
6. Klicken Sie auf **OK**. Hierdurch wird die Wiederherstellung der Datenbank ausgelöst. Nachdem der Vorgang abgeschlossen ist, müssen Sie die Datenbank "wideworldimporters" auf SQL Server-Instanz installiert.

### <a name="azure-sql-database"></a>Azure SQL-Datenbank

Um eine bacpac-Datei in eine neue SQL-Datenbank importieren, können Sie Management Studio verwenden.

1. (optional) Wenn Sie eine SQL Server in Azure noch nicht vorhanden sind, navigieren Sie zu der [Azure-Portal](https://portal.azure.com/) , und erstellen Sie eine neue SQL-Datenbank. Der Datenbank erstellen, erstellen Sie einen Server. Notieren Sie sich die Server.
   - Finden Sie unter [dieses Lernprogramms](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) zum Erstellen einer Datenbank in Minuten
2. Öffnen Sie SQL Server Management Studio, und verbinden Sie Ihre Server in Azure.
3. Mit der rechten Maustaste auf die **Datenbanken** Knoten, und wählen **Data-Tier-Anwendung importieren**.
4. In der **Importeinstellungen** wählen **vom lokalen Datenträger importieren** , und wählen Sie die bacpac-Datei der Beispieldatenbank aus dem Dateisystem.
5. Klicken Sie unter **Datenbankeinstellungen** ändern Sie den Datenbanknamen an *WideWorldImportersDW* , und wählen Sie die Ziel-Edition und der Dienst verwendet.
6. Klicken Sie auf **Weiter** und **Fertig stellen** um Bereitstellung starten. Es dauert einige Minuten. Wenn Sie einen Zielpunkt niedriger ist als S2 angeben kann es länger dauern.

## <a name="configuration"></a>Konfiguration

[Gilt für SQL Server 2016 (und höher) Enterprise/Developer/Evaluation-Edition]

Die Beispieldatenbank kann Nutzen des PolyBase zur Abfrage von Dateien in Hadoop oder Azure Blob-Speicher. Jedoch diese Funktion wird nicht standardmäßig installiert, mit SQL Server - müssen Sie es während des Setups von SQL Server auswählen. Aus diesem Grund ist ein Schritt nach der Installation erforderlich.

1. Herstellen einer Verbindung mit der Datenbank WideWorldImportersDW und ein neues Abfragefenster öffnen, in SQL Server Management Studio.
2. Führen Sie den folgenden T-SQL-Befehl, um die Verwendung von PolyBase in der Datenbank zu aktivieren:

   Führen Sie [Anwendung]. [Configuration_ApplyPolyBase]
