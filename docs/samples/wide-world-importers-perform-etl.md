---
title: WideWorldImportersDW - ETL-Workflows | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dae49099f938baa071149072b277411b99e63dc5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="wideworldimportersdw-etl-workflow"></a>WideWorldImportersDW ETL-Workflows
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Die ETL-Pakets WWI_Integration dient zum Migrieren von Daten aus der Datenbank "wideworldimporters" in der Datenbank WideWorldImportersDW sich mit den Daten. Das Paket wird in regelmäßigen Abständen ausgeführt (die am häufigsten täglich).

## <a name="overview"></a>Übersicht

Der Entwurf, der das Paket verwendet SQL Server Integration Services (SSIS) zum orchestrieren von Massenvorgängen T-SQL (und nicht als separate Transformationen in SSIS) hohe Leistung sicherzustellen.

Dimensionen werden zuerst geladen, gefolgt von Faktentabellen. Das Paket kann zu einem beliebigen Zeitpunkt nach einem Fehler erneut ausgeführt werden.

Der Workflow wird wie folgt:

 ![WideWorldImporters ETL-Workflows](media/wide-world-importers/wideworldimporters-etl-workflow.png)

Er beginnt mit einem funktioniert Task "Ausdruck" Umstellungsjahr für Angaben mit geeigneten Zeitpunkt. Dieses Mal wird die aktuelle Uhrzeit kleiner einigen Minuten. (Dies ist robuster als das Anfordern von Daten direkt auf die aktuelle Zeit). Es schneidet dann alle Millisekunden ab dem Zeitpunkt ab.

Die hauptverarbeitung, die durch Auffüllen der Tabelle Date-Dimension wird gestartet. Dadurch wird sichergestellt, dass alle Datumsangaben für das laufende Jahr in der Tabelle aufgefüllt wurden.

Anschließend lädt eine Reihe von Datenflusstasks jeder Dimension, und klicken Sie dann auf jede Faktentabelle.

## <a name="prerequisites"></a>Erforderliche Komponenten

- SQLServer 2016 (oder höher) mit den Datenbanken "wideworldimporters" und WideWorldImportersDW. Diese können auf der gleichen oder unterschiedliche Instanzen von SQL Server sein.
- SQL Server Management Studio (SSMS)
- SQL Server 2016 Integration Services (SSIS).
  - Stellen Sie sicher, dass Sie ein SSIS-Katalog erstellt haben. Falls nicht, mit der rechten Maustaste **Integration Services** im SSMS-Objekt-Explorer, und wählen Sie **Add Catalog**. Führen Sie die Standardeinstellungen aus. Fordert Sie zum Aktivieren von Sqlclr und ein Kennwort angeben.


## <a name="download"></a>Herunterladen

Die neueste Version des Beispiels:

[wide-world-importers-release](http://go.microsoft.com/fwlink/?LinkID=800630)

Laden Sie die SSIS-Paket-Datei **tägliche ETL.ispac**.

Quellcode und erstellen die Beispieldatenbank ist aus folgendem Ort verfügbar.

[Wide World-Importers befinden](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-integration-etl)

## <a name="install"></a>Install

1. Bereitstellen des SSIS-Pakets.
   - Öffnen Sie das Paket "Tägliche ETL.ispac" aus Windows Explorer. Hierdurch wird die Integration Services Deployment Wizard.
   - Führen Sie unter "Quelle auswählen" die Standardeinstellung Projektbereitstellung, mit dem Pfad verweist auf das Paket "Tägliche ETL.ispac" ein.
   - Geben Sie unter "Ziel auswählen" den Namen des Servers, der den SSIS-Katalog hostet.
   - Wählen Sie einen Pfad im SSIS-Katalog, z. B. in einem neuen Ordner "WideWorldImporters".
   - Dann auf bereitstellen, um den Assistenten zu beenden.

2. Erstellen Sie einen SQL Server-Agent-Auftrag für ETL-Prozess.
   - In SSMS-Auftrag mit der rechten Maustaste "SQL Server-Agent" und wählen Sie Neu >.
   - Wählen Sie einen Namen, z. B. "WideWorldImporters ETL".
   - Fügen Sie einen Auftragsschritt vom Typ "SQL Server Integration Services-Paket" hinzu.
   - Wählen Sie den Server mit dem SSIS-Katalog, und wählen Sie das Paket "Tägliche ETL".
   - Unter Configuration -> Verbindungs-Manager stellen Sie sicher, die Verbindungen mit den Quell- und Zielservern richtig konfiguriert sind. Der Standardwert ist eine Verbindung mit der lokalen Instanz herstellen.
   - Klicken Sie auf OK, um den Auftrag zu erstellen.

3. Führen Sie aus, oder planen Sie des Auftrags.
