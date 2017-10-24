---
title: Herstellen einer Verbindung mit lokalen Datenquellen mit Windows-Authentifizierung | Microsoft Docs
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 1e3d9736612211038991489a4bd858d1ff89d333
ms.openlocfilehash: 1b60d877c6c75a77dd16fa8cb1704e10baf36bdb
ms.contentlocale: de-de
ms.lasthandoff: 10/19/2017

---
# <a name="connect-to-on-premises-data-sources-with-windows-authentication"></a>Herstellen einer Verbindung mit lokalen Datenquellen mit Windows-Authentifizierung
Dieser Artikel beschreibt das Konfigurieren von SSIS-Katalog für Azure SQL-Datenbank zum Ausführen von Paketen, die Windows-Authentifizierung zu verwenden, um Verbindungen zu lokalen Datenquellen herstellen.

Die Anmeldeinformationen für die Domäne, die Sie angeben, wenn Sie die Schritte in diesem Artikel gelten für alle paketausführungen für die SQL-Datenbankinstanz, bis Sie ändern oder entfernen Sie die Anmeldeinformationen.

## <a name="prerequisite"></a>Voraussetzung
Bevor Sie Domänenanmeldeinformationen für die Windows-Authentifizierung eingerichtet haben, überprüfen Sie, ob eine Computer keiner Domäne angehören, Ihrer lokalen Datenquelle in eine Verbindung herstellen kann `runas` Modus.

### <a name="connecting-to-sql-server"></a>Herstellen einer Verbindung mit SQLServer
Um zu überprüfen, ob Sie eine Verbindung mit einer lokalen SQL Server herstellen können, führen Sie folgende Schritte aus:

1.  Zum Ausführen dieser Tests finden Sie einen Computer keiner Domäne angehören.

2.  Führen Sie den folgenden Befehl zum Starten von SQL Server Management Studio (SSMS) mit den Anmeldeinformationen für die Domäne, die Sie verwenden möchten, auf dem Computer keiner Domäne angehören:

    ```cmd
    runas.exe /netonly /user:<domain>\<username> SSMS.exe
    ```

3.  Überprüfen Sie, ob Sie eine Verbindung mit einer lokalen SQL Server herstellen können, die Sie verwenden möchten, in SSMS.

### <a name="connecting-to-a-file-share"></a>Herstellen einer Verbindung mit einer Dateifreigabe
Um zu überprüfen, ob Sie eine Verbindung mit einer lokalen Dateifreigabe herstellen können, führen Sie folgende Schritte aus:

1.  Zum Ausführen dieser Tests finden Sie einen Computer keiner Domäne angehören.

2.  Führen Sie den folgenden Befehl auf dem Computer keiner Domäne angehören. Dieser Befehl öffnet ein Befehl Prommpt mit Anmeldeinformationen für die Domäne, die Sie verwenden möchten, und klicken Sie dann testet die Verbindung mit der Dateifreigabe durch eine Verzeichnisliste abrufen.

    ```cmd
    runas.exe /netonly /user:<domain>\<username> cmd.exe
    dir \\fileshare
    ```

3.  Überprüfen Sie, ob die Verzeichnisliste zurückgegeben wird, für das lokale Freigabe Datei, die Sie verwenden möchten.

## <a name="provide-domain-credentials"></a>Geben Sie Anmeldeinformationen für die Domäne
Um Domänenanmeldeinformationen anzugeben, mit die Pakete, die Windows-Authentifizierung zu verwenden, um Verbindungen zu lokalen Datenquellen herstellen können, führen Sie folgende Schritte aus:

1.  Mit SQL Server Management Studio (SSMS) oder ein anderes Tool mit der SQL-Datenbank verbinden Sie, der als Host der SSIS-Katalogdatenbank (SSISDB). Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit der Datenbank SSISDB-Katalog in Azure](ssis-azure-connect-to-catalog-database.md).

2.  Öffnen Sie mit SSISDB als aktuelle Datenbank ein Abfragefenster.

3.  Führen Sie die folgende gespeicherte Prozedur, und geben Sie die richtigen Domänenanmeldeinformationen:

    ```sql
    catalog.set_execution_credential @user='<your user name>', @domain='<your domain name>', @password='<your password>'
    ```
4.  Die SSIS-Pakete ausführen. Die Pakete verwenden die Anmeldeinformationen, die Sie zum Herstellen einer lokalen Datenquellen mit Windows-Authentifizierung bereitgestellt.

## <a name="view-domain-credentials"></a>Anmeldeinformationen für die Domäne
Um die aktiven Domänenanmeldeinformationen anzuzeigen, führen Sie folgende Schritte aus:

1.  Mit SQL Server Management Studio (SSMS) oder ein anderes Tool mit der SQL-Datenbank verbinden Sie, der als Host der SSIS-Katalogdatenbank (SSISDB).

2.  Öffnen Sie mit SSISDB als aktuelle Datenbank ein Abfragefenster.

3.  Führen Sie die folgende gespeicherte Prozedur, und überprüfen Sie die Ausgabe:

    ```sql
    SELECT * 
    FROM catalog.master_properties
    WHERE property_name = 'EXECUTION_DOMAIN' OR property_name = 'EXECUTION_USER'
    ```

## <a name="clear-domain-credentials"></a>Anmeldeinformationen für die Domäne löschen
Um zu entfernen, und entfernen Sie die Anmeldeinformationen, die Sie bereitgestellt werden, wie in diesem Artikel beschrieben, führen Sie folgende Schritte aus:

1.  Mit SQL Server Management Studio (SSMS) oder ein anderes Tool mit der SQL-Datenbank verbinden Sie, der als Host der SSIS-Katalogdatenbank (SSISDB).

2.  Öffnen Sie mit SSISDB als aktuelle Datenbank ein Abfragefenster.

3.  Führen Sie die folgende gespeicherte Prozedur aus:

    ```sql
    catalog.set_execution_credential @user='', @domain='', @password=''
    ```

## <a name="connect-to-file-shares"></a>Verbindung zu Dateifreigaben herstellen
Sie können Windows-Authentifizierung verwenden, für die Verbindung zu Dateifreigaben im selben virtuellen Netzwerk wie der Azure SSIS-Integrationslaufzeit sowohl lokal als auch auf virtuellen Azure-Computern.

Um an eine Dateifreigabe auf einem virtuellen Azure-Computer zu verbinden, führen Sie folgende Schritte aus:

1.  Mit SQL Server Management Studio (SSMS) oder ein anderes Tool mit der SQL-Datenbank verbinden Sie, der als Host der SSIS-Katalogdatenbank (SSISDB).

2.  Öffnen Sie mit SSISDB als aktuelle Datenbank ein Abfragefenster.

3.  Führen Sie die folgende gespeicherte Prozedur aus:

    ```sql
    catalog.set_execution_credential @domain = N'.', @user = N'username of local account on Azure virtual machine', @password = N'password'
    ```

## <a name="next-steps"></a>Nächste Schritte
- Bereitstellen eines Pakets an. Weitere Informationen finden Sie unter [bereitstellen ein SSIS-Projekts mit SQL Server Management Studio (SSMS)](../ssis-quickstart-deploy-ssms.md).
- Ausführen eines Pakets. Weitere Informationen finden Sie unter [führen Sie ein SSIS-Paket mit SQL Server Management Studio (SSMS)](../ssis-quickstart-run-ssms.md).
- Planen eines Pakets an. Weitere Informationen finden Sie unter [Zeitplan SSIS-paketausführung in Azure](ssis-azure-schedule-packages.md)

