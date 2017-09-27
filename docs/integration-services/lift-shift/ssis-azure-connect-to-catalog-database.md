---
title: Herstellen einer Verbindung mit der Datenbank SSISDB-Katalog in Azure | Microsoft Docs
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: dbe6f832d4af55ddd15e12fba17a4da490fe19ae
ms.openlocfilehash: 646999095957abb4e615b59b316b6ca59155dea3
ms.contentlocale: de-de
ms.lasthandoff: 09/25/2017

---
# <a name="connect-to-the-ssisdb-catalog-database-on-azure"></a>Herstellen einer Verbindung mit der Datenbank SSISDB-Katalog in Azure

Abzurufen Sie die Verbindungsinformationen, müssen Sie für die Verbindung mit der SSISDB-Katalog-Datenbank auf einer Azure SQL-Datenbankserver gehostet. Benötigen Sie die folgenden Elemente für die Verbindung aus:
- vollqualifizierten Servernamen
- Datenbankname
- Anmeldeinformationen 

## <a name="prerequisites"></a>Erforderliche Komponenten
Bevor Sie beginnen, stellen Sie sicher, dass Sie Version 17.2 oder höher von SQL Server Management Studio verwenden. Informationen zum Herunterladen der neuesten Version von SSMS finden Sie unter [Download SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="get-the-connection-info-from-the-azure-portal"></a>Abrufen der Verbindungsinformationen vom Azure-portal
1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/)an.
2. Wählen Sie im Azure-Portal **SQL-Datenbanken** aus dem Menü links, und wählen Sie dann die `SSISDB` Datenbank auf die **SQL-Datenbanken** Seite. 
3. Auf der **Übersicht** Seite für die `SSISDB` Datenbank, überprüfen Sie den vollqualifizierten Servernamen, wie in der folgenden Abbildung dargestellt. Zeigen Sie auf den Servernamen, um die **klicken** Option.

    ![Verbindungsinformationen für Server](media/ssis-azure-connect-to-catalog-database/server-name.png) 

4. Wenn Sie die Anmeldeinformationen für den SQL-Datenbankserver vergessen haben, navigieren Sie zu der SQL Server-Datenbankseite. Es können Sie der Serveradministrator anzeigen benennen und bei Bedarf das Kennwort zurückzusetzen.

## <a name="connect-with-ssms"></a>Herstellen einer Verbindung mit SSMS
1. Öffnen Sie SQL Server Management Studio.

2. **Herstellen einer Verbindung mit dem Server**. In der **Verbindung mit Server herstellen** Dialogfeld Geben Sie die folgende Informationen:

   | Einstellung       | Empfohlener Wert | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Servertyp** | Datenbankmodul | Dieser Wert ist erforderlich. |
   | **Servername** | Die vollqualifizierten Servernamen | Der Name muss im folgenden Format: **mysqldbserver.database.windows.net**. |
   | **Authentifizierung** | SQL Server-Authentifizierung | Dieser Schnellstart verwendet SQL-Authentifizierung. |
   | **Anmeldename** | Serveradmin-Kontos | Dies ist das Konto, das Sie angegeben werden, wenn Sie auf den Server erstellt haben. |
   | **Kennwort** | Das Kennwort für Ihr serveradmin-Kontos | Dies ist das Kennwort, das Sie angegeben werden, wenn Sie auf den Server erstellt haben. |

3. **Herstellen einer Verbindung mit dem SSISDB-Datenbank**. Wählen Sie **Optionen** , erweitern die **Verbindung mit Server herstellen** (Dialogfeld). In den erweiterten **Verbindung mit Server herstellen** wählen Sie im Dialogfeld die **Verbindungseigenschaften** Registerkarte. In der **mit Datenbank verbinden** aktivieren, oder geben Sie `SSISDB`.

4. Wählen Sie dann **verbinden**.

5. Erweitern Sie im Objekt-Explorer **Integration Services-Kataloge** und schließlich **SSISDB** zum Anzeigen der Objekte in der SSIS-Katalogdatenbank.

## <a name="next-steps"></a>Nächste Schritte
- Bereitstellen eines Pakets an. Weitere Informationen finden Sie unter [bereitstellen ein SSIS-Projekts mit SQL Server Management Studio (SSMS)](../ssis-quickstart-deploy-ssms.md).
- Ausführen eines Pakets. Weitere Informationen finden Sie unter [führen Sie ein SSIS-Paket mit SQL Server Management Studio (SSMS)](../ssis-quickstart-run-ssms.md).
- Planen eines Pakets an. Weitere Informationen finden Sie unter [Zeitplan SSIS-paketausführung in Azure](ssis-azure-schedule-packages.md)

