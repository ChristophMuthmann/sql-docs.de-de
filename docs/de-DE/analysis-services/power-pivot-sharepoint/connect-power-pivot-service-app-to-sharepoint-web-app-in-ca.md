---
title: Verbinden von PowerPivot-Dienstanwendung in SharePoint-Web-App in der Zertifizierungsstelle | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a8e73be1fc5851ca1cb54b08083218c232e74303
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="connect-power-pivot-service-app-to-sharepoint-web-app-in-ca"></a>Verbinden von PowerPivot-Dienstanwendung in SharePoint-Web-App in der Zertifizierungsstelle
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung kann von einer beliebigen Anzahl von SharePoint-Webanwendungen in der Farm verwendet werden. Um eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung zur Verfügung zu stellen, fügen Sie sie einer Dienstzuordnungsliste hinzu.  
  
> [!IMPORTANT]  
>  Damit das [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Management-Dashboard ordnungsgemäß funktioniert, muss eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung in der Standardgruppe enthalten sein. Fügen Sie nicht mehr als eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung zu der Standardgruppe hinzu. Das Hinzufügen mehrerer Einträge des gleichen Dienstanwendungstyps ist keine unterstützte Konfiguration und könnte Fehler verursachen. Wenn Sie zusätzliche Dienstanwendungen erstellen, fügen Sie sie benutzerdefinierten Listen hinzu.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
 [Hinzufügen einer Power Pivot-Dienstanwendung zur Standardgruppe](#default)  
  
 [Hinzufügen einer Power Pivot-Dienstanwendung zu einer benutzerdefinierten Dienstzuordnungsliste](#custom)  
  
##  <a name="default"></a> Hinzufügen einer Dienstanwendung zur Standardgruppe  
 Eine Dienstanwendungsliste ist eine Liste freigegebener Dienste, die Ressourcen für andere SharePoint-Webanwendungen in der Farm bereitstellen. Es gibt eine Standardgruppe von Dienstzuordnungen für die Farm.  
  
 Eine [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung kann der Liste entweder hinzugefügt werden, wenn Sie die Anwendung erstellen oder im Anschluss daran mithilfe folgender Schritte.  
  
1.  Klicken Sie in der Zentraladministration unter **Anwendungsverwaltung**auf **Dienstanwendungszuordnungen konfigurieren**.  
  
2.  Klicken Sie unter Anwendungsproxygruppe auf **Standard**.  
  
3.  Aktivieren Sie das Kontrollkästchen neben der [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung (durch den Typnamen **Proxy der Power Pivot-Dienstanwendung**gekennzeichnet). Bei mehreren [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung wählen Sie nur eine Anwendung aus.  
  
4.  Klicken Sie auf **OK**.  
  
##  <a name="custom"></a> Hinzufügen einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendung zu einer benutzerdefinierten Dienstzuordnungsliste  
 Die Standardgruppe kann durch eine benutzerdefinierte Liste ersetzt werden. Eine benutzerdefinierte Liste wird speziell für eine einzelne SharePoint-Webanwendung erstellt. Dabei wird die Standardgruppe überschrieben und durch vom Farm- oder Dienstadministrator angegebene Dienstzuordnungen ersetzt. Wenn Sie mehrere [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungen erstellt haben, müssen Sie die zu verwendende Anwendung mithilfe einer benutzerdefinierten Liste angeben. Eine benutzerdefinierte Liste kann nicht von anderen Webanwendungen wiederverwendet werden. Sie gilt nur für die Webanwendung, für die sie erstellt wurde.  
  
1.  Klicken Sie in der Zentraladministration unter **Anwendungsverwaltung**auf **Webanwendungen verwalten**.  
  
2.  Wählen Sie die Anwendung (z. B. SharePoint -80) aus.  
  
3.  Klicken Sie in Webanwendungen unter „Verwalten“ auf **Dienstverbindungen**.  
  
4.  Wählen Sie unter **Folgende Zuordnungsgruppe bearbeiten**die Option **[Benutzerdefiniert]** aus.  
  
5.  Aktivieren Sie das Kontrollkästchen neben jeder Dienstanwendungsverbindung, die Sie verwenden möchten. Falls Sie über mehrere [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungen verfügen (am Typ **Proxy der Power Pivot-Dienstanwendung**erkennbar), achten Sie darauf, nur eine auszuwählen.  
  
6.  Klicken Sie auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Konfigurieren einer PowerPivot-Dienstanwendung in der Zentraladministration](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)   
 [Anfängliche Konfiguration (PowerPivot für SharePoint)](http://msdn.microsoft.com/en-us/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146)  
  
  
