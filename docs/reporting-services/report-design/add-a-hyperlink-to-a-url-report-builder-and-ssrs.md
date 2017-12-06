---
title: "Hinzufügen eines Links zu einer URL (Berichts-Generator und SSRS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 09/07/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d3392c0b-7b62-4d27-bc04-2bd0c5487d08
caps.latest.revision: "11"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 1f147d97fdd5f5a237bcc9fff20642ec60ee2151
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="add-a-hyperlink-to-a-url-report-builder-and-ssrs"></a>Hinzufügen eines Links zu einer URL (Berichts-Generator und SSRS)
Erfahren Sie, wie Sie Linkaktionen in paginierten [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]  -Berichten zu Textfeldern, Bildern, Diagrammen und Messgeräten hinzufügen. Links können zu anderen Berichten, zu Lesezeichen in einem Bericht oder zu statischen oder dynamischen URLs führen. 

 Eine Linkaktion kann jedem Element hinzugefügt werden, das über eine **Action** -Eigenschaft verfügt, z. B. ein Textfeld, ein Bild oder eine berechnete Reihe in einem Diagramm. Wenn der Benutzer auf das Berichtselement klickt, wird die von Ihnen definierte Aktion ausgeführt.  
  
*   Sie können **einen Link hinzufügen, der einen Browser mit einer URL öffnet** , die Sie angeben. Der Link kann eine statische URL oder ein Ausdruck sein, der zu einer URL ausgewertet wird. Wenn ein Feld in einer Datenbank URLs enthält, kann der Ausdruck dieses Feld enthalten, wodurch eine dynamische Liste von Links in dem Bericht entsteht. Stellen Sie sicher, dass die Leser Ihrer Berichte Zugriff auf die URL haben, die Sie bereitstellen.  
   
*  Sie können auch **URLs angeben, um Drillthroughs zu erstellen** Berichten auf beliebigen Berichtsservern führen, für die Sie und Ihre Benutzer über eine Leseberechtigung verfügen, indem Sie URL-Anforderungen an den Berichtsserver verwenden. Sie können z. B. einen Bericht angeben und die Dokumentstruktur für Benutzer ausblenden, wenn diese den Bericht zum ersten Mal anzeigen. Weitere Informationen finden Sie unter [URL-Zugriff (SSRS)](../../reporting-services/url-access-ssrs.md) und [Angeben von Pfaden zu externen Elementen (Berichts-Generator und SSRS)](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md).
 
 *  Außerdem können Sie **ein Lesezeichen an einem bestimmten Ort** im selben Bericht hinzufügen. 
  
Probieren Sie das Hinzufügen von Links mit Beispieldaten im [Tutorial: Format Text (Report VBuilder) (Tutorial: Formatieren von Text (Berichts-Generator))](../../reporting-services/tutorial-format-text-report-builder.md) aus.  
  
> [!NOTE]  
>  Links, die an Datasetfelder gebunden sind, sind unter Umständen anfällig für böswillige Manipulationen. Weitere Informationen finden Sie unter [Sichere Berichte und Ressourcen](../../reporting-services/security/secure-reports-and-resources.md).  
  
## <a name="to-add-a-hyperlink-and"></a>Vorgehensweise zum Hinzufügen eines Links und...   
  
1.  Klicken Sie in der Berichtsentwurfsansicht mit der rechten Maustaste auf das Textfeld, Bild oder Diagramm, dem Sie einen Link hinzufügen möchten, und klicken Sie dann auf **Eigenschaften**.  
  
2.  Klicken Sie im Dialogfeld „Eigenschaften“ auf die Registerkarte **Aktion** . Lesen Sie Informationen zu den Optionen.  

## <a name="-add-drillthrough-to-another-report"></a>... und Hinzufügen eines Drillthroughs zu einem anderen Bericht

1. Aktivieren Sie auf der Registerkarte **Aktion** die Option **Gehe zu Bericht**. 

2. Geben Sie den Zielbericht und die Parameter an, die Sie verwenden möchten. Die Parameternamen müssen mit den für den Zielbericht definierten Parametern übereinstimmen. 

3. Verwenden Sie die Schaltflächen **Hinzufügen** und **Löschen** , um Parameter hinzuzufügen oder zu löschen, und sortieren Sie die Liste der Parameter mithilfe der NACH-UNTEN- und der NACH-OBEN-TASTE.

4.  Sie können einen **Wert** zur Übergabe für den benannten Parameter im Drillthroughbericht eingeben oder auswählen. Klicken Sie auf die Schaltfläche „Ausdruck“ (fx), um den Ausdruck zu bearbeiten.

5. Wählen Sie **Auslassen** aus, um zu verhindern, dass der Parameter ausgeführt wird. Standardmäßig ist dieses Kontrollkästchen deaktiviert. Um das Kontrollkästchen zu aktivieren, klicken Sie auf die Schaltfläche „Ausdruck“ (fx), und geben Sie entweder „True“ ein, oder erstellen Sie einen Ausdruck. Das Kontrollkästchen wird aktiviert, wenn Sie im Dialogfeld „Ausdruck“ auf **OK** klicken.
  
   Weitere Informationen finden Sie unter [Hinzufügen einer Drillthroughaktion für einen Bericht](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md) . 
   
6. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
   
## <a name="-add-a-bookmark"></a>... Hinzufügen eines Lesezeichens

Sie können Links zu Lesezeichen für Positionen im aktuellen Bericht erstellen. Sie müssen zuerst die **Bookmark** -Eigenschaft eines Berichtselements festlegen, um einen Link zu einem Lesezeichen zu erstellen. Wählen Sie ein Berichtselement aus, und geben Sie im Bereich „Eigenschaften“ einen Wert oder einen Ausdruck für die Lesezeichen-ID ein, um die **Bookmark** -Eigenschaft festzulegen. Beispiel: „Umsatzdiagramm“ oder „5TopUmsätze“.

1. Aktivieren Sie auf der Registerkarte **Aktion** die Option **Gehe zu Lesezeichen**. 

2. Geben Sie direkt oder durch Auswählen die Lesezeichen-ID ein, zu der im Bericht gesprungen werden soll. Klicken Sie auf die Schaltfläche Ausdruck (fx), um den Ausdruck zu ändern. 

   Bei der Lesezeichen-ID kann es sich entweder um eine statische ID oder einen Ausdruck handeln, der zu einer Lesezeichen-ID ausgewertet wird. Der Ausdruck kann ein Feld mit einer Lesezeichen-ID enthalten.
   
   Weitere Informationen finden Sie unter [Hinzufügen eines Lesezeichens zu einem Bericht](../../reporting-services/report-design/add-a-bookmark-to-a-report-report-builder-and-ssrs.md) .
   
3. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="-add-a-hyperlink"></a>... Hinzufügen eines Links 
  
1. Aktivieren Sie auf der Registerkarte **Aktion** die Option **Gehe zu URL**. Im Dialogfeld für diese Option wird ein zusätzlicher Abschnitt angezeigt.  
  
4.  Geben Sie in **URL auswählen**eine URL oder einen Ausdruck, der eine URL ergibt, ein (bzw. wählen Sie diese aus), oder klicken Sie auf den Dropdownpfeil, und klicken Sie auf den Namen eines Felds, das eine URL enthält. 

    Verwenden Sie für ein Element, das auf einem für den einheitlichen Modus konfigurierten Berichtsserver veröffentlicht wurde, einen vollständigen oder relativen Pfad. Beispiel: `http://<servername>/images/image1.jpg`. 
    
    Verwenden Sie für ein Element, das auf einem im integrierten SharePoint-Modus konfigurierten Berichtsserver veröffentlicht wird, eine vollqualifizierte URL. Beispiel: `http://<SharePointservername>/<site>/Documents/images/image1.jpg`.
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="after-you-add-a-hyperlink"></a>Nach dem Hinzufügen eines Links
  
1.  (Optional) Der Text wird nicht automatisch als Link formatiert. Es empfiehlt sich, die Farbe und den Effekt des Texts zu ändern, um zu verdeutlichen, dass es sich um einen Link handelt. Ändern Sie im Abschnitt **Schriftart** auf der Registerkarte "Home" des Menübands z. B. die Farbe in Blau und den Effekt in "Unterstrichen".  
  
7.  Klicken Sie zum Testen des Links auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen, und klicken Sie dann auf das Berichtselement, für das Sie den Link festgelegt haben.  
  
## <a name="see-also"></a>Siehe auch  
 [Interaktive Sortierung, Dokumentstrukturen und Links &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [Erstellen einer Dokumentstruktur &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/create-a-document-map-report-builder-and-ssrs.md)  
  
  
