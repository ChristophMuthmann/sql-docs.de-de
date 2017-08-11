---
title: "Implementierungsanforderungen für benutzerdefinierte Berichtselemente | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom report items
ms.assetid: cfacd816-00d6-4a3d-be72-1bba6f7f6886
caps.latest.revision: 22
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 43770b0b167e2a40874d1b8f31b3b146e62ec2b5
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="custom-report-item-implementation-requirements"></a>Implementierungsanforderungen für benutzerdefinierte Berichtselemente
  In diesem Thema werden die Voraussetzungen zur Entwicklung und Bereitstellung von benutzerdefinierten Berichtselementen erläutert.  
  
## <a name="development-and-deployment-requirements"></a>Entwicklungs- und Bereitstellungsanforderungen  
 Die Entwicklung eines benutzerdefinierten Berichtselements für [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] erfordert Folgendes:  
  
-   Administratorzugriff auf einem Server mit [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] und [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
-   [!INCLUDE[vsprvsext](../../includes/vsprvsext-md.md)]oder höher mit der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Software Development Kit (SDK) installiert.  
  
-   Zugriff auf die [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -SDK-Dokumentation.  
  
-   Kenntnisse über die Komponentenerstellung und die Komponentenmodell-Namespaces in [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Weitere Informationen finden Sie in "Erstellen von Komponenten" und "Namespaces für Komponentenmodelle in Visual Studio" auf msdn.microsoft.com.  
  
## <a name="language-and-namespace-requirements"></a>Sprach- und Namespace-Anforderungen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]benutzerdefinierte Berichtselemente vollständig unterstützen die [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Sie können benutzerdefinierte Berichtselemente mithilfe einer Auswahl .NET-kompatibler Sprachen entwickeln.  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]bietet dem Entwickler die viele Tools und Funktionen zu vereinfachen und beschleunigen die iterativen Zyklen aus der Codierung, debugging und testen und um die Bereitstellung zu vereinfachen. Das [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -SDK enthält [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] und C#-Compiler sowie zugehörige Tools.  
  
-   Benutzerdefinierte Berichtselemente verwenden die **Microsoft.ReportDesigner** und <xref:Microsoft.ReportingServices.Interfaces> Namespaces. Diese werden in den Assemblys Microsoft.ReportingServices.Designer.DLL und Microsoft.ReportingServices.Interfaces.DLL gespeichert, die als Teil von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]installiert werden.  
  
-   Benutzerdefinierte Berichtselement-Entwurfszeitkomponenten müssen Schnittstellen aus der <xref:System.ComponentModel> Namespace in der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Die <xref:System.ComponentModel> finden Sie unter der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK-Dokumentation.  
  
> [!IMPORTANT]  
>  Standardmäßg wird [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installiert, das [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -SDK jedoch nicht. Die in diesem Abschnitt vorkommenden Links auf SDK-Inhalte funktionieren nur, wenn das SDK auf Ihrem Computer installiert und die SDK-Dokumentation in der Onlinedokumentation enthalten ist. Nach der Installation der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK, Sie können hinzufügen die SDK-Dokumentation der Onlinedokumentation und dem Inhaltsverzeichnis anhand der Anweisungen in [hinzufügen oder Entfernen von Produktdokumentation für SQL Server](http://msdn.microsoft.com/library/ef798cc8-87cf-4d60-a7bf-9e061bdd0052).  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen ein benutzerdefiniertes Element-Laufzeitkomponente](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [Erstellen einer benutzerdefinierten Bericht Element zur Entwurfszeit-Komponente](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)   
 [Vorgehensweise: Bereitstellen eines benutzerdefinierten Berichtselements](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)   
 [Klassenbibliotheken für benutzerdefinierten Berichts-Element](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)  
  
  
