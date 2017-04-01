---
title: "Neues in Master Data Services (MDS) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "07/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ad530f60-d480-4457-ba7a-93a10c8a1695
caps.latest.revision: 85
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 85
---
# Neues in Master Data Services (MDS)
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../includes/feedback-stackoverflow-msdn-connect-md.md)]

  In diesem Thema sind die Änderungen und Aktualisierungen in der [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]-Version von [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] zusammengefasst. 
  
 Einen Überblick darüber, wie Sie Daten in [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] organisieren, finden Sie unter [Übersicht über Master Data Services (MDS)](../master-data-services/master-data-services-overview-mds.md). 
  
 **Informationen zur Installation der Master Data Services, zur Einrichtung der Datenbank und Website und zur Bereitstellung der Beispielmodelle finden Sie unter** [Übersicht über Master Data Services (MDS)](../master-data-services/master-data-services-overview-mds.md).  
  
 **Download**  
  
-   Um [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]herunterzuladen, navigieren Sie zum  **[Evaluierungscenter](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**.  
  
-   Haben Sie ein Azure-Konto?  Wechseln Sie anschließend **[hierhin](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)** , um einen virtuellen Computer zu starten, auf dem [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] bereits installiert ist.  
  
##  <a name="improved-performance"></a>Verbesserte Leistung  
  
 Durch Leistungsverbesserungen können Sie größere Modelle erstellen, Daten effizienter laden und eine bessere Gesamtleistung erzielen. Dies umfasst die Verbesserung der Leistung für das Add-In für Microsoft, um die Ladezeiten von Daten zu verringern und es dem Add-In zu ermöglichen, größere Entitäten zu verarbeiten.  
  
 Weitere Informationen zum Add-In für Microsoft Excel finden Sie unter [Master Data Services Add-in for Microsoft Excel](../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md).  
  
 Die folgenden Funktionsverbesserungen sind enthalten.  
  
-   Auf der Entitätsebene erfolgt eine Datenkomprimierung, die standardmäßig aktiviert ist. Wenn die Datenkomprimierung aktiviert ist, werden die auf Tabellen und Indizes bezogenen Entitäten mit der SQL-Row-Level-Komprimierung komprimiert. Dies verringert die Datenträger-E/A beim Lesen oder Aktualisieren der Masterdaten erheblich. Das gilt insbesondere, wenn die Masterdaten Millionen von Zeilen und/oder viele Spalten mit NULL-Werten umfassen.  
  
     Da ein leichten Anstieg der CPU-Auslastung auf der Seite des SQL Server-Moduls zu erwarten ist, wenn der Server CPU-abhängig ist, können Sie die Datenkomprimierung deaktivieren, indem Sie die Entität bearbeiten.  
  
     Weitere Informationen finden Sie unter [Erstellen einer Entität &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md) und [Datenkomprimierung](../relational-databases/data-compression/data-compression.md).  
  
-   Das IIS-Feature zur Komprimierung dynamischer Inhalte ist standardmäßig aktiviert. Dadurch wird die Größe der XML-Antwort erheblich verringert und die Netzwerk-E/A reduziert, obwohl die CPU-Auslastung erhöht wird. Wenn der Server CPU-abhängig ist, können Sie die Datenkomprimierung durch Hinzufügen der folgenden Einstellung zur [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datei „Web.config“ deaktivieren.  
  
    ```  
    <configuration>  
       <system.webServer>  
          <urlCompression doStaticCompression="true" doDynamicCompression="false " />  
       </system.webServer>  
    </configuration>  
  
    ```  
  
     Weitere Informationen finden Sie unter [URL-Komprimierung](http://www.iis.net/configreference/system.webserver/urlcompression).  
  
-   Die folgenden neuen Aufträge des SQL Server-Agents übernehmen die Index- und Protokollverwaltung.  
  
    -   MDS_MDM_Sample_Index_Maintenace  
  
    -   MDS_MDM_Sample_Log_Maintenace  
  
 Der Auftrag MDS_MDM_Sample_Index_Maintenance wird standardmäßig wöchentlich ausgeführt. Sie können den Zeitplan ändern. Sie können den Auftrag auch zu einem beliebigen Zeitpunkt mit der gespeicherten Prozedur „udpDefragmentation“ manuell ausführen. Es wird empfohlen, die gespeicherte Prozedur bei jedem Einfügen oder Aktualisieren einer großen Menge von Masterdaten bzw. nach dem Erstellen einer neuen Version aus der vorhandenen Version ausgeführt wird.  
  
 Ein Index mit einer Fragmentierung, die über 30 % liegt, wird online neu erstellt. Während der Neuerstellung wird die Leistung beim CRUD-Vorgang für dieselbe Tabelle beeinflusst. Wenn die Leistungsverringerung Bedenken hervorruft, empfiehlt es sich, dass Sie die gespeicherte Prozedur außerhalb der Arbeitszeit ausführen. Weitere Informationen zum Fragmentieren von Indizes finden Sie unter [Reorganize and Rebuild Indexes](../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
 Weitere Informationen finden Sie in diesem Beitrag zum Master Data Services-Blog [Verbesserung der Leistung und Skalierung in SQL Server 2016](http://go.microsoft.com/fwlink/p/?LinkId=615375).  
  
##  <a name="improved-security"></a>Erhöhte Sicherheit  
  
 Über die neue Administratorfunktionsberechtigung erhält ein Benutzer oder eine Gruppe dieselben Berechtigungen wie der Serveradministrator in der vorherigen Version von [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Die Administratorberechtigung kann mehreren Benutzern und Gruppen zugewiesen werden. In der vorherigen Version war der Benutzer, der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] ursprünglich installiert hat, der Serveradministrator, und es war schwierig, diese Berechtigung einem anderen Benutzer oder einer Gruppe zu übertragen. Weitere Informationen finden Sie unter [Berechtigungen für Funktionsbereiche &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
 Einem Benutzer kann jetzt auf Modellebene explizit die Administratorberechtigung zugewiesen werden. Dies bedeutet, dass der Benutzer die Administratorberechtigung nicht verliert, wenn ihm später in der Modellunterstruktur andere Berechtigungen zugewiesen werden.  
  
 In dieser Version von [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] werden durch die Einführung der folgenden neuen Berechtigungen mehr Berechtigungsstufen bereitgestellt: Lesen, Erstellen, Aktualisieren und Löschen. Beispielsweise kann jetzt ein Benutzer, der nur über die Berechtigung „Aktualisieren“ verfügt, die Masterdaten aktualisieren, ohne Daten zu erstellen oder zu löschen. Wenn Sie einem Benutzer die Berechtigung „Erstellen“, „Aktualisieren“ oder „Löschen“ erteilen, erhält er auch automatisch die Berechtigung „Lesen“. Die Berechtigungen „Lesen“, „Erstellen“, „Aktualisieren“ und „Löschen“ können auch kombiniert werden.  
  
 Wenn Sie ein Upgrade auf [!INCLUDE[ssSQL15](../includes/sssql15-md.md)][!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] durchführen, werden alte Berechtigungen in neue Berechtigungen konvertiert, wie in der folgenden Tabelle veranschaulicht.  
  
|Berechtigung in der vorherigen Version|Neue Berechtigung|  
|------------------------------------|--------------------|  
|Der Benutzer, der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] ursprünglich installiert hat, verfügt über die Serveradministratorberechtigung.|Benutzer verfügt über die Administratorfunktionsberechtigung|  
|Benutzer verfügt über die Berechtigung „Aktualisieren“ auf Modellebene und verfügt in der Modellunterstruktur über keine Berechtigungen und ist daher implizit ein Modelladministrator.|Benutzer verfügt über explizite Administratorberechtigungen auf der Modellebene|  
|Benutzer verfügt über die Berechtigung „Lesen“|Der Benutzer verfügt über die Berechtigung für den Lesezugriff.|  
|Benutzer verfügt über die Berechtigung „Aktualisieren“|Der Benutzer verfügt über alle vier Zugriffsberechtigungen: Erstellen, Aktualisieren, Löschen und Lesen.|  
|Benutzer verfügt über die Berechtigung „Verweigern“|Benutzer verfügt über die Berechtigung „Verweigern“|  
  
 Weitere Informationen zu Berechtigungen finden Sie unter [Sicherheit &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md).  
  
##  <a name="improved-transaction-log-maintenance"></a>Verbesserte Verwaltung des Transaktionsprotokolls  
  
 Sie können jetzt Transaktionsprotokolle in festgelegten Intervallen oder nach Zeitplan über die Systemeinstellungen und auf Modellebene bereinigen. Für ein MDS-System mit umfangreichen Datenänderungen und ELT-Prozessen kann die Größe dieser Tabellen exponentiell zunehmen und zur Verringerung der Leistung sowie zu Speicherplatzproblemen führen.  
  
 Die folgenden Arten von Daten können aus den Protokollen entfernt werden.  
  
-   Ein Transaktionsverlauf, der älter als eine angegebene Anzahl von Tagen ist.  
  
-   Ein Überprüfungsproblemverlauf, der älter als eine angegebene Anzahl von Tagen ist.  
  
-   Stagingbatches, die vor einer angegebenen Anzahl von Tagen ausgeführt wurden.  
  
 Sie können die Häufigkeit mithilfe der Systemeinstellungen sowie auf der Modellebene konfigurieren, mit der Daten aus den Transaktionsprotokollen entfernt werden. Weitere Informationen finden Sie unter [Systemeinstellungen &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md) und [Erstellen eines Modells &#40;Master Data Services&#41;](../master-data-services/create-a-model-master-data-services.md). Weitere Informationen über Transaktionen finden Sie unter [Transaktionen &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md).  
  
 Der SQL Server-Agent-Auftrag „MDS_MDM_Sample_Log_Maintenace“ löst die Bereinigung der Transaktionsprotokolle aus und wird jede Nacht ausgeführt. Sie können den SQL Server-Agent zum Ändern des Zeitplans für diesen Auftrag verwenden.  
  
 Sie können auch gespeicherte Prozeduren aufrufen, um die Transaktionsprotokolle zu bereinigen. Weitere Informationen finden Sie unter [Transaktionen &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md).  
  
## <a name="improved-troubleshooting"></a>Verbesserte Problembehandlung  
  
 In [!INCLUDE[ssSQL15](../includes/sssql15-md.md)][!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] wurden Funktionen hinzugefügt, um das Debugging zu verbessern und die Problembehandlung zu vereinfachen. Weitere Informationen finden Sie unter [Ablaufverfolgung &#40;Master Data Services&#41;](../master-data-services/tracing-master-data-services.md).  
  
## <a name="improved-manageability"></a>Verbesserte Verwaltbarkeit  
  
 Verbesserungen hinsichtlich der Verwaltbarkeit können zu niedrigeren Wartungskosten führen und sich positiv auf die Rentabilität auswirken. Diese Verbesserungen umfassen die Wartung des Transaktionsprotokolls und eine erhöhte Sicherheit sowie die folgenden neuen Features.  
  
-   Verwenden von Attributnamen, die mehr als 50 Zeichen umfassen.  
  
-   Umbenennen und Ausblenden von Namen- und Codeattributen.  
  
 Weitere Informationen finden Sie in den nachfolgenden Themen.  
  
-   [Modelle &#40;Master Data Services&#41;](../master-data-services/models-master-data-services.md)  
  
-   [Entitäten &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
-   [Transaktionen &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md)  
  
-   [Sicherheit &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)  

## <a name="business-rule-improvements"></a>Verbesserungen der Geschäftsregel
 **Verwalten von Geschäftsregeln (MDS-Add-In für Excel)**  
  
 Im Master Data Services-Add-In für Excel können Sie Geschäftsregeln verwalten, indem Sie z. B. Geschäftsregeln erstellen und bearbeiten. Geschäftsregeln werden zum Überprüfen von Daten verwendet.  
 
 **Erweiterung der Geschäftsregeln**  
  
 Sie können benutzerdefinierte SQL-Skripts als Erweiterung von Geschäftsregelbedingungen und -aktionen anwenden. SQL-Funktionen können als Bedingung verwendet werden. Gespeicherte SQL-Prozeduren können als Aktion verwendet werden. Weitere Informationen finden Sie unter [Geschäftsregelerweiterung &#40;Master Data Services&#41;](../master-data-services/business-rules-extension-master-data-services.md). 
 
 **Neugestaltung der Geschäftsregelverwaltung**  
  
 Die Geschäftsregelverwaltung in MDS wurde völlig umgestaltet, um das Erlebnis zu optimieren. Weitere Informationen finden Sie unter [Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md).  
  
 **Entfernung von Verwaltungsfunktionen der Geschäftsregel aus dem MDS-Add-In für Excel**  
  
 Es wurden Geschäftsregelverwaltungsfunktionen aus dem MDS-Add-In für Excel entfernt, da das Erlebnis überarbeitet wurde.    

 **Neue Geschäftsregelbedingungen**  
  
 Es wurden sieben neue Geschäftsregelbedingungen hinzugefügt, um einen vollständigen Satz von Bedingungen bereitzustellen. Weitere Informationen finden Sie unter [Geschäftsregelbedingungen &#40;Master Data Services&#41;](../master-data-services/business-rule-conditions-master-data-services.md).  

## <a name="derived-hierarchy-improvements"></a>Abgeleitete Hierarchieverbesserungen

 **m:n-Beziehungen in abgeleiteten Hierarchien**  
  
 Sie können jetzt eine abgeleitete Hierarchie erstellen, in der m:n-Beziehungen angezeigt werden. Eine m:n-Beziehung zwischen zwei Entitäten kann mithilfe einer dritten Entität modelliert werden, die eine Zuordnung zwischen ihnen bietet. Die Zuordnungsentität ist eine Entität mit zwei oder mehr domänenbasierten Attributen, die auf andere Entitäten verweisen.  
  
 Die Entität M verfügt z. B. über ein domänenbasiertes Attribut, das auf A verweist, und über ein domänenbasiertes Attribut, das auf B verweist. Sie können mithilfe der Zuordnungsentität eine Hierarchie von A nach B erstellen.  
  
 Weitere Informationen finden Sie unter [Anzeigen von m:n-Beziehungen in abgeleiteten Hierarchien &#40;Master Data Services&#41;](../master-data-services/show-many-to-many-relationships-in-derived-hierarchies-master-data-services.md).  
 
 **Bearbeiten von m:n-Beziehungen in abgeleiteten Hierarchien**  
  
 Sie können die m:n-Beziehung bearbeiten, indem Sie die Elemente der Zuordnungsentität ändern. Weitere Informationen finden Sie unter [Anzeigen von m:n-Beziehungen in abgeleiteten Hierarchien &#40;Master Data Services&#41;](../master-data-services/show-many-to-many-relationships-in-derived-hierarchies-master-data-services.md).  
 
 **Verbessertes Erlebnis bei der Verwaltung abgeleiteter Hierarchien**  
  
 Das Erlebnis bei der Verwaltung abgeleiteter Hierarchien in MDS wurde verbessert. Weitere Informationen über diese Funktion finden Sie unter [Erstellen einer abgeleiteten Hierarchie &#40;Master Data Services&#41;](../master-data-services/create-a-derived-hierarchy-master-data-services.md).  
  
 Es wurden Geschäftsregelverwaltungsfunktionen aus dem MDS-Add-In für Excel entfernt, da das Erlebnis überarbeitet wurde.  
 
## <a name="attribute-improvements"></a>Attributverbesserungen   
    
 **Benutzerdefinierte Indizes**  
  
 Sie können einen benutzerdefinierten Index für ein Attribut (einzelner Index) oder für eine Liste von Attributen (zusammengesetzter Index) in einer Entität erstellen, um die Abfrageleistung zu verbessern. Weitere Informationen finden Sie unter [Benutzerdefinierter Index &#40;Master Data Services&#41;](../master-data-services/custom-index-master-data-services.md).  
 
  **Attributfilter**  
  
 Sie können für ein domenbasiertes Attribut für ein Blattelement einen übergeordneten Attributfilter verwenden, um die zulässigen Werte für das domänenbasierte Attribut zu beschränken. Weitere Informationen finden Sie unter [Erstellen eines domänenbasierten Attributs &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md).  
 
## <a name="entity-and-member-improvements"></a>Entitäts- und Elementverbesserungen 
  
 **Entitäten-Synchronisierungspartnerschaft**  
  
 Sie können Entitätsdaten für verschiedene Modelle gemeinsam nutzen, indem Sie eine Synchronisierungspartnerschaft erstellen. Weitere Informationen finden Sie unter [Entitäten-Synchronisierungspartnerschaft &#40;Master Data Services&#41;](../master-data-services/entity-sync-relationship-master-data-services.md).  
  
 **Dauerhaftes Löschen von vorläufig gelöschten Elementen**  
  
 Sie können jetzt alle vorläufig gelöschten Elemente in einer Modellversion dauerhaft löschen. Durch das Löschen eines Elements wird dieses lediglich deaktiviert (vorläufig gelöscht). Weitere Informationen finden Sie unter [Endgültiges Löschen von Versionselementen &#40;Master Data Services&#41;](../master-data-services/purge-version-members-master-data-services.md).  
 
## <a name="improvements-for-managing-changes"></a>Verbesserungen für die Verwaltung von Änderungen 
  
 **Elementrevisionsverlauf**  
  
 Ein Elementrevisionsverlauf wird aufgezeichnet, wenn ein Element geändert wird. Sie können für einen Revisionsverlauf einen Rollback durchführen sowie die verschiedenen Überarbeitungen anzeigen und kommentieren. Mithilfe der Eigenschaft **Protokollaufbewahrungszeit in Tagen** können Sie angeben, wie lange Verlaufsdaten beibehalten werden. Weitere Informationen finden Sie unter [Elementrevisionsverlauf &#40;Master Data Services&#41;](../master-data-services/member-revision-history-master-data-services.md).  
  
 **Konflikte zusammenführen**  
  
 Wenn Sie versuchen, Daten zu veröffentlichen, die von einem anderen Benutzer geändert wurden, tritt bei der Veröffentlichung ein Konfliktfehler auf. Um diesen Fehler zu beheben, können Sie die Konflikte zusammenführen und die Änderungen erneut veröffentlichen. Weitere Informationen finden Sie unter [Konflikte zusammenführen (Master Data Services)](../master-data-services/merge-conflicts-master-data-services.md) und [Konflikte zusammenführen (MDS-Add-In für Excel)](../master-data-services/microsoft-excel-add-in/merge-conflicts-mds-add-in-for-excel.md).  
  
 **Changesets**  
  
 Mithilfe von Changesets können Sie ausstehende Änderungen an einer Entität speichern sowie anzeigen und ändern. Wenn Änderungen für die Entität genehmigt werden müssen, müssen Sie die ausstehenden Änderungen in einem Changeset speichern und zur Genehmigung durch den Administrator übermitteln. Weitere Informationen finden Sie unter [Changesets &#40;Master Data Services&#41;](../master-data-services/changesets-master-data-services.md).  
  
 **Changeset: E-Mails und Verwaltung**  
  
 In dieser Version können Sie jetzt alle Änderungen nach Modell und Version anzeigen und verwalten. Sie können auch E-Mail-Benachrichtigungen erhalten, sobald der Changesetstatus für eine Entität geändert wird, für die eine Genehmigung erforderlich ist. Weitere Informationen finden Sie unter [Verwalten von Changesets &#40;Master Data Services&#41;](../master-data-services/manage-changesets-master-data-services.md) und [Benachrichtigungen &#40;Master Data Services&#41;](../master-data-services/notifications-master-data-services.md).  
  
 **Anzeigen und Verwalten des Revisionsverlaufs**  
  
 Sie können den Revisionsverlauf nach Entität und nach Element anzeigen und verwalten. Wenn Sie über Aktualisierungsberechtigungen verfügen, können Sie ein Element auf eine frühere Version zurücksetzen. Weitere Informationen finden Sie unter [Elementrevisionsverlauf &#40;Master Data Services&#41;](../master-data-services/member-revision-history-master-data-services.md).  
 
## <a name="tool-and-sample-improvements"></a>Tool und Beispielverbesserungen 
  
 **Speichern oder Öffnen von Abfragedateien im MDS-Add-In für Excel**  
  
 Sie können auf der Seite des Entitäts-Explorers auf **Excel** klicken, um die Shortcutabfragedateien zu speichern. Sie können auch die auf Ihrem Computer gespeicherte Abfragedatei im MDS-Add-In für Excel öffnen. Die gespeicherte Datei kann mithilfe der Anwendung „QueryOpener“ geöffnet werden. Weitere Informationen finden Sie unter [Shortcutabfragedateien &#40;MDS-Add-In für Excel&#41;](../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md).  
  
 Die Abfragedatei enthält die Filter und Hierarchieinformationen von der Explorer-Seite.  
   
 **Aktualisierung der Bereitstellungspakete für Beispielmodelle**  
  
 Die Beispielpakete wurden aktualisiert, um neue Szenarien zu unterstützen. Weitere Informationen finden Sie unter [Beispiele: Modellbereitstellungspakete (MDS)](../master-data-services/sql-server-samples-model-deployment-packages-mds.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Master Data Services und Data Quality Services-Funktionen, die von den Editionen von SQL Server 2016 unterstützt](../master-data-services/master data services and data quality services features support.md)  
 [Veraltete Funktionen von Master Data Services](../master-data-services/deprecated-master-data-services-features.md)   
 [Eingestellte Master Data Services-Funktionen](../master-data-services/discontinued-master-data-services-features.md)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../includes/feedback-stackoverflow-msdn-connect-md.md)]
