---
title: Installation und Konfiguration | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- samples
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6dd1f09b-dcff-4627-899a-eca5162d9e5b
caps.latest.revision: 4
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4102284612e0838fb876708b959266994a0f2b96
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="installation-and-configuration"></a>Installation und Konfiguration
Wide World Importers OLTP-Datenbank Installations- und konfigurationsanleitung für.

## <a name="prerequisites"></a>Erforderliche Komponenten

- [SQL Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) (oder höher) oder [Azure SQL-Datenbank](https://azure.microsoft.com/services/sql-database/). Verwenden Sie für die vollständige Version des Beispiels SQL Server-Evaluierung, Developer, Enterprise Edition ein.
- [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx). Für die besten Ergebnisse verwenden Sie das Release vom Juni 2016 oder höher.

## <a name="download"></a>Herunterladen

Die neueste Version des Beispiels:

[Wide World Importers-Version](http://go.microsoft.com/fwlink/?LinkID=800630)

Herunterladen Sie das Beispiel "wideworldimporters" Datenbank Backup/bacpac-Datei, die entspricht auf Ihre Edition von SQL Server oder Azure SQL-Datenbank.

Quellcode und erstellen die Beispieldatenbank ist aus folgendem Ort verfügbar. Beachten Sie, dass beim erneuten Erstellen des Beispiels zu geringfügigen Unterschieden in den Daten, führt da ein Zufallsfaktor in die datengenerierung vorhanden ist:

[Wide World-Importers befinden](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-database-scripts)

## <a name="install"></a>Install


### <a name="sql-server"></a>SQL Server

Um eine Sicherung einer SQL Server-Instanz wiederherzustellen, können Sie Management Studio verwenden.

1. Öffnen Sie SQL Server Management Studio, und Verbinden mit SQL Server-Zielinstanz.
2. Mit der rechten Maustaste auf die **Datenbanken** Knoten, und wählen **Restore Database**.
3. Wählen Sie **Gerät** , und klicken Sie auf die Schaltfläche mit den **...**
4. Klicken Sie im Dialogfeld **Sicherungsmedien auswählen**, klicken Sie auf **hinzufügen**, navigieren Sie zu der Sicherung in das Dateisystem des Servers, und wählen Sie die Sicherung. Klicken Sie auf **OK**.
5. Wenn erforderlich, ändern Sie den Zielspeicherort für die Daten und Protokolldateien, in der **Dateien** Bereich. Beachten Sie, dass es die bewährte Methode zum Hinzufügen von Daten und Protokolldateien auf verschiedenen Laufwerken handelt.
6. Klicken Sie auf **OK**. Hierdurch wird die Wiederherstellung der Datenbank ausgelöst. Nachdem der Vorgang abgeschlossen ist, müssen Sie die Datenbank "wideworldimporters" auf SQL Server-Instanz installiert.

### <a name="azure-sql-database"></a>Azure SQL Database

Um eine bacpac-Datei in eine neue SQL-Datenbank importieren, können Sie Management Studio verwenden.

1. (optional) Wenn Sie eine SQL Server in Azure noch nicht vorhanden sind, navigieren Sie zu der [Azure-Portal](https://portal.azure.com/) , und erstellen Sie eine neue SQL-Datenbank. Der Datenbank erstellen, erstellen Sie einen Server. Notieren Sie sich die Server.
   - Finden Sie unter [dieses Lernprogramms](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) zum Erstellen einer Datenbank in Minuten
2. Öffnen Sie SQL Server Management Studio, und verbinden Sie Ihre Server in Azure.
3. Mit der rechten Maustaste auf die **Datenbanken** Knoten, und wählen **Data-Tier-Anwendung importieren**.
4. In der **Importeinstellungen** wählen **vom lokalen Datenträger importieren** , und wählen Sie die bacpac-Datei der Beispieldatenbank aus dem Dateisystem.
5. Klicken Sie unter **Datenbankeinstellungen** ändern Sie den Datenbanknamen an *"wideworldimporters"* , und wählen Sie die Ziel-Edition und der Dienst verwendet.
6. Klicken Sie auf **Weiter** und **Fertig stellen** um Bereitstellung starten. Es wird ein paar Minuten auf eine P1. Wenn Sie eine niedrigere Preise Ebene gewünscht wird, es wird empfohlen, in eine neue P1-Datenbank importieren, und klicken Sie dann den Tarif ändern, auf die gewünschte Zugriffsstufe.

## <a name="configuration"></a>Konfiguration

### <a name="full-text-indexing"></a>Volltextindizierung

Die Beispieldatenbank kann Stellen der Volltextindizierung verwenden. Jedoch diese Funktion wird nicht standardmäßig installiert, mit SQL Server - müssen Sie es während des Setups von SQL Server auswählen (in Azure SQL-Datenbank standardmäßig aktiviert). Aus diesem Grund ist ein Schritt nach der Installation erforderlich.

1. Herstellen einer Verbindung mit der Datenbank "wideworldimporters", und öffnen Sie ein neues Abfragefenster, in SQL Server Management Studio.
2. Führen Sie den folgenden T-SQL-Befehl, um die Verwendung der Volltextindizierung in der Datenbank zu aktivieren:`EXECUTE Application.Configuration_ApplyFullTextIndexing`


### <a name="sql-server-audit"></a>SQL Server Audit

Gilt für: SQLServer

In SQL Server-Überwachung zu aktivieren, wird die Serverkonfiguration benötigen. Führen Sie die folgende Anweisung in der Datenbank, um SQL Server-Überwachung für das Beispiel "wideworldimporters" zu aktivieren:

    EXECUTE [Application].[Configuration_ApplyAuditing]

In Azure SQL-Datenbank, Überwachung konfiguriert ist, über die [Azure-Portal](https://portal.azure.com/).

### <a name="row-level-security"></a>Sicherheit auf Zeilenebene

Gilt für: Azure SQL-Datenbank

Sicherheit auf Zeilenebene ist nicht in der bacpac-Datei-Download von "wideworldimporters" standardmäßig aktiviert. Um Sicherheit auf Zeilenebene in der Datenbank zu aktivieren, führen Sie die folgende gespeicherte Prozedur aus:

    EXECUTE [Application].[Configuration_ApplyAuditing]


