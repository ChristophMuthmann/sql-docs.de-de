---
title: Verbinden von PowerPivot-Dienstanwendung in SharePoint-Web-App in der Zertifizierungsstelle | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: power-pivot-sharepoint
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a5da8e29-7ffd-44e7-bf61-344fa5bea8ce
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cbaf5f7fce645c4133c94a5ae1562b7aabcfc897
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="connect-power-pivot-service-app-to-sharepoint-web-app-in-ca"></a>Verbinden von PowerPivot-Dienstanwendung in SharePoint-Web-App in der Zertifizierungsstelle
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
  
4.  Wählen Sie unter **Folgende Zuordnungsgruppe bearbeiten**die Option **[Benutzerdefiniert]**aus.  
  
5.  Aktivieren Sie das Kontrollkästchen neben jeder Dienstanwendungsverbindung, die Sie verwenden möchten. Falls Sie über mehrere [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Dienstanwendungen verfügen (am Typ **Proxy der Power Pivot-Dienstanwendung**erkennbar), achten Sie darauf, nur eine auszuwählen.  
  
6.  Klicken Sie auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Konfigurieren einer PowerPivot-Dienstanwendung in der Zentraladministration](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)   
 [Anfängliche Konfiguration (PowerPivot für SharePoint)](http://msdn.microsoft.com/en-us/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146)  
  
  

