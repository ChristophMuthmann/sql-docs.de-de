---
title: AMO-Sicherheitsklassen | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Analysis Management Objects, security
- security [AMO]
- AMO, security
ms.assetid: e3d5012a-8121-40de-9244-1fc824228693
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b61917a7e0191e1645dedef69a311a8f901d12b9
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="amo-security-classes"></a>AMO-Sicherheitsklassen
  Dieses Thema enthält folgende Abschnitte:  
  
-   [Rollen und RoleMember-Objekte](#RolesMembers)  
  
-   [Berechtigungsobjekte](#Permissions)  
  
 Die folgende Abbildung zeigt die Beziehung der in diesem Thema erläuterten Klassen.  
  
 ![In diesem Thema im AMO-Sicherheitsklassen behandelt](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-securityclasses.gif "im AMO-Sicherheitsklassen in diesem Thema behandelt.")  
  
##  <a name="RolesMembers"></a>Rollen und RoleMember-Objekte  
 Ein <xref:Microsoft.AnalysisServices.Role>-Objekt wird erstellt, indem es der Rollenauflistung der Datenbank hinzugefügt und das <xref:Microsoft.AnalysisServices.Role>-Objekt auf dem Server mithilfe der Update-Methode aktualisiert wird. Ein <xref:Microsoft.AnalysisServices.Role> Objekt muss aktualisiert werden, bevor er verwendet werden kann.  
  
 So entfernen Sie eine <xref:Microsoft.AnalysisServices.Role> Objekt muss gelöscht werden, indem Sie mit der Drop-Methode, der die <xref:Microsoft.AnalysisServices.Role> Objekt. Die Remove-Methode aus der Rollenauflistung verhindert lediglich die Anzeige der Rolle in Ihrer Anwendung, Sie entfernt jedoch die Rolle nicht vom Server. Ein <xref:Microsoft.AnalysisServices.Role>-Objekt kann nicht gelöscht werden, wenn diesem Berechtigungen zugeordnet sind.  
  
 Ein <xref:Microsoft.AnalysisServices.RoleMember> Objekt wird erstellt, indem der Elementauflistung der Rolle einen Benutzer hinzufügen und Aktualisieren der <xref:Microsoft.AnalysisServices.Role> -Objekt auf dem Server mithilfe der Update-Methode. Nur Serveradministratoren und Datenbankadministratoren sind berechtigt, Rollen zu erstellen. Ein <xref:Microsoft.AnalysisServices.Role> Objekt auf dem Server aktualisiert werden muss, bevor eines seiner Member ist zulässig, die Objekte verwenden, die der Benutzer die Berechtigung verfügt.  
  
 Um ein <xref:Microsoft.AnalysisServices.RoleMember>-Objekt zu entfernen, muss es mithilfe der Remove-Methode der Auflistung aus der Auflistung entfernt werden, und anschließend muss die Rolle mithilfe der Update-Methode aktualisiert werden.  
  
 Weitere Informationen für diese Objekte verfügbaren Methoden und Eigenschaften finden Sie unter <xref:Microsoft.AnalysisServices.Role> und <xref:Microsoft.AnalysisServices.RoleMember> in der <xref:Microsoft.AnalysisServices>.  
  
##  <a name="Permissions"></a>Berechtigungsobjekte  
 Ein <xref:Microsoft.AnalysisServices.Permission> Objekt wird erstellt, indem es der berechtigungsauflistung des Objekts hinzugefügt, und Aktualisieren der <xref:Microsoft.AnalysisServices.Permission> -Objekt auf dem Server mithilfe der Update-Methode.  
  
 So entfernen Sie eine <xref:Microsoft.AnalysisServices.Permission> -Objekt, mit der Drop-Methode des Objekts gelöscht werden muss. Die Remove-Methode aus der Berechtigungsauflistung verhindert lediglich die Anzeige der Berechtigungen in Ihrer Anwendung, Sie entfernt jedoch das <xref:Microsoft.AnalysisServices.Permission>-Objekt nicht vom Server. Eine Rolle kann nicht gelöscht werden, wenn ihr eine Berechtigung zugeordnet ist.  
  
 Weitere Informationen zu verfügbaren Methoden und Eigenschaften finden Sie unter <xref:Microsoft.AnalysisServices.Permission> in <xref:Microsoft.AnalysisServices>.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.AnalysisServices>   
 [Programmieren AMO-Sicherheitsobjekten](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-security-objects.md)   
 [Berechtigungen und Zugriffsrechte &#40; Analysis Services – mehrdimensionale Daten &#41;](http://msdn.microsoft.com/library/59fa3573-f985-46cb-8042-7da71bd59a7b)   
 [Einführung in AMO-Klassen](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [Logische Architektur &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Datenbankobjekte &#40; Analysis Services – mehrdimensionale Daten &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
