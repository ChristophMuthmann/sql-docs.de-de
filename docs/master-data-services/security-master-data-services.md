---
title: Sicherheit (Master Data Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 56bc41ea-de28-4184-aa7e-99111ae55af5
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 200e7f97e0356fae1505bf3786ab11e483f839f8
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="security-master-data-services"></a>Sicherheit (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Verwenden Sie die Sicherheitseinstellungen in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], um dafür zu sorgen, dass Benutzer auf die speziellen Masterdaten zugreifen können, die sie für ihre Arbeit benötigen, nicht jedoch auf Daten, für die sie nicht zuständig sind.  
  
 Mithilfe der Sicherheit können Sie auch einem Administrator für ein bestimmtes Modell und einen Funktionsbereich bestimmen. Sie können es z. B. jemandem ermöglichen, Versionen des Kundenmodells zu erstellen oder Sicherheitsberechtigungen festzulegen.  
  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Sicherheit basiert auf lokalen oder Active Directory-Domänenbenutzern und -gruppen. Beim Bestimmen der Daten, auf die ein Benutzer zugreifen kann, können Sie mithilfe der MDS-Sicherheit eine präzise Detailebene verwenden. Aufgrund der hohen Detailgenauigkeit kann die Sicherheit leicht kompliziert werden. Gehen Sie deshalb bei der Verwendung sich überschneidender Benutzer und Gruppen vorsichtig vor. Weitere Informationen finden Sie unter [Überlappende Benutzer- und Gruppenberechtigungen &#40;Master Data Services&#41;](../master-data-services/overlapping-user-and-group-permissions-master-data-services.md).  
  
 Sie können den Sicherheitszugriff im Funktionsbereich **Benutzer- und Gruppenberechtigungen** der [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung oder mit dem Webdienst zuweisen.  
  
## <a name="types-of-users"></a>Arten von Benutzern  
 Es gibt zwei Arten von Benutzern in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]:  
  
-   Benutzer, die auf Daten in den Funktionsbereich **Explorer** zugreifen.  
  
-   Benutzer, die die Fähigkeit haben, administrative Tasks in anderen Bereichen als **Explorer**auszuführen. Diese Benutzer heißen [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
## <a name="how-to-set-security"></a>Festlegen der Sicherheit  
 Sie müssen Folgendes zuweisen, um einem Benutzer oder einer Gruppe die Berechtigung für den Zugriff zu erteilen:  
  
-   [Zugriff auf Funktionsbereiche](../master-data-services/functional-area-permissions-master-data-services.md). Damit wird bestimmt, auf welche der fünf Funktionsbereiche der Benutzeroberfläche ein Benutzer zugreifen kann.  
  
-   [Modellobjektberechtigungen](../master-data-services/model-object-permissions-master-data-services.md). Damit werden die Attribute bestimmt, auf die ein Benutzer zugreifen kann, und der Zugriffstyp (Lesen, Erstellen und Aktualisieren), den der Benutzer für diese Attribute besitzt. Der Benutzer kann auch Administratorberechtigungen auf der Modellebene zuweisen.  
  
-   [Hierarchieelementberechtigungen](../master-data-services/hierarchy-member-permissions-master-data-services.md)(optional). Damit werden die Elemente bestimmt, auf die ein Benutzer zugreifen kann, und der Zugriffstyp (Lesen, Aktualisieren und Löschen), den der Benutzer für diese Elemente besitzt.  
  
 Wenn Sie Attributen und Elementen Berechtigungen zuweisen, überschneiden sich die Berechtigungen. Dabei bestimmen Regeln, welche Berechtigung Vorrang hat. Weitere Informationen finden Sie unter [Vorgehensweise: Festlegen von Berechtigungen &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md).  
  
## <a name="security-in-the-add-in-for-excel"></a>Sicherheit im Add-In für Excel  
 Die in der [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Webanwendung festgelegten Sicherheitseinstellungen werden auch auf das [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]angewendet. Benutzer können nur die Daten anzeigen und verarbeiten, für die sie über Berechtigungen verfügen. Administratoren können administrative Tasks ausführen.  
  
 Es muss allerdings berücksichtigt werden, dass alle in [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] festgelegten Sicherheitseinstellungen in Excel erst nach 20 Minuten wirksam werden. Das Intervall wird durch die Einstellung *MdsMaximumUserInformationCacheInterval* in der Datei web.config definiert. Um das Intervall zu ändern, können Sie die Einstellung ändern und IIS neu starten.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Erstellen Sie einen Benutzer, der über die Vollberechtigung für ein Modell verfügt.|[Erstellen eines Modelladministrators &#40;Master Data Services&#41;](../master-data-services/create-a-model-administrator-master-data-services.md)|  
|Fügen Sie [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]eine Active Directory-Gruppe hinzu; dies ist der erste Schritt darin, einer Gruppe die Berechtigung für den Zugriff auf Daten in der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Webanwendung zu erteilen.|[Hinzufügen einer Gruppe &#40;Master Data Services&#41;](../master-data-services/add-a-group-master-data-services.md)|  
|Weisen Sie die Berechtigung einem Funktionsbereich der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Webanwendung zu.|[Zuweisen von Berechtigungen für Funktionsbereiche &#40;Master Data Services&#41;](../master-data-services/assign-functional-area-permissions-master-data-services.md)|  
|Weisen Sie die Berechtigung Attributwerten zu, indem Sie die Berechtigung zum Modellieren von Objekten zuweisen.|[Zuweisen von Berechtigungen für Modellobjekte &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)|  
|Weisen Sie die Berechtigung Elementwerten zu, indem Sie die Berechtigung Hierarchieknoten zuweisen.|[Zuweisen von Hierarchieelementberechtigungen &#40;Master Data Services&#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)   
 [Benutzer und Gruppen &#40;Master Data Services&#41;](../master-data-services/users-and-groups-master-data-services.md)   
 [Berechtigungen für Funktionsbereiche &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)   
 [Berechtigungen für Modellobjekte &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Berechtigungen für Hierarchieelemente &#40;Master Data Services&#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [Vorgehensweise: Festlegen von Berechtigungen &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  
