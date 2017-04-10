---
title: "Herstellen einer Verbindung mit dem Datenbankmodul unter Verwendung von Erweiterter Schutz | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Spoofingangriffe"
  - "Dienstbindung"
  - "Lockangriffe"
  - "SChannel"
  - "Kanalbindung"
  - "Erweiterter Schutz"
ms.assetid: ecfd783e-7dbb-4a6c-b5ab-c6c27d5dd57f
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Herstellen einer Verbindung mit dem Datenbankmodul unter Verwendung von Erweiterter Schutz
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Erweiterter Schutz **wird von** ab [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]unterstützt. **Erweiterter Schutz für die Authentifizierung** ist eine Funktion der vom Betriebssystem implementierten Netzwerkkomponenten. **Erweiterter Schutz** wird in Windows 7 und Windows Server 2008 R2 unterstützt. **Erweiterter Schutz** ist in Service Packs für ältere [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Betriebssystemen enthalten. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist sicherer, wenn Verbindungen möglichst mithilfe des **erweiterten Schutzes**hergestellt werden.  
  
> [!IMPORTANT]  
>  **Erweiterter Schutz** ist in Windows standardmäßig nicht aktiviert. Informationen zum Aktivieren von **Erweiterter Schutz** in Windows finden Sie unter [Erweiterter Schutz für die Authentifizierung](http://support.microsoft.com/kb/968389).  
  
## Beschreibung von "Erweiterter Schutz"  
 **Erweiterter Schutz** nutzt die Dienstbindung und die Kanalbindung, um Relayangriffe während der Authentifizierung zu verhindern. Bei einem Relayangriff während der Authentifizierung stellt ein Client, der in der Lage ist, NTLM-Authentifizierungen auszuführen (z. B. Windows-Explorer, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Outlook, eine .NET SqlClient-Anwendung usw.), eine Verbindung mit einem Angreifer her (z. B. einem feindlichen CIFS-Dateiserver). Der Angreifer verwendet die Anmeldeinformationen des Clients, um sich als der Client auszugeben und sich bei einem Dienst (z. B. einer Instanz des [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Diensts) zu authentifizieren.  
  
 Der Angriff kann auf zwei Arten erfolgen:  
  
-   Bei einem "Lockangriff" wird der Client dazu verleitet, freiwillig eine Verbindung mit dem Angreifer herzustellen.  
  
-   Bei einem Spoofingangriff beabsichtigt der Client, eine Verbindung mit einem gültigen Dienst herzustellen, bemerkt jedoch nicht, dass DNS und/oder IP-Routing manipuliert wurden, um die Verbindung an den Angreifer umzuleiten.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trägt mithilfe der Dienstbindung und Kanalbindung dazu bei, solche Angriffe auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen zu reduzieren.  
  
### Dienstbindung  
 Bei der Dienstbindung werden Lockangriffe dadurch verhindert, dass ein Client einen signierten Dienstprinzipalnamen (Service Principal Name, SPN) des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Diensts senden muss, mit dem der Client eine Verbindung herstellen möchte. Der Dienst überprüft als Teil der Authentifizierungsantwort, ob der im Paket empfangene SPN mit seinem eigenen SPN übereinstimmt. Wenn ein Client verleitet wird, eine Verbindung mit einem Angreifer herzustellen, sendet der Client den signierten SPN des Angreifers. Der Angreifer kann das Paket nicht übertragen, um sich beim echten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienst als Client zu authentifizieren, weil das Paket den SPN des Angreifers enthält. Bei der Dienstbindung fallen einmalig unwesentliche Kosten an, allerdings bietet sie keinen Schutz vor Spoofingangriffen. Dienstbindung tritt auf, wenn eine Clientanwendung keine Verschlüsselung verwendet, um eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herzustellen.  
  
### Kanalbindung  
 Bei der Kanalbindung wird zwischen einem Client und einer Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Diensts ein sicherer Kanal (SChannel) eingerichtet. Der Dienst überprüft die Echtheit des Clients, indem er das für den jeweiligen Kanal spezifische Kanalbindungsbindungstoken (Channel Binding Token, CBT) des Clients mit dem eigenen CBT vergleicht. Durch die Kanalbindung werden sowohl Lock- als auch Spoofingangriffe unterbunden. Diese Methode verursacht jedoch höhere Laufzeitkosten, da TLS (Transport Layer Security)-Verschlüsselung für den gesamten Sitzungsdatenverkehr erforderlich ist. Kanalbindung tritt auf, wenn eine Clientanwendung Verschlüsselungen verwendet, um eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herzustellen – unabhängig davon, ob Verschlüsselungen vom Client oder dem Server erzwungen werden.  
  
> [!WARNING]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[msCoName](../../includes/msconame-md.md)] -Datenanbieter für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützen TLS 1.0 und SSL 3.0. Wenn Sie ein anderes Protokoll (beispielsweise TLS 1.1 oder TLS 1.2) erzwingen, indem Sie Änderungen an der SChannel-Betriebssystemebene vornehmen, können Sie möglicherweise keine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herstellen.  
  
### Betriebssystemunterstützung  
 Die folgenden Links enthalten weitere Informationen dazu, wie **Erweiterter Schutz**von Windows unterstützt wird:  
  
-   [Integrierte Windows-Authentifizierung unter Verwendung von "Erweiterter Schutz" (möglicherweise auf Englisch)](http://msdn.microsoft.com/library/dd639324.aspx)  
  
-   [Microsoft-Sicherheitsempfehlung (973811): Erweiterter Schutz für die Authentifizierung (möglicherweise auf Englisch)](http://www.microsoft.com/technet/security/advisory/973811.mspx)  
  
## Einstellungen  
 Es gibt drei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verbindungseinstellungen, die sich auf die Dienstbindung und die Kanalbindung auswirken. Die Einstellungen können mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager oder der Windows-Verwaltungsinstrumentation konfiguriert und mithilfe des Facets **Serverprotokolleinstellung** der richtlinienbasierten Verwaltung angezeigt werden.  
  
-   **Erzwingen der Verschlüsselung**  
  
     Mögliche Werte sind **Ein** und **Aus**. Zur Verwendung der Kanalbindung muss **Verschlüsselung erzwingen** auf **Ein**festgelegt werden, sodass die Verschlüsselung auf allen Clients erzwungen wird. Bei der Einstellung **Aus**wird nur die Dienstbindung gewährleistet. **Verschlüsselung erzwingen** befindet sich im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager unter **Protokolle für MSSQLSERVER-Eigenschaften (Registerkarte „Flags“)**.  
  
-   **Erweiterter Schutz**  
  
     Mögliche Werte sind **Aus**, **Zulässig**und **Erforderlich**. Mit der Variablen **Erweiterter Schutz** können Benutzer die Ebene für **Erweiterter Schutz** für jede [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz konfigurieren. **Erweiterter Schutz** befindet sich im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager unter **Protokolle für MSSQLSERVER-Eigenschaften** (Registerkarte „Erweitert“).  
  
    -   Bei der Einstellung **Aus**ist **Erweiterter Schutz** deaktiviert. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz akzeptiert Verbindungen von jedem beliebigen Client, unabhängig davon, ob er geschützt ist oder nicht. **Aus** ist mit älteren und nicht gepatchten Betriebssystemen kompatibel, bietet aber weniger Sicherheit. Verwenden Sie diese Einstellung, wenn Sie wissen, dass die Clientbetriebssysteme keinen erweiterten Schutz unterstützen.  
  
    -   Bei der Einstellung **Zulässig**wird **Erweiterter Schutz** für Verbindungen von Betriebssystemen vorausgesetzt, die die Funktion **Erweiterter Schutz**unterstützen. Bei Verbindungen von Betriebssystemen, die**Erweiterter Schutz** nicht unterstützen, wird die Funktion **Erweiterter Schutz**ignoriert. Verbindungen von ungeschützten Clientanwendungen, die auf geschützten Clientbetriebssystemen ausgeführt werden, werden abgelehnt. Diese Einstellung ist sicherer als **Aus**, bietet jedoch nicht die höchste Sicherheit. Verwenden Sie diese Einstellung in gemischten Umgebungen, in denen einige Betriebssysteme die Funktion **Erweiterter Schutz** unterstützen, einige jedoch nicht.  
  
    -   Bei der Einstellung **Erforderlich**werden nur Verbindungen von geschützten Anwendungen auf geschützten Betriebssystemen akzeptiert. Dies ist die sicherste Einstellung. Von Betriebssystemen oder Anwendungen, die die Funktion **Erweiterter Schutz** nicht unterstützen, können jedoch keine Verbindungen mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt werden.  
  
-   **Akzeptierte NTLM-SPNs**  
  
     Die Variable **Akzeptierte NTLM-SPNs** wird benötigt, wenn ein Server durch mehr als einen SPN identifiziert wird. Wenn ein Client versucht, mithilfe eines gültigen, dem Server nicht bekannten SPNs eine Verbindung mit dem Server herzustellen, verursacht die Dienstbindung einen Fehler. Um dieses Problem zu vermeiden, können Benutzer mithilfe von **Akzeptierte NTLM-SPNs**mehrere SPNs für den Server angeben. **Akzeptierte NTLM-SPNs** umfasst eine Reihe durch Semikolons getrennter SPNs. Beispiel: Um die Verwendung der SPNs **MSSQLSvc/ HostName1.Contoso.com** und **MSSQLSvc/ HostName2.Contoso.com** zuzulassen, geben Sie im Feld **Akzeptierte NTLM-SPNs** die Zeichenfolge **MSSQLSvc/HostName1.Contoso.com;MSSQLSvc/HostName2.Contoso.com** ein. Die maximale Länge der Variablen beträgt 2.048 Zeichen. **Akzeptierte NTLM-SPNs** befindet sich im [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Konfigurations-Manager unter **Protokolle für MSSQLSERVER-Eigenschaften (Registerkarte „Erweitert“)**.  
  
## Aktivieren von "Erweiterter Schutz" für das Datenbankmodul  
 Zur Verwendung von **Erweiterter Schutz**benötigen sowohl der Server als auch der Client ein Betriebssystem, das **Erweiterter Schutz**unterstützt, und die Funktion **Erweiterter Schutz** muss für das Betriebssystem aktiviert sein. Weitere Informationen zum Aktivieren von **Erweiterter Schutz** für das Betriebssystem finden Sie unter [Erweiterter Schutz für die Authentifizierung](http://support.microsoft.com/kb/968389).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Erweiterter Schutz **wird von** ab [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]unterstützt. Für einige frühere**-Versionen wird** Erweiterter Schutz [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in zukünftigen Updates verfügbar sein. Nachdem Sie **Erweiterter Schutz** auf dem Servercomputer aktiviert haben, führen Sie die folgenden Schritte aus, um **Erweiterter Schutz**zu aktivieren:  
  
1.  Zeigen Sie im Menü **Start** auf **Alle Programme**, zeigen Sie auf **Microsoft SQL Server** , und klicken Sie dann auf **SQL Server-Konfigurations-Manager**.  
  
2.  Erweitern Sie **SQL Server-Netzwerkkonfiguration**, klicken Sie mit der rechten Maustaste auf **Protokolle für** *\<*Instanzname*>*, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Legen Sie sowohl für die Kanalbindung als auch für die Dienstbindung auf der Registerkarte **Erweitert** die geeignete Einstellung für die Funktion **Erweiterter Schutz** fest.  
  
4.  Wenn ein Server durch mehr als einen SPN identifiziert wird, konfigurieren Sie auf der Registerkarte **Erweitert** optional das Feld **Akzeptierte NTLM-SPNs** , wie im Abschnitt "Einstellungen" beschrieben.  
  
5.  Legen Sie für die Kanalbindung auf der Registerkarte **Flags** die Einstellung **Verschlüsselung erzwingen** auf **Ein**fest.  
  
6.  Starten Sie den [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Dienst neu.  
  
## Konfigurieren anderer SQL Server-Komponenten  
 Weitere Informationen zur Konfiguration von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] finden Sie unter [Extended Protection for Authentication with Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md) (Erweiterter Schutz für die Authentifizierung mit Reporting Services).  
  
 Wenn IIS verwendet wird, um über eine HTTP- oder HTTPS-Verbindung auf [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]-Daten zuzugreifen, kann [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] den von IIS bereitgestellten erweiterten Schutz nutzen. Weitere Informationen dazu, wie IIS für die Verwendung des erweiterten Schutzes konfiguriert wird, finden Sie unter [Konfigurieren von "Erweiterter Schutz" in IIS 7.5](http://go.microsoft.com/fwlink/?LinkId=181105)(möglicherweise auf Englisch).  
  
## Siehe auch  
 [Server-Netzwerkkonfiguration](../../database-engine/configure-windows/server-network-configuration.md)   
 [Client-Netzwerkkonfiguration](../../database-engine/configure-windows/client-network-configuration.md)   
 [Übersicht über den erweiterten Schutz für die Authentifizierung (möglicherweise auf Englisch)](http://go.microsoft.com/fwlink/?LinkID=177943)   
 [Integrierte Windows-Authentifizierung unter Verwendung von "Erweiterter Schutz" (möglicherweise auf Englisch)](http://go.microsoft.com/fwlink/?LinkId=179922)  
  
  