---
title: Speichern und Abrufen von Dateien auf Dateifreigaben (lokal und in Azure) | Microsoft-Dokumentation
description: In diesem Artikel wird beschrieben, wie Sie das Dateisystem und Dateifreigaben sowohl lokal als auch in Azure mit SSIS verwenden.
ms.date: 11/27/2017
ms.topic: article
ms.prod: sql
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b9fb260101c1f814c85360d3fe5998b6e9234101
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="store-and-retrieve-files-on-file-shares-on-premises-and-in-azure-with-ssis"></a>Speichern und Abrufen von Dateien auf lokalen Dateifreigaben und Dateifreigaben in Azure mit SSIS
In diesem Artikel wird beschrieben, wie Sie SSIS-Pakete (SQL Server Integration Services) aktualisieren, wenn Sie Pakete, die lokale Dateisysteme verwenden, per Lift & Shift zu SSIS in Azure migrieren.

> [!IMPORTANT]
> Die SSIS-Katalogdatenbank (SSISDB) unterstützt derzeit nur einen Satz von Anmeldeinformationen. Aus diesem Grund können mit der Azure SSIS Integration Runtime (IR) keine anderen Anmeldeinformationen zur Verbindung mit mehreren lokalen Dateifreigaben und Azure Files-Dateifreigaben verwendet werden.

## <a name="store-temporary-files"></a>Speichern von temporären Dateien
Wenn Sie temporäre Dateien während einer einzelnen Paketausführung speichern und verarbeiten müssen, können Pakete das aktuelle Arbeitsverzeichnis (`.`) oder den temporären Ordner (`%TEMP%`) Ihrer Azure SSIS Integration Runtime-Knoten verwenden.

## <a name="store-files-across-multiple-package-executions"></a>Speichern von Dateien für mehrere Paketausführungen
Wenn Sie permanente Dateien für mehrere Paketausführungen langfristig speichern und verarbeiten müssen, können Sie lokale Dateifreigaben oder Azure Files verwenden.

### <a name="use-on-premises-file-shares"></a>Verwenden von lokalen Dateifreigaben
Wenn Sie Pakete, die lokale Dateisysteme verwenden, zu SSIS in Azure migrieren und weiterhin **lokale Dateifreigaben** verwenden möchten, führen Sie die folgenden Schritte durch:
1.  Übertragen Sie die Dateien von den lokalen Dateisystemen auf die lokalen Dateifreigaben.
2.  Verknüpfen Sie die lokalen Dateifreigaben mit einem virtuellen Azure-Netzwerk.
3.  Verknüpfen Sie Ihre Azure SSIS IR mit demselben virtuellen Netzwerk. Weitere Informationen finden Sie unter [Verknüpfen einer Azure SSIS Integration Runtime mit einem virtuellen Netzwerk](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network).
4.  Verbinden Sie Ihre Azure SSIS IR mit den lokalen Dateifreigaben innerhalb des desselben virtuellen Netzwerks, indem Sie Anmeldeinformationen einrichten, die mit der Windows-Authentifizierung verwendet werden. Weitere Informationen finden Sie unter [Connect to on-premises data sources and Azure file shares with Windows Authentication (Herstellen einer Verbindung mit lokalen Datenquellen und Azure-Dateifreigaben mit der Windows-Authentifizierung)](ssis-azure-connect-with-windows-auth.md).
5.  Ändern Sie lokale Dateipfade in Ihren Paketen in UNC-Pfade, die auf lokale Dateifreigaben verweisen. Ändern Sie z.B. den Pfad `C:\abc.txt` in `\\<on-prem-server-name>\<share-name>\abc.txt`.

### <a name="use-azure-file-shares"></a>Verwenden von Azure-Dateifreigaben
Wenn Sie Pakete, die lokale Dateisysteme verwenden, zu SSIS in Azure migrieren und **Azure Files**verwenden möchten, führen Sie die folgenden Schritte durch:
1.  Übertragen Sie die Dateien von den lokalen Dateisystemen zu Azure Files. Weitere Informationen finden Sie unter [Azure Files](https://azure.microsoft.com/services/storage/files/).
2.  Verbinden Sie Azure SSIS IR mit Azure Files, indem Sie Anmeldeinformationen einrichten, die mit der Windows-Authentifizierung verwendet werden. Weitere Informationen finden Sie unter [Connect to on-premises data sources and Azure file shares with Windows Authentication (Herstellen einer Verbindung mit lokalen Datenquellen und Azure-Dateifreigaben mit der Windows-Authentifizierung)](ssis-azure-connect-with-windows-auth.md).
3.  Ändern Sie lokale Dateipfade in Ihren Paketen in UNC-Pfade, die auf Azure Files verweisen. Ändern Sie z.B. den Pfad `C:\abc.txt` in `\\<storage-account-name>.file.core.windows.net\<share-name>\abc.txt`.
