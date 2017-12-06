---
title: Integrieren von Reporting Services mithilfe der ReportViewer-Steuerelemente | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/06/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: application-integration
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- ReportViewer controls
- integrating reports [Reporting Services]
ms.assetid: 3ba47fb4-73a9-4059-89fd-329adebe94a8
caps.latest.revision: "26"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: b43ad81f907ff035170095bebbebc08b93526553
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="integrating-reporting-services-using-reportviewer-controls"></a>Integrieren von Reporting Services mithilfe der ReportViewer-Steuerelemente
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 2015 bietet zwei ReportViewer-Steuerelemente, mit denen Sie Berichtanzeigefunktionen in Ihre Anwendungen integrieren können. Es gibt eine Version für Windows Forms-Anwendungen und eine für WebForms-Anwendungen. Jedes Steuerelement verfügt über ähnliche Funktionen, wurde jedoch im Hinblick auf deren individuelle Umgebung konzipiert. Beide Steuerelemente können Berichte verarbeiten, die auf einem Berichtsserver bereitgestellt (Remoteverarbeitungsmodus) oder auf einen Computer kopiert wurden, auf dem [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nicht installiert ist (lokaler Verarbeitungsmodus).  
  
 DAs ReportViewer-Steuerelement enthält keine integrierte Unterstützung für dynamische Anpassung an verschiedene Geräte mit unterschiedlichen Bildschirmauflösungen.  
  
## <a name="remote-processing-mode"></a>Remoteverarbeitungsmodus  
 Der Remoteverarbeitungsmodus ist die bevorzugte Methode für die Anzeige von Berichten, die auf einen Berichtsserver übertragen wurden. Der Remoteverarbeitungsmodus bietet folgende Vorteile:  
  
-   Remoteverarbeitung ist eine optimierte Lösung für die Ausführung von Berichten, da der Bericht vom Berichtsserver verarbeitet wird.  
  
-   Da die gesamte Verarbeitung vom Berichtsserver gehandhabt wird, kann eine Berichtsanforderung von verschiedenen Berichtsservern in einer Anwendung für horizontales Skalieren oder auf einem Server mit mehreren Prozessoren für zentrales Skalieren verarbeitet werden.  
  
 Außerdem können im Remotemodus ausgeführte Berichte die kompletten Funktionen des Berichtsservers nutzen, einschließlich aller Rendering- und Datenerweiterungen.  
  
> [!NOTE]  
>  Die Liste der Erweiterungen, die für das Steuerelement ReportViewer im Remoteverarbeitungsmodus zur Verfügung stehen, hängt davon ab, welche Ausgabe von [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] auf dem Berichtsserver installiert ist.  
  
## <a name="local-processing-mode"></a>Lokaler Verarbeitungsmodus  
 Der lokale Verarbeitungsmodus stellt eine alternative Methode zum Anzeigen und Rendern von Berichten dar, wenn [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nicht installiert ist. Anders als bei der Remoteverarbeitung steht dem Steuerelement nur ein Teil der Funktionen zur Verfügung, die der Berichtsserver eigentlich enthält. Im lokalen Verarbeitungsmodus wird die Datenverarbeitung nicht vom Steuerelement gehandhabt, sondern sie wird von der Hostinganwendung implementiert. Die Berichtsverarbeitung wird jedoch vom Steuerelement selbst gehandhabt. Im lokalen Verarbeitungsmodus stehen nur die PDF-, Excel-, Word- und Bild-Renderingerweiterungen zur Verfügung.  
  
## <a name="see-also"></a>Siehe auch  
 [Integration von Reporting Services in Anwendungen](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [Verwenden des ReportViewer-Steuerelements in WebForms](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)   
 [Verwenden des ReportViewer-Steuerelements in WinForms](../../reporting-services/application-integration/using-the-winforms-reportviewer-control.md)  

  
  
