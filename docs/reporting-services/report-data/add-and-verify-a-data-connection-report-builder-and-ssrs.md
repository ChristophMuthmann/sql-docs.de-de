---
title: "Hinzuf&#252;gen und Pr&#252;fen einer Datenverbindung (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1d3b2573-e29d-480d-9dde-d26379c86618
caps.latest.revision: 11
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 11
---
# Hinzuf&#252;gen und Pr&#252;fen einer Datenverbindung (Berichts-Generator und SSRS)
  Im Berichts-Generator können Sie eine freigegebene Datenquelle des Berichtsservers hinzufügen oder eine eingebettete Datenquelle für Ihren Bericht erstellen. Im Berichts-Designer können Sie eine freigegebene Datenquelle oder eine eingebettete Datenquelle erstellen und sie auf einem Berichtsserver bereitstellen.  
  
 Navigieren Sie zu einem Berichtsserver, und wählen Sie eine freigegebene Datenquelle aus, um diese in den Bericht aufzunehmen. Die freigegebene Datenquelle im Bericht verweist auf die freigegebene Datenquellendefinition auf dem Berichtsserver.  
  
 Zum Erstellen einer eingebetteten Datenquelle benötigen Sie Informationen über die Verbindung mit der externen Datenquelle, und Sie müssen wissen, welche Berechtigungen für den Zugriff auf die Daten erforderlich sind. Diese Informationen erhalten Sie normalerweise vom Besitzer der Datenquelle. Sie können die Verbindung testen, um zu überprüfen, ob die angegebenen Anmeldeinformationen ausreichend sind.  
  
 Weitere Informationen finden Sie unter [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen im Berichts-Generator](../Topic/Data%20Connections,%20Data%20Sources,%20and%20Connection%20Strings%20in%20Report%20Builder.md) und [Angeben von Anmeldeinformationen im Berichts-Generator](../Topic/Specify%20Credentials%20in%20Report%20Builder.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### So erstellen Sie eine Verbindung zu einer freigegebenen Datenquellen im Berichts-Generator  
  
1.  Klicken Sie im Berichtsdatenbereich auf der Symbolleiste auf **Neu** und anschließend auf **Datenquelle**. Das Dialogfeld **Datenquelleneigenschaften** wird angezeigt.  
  
2.  Geben Sie in das Textfeld **Name** einen Namen für die Datenquelle ein.  
  
    > [!NOTE]  
    >  Dieser Name wird in der lokalen Berichtsdefinition gespeichert. Der Name entspricht nicht dem Namen der freigegebenen Datenquelle auf dem Berichtsserver.  
  
3.  Wählen Sie **Freigegebene Verbindung oder Berichtsmodell verwenden**aus. Die Liste der zuletzt verwendeten freigegebenen Datenquellen und Berichtsmodelle wird angezeigt. Klicken Sie zum Auswählen einer Datenquelle auf **Durchsuchen** , und suchen Sie den Ordner auf dem Berichtsserver mit den freigegebenen Datenquellen.  
  
4.  Wählen Sie die freigegebene Datenquelle aus, und klicken Sie dann auf **Öffnen**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Die Datenquelle wird im Berichtsdatenbereich angezeigt.  
  
### So überprüfen Sie eine Datenverbindung  
  
1.  Doppelklicken Sie auf der Symbolleiste im Berichtsdatenbereich auf die Datenquelle. Das Dialogfeld **Datenquelleneigenschaften** wird angezeigt.  
  
2.  Klicken Sie auf **Verbindung testen**.  
  
3.  Bei einer erfolgreichen Verbindung wird die folgende Meldung angezeigt: "Die Verbindung wurde erfolgreich erstellt". [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  Wenn die Verbindung nicht erfolgreich hergestellt werden kann, wird die folgende Meldung angezeigt: "Es konnte keine Verbindung mit der Datenquelle hergestellt werden".  
  
5.  Klicken Sie auf **Details**, und beheben Sie das Problem mithilfe der angezeigten Informationen.  
  
     Weitere Informationen finden Sie unter [Angeben von Anmeldeinformationen im Berichts-Generator](../Topic/Specify%20Credentials%20in%20Report%20Builder.md).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Siehe auch  
 [Berichtsdatasets &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Suchen, Anzeigen und Verwalten von Berichten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen in Berichts-Generator](../Topic/Data%20Connections,%20Data%20Sources,%20and%20Connection%20Strings%20in%20Report%20Builder.md)  
  
  