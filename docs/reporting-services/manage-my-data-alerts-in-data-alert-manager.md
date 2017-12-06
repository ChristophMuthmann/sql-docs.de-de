---
title: Verwalten meiner Datenwarnungen im Datenwarnungs-Manager | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- managing, alerts
- managing, data alerts
ms.assetid: e0e4ffdf-bd4c-4ebd-872b-07486cbb47c2
caps.latest.revision: "13"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 367f5055576045c3b2fb6a7c3a774540ad919361
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="manage-my-data-alerts-in-data-alert-manager"></a>Verwalten meiner Datenwarnungen im Datenwarnungs-Manager

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

SharePoint-Benutzer können eine Liste der Datenwarnungen, die sie erstellt haben, und Informationen zu den Warnungen anzeigen. Zudem haben Benutzer die Möglichkeit, ihre Warnungen zu löschen, Warnungsdefinitionen zur Bearbeitung im Datenwarnungs-Designer zu öffnen und ihre Warnungen auszuführen. Das folgende Bild zeigt die für Benutzer verfügbaren Funktionen in Datenwarnungs-Manager.

 ![Warnungs-Manager-Funktionen für SharePoint-Benutzer](../reporting-services/media/rs-alertmanageriw.gif "Alert Manager features for SharePoint users")

> [!NOTE]
> Die Integration von Reporting Services in SharePoint ist nach SQL Server 2016 nicht mehr möglich.

### <a name="to-view-a-list-of-your-alerts"></a>So zeigen Sie eine Liste Ihrer Warnungen an  
  
1.  Wechseln Sie zur SharePoint-Bibliothek. Hier haben Sie die Berichte gespeichert, für die Sie Datenwarnungen erstellt haben.  
  
2.  Klicken Sie auf das Symbol für das Dropdownmenü zum Erweitern in einem Bericht, und klicken Sie auf **Datenwarnungen verwalten**. Das folgende Bild zeigt das Dropdownmenü.  
  
     ![Öffnen von Warnungs-Manager im Kontextmenü „Bericht“](../reporting-services/media/rs-openalertmanager.gif "Open Alert Manager from report context menu")  
  
     Der Datenwarnungs-Manager wird geöffnet. Standardmäßig listet er die Warnungen für den in der Bibliothek ausgewählten Bericht auf.  
  
3.  Klicken Sie neben der Liste **Warnungen anzeigen für folgenden Bericht** auf den Pfeil nach unten, und wählen Sie einen Bericht aus, um die zugehörigen Warnungen anzuzeigen. Klicken Sie alternativ auf **Alle anzeigen** , um alle Warnungen aufzuführen.  
  
    > [!NOTE]  
    >  Verfügt der ausgewählte Bericht über keine Warnungen, müssen Sie nicht zur SharePoint-Bibliothek zurückkehren, um einen Bericht mit Warnungen auszuwählen. Klicken Sie stattdessen auf **Alle anzeigen** , um eine Liste mit allen Warnungen aufzurufen.  
  
     In einer Tabelle werden der Warnungsname, Berichtsname, Ihr Name als Ersteller der Warnung, die Nummer, mit der die Warnung gesendet wurde, die letzte Änderung der Warnungsdefinition und der Status der Warnung aufgeführt. Wenn die Warnung nicht generiert oder gesendet werden kann, enthält die Statusspalte Informationen zum Fehler und hilft Ihnen bei der Behebung des Problems.  
  
### <a name="to-edit-an-alert-definition"></a>So bearbeiten Sie eine Warnungsdefinition  
  
-   Klicken Sie mit der rechten Maustaste auf die Datenwarnung, deren Warnungsdefinition Sie bearbeiten möchten, und klicken Sie dann auf **Bearbeiten**.  
  
     Die Warnungsdefinition wird im Datenwarnungs-Designer geöffnet. Weitere Informationen finden Sie unter [Bearbeiten einer Datenwarnung im Warnungs-Designer](../reporting-services/edit-a-data-alert-in-alert-designer.md) und [Datenwarnungs-Designer](../reporting-services/data-alert-designer.md).  
  
    > [!NOTE]  
    >  Nur der Benutzer, der die Datenwarnungsdefinition erstellt hat, kann sie bearbeiten.  
  
    > [!NOTE]  
    >  Wenn der Bericht und die aus dem Bericht generierten Datenfeeds geändert wurden, ist die Warnungsdefinition möglicherweise nicht mehr gültig. Dies ist der Fall, wenn eine Spalte, auf die die Warnung in ihren Regeln verweist, aus dem Bericht gelöscht wird, der Datentyp geändert wird, die Spalte in einem anderen Datenfeed enthalten ist, oder wenn der Bericht gelöscht oder verschoben wurde. Sie können eine ungültige Warnungsdefinition öffnen. Sie können sie jedoch nicht erneut speichern, sofern sie nicht gemäß der aktuellen Version des Berichtsdatenfeeds gültig ist, auf dem sie basiert. Weitere Informationen dazu, wie Datenfeeds aus Berichten generiert werden, finden Sie unter [Generieren von Datenfeeds aus Berichten (Berichts-Generator und SSRS)](../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md).  
  
### <a name="to-delete-an-alert-definition"></a>So löschen Sie eine Warnungsdefinition  
  
-   Klicken Sie mit der rechten Maustaste auf die zu löschende Datenwarnung, und klicken Sie auf **Löschen**.  
  
     Wenn Sie die Warnung löschen, werden keine weiteren Warnmeldungen gesendet.  
  
### <a name="to-run-an-alert"></a>So führen Sie eine Warnung aus  
  
-   Klicken Sie mit der rechten Maustaste auf die auszuführende Datenwarnung, und klicken Sie auf **Ausführen**.  
  
     Die Warnungsinstanz wird erstellt, und die Datenwarnmeldung wird sofort gesendet – unabhängig von den Zeitplanoptionen, die Sie im Datenwarnungs-Designer angegeben haben. Beispielsweise wird eine Warnung gesendet, die so konfiguriert ist, dass sie wöchentlich und nur im Fall von Ergebnisänderungen zu senden ist.  

## <a name="see-also"></a>Siehe auch

[Datenwarnungs-Manager für Warnungsadministratoren](../reporting-services/data-alert-manager-for-alerting-administrators.md)   
[Reporting Services-Datenwarnungen](../reporting-services/reporting-services-data-alerts.md)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
