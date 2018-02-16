---
title: Rollen und Berechtigungen (Analysis Services) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [Analysis Services], about security
- security [Analysis Services - multidimensional data], about security
ms.assetid: bb885447-868b-4686-853c-8241f63d4370
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 77a8043d96f99543428121c3b98a58a7704ec0b2
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="roles-and-permissions-analysis-services"></a>Rollen und Berechtigungen (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Bietet rollenbasierte Autorisierungsmodell, die Zugriff auf Vorgänge, Objekte und Daten. Alle Benutzer, die auf eine [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Instanz oder -Datenbank zugreifen, müssen den Vorgang im Kontext einer Rolle ausführen.  
  
 Der [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] -Systemadministrator ist dafür verantwortlich, Mitgliedschaften für die **Serveradministratorrolle** zu gewähren, die uneingeschränkten Zugriff auf Servervorgänge bietet. Diese Rolle verfügt über feste Berechtigungen und kann nicht angepasst werden. Standardmäßig sind Mitglieder der lokalen Administratorgruppe automatisch Analysis Services-Systemadministratoren.  
  
 Benutzer, die keine Administratoren sind, und Daten abrufen oder verarbeiten, erhalten Zugriff über **Datenbankrollen**. Als Systemadministrator oder Datenbankadministrator können Sie die Rollen erstellen, mit denen die verschiedenen Zugriffsebenen innerhalb einer bestimmten Datenbank beschrieben werden, und jedem Benutzer, der Zugriff benötigt, eine Mitgliedschaft zuweisen. Jede Rolle besitzt einen benutzerdefinierten Satz von Berechtigungen, mit denen Benutzer in einer bestimmten Datenbank auf Objekte und Vorgänge zugreifen können. Sie können Berechtigungen auf folgenden Ebenen zuweisen: Datenbank, innere Objekte wie Cubes und Dimensionen (aber keine Perspektiven) sowie Zeilen.  
  
 Üblicherweise erfolgt das Erstellen von Rollen und Zuweisen von Mitgliedschaften voneinander getrennt. Der Modellentwickler fügt Rollen häufig in der Entwurfsphase hinzu. Auf diese Weise werden alle Rollendefinitionen in den Projektdateien widergespiegelt, durch die das Modell definiert wird. Rollenmitgliedschaften werden in der Regel später eingerichtet, wenn die Datenbank in die Produktionsumgebung eingebunden wird. Dafür sind normalerweise Datenbankadministratoren zuständig, die Skripts erstellen, die entwickelt, getestet und als unabhängiger Vorgang ausgeführt werden können.  
  
 Die gesamte Autorisierung basiert auf einer gültigen Windows-Benutzeridentität. In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] wird ausschließlich die Windows-Authentifizierung zum Authentifizieren von Benutzeridentitäten verwendet. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]stellt keine proprietäre Authentifizierungsmethode bereit. Finden Sie unter [von Analysis Services Unterstützte Authentifizierungsmethoden](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md).  
  
> [!IMPORTANT]  
>  Berechtigungen sind additiv für jeden Windows-Benutzer/jede Windows-Gruppe, über alle Rollen in der Datenbank hinweg. Wenn eine Rolle dem Benutzer oder der Gruppe das Ausführen bestimmter Tasks oder das Anzeigen bestimmter Daten untersagt, eine andere Rolle dem Benutzer oder der Gruppe diese Berechtigung allerdings erteilt, dann ist der Benutzer oder die Gruppe berechtigt, den Task auszuführen bzw. die Daten anzuzeigen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Autorisieren des Zugriffs auf Objekte und Vorgänge &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
-   [Erteilen Sie Datenbankberechtigungen für &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)  
  
-   [Gewähren von Cube oder modellberechtigungen &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)  
  
-   [Erteilen Sie Berechtigungen zum Verarbeiten &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)  
  
-   [Erteilen von Leseberechtigungen Definition für Objektmetadaten &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md)  
  
-   [Erteilen von Berechtigungen für ein Datenquellenobjekt &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md)  
  
-   [Erteilen von Berechtigungen für Datamining-Strukturen und Modelle &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)  
  
-   [Erteilen von Berechtigungen für eine Dimension &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-dimension-analysis-services.md)  
  
-   [Erteilen von benutzerdefiniertem Zugriff auf die dimension von Daten &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)  
  
-   [Erteilen von benutzerdefiniertem Zugriff auf die Zelle von Daten &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Verwalten von Rollen &#40; SSAS – tabellarisch &#41;](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)  
  
  
