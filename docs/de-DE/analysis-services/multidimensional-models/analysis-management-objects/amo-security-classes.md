---
title: AMO-Sicherheitsklassen | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: amo
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3f14e3c3dbf5ccacda2f714ace8adf88bd8e8857
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
 [Berechtigungen und Zugriffsrechte & #40; Analysis Services – mehrdimensionale Daten & #41;](http://msdn.microsoft.com/library/59fa3573-f985-46cb-8042-7da71bd59a7b)   
 [Einführung in AMO-Klassen](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [Logische Architektur & #40; Analysis Services – mehrdimensionale Daten & #41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Datenbankobjekte & #40; Analysis Services – mehrdimensionale Daten & #41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
