---
title: Erstellen Sie eine BI-Semantikmodell-Verbindung mit einer tabellarischen Modelldatenbank | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 69b306f6-ee8a-44d2-8f51-0cad2c0bc135
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7c4e9b6b1814994caf778e0c3d50a69ffc70d4ee
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-bi-semantic-model-connection-to-a-tabular-model-database"></a>Erstellen einer BI-Semantikmodellverbindung mit einer tabellarischen Modelldatenbank
  Verwenden Sie die Informationen in diesem Thema, um eine BI-Semantikmodellverbindung einzurichten, durch die eine Umleitung zu einer Datenbank für tabellarische Modelle erfolgt, die auf einer Analysis Services-Instanz außerhalb der SharePoint-Farm ausgeführt wird.  
  
 Nachdem Sie eine BI-Semantikmodellverbindung erstellt und SharePoint- und Analysis Services-Berechtigungen konfiguriert haben, kann diese Verbindung als Datenquelle für Excel- oder [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] -Berichte verwendet werden.  
  
 Das Thema enthält folgende Abschnitte: Führen Sie jede Aufgabe in der angegebenen Reihenfolge aus.  
  
 [Überprüfen der Voraussetzungen](#bkmk_prereq)  
  
 [Erteilen von Analysis Services-Administratorberechtigungen an gemeinsame Dienstanwendungen](#bkmk_ssas)  
  
 [Erteilen von Leseberechtigungen für die Datenbank für tabellarische Modelle](#bkmk_BISM)  
  
 [Erstellen einer BI-Semantikmodellverbindung mit einer tabellarischen Modelldatenbank](#bkmk_connect)  
  
 [Konfigurieren von SharePoint-Berechtigungen für die BI-Semantikmodellverbindung](#bkmk_permissions)  
  
 [Nächste Schritte](#bkmk_next)  
  
##  <a name="bkmk_prereq"></a> Überprüfen der Voraussetzungen  
 Sie benötigen Teilnahmeberechtigungen oder weiterreichende Berechtigungen, um eine BI Semantikmodell-Verbindungsdatei zu erstellen.  
  
 Sie benötigen eine Bibliothek, die den Inhaltstyp der BI Semantikmodellverbindung unterstützt. Weitere Informationen finden Sie unter [Hinzufügen eines BI-Semantikmodell-Verbindungs-Inhaltstyps zu einer Bibliothek &#40;PowerPivot für SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/add-bi-semantic-model-connection-content-type-to-library.md).  
  
 Sie müssen den Server und den Datenbanknamen kennen, für die Sie eine BI-Semantikmodellverbindung einrichten. Analysis Services muss für den Tabellenmodus konfiguriert werden. Die Datenbanken, die auf dem Server ausgeführt werden, müssen Datenbanken für tabellarische Modelle sein. Anweisungen, wie Sie den Servermodus überprüfen, finden Sie unter [Bestimmen des Servermodus einer Analysis Services-Instanz](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
 In bestimmten Szenarien müssen die freigegebenen Dienste in einer SharePoint-Umgebung über Administratorberechtigungen für die Analysis Services-Instanz verfügen. Zu diesen Diensten gehören [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungen, Reporting Services-Dienstanwendungen und PerformancePoint-Dienstanwendungen. Bevor Sie Administratorberechtigungen erteilen können, müssen Sie die Identität dieser Dienstanwendungen kennen. Sie können die Identität mithilfe der Zentraladministration ermitteln.  
  
 Sie müssen SharePoint-Dienstadministrator sein, um Sicherheitsinformationen in der Zentraladministration anzuzeigen.  
  
 Sie müssen Analysis Services-Systemadministrator sein, um Administratorrechte in Management Studio zu erteilen.  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Auf für SharePoint muss über Webanwendungen zugegriffen werden, die den klassischen Authentifizierungsmodus verwenden. BI-Semantikmodellverbindungen zu externen Datenquellen hängen von klassischer Modusanmeldung ab. Weitere Informationen finden Sie unter [Power Pivot-Authentifizierung und -Autorisierung](../../analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization.md).  
  
 Alle Computer und Benutzer, die Teil der Verbindungssequenz sind, müssen in der gleichen Domäne bzw. vertrauenswürdigen Domäne (bidirektionale Vertrauensstellung) enthalten sein.  
  
##  <a name="bkmk_ssas"></a> Erteilen von Analysis Services-Administratorberechtigungen an gemeinsame Dienstanwendungen  
 Verbindungen zwischen SharePoint und einer Datenbank für tabellarische Modelle auf einem Analysis Services-Server werden manchmal von einem gemeinsamen Dienst im Namen des Benutzers hergestellt, der die Daten anfordert. Der Dienst, von dem die Anforderung stammt, könnte eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung, Reporting Services-Dienstanwendung oder PerformancePoint-Dienstanwendung sein. Damit die Verbindung erfolgreich verläuft, muss der Dienst über Administratorberechtigungen für den Analysis Services-Server verfügen. In Analysis Services ist nur ein Administrator berechtigt, die Identität eines anderen Benutzers anzunehmen und für diesen eine Verbindung herzustellen.  
  
 Wenn die Verbindung unter folgenden Bedingungen verwendet wird, sind Administratorberechtigungen erforderlich:  
  
-   Wenn die Verbindungsinformationen während der Konfiguration einer Datei für eine BI-Semantikmodellverbindung überprüft werden.  
  
-   Wenn ein Power View-Bericht unter Verwendung einer BI-Semantikmodellverbindung gestartet wird.  
  
-   Wenn ein PerformancePoint-Webpart unter Verwendung einer BI-Semantikmodellverbindung aufgefüllt wird.  
  
 Um sicherzustellen, dass diese Verhaltensweisen erwartungsgemäß sind, erteilen Sie jeder Dienstidentität Administratorberechtigungen für die Analysis Services-Instanz. Verwenden Sie die folgenden Anweisungen, um die erforderliche Berechtigung zu erteilen.  
  
 **Hinzufügen von Dienstidentitäten zur Serveradministratorrolle**  
  
1.  Stellen Sie in SQL Server Management Studio eine Verbindung mit der Analysis Services-Instanz her.  
  
2.  Klicken Sie mit der rechten Maustaste auf den Servernamen, und wählen Sie **Eigenschaften**aus.  
  
3.  Klicken Sie auf **Sicherheit**, und klicken Sie anschließend auf **Hinzufügen**. Geben Sie das Windows-Benutzerkonto ein, das zum Ausführen der Dienstanwendung verwendet wird.  
  
     Sie können die Identität mithilfe der Zentraladministration ermitteln. Öffnen Sie im Abschnitt „Sicherheit“ die Option **Dienstkonten konfigurieren** , um festzustellen, welches Windows-Konto dem für die einzelnen Anwendungen verwendeten Dienstanwendungspool zugeordnet ist. Befolgen Sie anschließend die Anweisungen in diesem Thema, um dem Konto Administratorberechtigungen zu erteilen.  
  
##  <a name="bkmk_BISM"></a> Erteilen von Leseberechtigungen für die Datenbank für tabellarische Modelle  
 Da die Datenbank auf einem Server außerhalb der Farm ausgeführt wird, müssen im Rahmen der Verbindungseinrichtung Datenbankbenutzerberechtigungen auf dem Analysis Services-Backend-Server erteilt werden. Analysis Services verwendet ein rollenbasiertes Berechtigungsmodell. Benutzer, die eine Verbindung mit Modelldatenbanken herstellen, müssen dazu Leseberechtigungen oder höher über eine Rolle verwenden, die Lesezugriff auf die Elemente gewährt.  
  
 Rollen und gelegentlich Rollenmitgliedschaft werden definiert, wenn das Modell in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]erstellt wird. Sie können Rollen nicht mithilfe von SQL Server Management Studio erstellen, aber Sie können einer Rolle, die bereits definiert ist, Mitglieder hinzufügen. Weitere Informationen zum Erstellen von Rollen finden Sie unter [Erstellen und Verwalten von Rollen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md).  
  
#### <a name="assign-role-membership"></a>Zuweisen der Rollenmitgliedschaft  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung mit der Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]her, erweitern Sie die Datenbank im Objekt-Explorer, und erweitern Sie dann **Rollen**. In der Regel wird eine Rolle angezeigt, die bereits definiert ist. Wenn keine Rolle vorhanden ist, wenden Sie sich an den Autor des Modells und fordern Sie die Hinzufügung einer Rolle an. Das Modell muss erneut bereitgestellt werden, damit die Rolle in Management Studio sichtbar wird.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Rolle, und wählen Sie **Eigenschaften**aus.  
  
3.  Fügen Sie auf der Seite "Mitgliedschaft" die Windows-Gruppen- und Benutzerkonten hinzu, die Zugriff erfordern.  
  
##  <a name="bkmk_connect"></a> Erstellen einer BI-Semantikmodellverbindung mit einer tabellarischen Modelldatenbank  
 Nachdem Sie Berechtigungen in Analysis Services festgelegt haben, können Sie zu SharePoint zurückkehren und eine BI-Semantikmodellverbindung erstellen.  
  
1.  Klicken Sie in der Bibliothek, die die BI-Semantikmodellverbindung enthalten soll, auf **Dokumente** im SharePoint-Menüband.  
  
2.  Klicken Sie in „Neues Dokument“ auf den Pfeil nach unten, und wählen Sie **BI-Semantikmodell-Verbindungsdatei** aus, um die Seite Neue BI-Semantikmodellverbindung zu öffnen.  
  
3.  Legen Sie die **Server** -Eigenschaft und die **Database** -Eigenschaft fest. Wenn Sie sich beim Datenbanknamen nicht sicher sind, zeigen Sie mithilfe von SQL Server Management Studio eine Liste der auf dem Server bereitgestellten Datenbanken an.  
  
     **Servername** ist entweder der Netzwerkname des Servers, die IP-Adresse oder der vollqualifizierte Domänenname (z.B. „myserver.mydomain.corp.adventure-works.com“). Wenn der Server als benannte Instanz installiert wird, geben Sie den Servernamen in diesem Format ein: Computername\Instanzname.  
  
     **Datenbank** muss eine Tabellendatenbank sein, die aktuell auf dem Server verfügbar ist. Geben Sie keine andere BI Semantikmodell-Verbindungsdatei, Office-Datenverbindungsdatei, (.odc), Analysis Services-OLAP-Datenbank oder [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe an. Um den Datenbanknamen abzurufen, können Sie Management Studio verwenden, um eine Verbindung mit dem Server herzustellen und die Liste der verfügbaren Datenbanken anzuzeigen. Verwenden Sie die Eigenschaftenseite der Datenbank, um sicherzustellen, dass Sie den richtigen Namen angeben.  
  
4.  Klicken Sie auf **OK** , um die Seite zu speichern. An diesem Punkt wird die Verbindung von der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung überprüft.  
  
     Die Überprüfung ist erfolgreich, wenn die Verbindungsinformationen richtig sind und Sie der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung Administratorberechtigungen gewährt haben, damit diese im Namen des aktuellen Benutzers eine Verbindung mit Analysis Services herstellen kann.  
  
     Die Überprüfung schlägt fehl, wenn die Verbindungsinformationen falsch sind oder die Dienstanwendung keine ausreichenden Berechtigungen aufweist. Auf der Seite wird eine Überprüfungsmeldung mit der Frage angezeigt, ob Sie die Datei speichern möchten. Wenn Sie wissen, dass die Verbindung gültig ist, sollten Sie die Datei auf jeden Fall speichern, da der Fehler wahrscheinlicher auf fehlende Berechtigungen als auf ungültige Verbindungsinformationen zurückzuführen ist.  
  
     Sie können die Verbindung überprüfen, indem Sie sie in Excel oder Power View verwenden, um eine Verbindung mit einer Datenbank für tabellarische Modelle herzustellen. Wenn die Datenquellenverbindung erfolgreich ist, ist die Verbindung trotz der Überprüfungswarnung gültig.  
  
##  <a name="bkmk_permissions"></a> Konfigurieren von SharePoint-Berechtigungen für die BI-Semantikmodellverbindung  
 Damit eine BI-Semantikmodellverbindung als Datenquelle für eine Excel-Arbeitsmappe oder einen Reporting Services-Bericht verwendet werden kann, muss das BI-Semantikmodell-Verbindungselement über **Leseberechtigungen** in einer SharePoint-Bibliothek verfügen. Die Berechtigungsebene „Lesen“ schließt die Berechtigung **Elemente öffnen** ein, die das Herunterladen von BI-Semantikmodell-Verbindungsinformationen in eine Excel-Desktopanwendung ermöglicht.  
  
 Es gibt mehrere Möglichkeiten, Berechtigungen in SharePoint zu erteilen. Die folgenden Anweisungen erläutern, wie Sie eine neue Gruppe mit dem Namen **BISM-Benutzer** erstellen, die die Berechtigungsstufe **Lesen** haben.  
  
 Sie müssen Websitebesitzer sein, um Berechtigungen zu ändern.  
  
1.  Klicken Sie in „Websiteaktionen“ auf **Websiteberechtigungen**.  
  
2.  Klicken Sie auf **Gruppe erstellen** , und nennen Sie die neue Gruppe **BISM-Benutzer**.  
  
3.  Wählen Sie die Berechtigungsstufe **Lesen** aus, und klicken Sie auf **Erstellen**.  
  
4.  Wählen Sie **BISM-Benutzer** in „Personen und Gruppen“ aus.  
  
5.  Zeigen Sie auf „Neu“, klicken Sie auf **Benutzer hinzufügen**, und fügen Sie dann Benutzer- oder Gruppenkonten hinzu.  
  
     Diese Benutzer und die Gruppen haben jetzt Leseberechtigungen überall in der Website, einschließlich aller Bibliotheken und Listen, die Berechtigungen von der Websiteebene erben. Wenn diese Berechtigungen zu hoch sind, können Sie diese Gruppe aus bestimmten Bibliotheken, Listen oder Elementen selektiv entfernen.  
  
 Um Berechtigungen auf Elementebene selektiv zu entfernen, gehen Sie wie folgt vor:  
  
1.  Wählen Sie in einer Bibliothek ein Dokument aus. Klicken Sie auf den rechten Pfeil nach unten, und klicken Sie auf **Berechtigungen verwalten**.  
  
2.  Standardmäßig erbt ein Element Berechtigungen. Um die Berechtigungen von einzelnen Dokumenten in dieser Bibliothek zu ändern, klicken Sie auf **Berechtigungsvererbung beenden**.  
  
3.  Aktivieren Sie das Kontrollkästchen neben **BISM-Benutzer**.  
  
4.  Klicken Sie auf **Benutzerberechtigungen entfernen**.  
  
##  <a name="bkmk_next"></a> Nächste Schritte  
 Nachdem Sie eine BI-Semantikmodellverbindung erstellt und gesichert haben, können Sie sie als Datenquelle angeben. Weitere Informationen finden Sie unter [Verwenden einer BI-Semantikmodellverbindung in Excel oder Reporting Services](../../analysis-services/power-pivot-sharepoint/use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md).  
  
## <a name="see-also"></a>Siehe auch  
 [PowerPivot-BI-Semantikmodell-Verbindung &#40;.bism&#41;](../../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)   
 [Erstellen einer BI-Semantikmodellverbindung zu einer PowerPivot-Arbeitsmappe](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md)  
  
  

