---
title: Installieren von SQL Server-Machine Learning-Features auf virtuellen Azure-Computer | Microsoft Docs
ms.custom: 
ms.date: 10/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c3c223b8-75c4-412e-a319-d57ecf6533af
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 08c3434ec120003de6d62bc61da3637e9177bb88
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="installing-sql-server-machine-learning-features-on-an-azure-virtual-machine"></a>Installieren von SQL Server-Machine learning-Features auf virtuellen Azure-Computer
 
Wenn Sie einen virtuellen Azure-Computer bereitstellen, enthält [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], Machine Learning können jetzt als eine Funktion mit der Instanz hinzugefügt werden, bei der Erstellung des virtuellen Computers auswählen.

+ [Erstellen Sie einen neuen virtuellen Computer, der SQL Server 2016 und R Services enthält](#new)
+ [Hinzufügen von Machine Learning-Features mit einem vorhandenen virtuellen Computer mit SQL Server 2016](#existing)

> [!NOTE]
> Virtuelle Computer sind jetzt für SQL Server-2017 verfügbar! Finden Sie unter [dieser Ankündigung](https://azure.microsoft.com/blog/announcing-new-azure-vm-images-sql-server-2017-on-linux-and-windows/) Details.
> 
> R ist auch verfügbar als Vorschaufunktion in Azure SQL-Datenbank. Weitere Informationen finden Sie unter [mithilfe von R in Azure SQL-Datenbank](../r/using-r-in-azure-sql-database.md).

## <a name="create-a-new-sql-server-2017-virtual-machine"></a>Erstellen eines neuen SQL Server-2017 virtuellen Computers

Um in SQL Server-2017 R oder Python zu verwenden, werden Sie sicher, dass eine Windows-basierte virtuelle Maschine abrufen. [!INCLUDE[sscurrentlong-md](../../includes/sscurrentlong-md.md)]unter Linux unterstützt schnelle [native Bewertung](../sql-native-scoring.md) verwenden, die VORHERSAGEN T-SQL-Funktion, aber anderen Machine learning-Funktionen sind nicht verfügbar noch in dieser Edition.

Eine Liste der SQL Server-VM-Angebote, finden Sie im Artikel: [Übersicht über die von SQL Server auf Azure Virtual Machines (Windows)](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview).

### <a name="new"></a>Erstellen Sie eine neue SQL Server-Enterprise-VM mit Machine learning

1. Klicken Sie im Azure-Portal auf virtuelle Computer, und klicken Sie dann auf neu.
2. Wählen Sie SQL Server 2017 Enterprise Edition ein.
3. Konfigurieren Sie den Servernamen und die Kontoberechtigungen, und wählen Sie einen Tarif aus.
4. In **SQL Server-Einstellungen** (Schritt 4 in der VM-Setup-Assistenten), suchen Sie **Machine Learning-Dienste (Advanced Analytics)** , und klicken Sie auf **aktivieren**.
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
2. Aktivieren Sie die Ausführung des externen Skripts, und starten Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz erneut. Weitere Informationen finden Sie unter [Einrichten von SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).
3. (Optional) Konfigurieren Sie bei Bedarf den Datenbankzugriff für R-Workerkonten für die remote Skriptausführung.
   Weitere Informationen finden Sie unter [Einrichten von SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).
3. (Optional) Ändern Sie eine Firewallregel auf dem virtuellen Azure-Computer, wenn Sie beabsichtigen, die R-Skriptausführung von remoten Data Science-Clients zu ermöglichen. Weitere Informationen finden Sie unter [Aufhebung der Firewallblockierung](#firewall).
4. Installieren oder Aktivieren von erforderlichen Netzwerkbibliotheken. Weitere Informationen finden Sie unter [Hinzufügen von Netzwerkprotokollen](#network).

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
Weitere Informationen finden Sie unter [Einrichten von SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).

### <a name="network"></a>Hinzufügen von Netzwerkprotokollen

+ Aktivieren von Named Pipes
  
  Derzeit verwendet [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] das Named Pipes-Protokoll für Verbindungen zwischen dem Client und den Servercomputern und für einige externe Verbindungen. Wenn Named Pipes nicht aktiviert ist, müssen Sie es jeweils auf dem virtuellen Azure-Computer und auf alle Data Science-Clients installieren und aktivieren, die eine Verbindung mit dem Server herstellen.
  
+ Aktivieren von TCP/IP

  TCP/IP ist für Loopback-Verbindungen erforderlich. Wenn Sie die folgende Fehlermeldung angezeigt, aktivieren Sie TCP/IP auf dem virtuellen Computer, die die Instanz unterstützt:

  "DBNETLIB; SQL Server ist nicht vorhanden oder der Zugriff verweigert"

## <a name="related-resources"></a>Verwandte Ressourcen

[Verwendung von R in Azure SQL-Datenbank](../r/using-r-in-azure-sql-database.md)