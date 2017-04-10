---
title: "Problembehandlung f&#252;r eine PowerPivot f&#252;r SharePoint-Installation | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 97bc2ce7-af04-4372-ad79-c96b8c3417ab
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# Problembehandlung f&#252;r eine PowerPivot f&#252;r SharePoint-Installation
  Wenn Sie anstelle der erwateten Seiten und Funktionen Fehler erhalten, gehen Sie wie folgt vor.  
  
-   Lesen Sie die Versionsanmerkungen zu SharePoint sowie [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] , um Problemumgehungen für bekannte Installationsprobleme zu finden. Die Versionsanmerkungen werden mit den Installationsmedien sowie auf der Microsoft-Website bereitgestellt, von der Sie die Software heruntergeladen haben.  
  
    -   [Versionsanmerkungen zu SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)  
  
-   Weitere Informationen finden Sie im TechNet Wiki-Thema [Troubleshooting Installations of Power Pivot (and other add-ins)](http://social.technet.microsoft.com/wiki/contents/articles/13737.troubleshooting-installations-of-powerpivot-and-other-add-ins.aspx) (Behandeln von Problemen mit PowerPivot-Installationen (und anderen Add-Ins)).  
  
## Probleme  
  
### Miniaturbilder werden im PowerPivot-Katalog als rotes X dargestellt  
 Eine Möglichkeit besteht darin, dass die **[!INCLUDE[ssGemini](../includes/ssgemini-md.md)]-Funktionsintegration für Websitesammlungen** nicht aktiv ist. Führen Sie folgende Schritte aus:  
  
1.  Klicken Sie in der [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]-Katalogbibliothek auf **Siteeinstellungen**, entweder über das Zahnradsymbol ![SharePoint-Einstellungen](../analysis-services/media/as-sharepoint2013-settings-gear.png "SharePoint-Einstellungen") oder über die Liste **Home**.  
  
2.  Klicken Sie im Abschnitt **Websitesammlungsverwaltung** auf **Websitesammlungs-Features**.  
  
3.  Klicken Sie auf **Websitesammlungs-Features**.  
  
4.  Stellen Sie sicher, dass die **[!INCLUDE[ssGemini](../includes/ssgemini-md.md)]-Funktionsintegration für Websitesammlungen** auf **Aktiv** festgelegt ist.  
  
 Weitere Ursachen für dieses Problem finden Sie unter [Power Pivot Gallery shows Red X's for Icons](http://support.microsoft.com/kb/2361559) (Im PowerPivot-Katalog wird anstelle von Symbolen ein rotes X angezeigt) (http://support.microsoft.com/kb/2361559).  
  
  