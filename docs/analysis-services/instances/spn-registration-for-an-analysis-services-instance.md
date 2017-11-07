---
title: "SPN-Registrierung für Analysis Services-Instanz | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9e78dc37-a3f0-415d-847c-32fec69efa8c
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8d0d90aea6725bd45cded022791699cf910b7bdd
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="spn-registration-for-an-analysis-services-instance"></a>SPN-Registrierung für eine Analysis Services-Instanz
  Durch einen Dienstprinzipalnamen (Service Principal Name, SPN) wird eine Dienstinstanz in einer Active Directory-Domäne eindeutig identifiziert, wenn Kerberos zur gegenseitigen Authentifizierung von Client- und Dienstidentitäten verwendet wird. Ein SPN ist dem Anmeldekonto zugeordnet, unter dem die Dienstinstanz ausgeführt wird.  
  
 Bei Clientanwendungen, die über die Kerberos-Authentifizierung eine Verbindung mit Analysis Services herstellen, wird von den Analysis Services-Clientbibliotheken ein SPN erstellt. Dieser basiert auf der Verbindungszeichenfolge und anderen bekannten Variablen wie der Dienstklasse, die in der jeweiligen Analysis Services-Version fest definiert sind.  
  
 Damit die gegenseitige Authentifizierung funktioniert, müssen die vom Client erstellten SPNs einem SPN-Objekt für einen Active Directory-Domänencontroller (DC) entsprechen. Deshalb müssen möglicherweise mehrere SPNs für eine einzelne Analysis Services-Instanz registriert werden, um sämtliche Varianten abzudecken, wie der Hostname in einer Verbindungszeichenfolge von einem Benutzer angegeben werden kann. Beispielsweise benötigen Sie wahrscheinlich zwei SPNs, um sowohl den vollqualifizierten Domänennamen (FQDN) eines Servers als auch den kürzeren Computernamen zu unterstützen. Die richtige Registrierung des Analysis Services-SPNs ist wichtig für eine erfolgreiche Verbindung. Wenn der SPN nicht oder doppelt vorhanden ist bzw. ein falsches Format aufweist, tritt ein Verbindungsfehler auf.  
  
 Die SPN-Registrierung wird manuell vom Analysis Services-Administrator ausgeführt. Im Gegensatz zum SQL Server-Datenbankmodul wird der SPN von Analysis Services beim Dienststart nie automatisch registriert. Die manuelle Registrierung ist erforderlich, wenn Analysis Services unter dem virtuellen Standardkonto, einem Domänenbenutzerkonto oder einem integriertem Konto (einschließlich einer Pro-Dienst-SID) ausgeführt wird.  
  
 Die SPN-Registrierung ist nicht erforderlich, wenn der Dienst unter einem vordefinierten, verwalteten Dienstkonto ausgeführt wird, das von einem Domänenadministrator erstellt wird. Je nach Funktionsumfang der Domäne können für die Registrierung eines SPNs Domänenadministratorberechtigungen erforderlich sein.  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos-Konfigurations-Manager für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** ist ein Diagnosetool zur Behebung Kerberos-bezogener Verbindungsprobleme bei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Weitere Informationen finden Sie unter [Microsoft Kerberos-Konfigurations-Manager für SQL Server](http://www.microsoft.com/download/details.aspx?id=39046).  
  
 Dieses Thema enthält folgende Abschnitte:  
  
 [Wann die SPN-Registrierung erforderlich ist](#bkmk_scnearios)  
  
 [SPN-Format für Analysis Services](#bkmk_SPNSyntax)  
  
 [SPN-Registrierung für ein virtuelles Konto](#bkmk_virtual)  
  
 [SPN-Registrierung für ein Domänenkonto](#bkmk_domain)  
  
 [SPN-Registrierung für ein integriertes Konto](#bkmk_builtin)  
  
 [SPN-Registrierung für eine benannte Instanz](#bkmk_spnNamed)  
  
 [SPN-Registrierung für einen SSAS-Cluster](#bkmk_spnCluster)  
  
 [SPN-Registrierung für SSAS-Instanzen, die für den HTTP-Zugriff konfiguriert sind](#bkmk_spnHTTP)  
  
 [SPN-Registrierung für SSAS-Instanzen, die an festen Ports lauschen](#bkmk_spnFixedPorts)  
  
##  <a name="bkmk_scnearios"></a> Wann die SPN-Registrierung erforderlich ist  
 Jede Clientverbindung, bei der "SSPI=Kerberos" in der Verbindungszeichenfolge angegeben ist, erfordert die SPN-Registrierung für eine Analysis Services-Instanz.  
  
 Die SPN-Registrierung ist in folgenden Situationen erforderlich. Ausführlichere Informationen finden Sie unter [Configure Analysis Services for Kerberos constrained delegation](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md).  
  
-   Die Identitätsdelegierung ist erforderlich, um die Benutzeridentität von der Clientanwendung oder dem Dienst der mittleren Ebene an Analysis Services zu übertragen. Die Identitätsdelegierung wird normalerweise verwendet, wenn benutzerspezifische Berechtigungen oder Filter für bestimmte Objekte definiert werden.  
  
     Ein häufiges Szenario für die Identitätsdelegierung besteht darin, Dienste mittlerer Ebene, z. B. Excel Services oder Reporting Services, für die eingeschränkte Delegierung konfigurieren, damit beim Abrufen von Daten in Analysis Services eine Benutzeridentität angenommen werden kann. Um dieses Verhalten zu unterstützen, müssen Sie einen Analysis Services-SPN als Zieldienst bereitstellen, wenn Sie Excel Services oder Reporting Services für die eingeschränkte Delegierung konfigurieren.  
  
-   Analysis Services delegiert eine Benutzeridentität, wenn Daten aus einer relationalen SQL Server-Datenbank mithilfe des DirectQuery-Modus für tabellarische Datenbanken abgerufen werden. Dies ist das einzige Szenario, bei dem Analysis Services die Benutzeridentität an einen anderen Dienst delegiert.  
  
##  <a name="bkmk_SPNSyntax"></a> SPN-Format für Analysis Services  
 Verwenden Sie **setspn** , um einen SPN zu registrieren. Unter neueren Betriebssystemen wird **setspn** als Systemhilfsprogramm installiert. Weitere Informationen finden Sie unter [SetSPN](http://technet.microsoft.com/library/cc731241\(WS.10\).aspx).  
  
 In der folgenden Tabelle werden die einzelnen Bestandteile des Analysis Services-SPNs beschrieben.  
  
|Element|Description|  
|-------------|-----------------|  
|Dienstklasse|MSOLAPSvc.3 identifiziert den Dienst als Analysis Services-Instanz. Die " .3" ist ein Verweis auf die Version des XMLA-over-TCP/IP Protokolls, das für Analysis Services-Übertragungen verwendet wird. Die Zahl hat keinen Bezug zur Produktversion. Daher ist MSOLAPSvc.3 die richtige Dienstklasse für SQL Server 2005, 2008, 2008, 2012 R2 und jede zukünftige Version von Analysis Services, bis das Protokoll selbst überarbeitet wird.|  
|Hostname|Identifiziert den Computer, auf dem der Dienst ausgeführt wird. Das kann ein vollqualifizierter Domänenname oder ein NetBIOS-Name sein. Sie sollten einen SPN für beide Namen registrieren.<br /><br /> Wenn Sie einen SPN für den NetBIOS-Namen eines Servers registrieren, sollten Sie anhand von `SetupSPN –S` doppelte Registrierungseinträge suchen. NetBIOS-Namen sind innerhalb einer Gesamtstruktur nicht unbedingt eindeutig, und eine doppelte SPN-Registrierung führt zu einem Verbindungsfehler.<br /><br /> Bei Analysis Services-Clustern mit Lastenausgleich sollte der Hostname dem virtuellen Namen entsprechen, der dem Cluster zugewiesen ist.<br /><br /> Ein SPN sollte nie anhand der IP-Adresse erstellt werden. Kerberos verwendet die DNS-Auflösungsfunktionen der Domäne. Das wird umgangen, indem eine IP-Adresse angegeben wird.|  
|Portnummer|Obwohl die Portnummer Teil der SPN-Syntax ist, geben Sie bei der Registrierung eines Analysis Services-SPNs nie eine Portnummer an. Der Doppelpunkt (:), der in der SPN-Standardsyntax normalerweise zur Angabe einer Portnummer dient, wird von Analysis Services für den Instanznamen verwendet. Bei einer Analysis Services-Instanz wird davon ausgegangen, dass der Port dem Standardport (TCP 2383) oder einem Port entspricht, der vom SQL Server-Browserdienst (TCP 2382) zugewiesen wird.|  
|Instanzname|Analysis Services ist ein replizierbarer Dienst, der mehrmals auf demselben Computer installiert werden kann. Jede Instanz wird über den Instanznamen identifiziert.<br /><br /> Dem Instanznamen wird ein Doppelpunkt (:) vorangestellt. Bei einem Hostcomputer mit dem Namen "SRV01" und der benannten Instanz "SSAS-Tabular" sollte der SPN beispielsweise "SRV01:SSAS-Tabular" lauten.<br /><br /> Beachten Sie, dass sich die Syntax zum Angeben einer benannten Analysis Services-Instanz von der Syntax unterscheidet, die von anderen SQL Server-Instanzen verwendet wird. Andere Dienste verwenden einen umgekehrten Schrägstrich (\), um den Instanznamen in einem SPN anzufügen.|  
|Dienstkonto|Dies ist das Startkonto des Windows-Diensts **MSSQLServerOLAPService** . Es kann sich um ein Windows-Domänenbenutzerkonto, ein virtuelles Konto, ein verwaltetes Dienstkonto (MSA) oder ein integriertes Konto handeln, wie z. B. Pro-Dienst-SID, NetworkService oder LocalSystem. Ein Windows-Domänenbenutzerkonto "Domäne\Benutzer" formatiert werden kann oder user@domain.|  
  
##  <a name="bkmk_virtual"></a> SPN-Registrierung für ein virtuelles Konto  
 Virtuelle Konten sind der Standardkontotyp für SQL Server-Dienste. Das virtuelle Konto wird **NT Service\MSOLAPService** für eine Standardinstanz und **NT Service\MSOLAP$**\<Instanzname > für eine benannte Instanz.  
  
 Wie der Name bereits aussagt, sind diese Konten nicht in Active Directory enthalten. Ein virtuelles Konto ist nur auf dem lokalen Computer vorhanden. Bei der Verbindung mit externen Diensten, Anwendungen oder Geräten wird die Verbindung über das lokale Computerkonto hergestellt. Wenn der SPN also für eine Analysis Services-Instanz registriert wird, die unter einem virtuellen Konto ausgeführt wird, handelt es sich tatsächlich um eine SPN-Registrierung für das Computerkonto.  
  
 **Beispielsyntax für eine Standardinstanz, die als "NT Service\MSOLAPService" ausgeführt wird**  
  
 In diesem Beispiel wird die **setspn** -Syntax für eine Analysis Services-Standardinstanz veranschaulicht, die unter dem virtuellen Standardkonto ausgeführt wird. In diesem Beispiel lautet der Computerhostname **AW-SRV01**. Wie bereits erwähnt, muss für die SPN-Registrierung das *Computerkonto* und nicht das virtuelle Konto **NT Service\MSOLAPService**angegeben werden.  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
> [!NOTE]  
>  Denken Sie daran, zwei SPN-Registrierungen zu erstellen, eine für den NetBIOS-Hostnamen und einen zweiten für einen vollqualifizierten Domänennamen des Hosts. Unterschiedliche Clientanwendungen verwenden verschiedene Hostnamenskonventionen, wenn sie eine Verbindung mit Analysis Services herstellen. Durch die Erstellung beider SPN-Registrierungen wird sichergestellt, dass beide Versionen des Hostnamens berücksichtigt werden.  
  
 **Beispielsyntax für eine benannte Instanz ausgeführt wird als NT Service\MSOLAP$\<Instanzname >**  
  
 In diesem Beispiel wird die **setspn** -Syntax für eine benannte Instanz veranschaulicht, die unter dem virtuellen Standardkonto ausgeführt wird. Der Computerhostname lautet in diesem Fall **AW-SRV02**und der Instanzname **AW-FINANCE**. Es wird erneut, das Konto "Machine", die für den SPN angegeben wird, anstatt das virtuelle Konto **NT Service\MSOLAP$**\<Instanzname >.  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV02.AdventureWorks.com:AW-FINANCE AW-SRV02  
```  
  
##  <a name="bkmk_domain"></a> SPN-Registrierung für ein Domänenkonto  
 Üblicherweise wird zum Ausführen einer Analysis Services-Instanz ein Domänenkonto verwendet.  
  
 Für Analysis Services-Instanzen, die in einem Netzwerk oder Cluster mit Hardwarelastenausgleich ausgeführt werden, ist ein Domänenkonto erforderlich, wobei jede Instanz des Clusters unter demselben Domänenkonto ausgeführt wird.  
  
 **Beispielsyntax für eine Standardinstanz, die als Domänenbenutzer ausgeführt wird**  
  
 In diesem Beispiel wird die **setspn** -Syntax für eine Analysis Services-Standardinstanz veranschaulicht, die in der Domäne AdventureWorks unter dem Domänenbenutzerkonto **SSAS-Service**ausgeführt wird.  
  
```  
Setspn –s msolapsvc.3\AW-SRV01.Adventureworks.com AdventureWorks\SSAS-Service  
```  
  
> [!TIP]  
>  Überprüfen Sie, ob der SPN für den Analysis Services-Server erstellt wurde, indem Sie je nach SPN-Registrierung `Setspn -L <domain account>` oder `Setspn -L <machinename>`ausführen. Daraufhin sollte MSOLAPSVC.3/\<Hostname > in der Liste.  
  
##  <a name="bkmk_builtin"></a> SPN-Registrierung für ein integriertes Konto  
 Obwohl diese Vorgehensweise nicht empfohlen wird, sind ältere Analysis Services-Installationen manchmal für die Ausführung unter integrierten Konten wie Netzwerkdienst, Lokaler Dienst oder Lokales System konfiguriert.  
  
 **Beispielsyntax für eine Standardinstanz, die unter einem integrierten Konto ausgeführt wird**  
  
 Die SPN-Registrierung für einen Dienst, der unter einem integrierten Konto oder einer Pro-Dienst-SID ausgeführt wird, weist die gleiche SPN-Syntax wie für das virtuelle Konto auf. Verwenden Sie anstelle des Kontonamens das Computerkonto:  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
##  <a name="bkmk_spnNamed"></a> SPN-Registrierung für eine benannte Instanz  
 Für benannte Instanzen von Analysis Services werden dynamische Portzuweisungen verwendet, die vom SQL Server-Browserdienst erkannt werden. Registrieren Sie einen SPN bei Verwendung einer benannten Instanz sowohl für den SQL Server-Browserdienst als auch für die benannte Analysis Services-Instanz. Weitere Informationen finden Sie unter [Ein SPN für den SQL Server-Browser-Dienst ist erforderlich, wenn Sie eine Verbindung zu einer benannten Instanz von SQL Server Analysis Services oder von SQL Server herstellen](http://support.microsoft.com/kb/950599).  
  
 **SPN-Beispielsyntax für den SQL-Browserdienst, der als LocalService ausgeführt wird**  
  
 Der Name der Dienstklasse ist **MSOLAPDisco.3**. Dieser Dienst wird standardmäßig als NT AUTHORITY\LocalService ausgeführt, d. h., der SPN wurde für das Computerkonto registriert. In diesem Beispiel weist das Computerkonto den Namen **AW-SRV01**auf, der dem Computernamen entspricht.  
  
```  
Setspn -S MSOLAPDisco.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
##  <a name="bkmk_spnCluster"></a> SPN-Registrierung für einen SSAS-Cluster  
 Bei Analysis Services-Failoverclustern sollte der Hostname dem virtuellen Namen entsprechen, der dem Cluster zugewiesen ist. Dies ist der SQL Server-Netzwerkname, der während des Setups von SQL Server angegeben wurde, wenn Sie Analysis Services auf einem vorhandenen WSFC installiert haben. Sie finden diesen Namen in Active Directory. Sie finden ihn außerdem auf der Registerkarte **Failovercluster-Manager** | **Rolle** | **Ressourcen** . Der Servername auf der Registerkarte "Ressourcen" sollte als "virtueller Name" im SPN-Befehl verwendet werden.  
  
 **SPN-Syntax für einen Analysis Services-Cluster**  
  
```  
Setspn –s msolapsvc.3/<virtualname.FQDN > <domain user account>  
```  
  
 Beachten Sie, dass für Knoten in einem Analysis Services-Cluster der Standardport (TCP 2383) verwendet werden muss und dass die Knoten unter demselben Domänenbenutzerkonto ausgeführt werden müssen, sodass jeder Knoten über dieselbe SID verfügt. Weitere Informationen finden Sie unter [How to Cluster SQL Server Analysis Services](http://msdn.microsoft.com/library/dn736073.aspx) (in englischer Sprache).  
  
##  <a name="bkmk_spnHTTP"></a> SPN-Registrierung für SSAS-Instanzen, die für den HTTP-Zugriff konfiguriert sind  
 Je nach den Anforderungen der Lösung kann es erforderlich sein, Analysis Services für den HTTP-Zugriff zu konfigurieren. Wenn die Lösung IIS als Komponente der mittleren Ebene umfasst und die Kerberos-Authentifizierung von der Lösung vorausgesetzt wird, muss ein SPN ggf. manuell für IIS registriert werden. Weitere Informationen finden Sie unter "Konfigurieren der Einstellungen auf dem Computer, auf dem IIS ausgeführt wird" in [Konfigurieren von SQL Server 2008 Analysis Services und SQL Server 2005 Analysis Services, um Kerberos-Authentifizierung zu verwenden](http://support.microsoft.com/kb/917409).  
  
 Bei der SPN-Registrierung für die Analysis Services-Instanz macht es keinen Unterschied, ob eine Instanz für TCP oder HTTP konfiguriert ist. Wenn von IIS mithilfe der MSMDPUMP-ISAPI-Erweiterung eine Verbindung mit Analysis Services hergestellt wird, basiert diese immer auf TCP.  
  
 Das bedeutet, dass Sie bei der SPN-Registrierung die Anweisungen der vorherigen Abschnitte für Standardinstanzen oder benannte Instanzen verwenden können. Achten Sie beim Angeben des Hostnamens darauf, den Hostnamen zu verwenden, den Sie bei der Konfiguration des Dienstes für den HTTP-Zugriff in der Datei msmdpump.ini angegeben haben.  
  
 Weitere Informationen zum HTTP-Zugriff finden Sie unter [Konfigurieren von HTTP-Zugriff auf Analysis Services unter Internetinformationsdienste &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
##  <a name="bkmk_spnFixedPorts"></a> SPN-Registrierung für SSAS-Instanzen, die an festen Ports lauschen  
 Bei einer SPN-Registrierung für Analysis Services kann keine Portnummer angegeben werden. Wenn Sie Analysis Services als Standardinstanz installiert und für das Lauschen an einem festen Port konfiguriert haben, müssen Sie Analysis Services jetzt für das Lauschen am Standardport (TCP 2383) konfigurieren. Bei benannten Instanzen müssen Sie den SQL Server-Browserdienst und dynamische Portzuweisungen verwenden.  
  
 Eine Analysis Services-Instanz kann nur an einem einzelnen Port lauschen. Die Verwendung mehrerer Ports wird nicht unterstützt. Weitere Informationen zur Portkonfiguration finden Sie unter [Configure the Windows Firewall to Allow Analysis Services Access](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft-BI-Authentifizierung und Identitätsdelegierung](http://go.microsoft.com/fwlink/?LinkID=286576)   
 [Gegenseitige Authentifizierung mithilfe von Kerberos](http://go.microsoft.com/fwlink/?LinkId=299283)   
 [Gewusst wie: Konfigurieren von SQL Server 2008 Analysis Services und SQL Server 2005 Analysis Services, um die Kerberos-Authentifizierung verwenden](http://support.microsoft.com/kb/917409)   
 [Dienstprinzipalnamen (SPNs) SetSPN Syntax (Setspn.exe)](http://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx)   
 [Welchen SPN verwende ich, und wie gelangen es vorhanden?](http://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx)   
 [SetSPN](http://technet.microsoft.com/library/cc731241\(WS.10\).aspx)   
 [Schrittweise Anleitung für Dienstkonten](http://technet.microsoft.com/library/dd548356\(WS.10\).aspx)   
 [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [Gewusst wie: Verwenden von Dienstprinzipalnamen bei der Konfiguration von Webanwendungen, die gehostet werden auf Internetinformationsdienste (IIS)](http://support.microsoft.com/kb/929650)   
 [Neuigkeiten in Dienstkonten](http://technet.microsoft.com/library/dd367859\(WS.10\).aspx)   
 [Konfigurieren der Kerberos-Authentifizierung für SharePoint 2010-Produkte (Whitepaper)](http://technet.microsoft.com/library/ff829837.aspx)  
  
  

