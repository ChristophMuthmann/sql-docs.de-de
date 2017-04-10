---
title: "Installieren von SQL Server R Services auf virtuellen Azure-Computer | Microsoft Docs"
ms.custom: ""
ms.date: "12/07/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c3c223b8-75c4-412e-a319-d57ecf6533af
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# Installieren von SQL Server R Services auf virtuellen Azure-Computer
 
Wenn Sie einen virtuellen Azure-Computer bereitstellen, enthält [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], Sie können jetzt R Services als eine Funktion mit der Instanz hinzugefügt werden, bei der Erstellung des virtuellen Computers auswählen. 



+ [Erstellen Sie einen neuen virtuellen Computer mit SQL Server 2016 und R Services](#new)
+ [Hinzufügen von R Services zu einem vorhandenen virtuellen Computer mit SQL Server 2016](#existing)

## <a name="a-namenewacreate-a-new-sql-server-2016-enterprise-virtual-machine-with-r-services-enabled"></a><a name="new"></a>Erstellen Sie eine neue SQL Server 2016 Enterprise virtuelle Maschine mit R Services aktiviert

1. Klicken Sie im Azure-Portal auf VIRTUELLE COMPUTER, und klicken Sie dann auf NEU.
2. Wählen Sie SQL Server 2016 Enterprise Edition ein.
3. Konfigurieren Sie die Server und Berechtigungen, und wählen Sie einen Tarif.
4. Setup-Assistent, unter Schritt 4 auf dem virtuellen Computer **SQL Server-Einstellungen**, suchen Sie **R Services (Advanced Analytics)** und klicken Sie auf **aktivieren**.
5. Überprüfen Sie die Zusammenfassung angezeigt, für die Validierung und klicken Sie auf **OK**.
6. Wenn der virtuelle Computer bereit ist, eine Verbindung, und öffnen Sie SQL Server Management Studio vorinstalliert ist. R-Services ist für die Ausführung bereit. 
7. Um dies zu überprüfen, können Sie ein neues Abfragefenster öffnen und Ausführen eine einfache Anweisung wie z. B. Folgendes ein, die R verwendet wird, um eine Sequenz von Zahlen zwischen 1 und 10 generiert.
   ```
    execute sp_execute_external_script
    @language = N'R'
    , @script = N' OutputDataSet <- as.data.frame(seq(1, 10, ));'
    , @input_data_1 = N'   ;'
    WITH RESULT SETS (([Sequence] int NOT NULL));
   ```
6. Wenn Sie mit der Instanz von einem remote Data Science-Client herstellen möchte, führen Sie [zusätzliche Schritte](#additional-steps) nach Bedarf.


## <a name="additional-steps"></a>Zusätzliche Schritte  

Einige zusätzliche Schritte können erforderlich sein, um R-Services verwenden, wenn Sie davon ausgehen, Remoteclients dass auf den Server zugreifen, wie ein Remotecomputer mit SQL Server-computekontext.

### <a name="a-namefirewallaunblock-the-firewall"></a><a name="firewall"></a>Die Aufhebung der firewallblockierung  
  
Sie müssen eine Firewallregel auf dem virtuellen Computer, um sicherzustellen, dass Sie zugreifen können, ändern die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz anhand einer remote Data Science-Client.  Andernfalls, können Sie nicht in der Lage, Compute verwenden, die Kontexte, die erfordern Arbeitsbereichs des virtuellen Computers verwenden. 

Standardmäßig enthält die Firewall auf virtuellen Azure-Computer eine Regel, dass der Netzwerkzugriff für lokale Benutzerkonten für R blockiert.  
  
Zum Aktivieren des Zugriffs auf R-Dienste von remote Data Science-Clients:
1. Öffnen Sie auf dem virtuellen Computer Windows-Firewall mit erweiterter Sicherheit.
2. Wählen Sie **Ausgehende Regeln**
3. Deaktivieren Sie die folgende Regel:  
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`  
  
### <a name="enable-odbc-callbacks-for-remote-clients"></a>Aktivieren von ODBC-Rückrufe für Remoteclients

Wenn Sie erwarten, dass R-Clients, die den Server Aufrufen von ODBC-Abfragen als Teil ihrer R-Lösungen benötigen, müssen Sie sicherstellen, dass das Launchpad ODBC-Aufrufe für den Remoteclient ausführen kann. Zu diesem Zweck müssen Sie die SQL-Worker-Konten zulassen, die von Launchpad verwendet werden, bei der Instanz anmelden.
Weitere Informationen finden Sie unter [Festlegen von SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md). 

### <a name="a-namenetworkaadd-network-protocols"></a><a name="network"></a>Hinzufügen von Netzwerkprotokollen  
  
+ Aktivieren Sie Named Pipes
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] Named Pipes-Protokoll verwendet, für Verbindungen zwischen den Client- und Servercomputer, und für einige interne Verbindungen. Wenn Named Pipes nicht aktiviert ist, müssen Sie installieren und aktivieren Sie ihn auf beide virtuellen Azure-Computer und auf jeder Data Science-Clients, die mit dem Server verbinden.  
  
+ Aktivieren Sie TCP/IP

  TCP/IP ist für Loopbackverbindungen mit SQL Server R Services erforderlich. Wenn Sie die folgende Fehlermeldung angezeigt, aktivieren Sie TCP/IP auf dem virtuellen Computer, die die DBNETLIB-Instanz unterstützt; SQL Server ist nicht vorhanden oder der Zugriff verweigert.

## <a name="how-to-disable-r-services-on-an-instance"></a>Gewusst wie: Deaktivieren von R Services in einer Instanz

Sie können auch aktivieren oder deaktivieren das Feature auf einer vorhandenen virtuellen Maschine zu einem beliebigen Zeitpunkt. 

1. Öffnen Sie das Blatt für die virtuelle Maschine
2. Klicken Sie auf **Einstellungen**, und wählen Sie **SQL Server-Konfiguration**.


## <a name="a-nameexistingaadd-sql-server-r-services-to-an-existing-sql-server-2016-enterprise-virtual-machine"></a><a name="existing"></a>Hinzufügen von SQL Server R Services zu einer vorhandenen SQL Server 2016 Enterprise virtuellen Maschine

Wenn Sie ein Azure-VM mit SQL Server 2016, die R-Services nicht enthält erstellt, können Sie die Funktion hinzufügen, durch die folgenden Schritte:

1. Führen Sie erneut aus [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einrichten, und fügen Sie das Feature für die **Serverkonfiguration** Seite des Assistenten.
2. Ausführung externer Skripts aktivieren und Starten der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Instanz. Weitere Informationen finden Sie unter finden Sie unter [Festlegen von SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).
3. (Optional) Konfigurieren Sie Datenbankzugriff für R-Worker-Konten, bei Bedarf für die Remoteausführung von Skripts.
   Weitere Informationen finden Sie unter [Festlegen von SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md). 
3. (Optional) Ändern Sie eine Firewallregel auf dem virtuellen Computer in Azure, wenn Sie beabsichtigen, die Ausführung von R-Skripts aus remote Data Science-Clients zu ermöglichen. Weitere Informationen finden Sie unter [Firewallblockierung](#firewall).
4. Installieren oder Aktivieren von Netzwerkbibliotheken erforderlich. Weitere Informationen finden Sie unter [Hinzufügen Netzwerkprotokolle](#network).

## <a name="see-also"></a>Siehe auch
[Einrichten von Sql Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)