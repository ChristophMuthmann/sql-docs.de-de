---
title: Binden eines Berichts oder Modells an eine freigegebene Datenquelle (SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shared data sources [Reporting Services]
- data sources [Reporting Services], shared
ms.assetid: 23cc15f2-2883-48e2-bc6c-fa0ab61a2e21
caps.latest.revision: 11
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 50893ee7140f33086d432fdc00f660f6371fe282
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="bind-a-report-or-model-to-a-shared-data-source-ssrs"></a>Binden eines Berichts oder Modells an eine freigegebene Datenquelle (SSRS)
  In einigen Situationen, z. B., wenn Sie einen Bericht oder ein Modell von einem Testserver auf einen Produktionsserver verschieben, möchten Sie die Datei vielleicht auf dem lokalen Computer speichern und anschließend auf einen anderen Berichtsserver hochladen. Wenn Sie den Bericht oder das Modell auf den neuen Server hochladen, müssen Sie ihn oder es erneut an eine freigegebene, auf dem neuen Berichtsserver gespeicherte Datenquelle binden. Wenn Sie den Bericht oder das Modell nicht erneut binden, können sie bei einem Zugriff vom neuen Berichtsserver nicht ordnungsgemäß verwendet werden.  
  
> [!IMPORTANT]  
>  Vor dem erneuten Binden eines Berichts oder Modells an eine freigegebene Datenquelle müssen die Daten bereits auf dem Berichtsserver oder in der SharePoint-Bibliothek vorhanden sein. Weitere Informationen zu Datenquellen finden Sie unter [Erstellen, Ändern und Löschen von freigegebenen Datenquellen &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md).  
  
### <a name="to-bind-a-report-or-model-to-a-shared-data-source-on-a-report-server-running-in-native-mode"></a>So binden Sie einen Bericht oder ein Modell an eine freigegebene Datenquelle auf einem Berichtsserver im einheitlichen Modus  
  
1.  Klicken Sie in **Berichts-Manager**auf den Namen des Berichts oder Modells, den oder das Sie auf den Server hochladen möchten.  
  
     Die Registerkarte Eigenschaften wird geöffnet.  
  
2.  Klicken Sie auf **Datenquellen**.  
  
3.  Klicken Sie auf **Durchsuchen**, und navigieren Sie dann zu der Datenquelle, an die Sie den Bericht oder das Modell binden möchten.  
  
4.  Wählen Sie die Datenquelle aus, und klicken Sie dann auf **OK**.  
  
5.  Klicken Sie auf **Anwenden**.  
  
     Der Bericht oder das Modell ist nun an die ausgewählte Datenquelle gebunden.  
  
### <a name="to-bind-a-report-or-model-to-a-shared-data-source-on-a-report-server-running-in-sharepoint-integrated-mode"></a>So binden Sie einen Bericht oder ein Modell an eine freigegebene Datenquelle auf einem Berichtsserver im integrierten SharePoint-Modus  
  
1.  Klicken Sie auf der Schnellstartleiste auf den Namen der Bibliothek, wenn sie nicht bereits geöffnet ist. Wenn der Name der Bibliothek nicht angezeigt wird, klicken Sie auf **Alle Websiteinhalte einblenden**und anschließend auf den Namen der Bibliothek.  
  
2.  Zeigen Sie auf den Bericht oder das Modell, und klicken Sie auf den Pfeil nach unten.  
  
3.  Klicken Sie auf **Datenquellen verwalten**.  
  
4.  Klicken Sie auf **dataSource1**.  
  
5.  Überprüfen Sie im Bereich **Verbindungstyp** , ob **Freigegebene Datenquelle** ausgewählt ist.  
  
6.  Klicken Sie im Bereich **Datenquellenlink** auf die Schaltfläche mit den Auslassungspunkten (...).  
  
7.  Suchen Sie die Datenquelle, die Sie verwenden möchten.  
  
8.  Wählen Sie die Datenquelle aus, und klicken Sie auf **OK**.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. Klicken Sie auf **Schließen**.  
  
## <a name="see-also"></a>Siehe auch  
 [Hochladen einer Datei oder eines Berichts &#40; Berichts-Manager &#41;](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)   
 [Hochladen von Dokumenten in einer SharePoint-Bibliothek &#40; Reporting Services im SharePoint-Modus &#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)   
 [Erstellen Sie und verwalten Sie freigegebene Datenquellen &#40; Reporting Services in SharePoint integrierten Modus &#41;](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76)   
 [Erstellen Sie, löschen Sie oder ändern Sie einer freigegebenen Datenquelle &#40; Berichts-Manager &#41;](http://msdn.microsoft.com/library/cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2)   
 [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen (Berichts-Generator und SSRS)](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Datenquellen unterstützt, die von Reporting Services &#40; SSRS &#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  
  
  
