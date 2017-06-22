---
title: "Debuggen von Code für Datenverarbeitungserweiterungen | Microsoft Docs"
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
- debugging data processing extensions [Reporting Services]
- troubleshooting [Reporting Services], data processing extensions
- data processing extensions [Reporting Services], debugging
ms.assetid: e963e205-9ae0-446d-97df-028a1d2727d9
caps.latest.revision: 40
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 7af6b33039d19029d1595ac08f5d5345cdaa1c58
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="debugging-data-processing-extension-code"></a>Debuggen von Code für Datenverarbeitungserweiterungen
  Die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] bietet mehrere Tools zum Debuggen, die Ihnen helfen, Analysieren von Code für die Datenverarbeitung und Fehlersuche im. Welches Tool dafür am besten geeignet ist, hängt von Ihrer Zielsetzung ab. In diesem Beispiel wird [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)]verwendet.  
  
#### <a name="to-debug-your-data-processing-extension-code"></a>So debuggen Sie Code für Datenverarbeitungserweiterungen  
  
1.  Starten Sie [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)], und öffnen Sie das Projekt für die Datenverarbeitungserweiterung.  
  
2.  Erstellen Sie das Projekt, und stellen Sie die Assembly der Datenverarbeitungserweiterung und die dazugehörige PDB-Datei im Berichts-Designer bereit. Weitere Informationen zur Bereitstellung finden Sie unter [Vorgehensweise: Bereitstellen einer Datenverarbeitungserweiterung für Berichts-Designer](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-report-designer.md).  
  
3.  Öffnen Sie ein neues Berichtsprojekt in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], ohne vorher den Code für die Datenverarbeitungserweiterungen in einem anderen Fenster von [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] zu schließen.  
  
4.  Wechseln Sie zu dem [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]-Fenster, das das Projekt für die Datenverarbeitungserweiterung enthält, und legen Sie einige Breakpoints im Code fest.  
  
5.  Die Datenverarbeitung Erweiterung Projektfenster noch aktiv, und klicken Sie auf **an den Prozess anhängen** auf die **Debuggen** Menü.  
  
     Die **an den Prozess anhängen** Dialogfeld wird geöffnet.  
  
6.  Aus der Liste der Prozesse, wählen Sie den Prozess devenv.exe, der dem Berichtsprojekt entspricht, und klicken Sie auf **Anfügen**.  
  
7.  Definieren Sie Data Source mithilfe der **Berichtsdaten** Registerkarte des Berichtsprojekts. Sie verwenden wahrscheinlich den generischen Abfrage-Designer, um eine Abfrage für die benutzerdefinierte Datenquelle auszuführen. Dadurch sollte der Debugger aufgerufen und Code den Breakpoints gemäß ausgeführt werden.  
  
8.  Gehen Sie den Code schrittweise mit der F11-Taste durch. Weitere Informationen zum Debuggen mit [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] finden Sie in der Dokumentation zu [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Siehe auch  
 [Deploying a Data Processing Extension](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [Reporting Services-Erweiterungen](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementing a Data Processing Extension](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
