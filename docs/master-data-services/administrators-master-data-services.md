---
title: Administratoren (Master Data Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- administrators [Master Data Services], about administrators
- administrators [Master Data Services]
- models [Master Data Services], administrators
ms.assetid: d330aa4e-6ade-4b09-b376-1b15d6c78f7d
caps.latest.revision: 14
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 76e3c0c6c0bc16ef7a8f1bfe9bd723cd9d35bc6c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="administrators-master-data-services"></a>Administratoren (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In diesem Artikel werden die verschiedenen Administratortypen in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]beschrieben: Modelladministrator, Entitätsadministrator und Administrator.  
  
## <a name="model-administrators"></a>Modelladministratoren  
 In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]wird ein Benutzer als Modelladministrator bezeichnet, wenn er für das Modellobjekt der obersten Ebene über die in der Registerkarte **Model Objects** (Modellobjekte) zugewiesene **Administratorberechtigung** verfügt. Wenn ein Benutzer die Administratorberechtigung für ein bestimmtes Modell besitzt, werden alle anderen Berechtigungen für untergeordnete Objekte des Modells (sowohl Modellobjekt- als auch Elementberechtigungen) von der **Administratorberechtigung** des Modells übertrumpft und ignoriert.  
  
-   Wenn der Benutzer Zugriff auf den Funktionsbereich **Explorer** hat, kann er alle Masterdaten in diesem Bereich hinzufügen, löschen und aktualisieren.  
  
-   Wenn der Benutzer Zugriff auf andere Funktionsbereiche hat, kann der Benutzer alle im Funktionsbereich verfügbaren administrativen Tasks ausführen.  
  
 Jedes Modell kann mehrere Administratoren aufweisen. Ein Benutzer kann als Modelladministrator für ein Modell, mehrere oder alle Modelle in der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Bereitstellung definiert sein.  
  
 Er wird entweder in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] oder programmgesteuert als Modelladministrator festgelegt. Weitere Informationen finden Sie unter [Erstellen eines Modelladministrators &#40;Master Data Services&#41;](../master-data-services/create-a-model-administrator-master-data-services.md).  
  
## <a name="entity-administrators"></a>Entitätsadministratoren  
 In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]wird ein Benutzer als Entitätsadministrator bezeichnet, wenn er für das Entitätsobjekt über die in der Registerkarte „Model Objects“(Modellobjekte) zugewiesene Administratorberechtigungen verfügt. Wenn ein Benutzer Administratorberechtigungen für eine Entität hat, werden alle anderen Berechtigungen für untergeordnete Objekte der Entität (sowohl Modellobjekt- als auch Elementberechtigungen) von den Administratorberechtigungen abgelöst und ignoriert.  
  
-   Wenn der Benutzer Zugriff auf den Funktionsbereich **Explorer** hat, kann er alle Masterdaten in diesem Bereich hinzufügen, löschen und aktualisieren.  
  
-   Wenn die Entitätsänderungen eine Administratorberechtigung erfordern, kann ein Entitätsadministrator die Änderungen prüfen und Changesets anschließend zulassen oder ablehnen.  
  
 Jede Entität kann mehrere Administratoren besitzen. Jeder Benutzer kann als Entitätsadministrator für eine, mehrere oder alle Entitäten definiert sein.  
  
 Er wird entweder in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] oder programmgesteuert als Entitätsadministrator festgelegt. Weitere Informationen finden Sie unter [Erstellen eines Entitätsadministrators &#40;Master Data Services&#41;](../master-data-services/create-an-entity-administrator-master-data-services.md).  
  
## <a name="master-data-services-super-user"></a>Master Data Services-Administrator  
 In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]können Sie einem Benutzer Berechtigungen für den Funktionsbereich „Administrator“ zuweisen. Ein Benutzer mit Berechtigungen für den Funktionsbereich „Administrator“ verfügt über Administratorberechtigungen für alle Modelle und über Berechtigungen für alle anderen Funktionsbereiche. Informationen zu den Berechtigungen für Funktionsbereiche finden Sie unter [Berechtigungen für Funktionsbereiche &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
 Der Standardadministrator wird für das **Administratorkonto** angegeben, wenn mithilfe des [Datenbankerstellungs-Assistenten &#40;Master Data Services-Konfigurations-Manager&#41;](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md) die [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]-Datenbank erstellt wird.  
  
 Der Administrator verfügt über die folgenden Berechtigungen:  
  
-   Zugriff auf alle Funktionsbereiche  
  
-   Hinzufügen, Löschen und Aktualisieren aller Masterdaten für alle Modelle im Funktionsbereich **Explorer**  
  
 Sie können mehreren Benutzer bzw. Benutzergruppen Administratorberechtigungen zuweisen.  
  
## <a name="comparing-administrator-types"></a>Vergleichen von Administratortypen  
  
|Administratortyp|Description|  
|------------------------|-----------------|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Administrator|Im [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] zugewiesene Berechtigungen wirken sich nicht auf den Zugriff des Administrators aus.<br /><br /> Kann ein Administrator sein, je nach den explizit zugewiesenen oder von einer Gruppe geerbten Berechtigungen für Funktionsbereiche.<br /><br /> Verfügt automatisch über alle Berechtigungen für alle Modelle.<br /><br /> Verfügt automatisch über Zugriff auf alle Funktionsbereiche.|  
|Modelladministrator|Kann ein Modelladministrator sein, je nach den explizit zugewiesenen oder von einer Gruppe geerbten Adminberechtigungen.<br /><br /> Verfügt nur über Zugriff auf Funktionsbereiche, für die ihm eine Berechtigung gewährt wurde.<br /><br /> Verfügt automatisch über alle Berechtigungen für alle Objekte und Elemente in dem bestimmten Modell.|  
|Entitätsadministrator|Kann ein Entitätsadministrator sein, je nach den explizit zugewiesenen oder von einer Gruppe geerbten Administratorberechtigungen.<br /><br /> Verfügt nur über Zugriff auf Funktionsbereiche, für die ihm eine Berechtigung gewährt wurde.<br /><br /> Verfügt automatisch über alle Berechtigungen für alle Objekte und Elemente in der bestimmten Entität.<br /><br /> Können die ausstehenden Changesets genehmigen, wenn die Entitätsänderungen genehmigt werden müssen.|  
  
## <a name="external-resources"></a>Externe Ressourcen  
 Blogbeitrag [Sicherheitsverbesserungen](http://go.microsoft.com/fwlink/p/?LinkId=615376), auf msdn.com.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen eines Modelladministrators &#40;Master Data Services&#41;](../master-data-services/create-a-model-administrator-master-data-services.md)   
 [Erstellen einer Master Data Services-Datenbank](../master-data-services/install-windows/create-a-master-data-services-database.md)   
 [Benachrichtigungen &#40;Master Data Services&#41;](../master-data-services/notifications-master-data-services.md)  
  
  
