---
title: "Debuggen von Code für Datenverarbeitungserweiterungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- debugging data processing extensions [Reporting Services]
- troubleshooting [Reporting Services], data processing extensions
- data processing extensions [Reporting Services], debugging
ms.assetid: e963e205-9ae0-446d-97df-028a1d2727d9
caps.latest.revision: "40"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6a21ea00e93516c6e6fd60e3102c618674a4304d
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="debugging-data-processing-extension-code"></a>Debuggen von Code für Datenverarbeitungserweiterungen
  Das [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] stellt mehrere hilfreiche Tools zum Debuggen bereit, die Sie bei der Analyse des Codes für Datenverarbeitungserweiterungen und bei der Fehlersuche darin unterstützen. Welches Tool dafür am besten geeignet ist, hängt von Ihrer Zielsetzung ab. In diesem Beispiel wird [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)]verwendet.  
  
#### <a name="to-debug-your-data-processing-extension-code"></a>So debuggen Sie Code für Datenverarbeitungserweiterungen  
  
1.  Starten Sie [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)], und öffnen Sie das Projekt für die Datenverarbeitungserweiterung.  
  
2.  Erstellen Sie das Projekt, und stellen Sie die Assembly der Datenverarbeitungserweiterung und die dazugehörige PDB-Datei im Berichts-Designer bereit. Weitere Informationen zur Bereitstellung finden Sie unter [Vorgehensweise: Bereitstellen einer Datenverarbeitungserweiterung für den Berichts-Designer](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-report-designer.md).  
  
3.  Öffnen Sie ein neues Berichtsprojekt in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], ohne vorher den Code für die Datenverarbeitungserweiterungen in einem anderen Fenster von [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] zu schließen.  
  
4.  Wechseln Sie zu dem [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]-Fenster, das das Projekt für die Datenverarbeitungserweiterung enthält, und legen Sie einige Breakpoints im Code fest.  
  
5.  Klicken Sie im Menü **Debuggen** auf **An den Prozess anhängen**, während das Fenster des Projekts für die Datenverarbeitungserweiterung noch aktiv ist.  
  
     Das Dialogfeld **An den Prozess anhängen** wird geöffnet.  
  
6.  Wählen Sie aus der Liste der Prozesse „devenv.exe“ aus (entspricht dem Berichtsprojekt), und klicken Sie auf **Anfügen**.  
  
7.  Definieren Sie mithilfe der Registerkarte **Berichtsdaten** des Berichtsprojekts die Berichtsdatenquelle. Sie verwenden wahrscheinlich den generischen Abfrage-Designer, um eine Abfrage für die benutzerdefinierte Datenquelle auszuführen. Dadurch sollte der Debugger aufgerufen und Code den Breakpoints gemäß ausgeführt werden.  
  
8.  Gehen Sie den Code schrittweise mit der F11-Taste durch. Weitere Informationen zum Debuggen mit [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] finden Sie in der Dokumentation zu [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Bereitstellen von Datenverarbeitungserweiterungen](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [Erweiterungen für Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementieren von Datenverarbeitungserweiterungen](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services Extension Library (Reporting Services-Erweiterungsbibliothek)](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
