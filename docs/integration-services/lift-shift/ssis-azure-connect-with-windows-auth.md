---
title: Herstellen einer Verbindung mit lokalen Datenquellen und Azure-Dateifreigaben mit der Windows-Authentifizierung | Microsoft-Dokumentation
ms.date: 09/25/2017
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
ms.openlocfilehash: 9235ffd3225e76ee94067519c72e997c451d9893
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="connect-to-on-premises-data-sources-and-azure-file-shares-with-windows-authentication"></a>Herstellen einer Verbindung mit lokalen Datenquellen und Azure-Dateifreigaben mit der Windows-Authentifizierung
In diesem Artikel wird beschrieben, wie Sie den SSIS-Katalog auf Azure SQL-Datenbank so konfigurieren, dass er Pakete ausführt, die die Windows-Authentifizierung verwenden, um eine Verbindung mit lokalen Datenquellen und Azure-Dateifreigaben herzustellen.

Die Anmeldeinformationen für die Domäne, die Sie beim Ausführen der in diesem Artikel dargestellten Schritte angeben, gelten solange für alle Paketausführungen auf der SQL-Datenbank-Instanz, bis Sie die Anmeldeinformationen ändern oder entfernen.

## <a name="connect-to-on-premises-data-sources"></a>Herstellen einer Verbindung mit lokalen Datenquellen

### <a name="prerequisite"></a>Voraussetzung
Bevor Sie die Anmeldeinformationen für die Domäne für die Windows-Authentifizierung einrichten, überprüfen Sie, ob ein Computer, der nicht mit einer Domäne verknüpft ist, eine Verbindung mit der lokalen Datenquelle im `runas`-Modus herstellen kann.

#### <a name="connecting-to-sql-server"></a>Herstellen einer Verbindung mit SQL Server
Führen Sie folgende Schritte aus, um zu überprüfen, ob Sie eine Verbindung mit einem lokalen SQL-Server herstellen können:

1.  Suchen Sie einen Computer, der nicht mit einer Domäne verknüpft ist, um diesen Test auszuführen.

2.  Führen Sie auf dem Computer, der nicht mit einer Domäne verknüpft ist, folgenden Befehl aus, um SQL Server Management Studio (SSMS) mit den Anmeldeinformationen für die Domäne zu starten, die Sie verwenden möchten:

    ```cmd
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
    ```

3.  Überprüfen Sie über SSMS, ob Sie eine Verbindung mit dem lokalen SQL Server herstellen können, den Sie verwenden möchten.

#### <a name="connecting-to-a-file-share"></a>Herstellen einer Verbindung mit einer Dateifreigabe
Führen Sie die folgenden Schritte aus, um zu überprüfen, ob Sie eine Verbindung mit einer lokalen Dateifreigabe herstellen können:

1.  Suchen Sie einen Computer, der nicht mit einer Domäne verknüpft ist, um diesen Test auszuführen.

2.  Führen Sie den folgenden Befehl auf dem Computer aus, der nicht mit einer Domäne verknüpft ist. Über diesen Befehl öffnen Sie zunächst ein Eingabeaufforderungsfenster mit den Anmeldeinformationen der Domäne, die Sie verwenden möchten, und testen dann die Konnektivität in der Dateifreigabe, indem Sie eine Verzeichnisliste abrufen.

    ```cmd
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
    ```

3.  Überprüfen Sie, ob die Verzeichnisliste für die lokale Dateifreigabe zurückgegeben wird, die Sie verwenden möchten.

### <a name="provide-domain-credentials"></a>Angeben von Anmeldeinformationen für eine Domäne
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

## <a name="connect-to-file-shares"></a>Herstellen einer Verbindung mit Dateifreigaben
Sie können sowohl lokal als auch auf Azure-VMs und in Azure Files die Windows-Authentifizierung verwenden, um eine Verbindung mit Dateifreigaben in demselben Netzwerk herzustellen, auf dem Azure SSIS Integration Runtime ausgeführt wird. Weitere Informationen zu Azure Files finden Sie unter [Azure Files](https://azure.microsoft.com/services/storage/files/).

Führen Sie die folgenden Schritte aus, um eine Verbindung mit einer Dateifreigabe auf einer Azure-VM oder einer Azure-Dateifreigabe herzustellen.

1.  Stellen Sie mit SQL Server Management Studio (SSMS) oder einem anderen Tool eine Verbindung mit der SQL-Datenbank her, die die SSIS-Katalogdatenbank (SSISDB) hostet.

2.  Öffnen Sie ein Abfragefragefenster mit SSISDB als aktuelle Datenbank.

3.  Führen Sie die gespeicherte `catalog.set_execution_credential`-Prozedur aus, wie in den folgenden Optionen beschrieben:

    a.  Führen Sie die folgende gespeicherte Prozedur aus, um eine Verbindung mit einer Dateifreigabe auf einer Azure-VM herzustellen:

    ```sql
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
    ```

    b.  Führen Sie die folgende gespeicherte Prozedur aus, um eine Verbindung mit einer Azure-Dateifreigabe (d.h. in Azure Files) herzustellen:

    ```sql
    catalog.set_execution_credential @domain = N'Azure', @user = N'<storage-account-name>', @password = N'<storage-account-key>'
    ```

## <a name="next-steps"></a>Nächste Schritte
- Stellen Sie ein Paket bereit. Weitere Informationen finden Sie unter [Deploy an SSIS project with SQL Server Management Studio (SSMS) (Bereitstellen eines SSIS-Projekts mit SQL Server Management Studio (SSMS))](../ssis-quickstart-deploy-ssms.md).
- Führen Sie ein Paket aus. Weitere Informationen finden Sie unter [Run an SSIS package with SQL Server Management Studio (SSMS) (Ausführen eines SSIS-Pakets mit SQL Server Management Studio (SSMS))](../ssis-quickstart-run-ssms.md).
- Planen Sie ein Paket. Weitere Informationen finden Sie unter [Schedule SSIS package execution on Azure (Planen der Ausführung von SSIS-Paketen in Azure)](ssis-azure-schedule-packages.md).
