---
title: Systemrolleneigenschaften (Management Studio) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.reportserver.systemroleproperties.f1
ms.assetid: 0210fc2a-74fb-41dd-8e39-4830047ec417
caps.latest.revision: 30
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 68038228fd6fb7b2af8dd6f1bb5ae50b7f63daac
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="system-role-properties-management-studio"></a>Systemrolleneigenschaften (Management Studio)
  Mithilfe der Seite Systemrollen können Sie die Systemrollendefinitionen anzeigen, die aktuell für den Berichtsserver definiert sind. Eine Systemrollendefinition enthält eine benannte Auflistung von Aufgaben, die in Bezug auf die gesamte Site statt nur für ein einzelnes Element ausgeführt werden. Rollendefinitionen werden Benutzern oder Gruppen zugewiesen, um eine Rollenzuweisung zu erstellen. Die Aufgaben in der Rollendefinition geben die Aktionen an, die der Benutzer oder die Gruppe ausführen kann.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]besitzt zwei vordefinierte Systemrollendefinitionen: **Systemadministrator** und **Systembenutzer**. Sie können die Rollendefinitionen ändern, indem Sie ihre Aufgabenlisten ändern. Oder Sie erstellen eine neue Systemrolle, die eine andere Kombination von Aufgaben unterstützt. Die Bearbeitung einer Rollendefinition wirkt sich auf alle Rollenzuweisungen aus, die diese Rollendefinition enthalten.  
  
> [!NOTE]  
>  Systemrollenzuweisungen werden nur auf einem Berichtsserver verwendet, der im einheitlichen Modus ausgeführt wird. Ist der Berichtsserver für den integrierten SharePoint-Modus konfiguriert, ist diese Seite nicht verfügbar.  
  
## <a name="options"></a>enthalten  
 **Name**  
 Gibt den Namen der Systemrollendefinition an.  
  
 **Description**  
 Zeigt eine Beschreibung der Systemrollendefinition. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]wird diese Beschreibung nur auf dieser Seite angezeigt. Benutzer, die dieses Element über den Berichts-Manager anzeigen, sehen diese Beschreibung möglicherweise, wenn Sie die Ordnerhierarchie durchsuchen.  
  
 **Task**  
 Listet alle Tasks auf Systemebene auf, die für diese Rollendefinition ausgewählt werden können. Sie können in der vordefinierten Aufgabenliste Elemente hinzufügen oder löschen, um zu definieren, wie Benutzer über die Rolle auf ein bestimmtes Element zugreifen können. Sie können keine neuen Tasks erstellen oder vorhandene Tasks ändern.  
  
 **Description**  
 Bietet Informationen zu den einzelnen Tasks. Taskbeschreibungen können Sie nicht ändern.  
  
## <a name="see-also"></a>Siehe auch  
 [Berichtsserver im Management Studio F1-Hilfe](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Aufgaben auf Systemebene](../../reporting-services/security/tasks-and-permissions-system-level-tasks.md)   
 [Aufgaben und Berechtigungen](../../reporting-services/security/tasks-and-permissions.md)   
 [Vordefinierte Rollen](../../reporting-services/security/role-definitions-predefined-roles.md)  
  
  
