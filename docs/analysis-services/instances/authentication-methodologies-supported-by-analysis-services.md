---
title: "Von Analysis Services unterst&#252;tzte Authentifizierungsmethoden | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b7aee903-d33a-4c20-86c2-aa013a50949f
caps.latest.revision: 8
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 8
---
# Von Analysis Services unterst&#252;tzte Authentifizierungsmethoden
  Verbindungen zwischen einer Clientanwendung und einer Analysis Services-Instanz erfordern die (integrierte) Windows-Authentifizierung. Sie können eine Windows-Benutzeridentität mithilfe einer der folgenden Methoden angeben:  
  
-   NTLM  
  
-   Kerberos (siehe [Konfigurieren von Analysis Services für die eingeschränkte Kerberos-Delegierung](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md))  
  
-   EffectiveUserName-Eigenschaft in der Verbindungszeichenfolge  
  
-   Standard- oder anonyme Authentifizierung (erfordert die Konfiguration des HTTP-Zugriffs)  
  
-   Gespeicherte Anmeldeinformationen  
  
 Beachten Sie, dass die anspruchsbasierte Authentifizierung nicht unterstützt wird. Sie können kein anspruchsbasiertes Windows-Token für den Zugriff auf Analysis Services verwenden. Die Analysis Services-Clientbibliotheken funktionieren nur mit Windows-Sicherheitsprinzipalen. Wenn die BI-Lösung Forderungsidentitäten umfasst, benötigen Sie für jeden Benutzer Schattenkonten für Windows-Identitäten. Alternativ können Sie gespeicherte Anmeldeinformationen für den Zugriff auf Analysis Services-Daten verwenden.  
  
 Weitere Informationen zu BI- und Analysis Services-Authentifizierungsabläufen finden Sie unter [Microsoft BI-Authentifizierung und Identitätsdelegierung](http://go.microsoft.com/fwlink/?LinkID=286576).  
  
##  <a name="bkmk_auth"></a> Grundlegendes zu alternativen Authentifizierungsformen  
 Verbindungen mit einer Analysis Services-Datenbank erfordern eine Windows-Benutzeridentität bzw. die Mitgliedschaft in einer Windows-Gruppe sowie die zugehörigen Berechtigungen. Die Identität kann allgemeingültig sein, wenn sich ein Benutzer z. B. anmeldet, um einen Bericht anzuzeigen. Das wahrscheinlichere Szenario ist jedoch, die den einzelnen Benutzern zugewiesenen Identitäten zu verwenden.  
  
 Ein tabellarisches oder mehrdimensionales Modell verfügt häufig über verschiedene Datenzugriffsebenen. Abhängig von der Person, die die Authentifizierungsanforderung sendet, sind diese nach Objekt oder innerhalb der Daten festgelegt. NTLM, Kerberos, EffectiveUserName oder die Standardauthentifizierung stehen zur Verfügung, um die Vorgaben zu erfüllen. Bei allen diesen Verfahren kann für jede Verbindung eine andere Benutzeridentität übergeben werden. Meistens setzen diese Optionen jedoch Single-Hop-Verbindungen voraus. Nur die Kerberos-Authentifizierung mit Delegierung macht es möglich, die ursprüngliche Benutzeridentität über mehrere Computerverbindungen hinweg bis zu einem Back-End-Datenspeicher auf einem Remoteserver beizubehalten.  
  
 **NTLM**  
  
 Bei Verbindungen mit `SSPI=Negotiate`wird NTLM zu Sicherungszwecken als Authentifizierungssubsystem verwendet, wenn kein Kerberos-Domänencontroller verfügbar sein sollte. Unter NTLM kann jede Benutzer- oder Clientanwendung unter den folgenden Voraussetzungen auf eine Serverressource zuzugreifen: die Anforderung wird über eine direkte Client-Server-Verbindung gesendet; die Person, die die Verbindung anfordert, verfügt über eine Berechtigung für die Ressource; und Client- und Servercomputer befinden sich in derselben Domäne.  
  
 Bei Multi-Tier-Lösungen können die von NTLM vorausgesetzten Single-Hop-Verbindungen eine erhebliche Einschränkung bedeuten. Die Identität des Benutzers, der die Anforderung sendet, kann genau auf einem Remoteserver, aber auf keinem weiteren angenommen werden. Wenn der aktuelle Vorgang Dienste auf mehreren Computern erfordert, müssen Sie die eingeschränkte Kerberos-Delegierung konfigurieren, um das Sicherheitstoken auf Back-End-Servern wiederzuverwenden. Alternativ können Sie gespeicherte Anmeldeinformationen oder die Standardauthentifizierung verwenden, um neue Identitätsinformationen über eine Single-Hop-Verbindung zu übergeben.  
  
 **Kerberos-Authentifizierung und eingeschränkte Kerberos-Delegierung**  
  
 Die Kerberos-Authentifizierung bildet die Grundlage der integrierten Windows-Sicherheit in Active Directory-Domänen. Wie bei NTLM ist der Identitätswechsel unter Kerberos auf Single-Hop-Verbindungen beschränkt, solange die Delegierung nicht aktiviert ist.  
  
 Zur Unterstützung von Multi-Hop-Verbindungen bietet Kerberos sowohl die eingeschränkte als auch die nicht eingeschränkte Delegierung. In den meisten Szenarien ist jedoch die eingeschränkte Delegierung als bewährte Sicherheitsmethode anzusehen. Bei der eingeschränkten Delegierung ist ein Dienst in der Lage, das Sicherheitstoken der Benutzeridentität an einen bestimmten untergeordneten Dienst auf einem Remotecomputer zu übergeben. Multi-Tier-Anwendungen machen es im Allgemeinen erforderlich, eine Benutzeridentität von einem Anwendungsserver der mittleren Ebene an eine Back-End-Datenbank (z. B. Analysis Services) zu delegieren. Beispielsweise erfordert ein tabellarisches oder mehrdimensionales Modell, das je nach Benutzeridentität unterschiedliche Daten zurückgibt, die Identitätsdelegierung von einem Dienst der mittleren Ebene. So wird vermieden, dass der Benutzer Anmeldeinformationen erneut eingeben oder Sicherheitsanmeldeinformationen auf andere Weise bereitstellen muss.  
  
 Die eingeschränkte Delegierung erfordert zusätzliche Konfigurationsschritte in Active Directory. Hier wird festgelegt, welche Dienste auf Sender- und Empfängerseite zur Delegierung berechtigt sind. Diese Methode erfordert zwar einigen Konfigurationsaufwand im Vorfeld, ermöglicht jedoch nach der Konfiguration des Dienstes die unabhängige Verwaltung von Kennwortaktualisierungen in Active Directory. In diesem Fall müssen die in Anwendungen gespeicherten Kontoinformationen nicht aktualisiert werden wie etwa bei Verwendung der gespeicherten Anmeldeinformationen, die weiter unten beschrieben sind.  
  
 Weitere Informationen zum Konfigurieren von Analysis Services für die eingeschränkte Delegierung finden Sie unter [Configure Analysis Services for Kerberos constrained delegation](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md).  
  
> [!NOTE]  
>  Windows Server 2012 unterstützt die eingeschränkte Delegierung über mehrere Domänen hinweg. Im Gegensatz dazu erfordert die eingeschränkte Kerberos-Delegierung – wenn sie für Domänen einer niedrigeren Funktionsebene wie Windows Server 2008 oder 2008 R2 konfiguriert wird – dass sowohl Client- als auch Servercomputer Mitglied derselben Domäne sind.  
  
 **EffectiveUserName**  
  
 EffectiveUserName ist eine Verbindungszeichenfolgen-Eigenschaft, die für die Übergabe von Identitätsinformationen an Analysis Services verwendet wird. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint verwendet die Eigenschaft, um Benutzeraktivitäten in Nutzungsprotokollen zu erfassen. Excel Services und PerformancePoint Services ermöglichen das Abrufen von Daten, die von Arbeitsmappen oder Dashboards in SharePoint verwendet werden. Sie können auch in benutzerdefinierten Anwendungen oder Skripts verwendet werden, die Vorgänge für eine Analysis Services-Instanz ausführen.  
  
 Weitere Informationen zur Verwendung von EffectiveUserName in SharePoint finden Sie unter [Verwenden von "EffectiveUserName" der Analysis Services in SharePoint Server 2010](http://go.microsoft.com/fwlink/?LinkId=311905).  
  
 **Standardauthentifizierung und anonyme Authentifizierung**  
  
 Die Standardauthentifizierung bietet eine vierte Alternative, mit der ein bestimmter Benutzer eine Verbindung mit einem Back-End-Server herstellen kann. Bei der Standardauthentifizierung werden Windows-Benutzername und Kennwort in der Verbindungszeichenfolge übergeben. Das erfordert jedoch zusätzliche Verschlüsselungsmethoden während der Übertragung, damit vertrauliche Informationen geschützt bleiben. Ein zentraler Vorteil der Standardauthentifizierung besteht darin, dass die Authentifizierungsanforderung domänenübergreifend übertragen werden kann.  
  
 Bei der anonymen Authentifizierung können Sie die anonyme Benutzeridentität auf ein bestimmtes Windows-Benutzerkonto (standardmäßig IUSR_GUEST) oder eine Anwendungspoolidentität festlegen. Das anonyme Benutzerkonto wird für die Analysis Services-Verbindung verwendet und muss über Datenzugriffsberechtigungen auf der Analysis Services-Instanz verfügen. Bei diesem Ansatz wird für die Verbindung nur die Benutzeridentität verwendet, die dem anonymen Konto zugewiesen ist. Wenn die Anwendung eine zusätzliche Identitätsverwaltung erforderlich macht, sollten Sie sich für eine der anderen Methoden entscheiden oder eine zusätzliche Identitätsverwaltungslösung implementieren.  
  
 Die Standardauthentifizierung und die anonyme Authentifizierung sind nur verfügbar, wenn Sie Analysis Services für den HTTP-Zugriff konfigurieren, d. h. die Verbindung mit IIS und msmdpump.dll herstellen. Weitere Informationen finden Sie unter [Konfigurieren von HTTP-Zugriff auf Analysis Services unter Internetinformationsdienste &#40;IIS&#41; 8.0](../../analysis-services/instances/configure http access to analysis services on iis 8.0.md).  
  
 **Gespeicherte Anmeldeinformationen**  
  
 Die meisten Anwendungsdienste der mittleren Ebene umfassen Funktionen zum Speichern von Benutzernamen und Kennwörtern, die anschließend verwendet werden, um Daten aus einem untergeordneten Datenspeicher wie Analysis Services oder dem relationalen SQL Server-Modul abzurufen. So gesehen bieten gespeicherte Anmeldeinformationen eine fünfte Alternative zum Abrufen von Daten. Die Beschränkungen dieser Vorgehensweise liegen im erhöhten Wartungsaufwand, der mit der Aktualisierung von Benutzernamen und Kennwörtern verbunden ist, und der Verwendung einer einzelnen Identität für die Verbindung. Wenn Ihre Lösung die Identität des ursprünglichen Aufrufers erfordert, sind gespeicherte Anmeldeinformationen keine geeignete Alternative.  
  
 Weitere Informationen zu gespeicherten Anmeldeinformationen finden Sie unter [Erstellen, Ändern und Löschen von freigegebenen Datenquellen &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md) und [Verwenden von Excel Services mit Secure Store Service in SharePoint Server 2013](http://go.microsoft.com/fwlink/?LinkID=309869).  
  
## Siehe auch  
 [Verwenden des Identitätswechsels mit Transportsicherheit](http://go.microsoft.com/fwlink/?LinkId=311727)   
 [Konfigurieren von HTTP-Zugriff auf Analysis Services unter Internetinformationsdienste &#40;IIS&#41; 8.0](../../analysis-services/instances/configure http access to analysis services on iis 8.0.md)   
 [Konfigurieren von Analysis Services für die eingeschränkte Kerberos-Delegierung](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)   
 [SPN-Registrierung für eine Analysis Services-Instanz](../../analysis-services/instances/spn-registration-for-an-analysis-services-instance.md)   
 [Verbindung mit Analysis Services herstellen](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  