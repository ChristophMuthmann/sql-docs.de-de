---
title: Herstellen einer Verbindung mit der SSISDB-Katalogdatenbank in Azure | Microsoft-Dokumentation
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
ms.openlocfilehash: 10be16cbc85cccce51fafbcd733045c653b7be0a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="connect-to-the-ssisdb-catalog-database-on-azure"></a>Herstellen einer Verbindung mit der SSISDB-Katalogdatenbank in Azure

Rufen Sie die Verbindungsinformationen ab, die benötigt werden, um eine Verbindung mit der auf einem Azure SQL-Datenbankserver gehosteten SSISDB-Katalogdatenbank herzustellen. Sie benötigen Folgendes, um eine Verbindung herzustellen:
- Vollqualifizierten Servernamen
- Datenbanknamen
- Anmeldeinformationen 

## <a name="prerequisites"></a>Erforderliche Komponenten
Prüfen Sie, ob Sie über die Version 17.2 oder höher von SQL Server Management Studio verfügen, bevor Sie beginnen. Um die neueste Version von SSMS herunterzuladen, lesen Sie [Herunterladen von SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="get-the-connection-info-from-the-azure-portal"></a>Abrufen der Verbindungsinformationen vom Azure-Portal
1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/)an.
2. Wählen Sie im Azure-Portal im Menü auf der linken Seite **SQL-Datenbanken** aus, und wählen Sie dann auf der Seite **SQL-Datenbanken** die `SSISDB`-Datenbank aus. 
3. Überprüfen Sie auf der Seite **Übersicht** Ihrer `SSISDB`-Datenbank den vollqualifizierten Servernamen, wie in der folgenden Abbildung gezeigt wird. Zeigen Sie auf den Servernamen, damit die Option **Klicken Sie zum Kopieren** angezeigt wird.

    ![Serververbindungsinformationen](media/ssis-azure-connect-to-catalog-database/server-name.png) 

4. Wenn Sie die Anmeldeinformationen für den SQL-Datenbankserver vergessen haben, navigieren Sie zur Seite „SQL-Datenbankserver“. Dort können Sie den Namen des Serveradministrators einsehen und ggf. das Kennwort zurücksetzen.

## <a name="connect-with-ssms"></a>Herstellen einer Verbindung mit SSMS
1. Öffnen Sie SQL Server Management Studio.

2. **Stellen Sie eine Verbindung mit dem Server her**. Geben Sie im Dialogfeld **Mit Server verbinden** die folgenden Informationen ein:

   | Einstellung       | Vorgeschlagener Wert | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Servertyp** | Datenbankmodul | Dieser Wert ist erforderlich. |
   | **Servername** | Der vollqualifizierte Servername | Der Name muss das folgende Format aufweisen: **mysqldbserver.database.windows.net**. |
   | **Authentifizierung** | SQL Server-Authentifizierung | In diesem Schnellstart wird die SQL-Authentifizierung verwendet. |
   | **Anmeldename** | Das Konto des Serveradministrators | Dabei handelt es sich um das Konto, das Sie beim Erstellen des Servers angegeben haben. |
   | **Kennwort** | Das Kennwort für das Konto des Serveradministrators | Dabei handelt es sich um das Kennwort, das Sie beim Erstellen des Servers angegeben haben. |

3. **Stellen Sie eine Verbindung mit der SSISDB-Datenbank her**. Wählen Sie **Optionen**  aus, um das Dialogfeld **Mit Server verbinden** zu erweitern. Wählen Sie im erweiterten Dialogfeld **Mit Server verbinden** die Registerkarte **Verbindungseigenschaften** aus. Wählen Sie `SSISDB` im Feld **Mit Datenbank verbinden** aus, oder geben Sie es ein.

    > [!IMPORTANT]
    > Wenn Sie beim Herstellen einer Verbindung nicht `SSISDB` auswählen, wird der SSIS-Katalog möglicherweise nicht im Objekt-Explorer angezeigt.

4. Wählen Sie anschließend **Verbinden** aus.

5. Erweitern Sie im Objekt-Explorer **Integration Services-Kataloge** und dann **SSISDB**, um die Objekte in der SSIS-Katalogdatenbank anzuzeigen.

## <a name="next-steps"></a>Nächste Schritte
- Stellen Sie ein Paket bereit. Weitere Informationen finden Sie unter [Bereitstellen eines SSIS-Projekts mit SQL Server Management Studio (SSMS)](../ssis-quickstart-deploy-ssms.md).
- Führen Sie ein Paket aus. Weitere Informationen finden Sie unter [Ausführen eines SSIS-Pakets mit SQL Server Management Studio (SSMS)](../ssis-quickstart-run-ssms.md).
- Planen Sie ein Paket. Weitere Informationen finden Sie unter [Planen der Ausführung von SSIS-Paketen in Azure](ssis-azure-schedule-packages.md).
