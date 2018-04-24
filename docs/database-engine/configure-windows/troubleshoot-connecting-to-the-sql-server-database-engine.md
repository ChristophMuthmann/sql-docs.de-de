---
title: Beheben von Verbindungsfehlern mit dem SQL Server-Datenbankmodul | Microsoft-Dokumentation
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- troubleshooting, connecting to Database Engine
- connecting to Database Engine, troubleshooting
ms.assetid: 474c365b-c451-4b07-b636-1653439f4b1f
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: e2879b9962e7244afb47ec0270f70a7742b46bda
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="troubleshoot-connecting-to-the-sql-server-database-engine"></a>Beheben von Verbindungsfehlern mit dem SQL Server-Datenbankmodul
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Dies ist eine Liste der Problembehandlungstechniken, die verwendet werden, wenn Sie keine Verbindung mit dem SQL Server-Datenbankmodul herstellen können. Diese Schritte beginnen nicht mit den häufigsten Problemen, auf die Sie sicher schon geprüft haben. Stattdessen beginnen sie mit den grundlegendsten Problemen und arbeitet sich vor bis hin zu komplexeren Problemen. Diese Schritte sind in der Reihenfolge von den grundlegendsten Problemen bis hin zu den komplexeren. Diese Schritte setzen voraus, dass Sie von einem anderen Computer aus eine Verbindung mit SQL Server herstellen, indem Sie das TCP/IP-Protokoll verwenden was am weit verbreitetsten ist. Diese Schritte wurden für SQL Server 2016 geschrieben, wobei jeweils der SQL Server als auch die Clientanwendungen unter Windows 10 laufen. Jedoch können Sie die Schritte in der Regel mit anderen Versionen von SQL Server und anderen Betriebssystemen ausführen. Dafür sind nur kleine Änderungen notwendig.

Diese Anweisungen sind besonders für die Problembehandlung des Fehlers „**Verbinden mit dem Server**“ nützlich, der die Fehlernummer 11001 (oder 53) besitzen kann, den Schweregrad 20, den Status 0 sowie Fehlermeldungen wie:

*   „Netzwerkbezogener oder instanzspezifischer Fehler beim Herstellen einer Verbindung mit SQL Server. Der Server wurde nicht gefunden, oder auf ihn kann nicht zugegriffen werden. Überprüfen Sie, ob der Instanzname richtig ist und ob SQL Server Remoteverbindungen zulässt. " 

*   „(Anbieter: Named Pipes-Anbieter, Fehler: 40 – Es konnte keine Verbindung mit SQL Server hergestellt werden) (Microsoft SQL Server, Error: 53)“ oder „(Anbieter: TCP-Anbieter, Fehler: 0 – Der angegebene Host ist unbekannt.) (Microsoft SQL Server, Error: 11001)“ 

Dieser Fehler bedeutet normalerweise, dass der SQL Server-Computer nicht gefunden werden kann oder die TCP-Portnummer entweder nicht bekannt ist, die Portnummer falsch ist, oder die Portnummer von einer Firewall blockiert wird.

>  [!TIP]
>  Eine interaktive Seite zur Problembehebung im [!INCLUDE[msCoName_md](../../includes/msconame-md.md)]-Kundendienst unter [Solving Connectivity errors to SQL Server (Lösen von Verbindungsproblemen zu SQL Server)](https://support.microsoft.com/help/4009936/solving-connectivity-errors-to-sql-server) verfügbar.

### <a name="not-included"></a>Nicht enthalten

* Dieses Thema enthält keine Informationen zu SSPI-Fehlern. SSPI-Fehler finden Sie unter [Problembehandlung bei der Fehlermeldung "SSPI-Kontext kann nicht generiert werden"](http://support.microsoft.com/kb/811889).  
* Dieses Thema enthält keine Informationen zu Kerberos-Fehlern. Hilfe finden Sie im [Microsoft Kerberos-Konfigurations-Manager für SQL Server](http://www.microsoft.com/download/details.aspx?id=39046).
* Dieses Thema enthält keine Informationen zur SQL Azure-Verbindung. Hilfe finden Sie unter [Troubleshooting connectivity issues with Microsoft Azure SQL Database (Problembehandlung bei Verbindungsproblemen mit Microsoft Azure SQL-Datenbank)](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database). 

## <a name="gathering-information-about-the-instance-of-sql-server"></a>Sammeln von Informationen über die SQL Server-Instanz

Zunächst müssen Sie grundlegende Informationen über das Datenbankmodul sammeln.

1. Bestätigen Sie, dass die Instanz des SQL Server-Datenbankmoduls installiert ist und ausgeführt wird.
    1.  Melden Sie sich auf dem Hostcomputer der SQL Server-Instanz an.
    2.  Starten Sie den SQL Server-Konfigurations-Manager. (Der Konfigurations-Manager wird automatisch auf dem Computer installiert, wenn SQL Server installiert ist. Anweisungen zum Starten des Konfigurations-Managers variieren geringfügig, je nach SQL Server- und Windows-Version.) Hilfe zum Starten des Konfigurations-Managers finden Sie unter [SQL Server Konfigurations-Manager](../../relational-databases/sql-server-configuration-manager.md).)
    3.  Wählen Sie im Konfigurations-Manager im linken Bereich **SQL Server-Dienste**aus. Bestätigen Sie im rechten Bereich, dass die Instanz des Datenbankmoduls vorhanden ist und ausgeführt wird. Eine Instanz namens **SQL Server (MSSQLSERVER)** ist eine standardmäßige (unbenannte) Instanz. Es kann nur eine Standardinstanz vorhanden sein. Die Namen der anderen (benannten) Instanzen sind zwischen den Klammern aufgelistet. SQL Server Express verwendet den Namen **SQL Server (SQLEXPRESS)** als den Instanznamen, es sei denn, er wurde während der Installation umbenannt. Notieren Sie sich den Namen der Instanz, zu der Sie eine Verbindung herstellen möchten. Bestätigen Sie außerdem, dass die Instanz ausgeführt wird, indem Sie auf den grünen Pfeil achten. Wenn die Instanz ein rotes Quadrat besitzt, klicken Sie mit der rechten Maustaste auf die Instanz, und klicken Sie anschließend auf **Start**. Das Quadrat sollte nun grün sein.
     4. Wenn Sie versuchen, eine Verbindung zu einer benannten Instanz herzustellen, stellen Sie sicher, dass der SQL Server-Browserdienst ausgeführt wird.
 

2.  Rufen Sie die IP-Adresse des Computers ab.
    1. Klicken Sie im Startmenü auf **Ausführen**. Geben Sie im Fenster **Ausführen** **cmd**ein, und klicken Sie anschließend auf **OK**.
    2.  Geben Sie im Eingabeaufforderungsfenster **ipconfig** ein, und drücken Sie die EINGABETASTE. Notieren Sie sich die **IPv4** Adresse und die **IPv6** Adresse. (SQL Server kann eine Verbindung mit dem alten Protokoll IP Version 4 oder dem neueren Protokoll IP Version 6 herstellen. Ihr Netzwerk kann eine oder beide Möglichkeiten zulassen. Die meisten Benutzer fangen an, indem sie die Probleme der **IPv4** -Adresse behandeln. Dies ist kürzer und leichter einzugeben.)


3.  Abrufen der von SQL Server verwendeter TCP-Portnummer In den meisten Fällen stellen Sie eine Verbindung zum Datenbankmodul von einem anderen Computer aus her, der das TCP-Protokoll verwendet.
    1.  Verwenden Sie SQL Server Management Studio auf dem Computer, auf dem SQL Server ausgeführt wird, und stellen Sie eine Verbindung mit SQL Server her. Erweitern Sie im Objekt-Explorer **Management**und **SQL Server-Protokolle**, und doppelklicken Sie auf das aktuelle Protokoll.
    2.  Klicken Sie im Protokoll-Viewer auf der Symbolleiste auf die Schaltfläche **Filter** . Tippen Sie im Feld **Meldung enthält Text** **server is listening on**, klicken Sie auf **Filter anwenden**und anschließend auf **OK**.
    3.  Eine ähnliche Meldung **server is listening on ['beliebig' \<ipv4> 1433]** sollte aufgelistet sein. Diese Meldung gibt an, dass diese Instanz von SQL Server an alle IP-Adressen auf diesen Computer (für IP-Version 4) lauscht sowie an den TCP-Port 1433. (TCP-Port 1433 ist in der Regel der Port, der vom Datenbankmodul verwendet wird. Nur eine Instanz von SQL Server kann einen Port verwenden. Falls also mehr als eine Instanz von SQL Server installiert ist, müssen einige Instanzen andere Portnummern verwenden.) Notieren Sie sich die von der Instanz von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] verwendete Portnummer, zu der Sie eine Verbindung herstellen möchten. 

    >    [!NOTE] 
    >    Die IP-Adresse 127.0.0.1 ist möglicherweise aufgelistet. Sie heißt Loopbackadapter-Adresse und kann nur von einem Prozess auf demselben Computer eine Verbindung herstellen. Sie kann für die Problembehandlung nützlich sein, aber Sie können diese Adresse nicht für Verbindungen von einem anderen Computer aus verwenden.

## <a name="enable-protocols"></a>Aktivieren von Protokollen

Bei einigen Installationen von SQL Server ist die Verbindung zum Datenbankmodul von einem anderen Computer aus nicht aktiviert, es sei denn, ein Administrator verwendet den Konfigurations-Manager, um die Verbindung zu aktivieren. So aktivieren Sie Verbindungen von einem anderen Computer:

1.  Öffnen Sie den SQL Server-Konfigurations-Manager, wie zuvor beschrieben. 
2.  Erweitern Sie im linken Bereich des Konfigurations-Managers **SQL Server-Netzwerkkonfiguration**, und wählen Sie anschließend die SQL Server-Instanz, mit der Sie eine Verbindung herstellen möchten. Der rechte Bereich listet die verfügbaren Verbindungsprotokolle auf. Shared Memory ist in der Regel aktiviert. Es kann nur auf demselben Computer verwendet werden, deshalb haben die meisten Installationen Shared Memory aktiviert. Sie verwenden in der Regel TCP/IP, um eine Verbindung mit SQL Server von einem anderen Computer aus herzustellen. Falls TCP/IP nicht aktiviert ist, klicken Sie mit der rechten Maustaste auf **TCP/IP**und anschließend auf **Aktivieren**. 
3.  Falls Sie die Aktivierungseinstellung für ein Protokoll geändert haben, müssen Sie das Datenbankmodul erneut starten. Wählen Sie im linken Bereich **SQL Server-Dienste**aus. Klicken Sie im rechten Bereich mit der rechten Maustaste auf die Instanz des Datenbankmoduls, und klicken Sie anschließend auf **Neu starten**. 

## <a name="testing-tcpip-connectivity"></a>Testen der TCP/IP-Konnektivität

Das Herstellen einer Verbindung mit SQL Server über TCP/IP erfordert, dass Windows die Verbindung herstellen kann. Verwenden Sie das `ping` -Tool zum Testen von TCP.
1.  Klicken Sie im Startmenü auf **Ausführen**. Geben Sie im Fenster **Ausführen** **cmd**ein, und klicken Sie anschließend auf **OK**. 
2.  Geben Sie im Eingabeaufforderungsfenster `ping` ein, und anschließend die IP-Adresse des Computers, auf dem SQL Server ausgeführt wird. Beispielsweise `ping 192.168.1.101` mit einer IPv4-Adresse oder `ping fe80::d51d:5ab5:6f09:8f48%11` mit einer IPv6-Adresse. (Sie müssen die Zahlen nach ping mit den IP-Adressen auf Ihrem Computer ersetzen, die Sie zuvor gesammelt haben.) 
3.  Wenn das Netzwerk richtig konfiguriert ist, erhalten Sie eine Antwort wie z.B. **Antwort von \<IP-Adresse>**, gefolgt von einigen zusätzlichen Informationen. Wenn Sie eine Fehlermeldung, wie z.B. **Zielhost nicht erreichbar.** oder **Timeout für die Sperranforderung** erhalten, dann ist TCP/IP nicht ordnungsgemäß konfiguriert. (Überprüfen Sie, ob die IP-Adresse richtig ist und richtig eingegeben wurde.) An diesem Punkt können Fehler auf ein Problem mit dem Clientcomputer oder dem Servercomputer hindeuten, oder dass etwas mit dem Netzwerk, z.B. dem Router, nicht in Ordnung ist. Das Internet bietet viele Ressourcen für die Problembehandlung bei TCP/IP. Ein guter Anfang ist der Artikel aus dem Jahr 2006 [Chapter 16 – Troubleshooting TCP/IP](http://support.microsoft.com/kb/169790)(Kapitel 16 – Problembehebung von TCP/IP).
4.  Wenn der Ping-Test mithilfe der IP-Adresse erfolgreich war, überprüfen Sie, ob der Computername in einer TCP/IP-Adresse aufgelöst wird. Geben Sie im Eingabeaufforderungsfenster auf dem Clientcomputer `ping` ein, und anschließend den Computernamen, auf dem SQL Server ausgeführt wird. Beispielsweise `ping newofficepc` 
5.  Wenn Sie die IP-Adresse mit dem Ping-Befehl erreichen konnten, aber jetzt eine Fehlermeldung wie **Zielhost nicht erreichbar** oder **Timeout für die Sperranforderung** erhalten, besitzen Sie möglicherweise alte (veraltete) Namensauflösungsinformationen, die auf dem Clientcomputer zwischengespeichert sind. Tippen Sie `ipconfig /flushdns` ein, um den DNS-Cache (Dynamic Name Resolution) zu leeren. Pingen Sie den Computer anschließend mithilfe des Namens erneut an. Der Clientcomputer sucht mit dem geleerten DNS-Cache nach den neuesten Informationen zu der IP-Adresse für den Servercomputer. 
6.  Wenn das Netzwerk richtig konfiguriert ist, erhalten Sie eine Antwort wie z.B. **Antwort von \<IP-Adresse>**, gefolgt von einigen zusätzlichen Informationen. Wenn Sie den Servercomputer erfolgreich mit der IP-Adresse pingen können, jedoch einen Fehler wie **Zielhost nicht erreichbar.** oder **Timeout für die Sperranforderung** erhalten, wenn Sie nach Computername gepingt haben, ist die Namensauflösung nicht korrekt konfiguriert. (Weitere Informationen finden Sie im Artikel aus dem Jahr 2006, der zuvor erwähnt wurde, [Chapter 16 – Troubleshooting TCP/IP](http://support.microsoft.com/kb/169790) (Kapitel 16 – Problembehebung von TCP/IP).) Die erfolgreiche Namensauflösung ist für die Verbindung mit SQL Server nicht erforderlich, aber wenn der Computername zu einer IP-Adresse aufgelöst werden kann, müssen die Verbindungen mit Angabe der IP-Adresse hergestellt werden. Dies ist nicht ideal, aber die Namensauflösung kann später korrigiert werden.
  
  
## <a name="testing-a-local-connection"></a>Testen einer lokalen Verbindung

Überprüfen Sie vor der Problembehandlung eines Verbindungsproblems von einem anderen Computer zunächst, ob Sie eine Verbindung von einer Clientanwendung aus herstellen können, die auf dem Computer installiert ist, der SQL Server ausführt. (Dadurch können keine Probleme mit der Firewall auftreten) Dieses Verfahren verwendet SQL Server Management Studio. Wenn Sie Management Studio nicht installiert haben, besuchen Sie das [Download Center von SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md). (Wenn Sie Management Studio nicht installieren können, können Sie die Verbindung mithilfe des Hilfsprogramms `sqlcmd.exe` überprüfen, die mit dem Datenbankmodul installiert sind. Weitere Informationen zu `sqlcmd.exe`finden Sie unter [sqlcmd (Hilfsprogramm)](../../tools/sqlcmd-utility.md).)
1.  Melden Sie sich mithilfe eines Anmeldenamens, der über Zugriffsberechtigung für SQL Server verfügt, auf dem Computer an, auf dem SQL Server installiert ist. (Während der Installation benötigt SQL Server mindestens einen Anmeldenamen, der als SQL Server-Administrator angegeben ist. Wenn Ihnen kein Administrator bekannt ist, gehen Sie unter [Herstellen einer Verbindung mit SQL Server, wenn Systemadministratoren gesperrt sind](http://msdn.microsoft.com/library/dd207004.aspx).)
2.   Tippen Sie auf der Startseite oder auf älteren Versionen von Windows im Startmenü **SQL Server Management Studio**ein, zeigen Sie auf **Alle Programme**und anschließend auf **Microsoft SQL Server**, und klicken Sie anschließend auf **SQL Server Management Studio**.
3.  Wählen Sie im Dialogfeld **Verbindung mit Server herstellen** , im Feld **Server** die Option **Datenbankmodul**aus. Wählen Sie im Feld **Authentifizierung** die Option **Windows-Authentifizierung**. Geben Sie im Feld **Servername** eine der folgenden Möglichkeiten ein:

|Verbinden mit:|Typ:|Beispiel:|
|-----------------|---------------|-----------------|
|Standardinstanz|Der Computername|ACCNT27|
|Benannte Instanz|Der Computername\Instanzname|ACCNT27\PAYROLL|

>  [!NOTE] 
>  Bei der Verbindung mit einem SQL Server von einer Clientanwendung auf dem gleichen Computer wird das Shared Memory-Protokoll verwendet. Shared Memory ist ein Typ einer lokalen Named Pipe. Manchmal treten jedoch Fehler bezüglich der Pipes auf.

Wenn Sie zu diesem Zeitpunkt eine Fehlermeldung erhalten, müssen Sie den Fehler beheben, bevor Sie fortfahren. Viele Dinge könnten ein Problem darstellen. Ihr Anmeldename ist möglicherweise nicht autorisiert, eine Verbindung herzustellen. Möglicherweise ist Ihre Standarddatenbank nicht vorhanden.

>    [!NOTE] 
>    Einige Fehlermeldungen, die absichtlich an den Client übergeben wurden, stellen nicht genügend Informationen bereit, wie das Problem behoben werden kann. Dies ist eine Sicherheitsfunktion, die verhindern soll, dass Informationen über SQL Server an einen Angreifer übermittelt werden. Sehen Sie sich das SQL Server-Fehlerprotokoll an, um alle Informationen über den Fehler anzuzeigen. Dort finden Sie die Einzelheiten. Wenn Sie den Fehler **18456 Fehler bei der Anmeldung für den Benutzer**erhalten, sehen Sie sich das Thema [MSSQLSERVER_18456](http://msdn.microsoft.com/library/cc645917) in der Onlinedokumentation an, um weitere Informationen über Fehlercodes zu erhalten. Auf Aaron Bertrands Blog unter [Troubleshooting Error 18456](http://www2.sqlblog.com/blogs/aaron_bertrand/archive/2011/01/14/sql-server-v-next-denali-additional-states-for-error-18456.aspx)(Problembehandlung von Error 18456) finden Sie ebenso eine umfangreiche Liste mit Fehlercodes. Sie können das Fehlerprotokoll mit SSMS (falls Sie eine Verbindung herstellen können) im Abschnitt „Verwaltung“ des Objekt-Explorers anzeigen. Andernfalls können Sie das Fehlerprotokoll mit dem Windows-Editor anzeigen. Der standardmäßige Speicherort variiert je nach Version und kann während des Setups geändert werden. Der Standardspeicherort für [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] ist `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log\ERRORLOG`.  

4.   Wenn Sie keine Verbindung mithilfe von Shared Memory herstellen können, versuchen Sie eine Verbindung mithilfe von TCP herzustellen. Sie können eine TCP-Verbindung durch Angabe von **tcp:** vor dem Namen erzwingen. Zum Beispiel:

|Verbinden mit:|Typ:|Beispiel:|
|-----------------|---------------|-----------------|
|Standardinstanz|tcp: der Computername|tcp:ACCNT27|
|Benannte Instanz|tcp: der Computername\Instanzname|tcp:ACCNT27\PAYROLL|
  
Wenn Sie zwar mit Shared Memory eine Verbindung herstellen können, jedoch nicht mit TCP, müssen Sie das TCP-Problem beheben. Am wahrscheinlichsten ist es, dass TCP nicht aktiviert ist. Gehen Sie zu den Schritten **Aktivieren von Protokollen** weiter oben, um TCP zu aktivieren.

5.   Wenn Sie sich mit einem anderen Konto als mit dem Administratorkonto verbinden möchten, versuchen Sie, erneut eine Verbindung herzustellen. Dazu verwenden Sie die Windows-Authentifizierungsanmeldung oder die SQL Server-Authentifizierungsanmeldung, die von der Clientanwendung verwendet werden wird.

## <a name="opening-a-port-in-the-firewall"></a>Öffnen eines Ports in der Firewall

Vor vielen Jahren wurde die Windows-Firewall auf Windows XP Service Pack 2 aktiviert und blockiert Verbindungen von einem anderen Computer. Sie müssen auf dem SQL Server-Computer die Firewall so konfigurieren, dass sie Verbindungen zum TCP-Port zulässt, der vom Datenbankmodul verwendet wird, um eine Verbindung mithilfe vom TCP/IP von einem anderen Computer herzustellen. Wie bereits erwähnt, lauscht die Standardinstanz in der Regel auf TCP-Port 1433. Wenn Sie über benannte Instanzen verfügen oder die Standardeinstellung geändert haben, lauscht der [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] -TCP-Port möglicherweise auf einem anderen Port. Informationen zum Erfassen von Informationen zum Ermitteln des Ports finden Sie im einleitenden Abschnitt.  
Wenn Sie eine Verbindung zu einer benannten Instanz oder einem anderen Port als TCP-Port 1433 herstellen, müssen Sie auch den UDP-Port 1434 für den SQL Server-Browserdienst öffnen. Eine Schritt-für-Schritt-Anleitung zum Öffnen eines Ports in der Windows-Firewall finden Sie unter [Konfigurieren einer Windows-Firewall für Datenbankmodulzugriff](https://msdn.microsoft.com/library/ms175043).

## <a name="testing-the-connection"></a>Testen der Verbindung

Wenn Sie eine Verbindung mithilfe von TCP auf dem gleichen Computer herstellen können, dann ist es an der Zeit, eine Verbindung vom Clientcomputer herzustellen. Theoretisch können Sie jede beliebige Clientanwendung verwenden. Um jedoch zusätzliche Komplexität zu vermeiden, installieren Sie die SQL Server Management-Tools auf dem Client, und führen Sie einen Versuch mit SQL Server Management Studio durch.

1. Versuchen Sie auf dem Client-Computer mit SQL Server Management Studio, eine Verbindung über die IP-Adresse und die TCP-Portnummer im Format „IP-Adresse, Komma (,), Portnummer“ herzustellen. Zum Beispiel **192.168.1.101,1433** . Wenn dies nicht funktioniert, haben Sie wahrscheinlich eines der folgenden Probleme:

    * **Ping** der IP-Adresse funktioniert nicht, was ein allgemeines TCP-Konfigurationsproblem darstellt. Wechseln Sie zurück zum Abschnitt **Testen der TCP/IP-Konnektivität**. 
    *   Das TCP-Protokoll ist für SQL Server nicht aktiviert. Wechseln Sie zurück zum Abschnitt **Aktivieren von Protokollen**. 
    *   SQL Server lauscht an einen anderen Port als den Port, die Sie angegeben haben. Wechseln Sie zurück zum Abschnitt **Sammeln von Informationen über die SQL Server-Instanz**. 
    *   Der SQL Server TCP-Port wird durch die Firewall blockiert. Wechseln Sie zurück zum Abschnitt **Öffnen eines Ports in der Firewall**.


2. Sobald Sie eine Verbindung mithilfe der IP-Adresse und der Portnummer herstellen können, versuchen Sie eine Verbindung mit der IP-Adresse ohne eine Portnummer herzustellen. Für eine Standardinstanz müssen Sie nur die IP-Adresse verwenden. Für eine benannte Instanz, verwenden Sie die IP-Adresse und den Instanznamen im Format „IP-Adresse, umgekehrter Schrägstrich (\), Instanzname“, also z.B. **192.168.1.101\PAYROLL** . Wenn dies nicht funktioniert, haben Sie wahrscheinlich eines der folgenden Probleme:

    *   Wenn Sie eine Verbindung mit der Standardinstanz herstellen, lauscht diese möglicherweise an einen anderen Port als TCP-Port 1433, und der Client versucht nicht, eine Verbindung mit der richtigen Portnummer herzustellen.
    *   Wenn Sie eine Verbindung zu einer benannten Instanz herstellen, wird die Port-Nummer nicht an den Client zurückgegeben.  

Beide Probleme beziehen sich auf den SQL Server-Browserdienst, der die Portnummer an dem Client bereitstellt. Die Lösungen sind:

  * Starten des SQL-Browserdiensts. Wechseln Sie zurück zum Abschnitt **Sammeln von Informationen über die SQL Server-Instanz**, Abschnitt 1.D.
  * Der SQL Server-Browserdienst wird durch die Firewall blockiert. Öffnen von UDP-Port 1434 in der Firewall. Wechseln Sie zurück zum Abschnitt **Öffnen eines Ports in der Firewall**. (Stellen Sie sicher, dass Sie einen UDP-Port öffnen, nicht einen TCP-Port. Diese unterscheiden sich voneinander.)
  * Die Informationen über den UDP-Port 1434 werden durch einen Router gesperrt. Die UDP-Kommunikation (User Datagram-Protokoll) ist nicht dafür ausgelegt, Router zu durchlaufen. Dadurch wird verhindert, dass das Netzwerk mit Datenverkehr mit niedriger Priorität gefüllt wird. Möglicherweise können Sie Ihren Router so konfigurieren, dass er UDP-Datenverkehr weiterleitet, oder Sie stellen immer die Portnummer bereit, wenn Sie eine Verbindung herstellen.
  * Wenn der Clientcomputer Windows 7 oder Windows Server 2008 (oder ein neueres Betriebssystem) verwendet, wird der UDP-Datenverkehr möglicherweise vom Clientbetriebssystem gelöscht, da die Antwort vom Server von einer anderen IP-Adresse zurückgegeben wird, als von der, von der abgefragt wurde. Hierbei handelt es sich um eine Sicherheitsfunktion, die „Loose Source Mapping“ (Lockere Quellzuordnung) blockiert. Weitere Informationen finden Sie im Abschnitt **Mehrere Server-IP-Adressen** der Onlinedokumentation [Problembehandlung: Das Timeout ist abgelaufen](http://msdn.microsoft.com/library/ms190181.aspx). Dies ist ein Artikel aus SQL Server 2008 R2, aber die Prinzipale sind weiterhin gültig. Möglicherweise können Sie den Client so konfigurieren, dass er die korrekte IP-Adresse verwendet, oder Sie stellen immer die Portnummer bereit, wenn Sie eine Verbindung herstellen.
     
3. Nachdem Sie eine Verbindung mithilfe der IP-Adresse (oder mithilfe der IP-Adresse und des Instanznamens für eine benannte Instanz) hergestellt haben, versuchen Sie, eine Verbindung über den Computernamen (oder über einen Computernamen und einen Instanznamen für eine benannte Instanz) herzustellen. Fügen Sie `tcp:` vor dem Computernamen ein, um eine TCP/IP-Verbindung zu erzwingen. Verwenden Sie `ACCNT27`für die Standardinstanz auf einem Computer mit dem Namen `tcp:ACCNT27` . Verwenden Sie `PAYROLL`für eine benannte Instanz mit dem Namen `tcp:ACCNT27\PAYROLL` auf diesem Computer. Wenn Sie eine Verbindung über die IP-Adresse, jedoch nicht über den Computernamen herstellen können, haben Sie ein Problem mit der Auflösung des Computernamens. Wechseln Sie zurück zum Abschnitt **Testen der TCP/IP-Konnektivität**, Abschnitt 4.

4. Nachdem Sie eine Verbindung über den Computernamen hergestellt haben und TCP erzwungen haben, versuchen Sie, eine Verbindung über den Computernamen herzustellen und das TCP nicht zu erzwingen. Verwenden Sie für eine Standardinstanz z.B. nur den Computernamen, wie `CCNT27` . Verwenden Sie für eine benannte Instanz den Computernamen und den Instanznamen, z.B. `ACCNT27\PAYROLL` . Wenn Sie eine Verbindung herstellen können, während Sie das TCP erzwingen, aber nicht ohne das TCP zu erzwingen, verwendet der Client möglicherweise ein anderes Protokoll (so wie Named Pipes).

    1. Erweitern Sie auf dem Clientcomputer im linken Bereich des SQL Server-Konfigurations-Managers **SQL Native Client** *Version* **Configuration**, and then select **Client Protocols**.
    2. Überprüfen Sie, ob TCP/IP im rechten Bereich aktiviert ist. Falls TCP/IP nicht aktiviert ist, klicken Sie mit der rechten Maustaste auf **TCP/IP** und anschließend auf **Aktivieren**.
    3. TC/IP muss in der Reihenfolge der Protokolle vor „Named Pipes“ (oder „VIA“ für ältere Versionen) stehen. Im Allgemeinen sollten Sie Shared Memory als Reihenfolge 1 und TCP/IP als Reihenfolge 2 lassen. Shared Memory wird nur verwendet, wenn der Client und SQL Server auf dem gleichen Computer ausgeführt werden. Alle aktivierten Protokolle werden in dieser Reihenfolge getestet, bis eine Verbindung hergestellt ist, es sei denn, gemeinsam genutzter Speicher wird übersprungen, wenn die Verbindung nicht auf demselben Computer vorhanden ist. 

