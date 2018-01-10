---
title: "Hinzufügen, Ändern oder Löschen von verfügbaren Werten für einen Berichtsparameter | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rtp.rptdesigner.reportparameters.availablevalues.f1
- "10455"
- "10071"
ms.assetid: 0e03264c-523f-4c59-b71b-ceef600f75f6
caps.latest.revision: "11"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ff3ae7e2e01eab4629fa30f4ab188ac714d4fd2e
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="add-change-or-delete-available-values-for-a-report-parameter"></a>Hinzufügen, Ändern oder Löschen von verfügbaren Werten für einen Berichtsparameter
  Nachdem Sie einen Berichtsparameter erstellt haben, können Sie eine Liste mit verfügbaren Werten angeben, die dem Benutzer angezeigt werden soll. Eine Liste verfügbarer Werte schränkt die Auswahl, die ein Benutzer treffen kann, auf die gültigen Werte für den Parameter ein.  
  
 Verfügbare Werte werden bei Ausführung des Berichts neben dem Berichtsparameter auf der Symbolleiste in einer Dropdownliste angezeigt. Berichtsparameter können einen Wert oder mehrere Werte darstellen. Bei mehreren Werten beginnt die Liste mit der Funktion **Alles auswählen** , sodass der Benutzer alle Werte mit einem einzigen Mausklick auswählen oder löschen kann.  
  
 Sie können eine statische Liste mit Werten oder eine Liste anhand eines Berichtsdatasets bereitstellen. Sie können optional einen Anzeigenamen für Werte bereitstellen, indem Sie ein Bezeichnungsfeld angeben. Zum Beispiel können Sie für einen Parameter auf Grundlage eines `ProductID` -Felds das `ProductName` -Feld in der Parameterbezeichnung anzeigen. Wenn der Bericht ausgeführt wird, kann der Benutzer eine Auswahl aus den Produktnamen treffen. Der tatsächlich ausgewählte Wert ist jedoch die entsprechende `ProductID`.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Nachdem ein Bericht veröffentlicht wurde, können Sie die verfügbaren Standardwerte, die Sie im Bericht im Berichterstellungstool definieren, durch Festlegen von Parametereigenschaftswerten auf dem Berichtsserver überschreiben. Weitere Informationen finden Sie unter [Berichtsparameter &#40;Berichts-Generator und Berichts-Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)" basiert.  
  
### <a name="to-add-or-change-the-available-values-for-a-report-parameter"></a>So ändern Sie die verfügbaren Werte für einen Berichtsparameter  
  
1.  Erweitern Sie im Berichtsdatenbereich den Knoten Parameter. Klicken Sie mit der rechten Maustaste auf den Parameter, und klicken Sie auf **Parametereigenschaften**. Das Dialogfeld **Berichtsparametereigenschaften** wird geöffnet.  
  
    > [!NOTE]  
    >  Zum Anzeigen des Berichtsdatenbereichs klicken Sie im Menü **Ansicht** auf **Berichtsdaten**.  
  
2.  Klicken Sie auf **Verfügbare Werte**. Wählen Sie eine Option für die verfügbaren Werte aus:  
  
    -   Klicken Sie auf **Werte angeben** , um manuell eine Liste von Werten und optional Anzeigenamen (die Bezeichnungen) für die Werte bereitzustellen.  
  
         Klicken Sie auf **Hinzufügen** , und geben Sie dann den Wert im Textfeld **Wert** und optional die Bezeichnung im Textfeld **Bezeichnung** ein. Wenn Sie keine Bezeichnung angeben, wird der Wert verwendet. Sie können einen Ausdruck für einen Wert schreiben. Der Datentyp muss mit dem Datentyp des Parameters übereinstimmen. In einem Ausdruck für einen Parameter können keine Feldnamen verwendet werden. Beispiele finden Sie unter [Häufig verwendete Filter (Berichts-Generator und SSRS)](../../reporting-services/report-design/commonly-used-filters-report-builder-and-ssrs.md).  
  
         Wiederholen Sie diesen Schritt für so viele Werte, wie Sie bereitstellen möchten. Die Reihenfolge der in dieser Liste angezeigten Elemente bestimmt die Reihenfolge, die Benutzer in der Dropdownliste sehen. Um die Position eines Elements in der Liste zu ändern, klicken Sie zur Auswahl des Elements auf das Textfeld **Wert** oder **Bezeichnung** . Bewegen Sie das Element dann mit den Nach-oben- und Nach-unten-Pfeilen in der Liste nach oben oder nach unten.  
  
    -   Klicken Sie auf **Werte aus Abfrage abrufen** , um den Namen eines vorhandenen Datasets bereitzustellen, mit dem die Werte und optional die Anzeigenamen für diesen Parameter abgerufen werden.  
  
        > [!IMPORTANT]  
        >  Wenn das gleiche Dataset den entsprechenden Abfrageparameter für den Berichtsparameter enthält, wird bei dem Versuch, den Bericht auszuführen, eine Fehlermeldung angezeigt. Um diesen Fehler zu beheben, verwenden Sie ein anderes Dataset zum Abrufen der Werte.  
  
         Wählen Sie unter **Dataset**den Namen des Datasets aus.  
  
         Wählen Sie unter **Wertfeld**den Namen des Felds aus, das Parameterwerte bereitstellt.  
  
         Wählen Sie in **Bezeichnungsfeld**den Namen des Felds aus, das Anzeigenamen für den Parameter bereitstellt. Wenn es kein separates Feld für Anzeigenamen gibt, wählen Sie das gleiche Feld aus, das Sie für das Feld **Wert** ausgewählt haben.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Wenn Sie den Bericht in der Vorschau anzeigen, sehen Sie eine Dropdownliste mit verfügbaren Werten für den Parameter.  
  
### <a name="to-remove-the-available-values-for-a-report-parameter"></a>So entfernen Sie die verfügbaren Werte für einen Berichtsparameter  
  
1.  Erweitern Sie im Berichtsdatenbereich den Knoten Parameter. Klicken Sie mit der rechten Maustaste auf den Parameter, und klicken Sie auf **Parametereigenschaften**. Das Dialogfeld **Berichtsparameter** wird geöffnet.  
  
2.  Klicken Sie auf **Verfügbare Werte**.  
  
3.  Klicken Sie in **Wählen Sie eine der folgenden Optionen aus**auf **Keine**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Wenn Sie den Bericht in der Vorschau anzeigen, wird die Dropdownliste mit verfügbaren Werten für den Parameter nicht mehr angezeigt.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Ändern der Reihenfolge von Berichtsparametern &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [Hinzufügen, Ändern oder Löschen von Berichtsparametern &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [Hinzufügen von kaskadierenden Parametern zu einem Bericht &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Hinzufügen, Ändern oder Löschen von Standardwerten für einen Berichtsparameter (Berichts-Generator und SSRS)](../../reporting-services/report-design/add-change-or-delete-default-values-for-a-report-parameter.md)   
 [Parameters Collection References (Report Builder and SSRS) (Verweise auf Parameterauflistungen (Berichts-Generator und SSRS))](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [Tutorial: Add a Parameter to Your Report (Report Builder) (Tutorial: Hinzufügen eines Parameters zu einem Bericht (Berichts-Generator))](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
