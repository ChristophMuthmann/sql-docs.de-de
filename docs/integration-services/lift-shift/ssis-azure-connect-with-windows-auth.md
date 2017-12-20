---
title: Herstellen einer Verbindung mit lokalen Datenquellen und Azure-Dateifreigaben mit der Windows-Authentifizierung | Microsoft-Dokumentation
ms.date: 11/27/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c0f5e1e2319e58e9013b1f67e8a81efa9a07d556
ms.sourcegitcommit: 6bbecec786b0900db86203a04afef490c8d7bfab
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="connect-to-on-premises-data-sources-and-azure-file-shares-with-windows-authentication"></a>Herstellen einer Verbindung mit lokalen Datenquellen und Azure-Dateifreigaben mit der Windows-Authentifizierung
In diesem Artikel wird beschrieben, wie Sie den SSIS-Katalog auf Azure SQL-Datenbank so konfigurieren, dass er Pakete ausführt, die die Windows-Authentifizierung verwenden, um eine Verbindung mit lokalen Datenquellen und Azure-Dateifreigaben herzustellen. Sie können sowohl lokal als auch auf Azure-VMs und in Azure Files die Windows-Authentifizierung verwenden, um eine Verbindung mit Datenquellen in demselben Netzwerk herzustellen, in dem Azure SSIS Integration Runtime ausgeführt wird.

Die Anmeldeinformationen für die Domäne, die Sie beim Ausführen der in diesem Artikel dargestellten Schritte angeben, gelten solange für alle Paketausführungen auf der SQL-Datenbank-Instanz, bis Sie die Anmeldeinformationen ändern oder entfernen.

## <a name="provide-domain-credentials-for-windows-authentication"></a>Angeben von Domänenanmeldeinformationen für die Windows-Authentifizierung
Führen Sie die folgenden Schritte, um Anmeldeinformationen für die Domäne anzugeben, die es erlaubt, dass Pakete die Windows-Authentifizierung verwenden, um eine Verbindung mit lokalen Datenquellen herzustellen:

1.  Stellen Sie mit SQL Server Management Studio (SSMS) oder einem anderen Tool eine Verbindung mit der SQL-Datenbank her, die die SSIS-Katalogdatenbank (SSISDB) hostet. Weitere Informationen finden Sie unter [Connect to the SSISDB Catalog database on Azure (Herstellen einer Verbindung mit der SSIS-Katalogdatenbank in Azure)](ssis-azure-connect-to-catalog-database.md).

2.  Öffnen Sie ein Abfragefragefenster mit SSISDB als aktuelle Datenbank.

3.  Führen Sie die folgenden gespeicherten Prozeduren aus, und stellen Sie passende Anmeldeinformationen für die Domäne bereit:

    ```sql
    catalog.set_execution_credential @user='<your user name>', @domain='<your domain name>', @password='<your password>'
    ```

4.  Führen Sie die SSIS-Pakete aus. Die Pakete verwenden die Anmeldeinformationen, die Sie angegeben haben, um eine Verbindung mit den lokalen Datenquellen mithilfe der Windows-Authentifizierung herzustellen.

### <a name="view-domain-credentials"></a>Anzeigen von Anmeldeinformationen für eine Domäne
Führen Sie die folgenden Schritte aus, um die aktiven Anmeldeinformationen einer Domäne anzuzeigen:

1.  Stellen Sie mit SQL Server Management Studio (SSMS) oder einem anderen Tool eine Verbindung mit der SQL-Datenbank her, die die SSIS-Katalogdatenbank (SSISDB) hostet.

2.  Öffnen Sie ein Abfragefragefenster mit SSISDB als aktuelle Datenbank.

3.  Führen Sie die folgende gespeicherte Prozedur aus, und überprüfen Sie die Ausgabe:

    ```sql
    SELECT * 
    FROM catalog.master_properties
    WHERE property_name = 'EXECUTION_DOMAIN' OR property_name = 'EXECUTION_USER'
    ```

### <a name="clear-domain-credentials"></a>Löschen von Anmeldeinformationen für eine Domäne
Führen Sie die folgenden Schritte aus, um die Anmeldeinformationen, die Sie angegeben haben, wie in diesem Artikel beschrieben, zu löschen und zu entfernen:

1.  Stellen Sie mit SQL Server Management Studio (SSMS) oder einem anderen Tool eine Verbindung mit der SQL-Datenbank her, die die SSIS-Katalogdatenbank (SSISDB) hostet.

2.  Öffnen Sie ein Abfragefragefenster mit SSISDB als aktuelle Datenbank.

3.  Führen Sie die folgende gespeicherte Prozedur aus:

    ```sql
    catalog.set_execution_credential @user='', @domain='', @password=''
    ```

## <a name="connect-to-an-on-premises-sql-server"></a>Herstellen einer Verbindung zu einer lokalen SQL Server-Instanz
Führen Sie folgende Schritte aus, um zu überprüfen, ob Sie eine Verbindung mit einem lokalen SQL-Server herstellen können:

1.  Suchen Sie einen Computer, der nicht mit einer Domäne verknüpft ist, um diesen Test auszuführen.

2.  Führen Sie auf dem Computer, der nicht mit einer Domäne verknüpft ist, folgenden Befehl aus, um SQL Server Management Studio (SSMS) mit den Anmeldeinformationen für die Domäne zu starten, die Sie verwenden möchten:

    ```cmd
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
    ```

3.  Überprüfen Sie über SSMS, ob Sie eine Verbindung mit dem lokalen SQL Server herstellen können, den Sie verwenden möchten.

### <a name="prerequisites"></a>Erforderliche Komponenten
Um eine Verbindung mit einer lokalen SQL Server-Instanz von einem Paket aus herzustellen, das unter Azure ausgeführt wird, müssen Sie die folgenden Voraussetzungen erfüllen:

1.  Aktivieren Sie in SQL Server-Konfigurations-Manager das TCP/IP-Protokoll.
2.  Lassen Sie den Zugriff über die Windows-Firewall zu. Weitere Informationen finden Sie unter [Konfigurieren der Windows-Firewall für den SQL Server-Zugriff](https://docs.microsoft.com/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access).
3.  Um eine Verbindung mit der Windows-Authentifizierung herzustellen, stellen Sie sicher, dass die Azure SSIS Integration Runtime zu einem virtuellen Netzwerk (VNet) gehört, das ebenso die lokale Instanz von SQL Server enthält.  Weitere Informationen finden Sie unter [Verknüpfen einer Azure SSIS Integration Runtime mit einem virtuellen Netzwerk](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network). Verwenden Sie dann `catalog.set_execution_credential`, um Anmeldeinformationen wie in diesem Artikel beschrieben bereitzustellen.

## <a name="connect-to-an-on-premises-file-share"></a>Herstellen einer Verbindung zu einer lokalen Dateifreigabe
Führen Sie die folgenden Schritte aus, um zu überprüfen, ob Sie eine Verbindung mit einer lokalen Dateifreigabe herstellen können:

1.  Suchen Sie einen Computer, der nicht mit einer Domäne verknüpft ist, um diesen Test auszuführen.

2.  Führen Sie den folgenden Befehl auf dem Computer aus, der nicht mit einer Domäne verknüpft ist. Über diesen Befehl öffnen Sie zunächst ein Eingabeaufforderungsfenster mit den Anmeldeinformationen der Domäne, die Sie verwenden möchten, und testen dann die Konnektivität in der Dateifreigabe, indem Sie eine Verzeichnisliste abrufen.

    ```cmd
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
    ```

3.  Überprüfen Sie, ob die Verzeichnisliste für die lokale Dateifreigabe zurückgegeben wird, die Sie verwenden möchten.

## <a name="connect-to-a-file-share-on-an-azure-vm"></a>Herstellen einer Verbindung zu einer Dateifreigabe auf einer Azure-VM
Führen Sie die folgenden Schritte aus, um eine Verbindung mit einer Dateifreigabe auf einer Azure-VM herzustellen:

1.  Stellen Sie mit SQL Server Management Studio (SSMS) oder einem anderen Tool eine Verbindung mit der SQL-Datenbank her, die die SSIS-Katalogdatenbank (SSISDB) hostet.

2.  Öffnen Sie ein Abfragefragefenster mit SSISDB als aktuelle Datenbank.

3.  Führen Sie die gespeicherte `catalog.set_execution_credential`-Prozedur aus, wie in den folgenden Optionen beschrieben:

    ```sql
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
    ```

## <a name="connect-to-a-file-share-in-azure-files"></a>Herstellen einer Verbindung mit einer Dateifreigabe in Azure Files
Weitere Informationen zu Azure Files finden Sie unter [Azure Files](https://azure.microsoft.com/services/storage/files/).

Führen Sie die folgenden Schritte aus, um eine Verbindung mit einer Dateifreigabe auf einer Azure-Dateifreigabe herzustellen:

1.  Stellen Sie mit SQL Server Management Studio (SSMS) oder einem anderen Tool eine Verbindung mit der SQL-Datenbank her, die die SSIS-Katalogdatenbank (SSISDB) hostet.

2.  Öffnen Sie ein Abfragefragefenster mit SSISDB als aktuelle Datenbank.

3.  Führen Sie die gespeicherte `catalog.set_execution_credential`-Prozedur aus, wie in den folgenden Optionen beschrieben:

    ```sql
    catalog.set_execution_credential @domain = N'Azure', @user = N'<storage-account-name>', @password = N'<storage-account-key>'
    ```

## <a name="next-steps"></a>Nächste Schritte
- Stellen Sie ein Paket bereit. Weitere Informationen finden Sie unter [Deploy an SSIS project with SQL Server Management Studio (SSMS) (Bereitstellen eines SSIS-Projekts mit SQL Server Management Studio (SSMS))](../ssis-quickstart-deploy-ssms.md).
- Führen Sie ein Paket aus. Weitere Informationen finden Sie unter [Run an SSIS package with SQL Server Management Studio (SSMS) (Ausführen eines SSIS-Pakets mit SQL Server Management Studio (SSMS))](../ssis-quickstart-run-ssms.md).
- Planen Sie ein Paket. Weitere Informationen finden Sie unter [Schedule SSIS package execution on Azure (Planen der Ausführung von SSIS-Paketen in Azure)](ssis-azure-schedule-packages.md).
