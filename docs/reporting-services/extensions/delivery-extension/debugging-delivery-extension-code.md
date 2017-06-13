---
title: "Debuggen von Übermittlungserweiterungscode | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
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
- delivery extensions [Reporting Services], debugging
- debugging delivery extensions [Reporting Services]
- troubleshooting [Reporting Services], delivery extensions
ms.assetid: a7d959da-5005-4a50-aca7-2cef36aa9947
caps.latest.revision: 35
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: d3e683887f02436ad948b6a6aedb64ef749a7547
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="debugging-delivery-extension-code"></a>Debuggen von Übermittlungserweiterungscode
  Die [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] stellt mehrere Tools zum Debuggen, die Sie unterstützen der Analyse von Code der übermittlungserweiterung und Fehlersuche im. Welches Tool dafür am besten geeignet ist, hängt von Ihrer Zielsetzung ab. In diesem Beispiel wird [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)]verwendet.  
  
#### <a name="to-debug-your-delivery-extension-code"></a>So debuggen Sie Code für Übermittlungserweiterungen  
  
1.  Starten Sie [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)] , und öffnen Sie das Projekt der übermittlungserweiterung.  
  
2.  Erstellen Sie das Projekt, und stellen Sie die Assembly der Übermittlungserweiterung und die dazugehörige PDB-Datei im Berichtsserver und im Berichts-Manager bereit. Weitere Informationen zur Bereitstellung finden Sie unter [Deploying a Delivery Extension](../../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md).  
  
3.  Wenn Sie eine Abonnementbenutzeroberfläche zur Erweiterung des Berichts-Managers geschrieben haben, öffnen Sie den Internet Explorer, und navigieren Sie zum Berichts-Manager, während Sie den Code der Übermittlungserweiterung in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] geöffnet lassen. Wenn Sie keine Abonnementbenutzeroberfläche auf dem Berichts-Manager eingesetzt haben, öffnen Sie einfach mithilfe der SOAP-API die Clientanwendung, von der Sie die Übermittlungserweiterung aufrufen.  
  
4.  Wechseln Sie zu [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] und zum Projekt der Übermittlungserweiterung, und legen Sie einige Breakpoints im Code fest.  
  
5.  Das Projekt der übermittlungserweiterung noch immer das aktive Fenster, und klicken Sie auf **an den Prozess anhängen** auf die **Debuggen** Menü.  
  
     Die **an den Prozess anhängen** Dialogfeld wird geöffnet.  
  
6.  Die Liste der Prozesse, wählen Sie den Prozess aspnet_wp.exe (oder w3wp.exe, wenn Ihre Anwendung auf IIS 6.0 bereitgestellt wird), und klicken Sie auf **Anfügen**.  
  
7.  Definieren Sie mithilfe der Übermittlungserweiterung ein neues Abonnement. Höchstwahrscheinlich verwenden Sie den Berichts-Manager oder die SOAP-API. Dadurch sollte der Debugger aufgerufen und Code den Breakpoints gemäß ausgeführt werden.  
  
8.  Schrittweises Durchlaufen von dem Code mit der **F11** Schlüssel. Weitere Informationen zum Debuggen mit [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] finden Sie in der Dokumentation zu [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Siehe auch  
 [Implementing a Delivery Extension](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
