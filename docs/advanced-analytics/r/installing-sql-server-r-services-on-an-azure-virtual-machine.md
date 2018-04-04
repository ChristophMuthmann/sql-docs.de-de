---
title: Installieren von SQL Server-Machine Learning-Features auf virtuellen Azure-Computer | Microsoft Docs
ms.custom: ''
ms.date: 03/21/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: bb1cd5e695e59c898a0e5dbcad279e1a8796bb63
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="install-sql-server-machine-learning-features-on-an-azure-virtual-machine"></a>Installieren von SQL Server-Machine learning-Features auf virtuellen Azure-Computer
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
Es wird empfohlen, die [Data Science Virtual Machine](ttps://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/provision-vm), aber Sie gegebenenfalls einen virtuellen Computer, die nur für SQL Server 2017 Machine Learning Services oder SQL Server 2016 R Services hat dieser Artikel leitet Sie durch die Schritte.

## <a name="create-a-virtual-machine-on-azure"></a>Erstellen eines virtuellen Computers in Azure

1. Klicken Sie im Azure-Portal in der linken Liste auf **VMs** , und klicken Sie dann auf **hinzufügen**.
2. Suche nach SQL Server 2017 Enterprise Edition oder SQL Server 2016 Enterprise Edition.
3. Konfigurieren Sie den Servernamen und die Kontoberechtigungen, und wählen Sie einen Tarif aus.
4. In **SQL Server-Einstellungen** (Schritt 4 in der VM-Setup-Assistenten), suchen Sie **Machine Learning-Dienste (Advanced Analytics)** (oder **R Services** für SQL Server 2016), und klicken Sie auf  **Aktivieren Sie**.
5. Überprüfen Sie die Zusammenfassung, die für die Validierung dargestellt ist, und klicken Sie auf **OK**.
6. Wenn der virtuelle Computer bereit ist, stellen Sie eine Verbindung her, und öffnen Sie SQL Server Management Studio, was bereits installiert ist. Machine Learning ist für die Ausführung bereit.
7. Um dies zu überprüfen, können Sie ein neues Abfragefenster öffnen eine einfache Anweisung wie diese ausführen, die R verwendet, um eine Sequenz von Zahlen von 1 bis 10 zu generieren.

    ```
    EXEC sp_execute_external_script
    @language = N'R'
    , @script = N' OutputDataSet <- as.data.frame(seq(1, 10, ));'
    , @input_data_1 = N'   ;'
    WITH RESULT SETS (([Sequence] int NOT NULL));
    ```

6. Wenn Sie von einem remote Data Science-Client mit der Instanz herstellen möchten, führen Sie [zusätzliche Schritte](#additional-steps) nach Bedarf.

### <a name="disable-machine-learning-features-on-a-sql-server-vm"></a>Deaktivieren von Machine Learning-Features auf einer SQL Server-VM

Sie können auch aktivieren oder deaktivieren Sie die Funktion auf einem vorhandenen SQL Server-virtuellen Computer zu einem beliebigen Zeitpunkt.

1. Öffnen Sie das Blatt für die virtuelle Maschine an.
2. Klicken Sie auf **Einstellungen**, und wählen Sie **SQL Server-Konfiguration** aus.
3. Nehmen Sie Änderungen an Funktionen, und wenden.

### <a name="existing"></a>Hinzufügen von R Services zu einer vorhandenen SQL Server 2016 Enterprise-VM

Wenn Sie einen virtuellen Azure-Computer, der SQL Server ohne Machine learning-enthalten erstellt, können Sie die Funktion hinzufügen, durch die folgenden Schritte:

1. Führen Sie erneut das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup aus, und fügen Sie die Funktion auf der Seite **Serverkonfiguration** des Assistenten hinzu.
2. Aktivieren Sie die Ausführung des externen Skripts, und starten Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz erneut. Weitere Informationen finden Sie unter [Installieren von SQL Server 2016 R Services](../install/sql-r-services-windows-install.md).
3. (Optional) Konfigurieren Sie bei Bedarf den Datenbankzugriff für R-Workerkonten für die remote Skriptausführung.
4. (Optional) Ändern Sie eine Firewallregel auf dem virtuellen Azure-Computer, wenn Sie beabsichtigen, die R-Skriptausführung von remoten Data Science-Clients zu ermöglichen. Weitere Informationen finden Sie unter [Aufhebung der Firewallblockierung](#firewall).
5. Installieren oder Aktivieren von erforderlichen Netzwerkbibliotheken. Weitere Informationen finden Sie unter [Hinzufügen von Netzwerkprotokollen](#network).

## <a name="additional-steps"></a>Zusätzliche Schritte

Einige zusätzliche Schritte sind erforderlich, wenn Sie davon ausgehen, dass Remoteclients Zugriff auf den Server als remote SQL Server-computekontext.

### <a name="firewall"></a>Aufhebung der Firewallblockierung

Standardmäßig enthält die Firewall auf virtuellen Azure-Computer eine Regel, dass der Netzwerkzugriff für lokale Benutzerkonten blockiert.

Sie müssen diese Regel klicken, um sicherzustellen, dass Sie zugreifen können, Deaktivieren der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz anhand einer remote Data Science-Client.  Andernfalls kann Ihrer für maschinelles lernen von Code in rechenkontexte ausführen, die Arbeitsbereichs des virtuellen Computers verwenden.

So aktivieren Sie den Zugriff auf remote Data Science-clients

1. Öffnen Sie auf dem virtuellen Computer die Windows-Firewall mit erweiterter Sicherheit.
2. Wählen Sie **Ausgehende Regeln** aus.
3. Deaktivieren Sie die folgende Regel:
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
### <a name="enable-odbc-callbacks-for-remote-clients"></a>ODBC-Rückrufe für Remoteclients aktivieren

Wenn Sie erwarten, dass Clients den Server Aufrufen von ODBC-Abfragen als Teil ihrer den Machine learning-Lösungen benötigen, müssen Sie sicherstellen, dass das Launchpad ODBC-Aufrufe für den Remoteclient ausführen kann. Zu diesem Zweck müssen Sie die SQL-Workerkonten zulassen, die vom Launchpad für die Anmeldung bei der Instanz verwendet werden.
Weitere Informationen finden Sie unter [Installieren von SQL Server 2016 R Services](../install/sql-r-services-windows-install.md).

### <a name="network"></a>Hinzufügen von Netzwerkprotokollen

+ Aktivieren von Named Pipes
  
  Derzeit verwendet [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] das Named Pipes-Protokoll für Verbindungen zwischen dem Client und den Servercomputern und für einige externe Verbindungen. Wenn Named Pipes nicht aktiviert ist, müssen Sie es jeweils auf dem virtuellen Azure-Computer und auf alle Data Science-Clients installieren und aktivieren, die eine Verbindung mit dem Server herstellen.
  
+ Aktivieren von TCP/IP

  TCP/IP ist für Loopback-Verbindungen erforderlich. Wenn Sie die folgende Fehlermeldung angezeigt, aktivieren Sie TCP/IP auf dem virtuellen Computer, die die Instanz unterstützt:

  "DBNETLIB; SQL Server ist nicht vorhanden oder der Zugriff verweigert"