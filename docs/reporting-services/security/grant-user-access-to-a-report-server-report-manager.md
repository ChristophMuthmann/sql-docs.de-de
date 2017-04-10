---
title: "Gew&#228;hren von Benutzerzugriff auf einen Berichtsserver (Berichts-Manager) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Entfernen von Rollenzuweisungen"
  - "Berechtigungen [Reporting Services], Erteilen des Zugriffs auf Berichtsserver"
  - "Rollen [Reporting Services], Zuweisungen"
  - "Ändern von Rollenzuweisungen"
  - "Löschen von Rollenzuweisungen"
ms.assetid: 2144c020-3253-4b47-8cda-e14c928bb471
caps.latest.revision: 54
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 54
---
# Gew&#228;hren von Benutzerzugriff auf einen Berichtsserver (Berichts-Manager)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] verwendet rollenbasierte Sicherheit, um Benutzerzugriff auf einen Berichtsserver zu gewähren. Bei der Installation eines neuen Berichtsservers haben nur Benutzer, die Mitglieder der lokalen Administratorengruppe sind, Zugriff auf Berichtsserverinhalte und -vorgänge. Damit der Berichtsserver auch von anderen Benutzern verwendet werden kann, müssen Sie Rollenzuweisungen erstellen, mit denen Benutzer- oder Gruppenkonten einer vordefinierten Rolle zugeordnet werden, die eine Auflistung von Tasks festlegt.  
  
 **Berichtsserver im SharePoint-Modus:** Für Berichtsserver, die für den integrierten SharePoint-Modus konfiguriert sind, muss der Zugriff von einer SharePoint-Website mit SharePoint-Berechtigungen konfiguriert werden. Die Berechtigungsebenen der SharePoint-Website legen den Zugriff auf Berichtsserverinhalt und -vorgänge fest. Sie müssen Websiteadministrator sein, um Berechtigungen auf einer SharePoint-Website gewähren zu können. Weitere Informationen finden Sie unter [Erteilen von Berechtigungen für Berichtsserverelemente auf einer SharePoint-Website](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md).  
  
 **Berichtsserver im einheitlichen Modus:** In diesem Thema liegt der Schwerpunkt auf einem für den einheitlichen Modus konfigurierten Berichtsserver und der Verwendung des Berichts-Managers zum Zuweisen von Benutzern zu Rollen. Die folgenden beiden Rollen stehen zur Verfügung:  
  
-   Rollen auf Elementebene werden verwendet, um Berichtsserverinhalte, Abonnements, Berichtsverarbeitung und Berichtsverlauf anzuzeigen, hinzuzufügen und zu verwalten. Rollenzuweisungen auf Elementebene werden im Stammknoten (dem Stammordner) oder in bestimmten Ordnern oder Elementen weiter unten in der Hierarchie definiert.  
  
-   Rollen auf Systemebene gewähren Zugriff auf siteweite Vorgänge, die an kein bestimmtes Element gebunden sind. Beispiele sind die Verwendung des Berichts-Generators und die Verwendung von freigegebenen Zeitplänen.  
  
     Diese beiden Rollentypen ergänzen sich gegenseitig und sollten zusammen verwendet werden. Das Hinzufügen eines Benutzers zu einem Berichtsserver ist daher ein Vorgang mit zwei Teilvorgängen. Wenn Sie einen Benutzer einer Rolle auf Elementebene zuweisen, sollten Sie ihn ebenfalls einer Rolle auf Systemebene zuweisen. Beim Zuweisen eines Benutzers zu einer Rolle müssen Sie eine bereits definierte Rolle wählen. Verwenden Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], um Rollen zu erstellen, zu ändern oder zu löschen. Weitere Informationen finden Sie unter [Erstellen, Löschen oder Ändern einer Rolle &#40;Management Studio&#41;](../../reporting-services/security/create-delete-or-modify-a-role-management-studio.md).  
  
## Vorbereitungen  
 Überprüfen Sie die folgende Liste vor dem Hinzufügen von Benutzern zu einem Berichtsserver im einheitlichen Modus.  
  
-   Sie müssen ein Mitglied der lokalen Administratorengruppe auf dem Berichtsservercomputer sein. Wenn Sie [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] auf [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] oder Windows Server 2008 bereitstellen, sind zusätzliche Konfigurationsschritte erforderlich, bevor Sie einen Berichtsserver lokal verwalten können. Weitere Informationen finden Sie unter [Konfigurieren eines Berichtsservers im einheitlichen Modus für die lokale Verwaltung &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
-   Um diese Aufgabe an andere Benutzer zu delegieren, erstellen Sie Rollenzuweisungen, die Benutzerkonten den Rollen Inhalts-Manager und Systemadministrator zuordnen. Benutzer, die über Inhalts-Manager- und Systemadministrator-Berechtigungen verfügen, können einem Berichtsserver Benutzer hinzufügen.  
  
-   Sehen Sie sich in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]die vordefinierten Systemrollen und Benutzerrollen an, damit Ihnen die mit den einzelnen Rollen verbundenen Tasks vertraut sind. Im Berichts-Manager stehen keine Taskbeschreibungen zur Verfügung, sodass Sie die Rollen kennen sollten, bevor Sie Benutzer hinzufügen.  
  
-   Passen Sie die Rollen optional an, oder definieren Sie zusätzliche Rollen, um die Auflistung von benötigten Tasks einzuschließen. Wenn Sie zum Beispiel benutzerdefinierte Sicherheitseinstellungen für einzelne Elemente verwenden möchten, können Sie eine neue Rollendefinition erstellen, die Lesezugriff für Ordner gewährt.  
  
### So fügen Sie einer Systemrolle einen Benutzer oder eine Gruppe hinzu  
  
1.  Starten Sie den [Berichts-Manager im einheitlichen SSRS-Modus](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md).  
  
2.  Klicken Sie auf **Siteeinstellungen**.  
  
3.  Klicken Sie auf **Sicherheit**.  
  
4.  Klicken Sie auf **Neue Rollenzuweisung**.  
  
5.  Geben Sie unter **Gruppen- oder Benutzername** ein Windows-Domänenbenutzer- oder ein -Gruppenkonto im folgenden Format ein: \<Domäne>\\<Konto\>. Wenn Sie die Formularauthentifizierung oder die benutzerdefinierte Sicherheit verwenden, geben Sie das Benutzer- oder Gruppenkonto in dem für Ihre Bereitstellung richtigen Format an.  
  
6.  Wählen Sie eine Systemrolle aus, und klicken Sie anschließend auf **OK**.  
  
     Rollen sind kumulativ, das heißt, wenn Sie sowohl die Systemadministrator- als auch die Systembenutzerrolle wählen, kann ein Benutzer oder eine Gruppe die Tasks beider Rollen ausführen.  
  
7.  Wiederholen Sie den Vorgang, um weiteren Benutzern oder Gruppen Rollen zuzuweisen.  
  
### So fügen Sie einem Benutzer oder einer Gruppe eine Elementrolle hinzu  
  
1.  Starten Sie den **Berichts-Manager** , und suchen Sie das Berichtselement, für das Sie einen Benutzer oder eine Gruppe hinzufügen möchten.  
  
2.  Zeigen Sie auf das Element, und klicken Sie auf den Dropdownpfeil.  
  
3.  Klicken Sie im Dropdownmenü auf **Sicherheit**.  
  
4.  Klicken Sie auf **Neue Rollenzuweisung**.  
  
    > [!NOTE]  
    >  Falls ein Element aktuell die Sicherheitseinstellungen eines übergeordneten Elements erbt, klicken Sie auf der Symbolleiste auf **Elementsicherheit bearbeiten** , um die Sicherheitseinstellungen zu ändern. Klicken Sie dann auf **Neue Rollenzuweisung**.  
  
5.  Geben Sie unter **Gruppen- oder Benutzername** ein Windows-Domänenbenutzer- oder ein -Gruppenkonto im folgenden Format ein: \<Domäne>\\<Konto\>. Wenn Sie die Formularauthentifizierung oder die benutzerdefinierte Sicherheit verwenden, geben Sie das Benutzer- oder Gruppenkonto in dem für Ihre Bereitstellung richtigen Format an.  
  
6.  Wählen Sie mindestens eine Rollendefinition aus, die beschreibt, wie der Benutzer oder die Gruppe auf das Element zugreifen soll, und klicken Sie dann auf **OK**.  
  
7.  Wiederholen Sie den Vorgang, um weiteren Benutzern oder Gruppen Rollen zuzuweisen.  
  
## Siehe auch  
 [Erstellen und Verwalten von Rollenzuweisungen](../../reporting-services/security/create-and-manage-role-assignments.md)   
 [Neue Rollenzuweisung: Seite „Rollenzuweisung bearbeiten“ &#40;Berichts-Manager&#41;](../Topic/New%20Role%20Assignment:%20Edit%20Role%20Assignment%20Page%20\(Report%20Manager\).md)   
 [Sicherheit (Eigenschaftenseite) &#40;Elemente, Berichts-Manager&#41;](../Topic/Security%20Properties%20Page,%20Items%20\(Report%20Manager\).md)   
 [Rollenzuweisungen](../../reporting-services/security/role-assignments.md)   
 [Rollendefinitionen](../../reporting-services/security/role-definitions.md)  
  
  