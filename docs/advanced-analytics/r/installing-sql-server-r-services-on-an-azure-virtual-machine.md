---
title: Installieren von SQL Server R Services auf einem virtuellen Azure-Computer | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c3c223b8-75c4-412e-a319-d57ecf6533af
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e673268b1f6b56890f22576d293135b2675ed4ab
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="installing-sql-server-r-services-on-an-azure-virtual-machine"></a>Installieren von SQL Server R Services auf einem virtuellen Azure-Computer
 
Wenn Sie einen virtuellen Azure-Computer bereitstellen, enthält [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], Machine Learning können jetzt als eine Funktion mit der Instanz hinzugefügt werden, bei der Erstellung des virtuellen Computers auswählen.

+ [Erstellen eines neuen virtuellen Computers mit SQL Server 2016 und R Services](#new)
+ [Hinzufügen von R Services zu einem vorhandenen virtuellen Computer mit SQL Server 2016](#existing)

## <a name="new"></a>Erstellen eines neuen virtuellen SQL Server 2016 Enterprise-Computers auf dem R Services aktiviert ist

1. Klicken Sie im Azure-Portal auf virtuelle Computer, und klicken Sie dann auf neu.
2. Wählen Sie SQL Server 2016 Enterprise Edition aus.
3. Konfigurieren Sie den Servernamen und die Kontoberechtigungen, und wählen Sie einen Tarif aus.
4. Suchen Sie in Schritt 4 im Setupassistenten des virtuellen Computers unter **SQL Server-Einstellungen** nach **R Services (erweiterte Analyse)**, und klicken Sie auf **Aktivieren**.
5. Überprüfen Sie die Zusammenfassung, die für die Validierung dargestellt ist, und klicken Sie auf **OK**.
6. Wenn der virtuelle Computer bereit ist, stellen Sie eine Verbindung her, und öffnen Sie SQL Server Management Studio, was bereits installiert ist. R Services ist nun zur Ausführung bereit.
7. Um dies zu überprüfen, können Sie ein neues Abfragefenster öffnen eine einfache Anweisung wie diese ausführen, die R verwendet, um eine Sequenz von Zahlen von 1 bis 10 zu generieren.
   ```
    execute sp_execute_external_script
    @language = N'R'
    , @script = N' OutputDataSet <- as.data.frame(seq(1, 10, ));'
    , @input_data_1 = N'   ;'
    WITH RESULT SETS (([Sequence] int NOT NULL));
   ```
6. Wenn Sie eine Verbindung mit der Instanz eines remoten Data Science-Clients herstellen, führen Sie die [zusätzlichen Schritte](#additional-steps) wie erforderlich aus.


## <a name="additional-steps"></a>Zusätzliche Schritte  

Einige zusätzliche Schritte sind erforderlich, wenn Sie davon ausgehen, dass Remoteclients Zugriff auf den Server als remote SQL Server-computekontext.

### <a name="firewall"></a>Aufhebung der Firewallblockierung

Die Firewall enthält auf virtuellen Azure-Computern standardmäßig eine Regel, die den Netzwerkzugriff für lokale Benutzerkonten für R blockiert.

Sie müssen diese Regel klicken, um sicherzustellen, dass Sie zugreifen können, Deaktivieren der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz anhand einer remote Data Science-Client.  Andernfalls kann nicht R-Code in rechenkontexte, die im Arbeitsbereich des virtuellen Computers verwenden ausgeführt, selbst wenn andere R-Code der SQL Server-computekontext ohne Probleme verwendet.

So aktivieren Sie den Zugriff auf R-Services von remoten Data Science-Clients:

1. Öffnen Sie auf dem virtuellen Computer die Windows-Firewall mit erweiterter Sicherheit.
2. Wählen Sie **Ausgehende Regeln** aus.
3. Deaktivieren Sie die folgende Regel:
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
### <a name="enable-odbc-callbacks-for-remote-clients"></a>ODBC-Rückrufe für Remoteclients aktivieren

Wenn Sie erwarten, dass R-Clients, die den Server aufrufen, ODBC-Anfragen als Teil ihrer R-Lösungen ausstellen, müssen Sie sicherstellen, dass das Launchpad ODBC-Aufrufe für den Remoteclient ausführen kann. Zu diesem Zweck müssen Sie die SQL-Workerkonten zulassen, die vom Launchpad für die Anmeldung bei der Instanz verwendet werden.
Weitere Informationen finden Sie unter [Einrichten von SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).

### <a name="network"></a>Hinzufügen von Netzwerkprotokollen

+ Aktivieren von Named Pipes
  
  Derzeit verwendet [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] das Named Pipes-Protokoll für Verbindungen zwischen dem Client und den Servercomputern und für einige externe Verbindungen. Wenn Named Pipes nicht aktiviert ist, müssen Sie es jeweils auf dem virtuellen Azure-Computer und auf alle Data Science-Clients installieren und aktivieren, die eine Verbindung mit dem Server herstellen.
  
+ Aktivieren von TCP/IP

  TCP/IP ist für Loopbackverbindungen zu SQL Server R Services erforderlich. Wenn Sie die folgende Fehlermeldung angezeigt, aktivieren Sie TCP/IP auf dem virtuellen Computer, die die Instanz unterstützt:

  "DBNETLIB; SQL Server ist nicht vorhanden oder der Zugriff verweigert"

## <a name="how-to-disable-r-services-on-an-instance"></a>So deaktivieren Sie R Services auf einer Instanz

Sie können ebenso die Funktion auf einem vorhandenen virtuellen Computer jederzeit aktivieren oder deaktivieren.

1. Öffnen des Blatts „Virtueller Computer“
2. Klicken Sie auf **Einstellungen**, und wählen Sie **SQL Server-Konfiguration** aus.

## <a name="existing"></a>Hinzufügen von SQL Server R Services zu einer vorhandenen SQL Server 2016 Enterprise virtuellen Maschine

Wenn Sie einen virtuellen Azure-Computer, der R-Services nicht enthält erstellt, können Sie die Funktion hinzufügen, durch die folgenden Schritte:

1. Führen Sie erneut das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Setup aus, und fügen Sie die Funktion auf der Seite **Serverkonfiguration** des Assistenten hinzu.
2. Aktivieren Sie die Ausführung des externen Skripts, und starten Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz erneut. Weitere Informationen finden Sie unter [Einrichten von SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).
3. (Optional) Konfigurieren Sie bei Bedarf den Datenbankzugriff für R-Workerkonten für die remote Skriptausführung.
   Weitere Informationen finden Sie unter [Einrichten von SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).
3. (Optional) Ändern Sie eine Firewallregel auf dem virtuellen Azure-Computer, wenn Sie beabsichtigen, die R-Skriptausführung von remoten Data Science-Clients zu ermöglichen. Weitere Informationen finden Sie unter [Aufhebung der Firewallblockierung](#firewall).
4. Installieren oder Aktivieren von erforderlichen Netzwerkbibliotheken. Weitere Informationen finden Sie unter [Hinzufügen von Netzwerkprotokollen](#network).

## <a name="related-resources"></a>Verwandte Ressourcen

[Einrichten von SQL Server R Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

