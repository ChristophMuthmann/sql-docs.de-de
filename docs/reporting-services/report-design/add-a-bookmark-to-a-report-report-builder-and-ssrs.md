---
title: "Hinzuf&#252;gen eines Lesezeichens zu einem Bericht (Berichts-Generator und SSRS) | Microsoft Docs"
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
ms.assetid: f130562e-5673-40e3-8e01-de7227a21d41
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# Hinzuf&#252;gen eines Lesezeichens zu einem Bericht (Berichts-Generator und SSRS)
  Fügen Sie einem Bericht Lesezeichen und Lesezeichenlinks hinzu, wenn Sie ein benutzerdefiniertes Inhaltsverzeichnis oder benutzerdefinierte interne Navigationslinks bereitstellen möchten. In der Regel fügen Sie Lesezeichen an Positionen im Bericht hinzu, an die Benutzer verwiesen werden sollen, wie beispielsweise Tabellen, Diagramme oder eindeutige Gruppenwerte, die in einer Tabelle oder Matrix angezeigt werden. Sie können eigene Zeichenfolgen zur Verwendung als Lesezeichen erstellen. Bei Gruppen können Sie das Lesezeichen auf den Gruppierungsausdruck festlegen.  
  
 Nachdem Sie Lesezeichen erstellt haben, können Sie Berichtselemente hinzufügen, auf die der Benutzer klicken kann, um zu den einzelnen Lesezeichen zu wechseln. Bei diesen Elementen handelt es sich in der Regel um Textfelder oder Bilder.  
  
 Wenn der Bericht beispielsweise eine nach Farbe gruppierte Tabelle enthält, fügen Sie dem Gruppenkopf ein Lesezeichen hinzu, das auf dem Gruppierungsausdruck basiert. Anschließend fügen Sie am Anfang des Berichts eine Tabelle mit einem einzelnen Textfeld hinzu, das die Farbwerte anzeigt, und legen den Lesezeichenlink auf dieses Textfeld fest. Wenn der Benutzer auf eine Farbe klickt, wird er zu der Seite mit der Gruppenkopfzeile für diese Farbe geleitet.  
  
 Sie können jedem beliebigen Berichtselement Lesezeichen und jedem Element mit einer Eigenschaft **Aktion** Lesezeichenlinks hinzufügen (z. B. einem Textfeld, einem Bild oder einer berechneten Reihe in einem Diagramm). Weitere Informationen finden Sie unter [Aktionseigenschaften, Dialogfeld „Achsenoptionen“, &#40;Berichts-Generator und SSRS&#41;](../Topic/Action%20Properties%20Dialog%20Box%20\(Report%20Builder%20and%20SSRS\).md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### So fügen Sie ein Lesezeichen hinzu  
  
1.  Wählen Sie in der Berichtsentwurfssicht ein Textfeld, Bild, Diagramm oder ein anderes Berichtselement aus, dem Sie ein Lesezeichen hinzufügen möchten. Die Eigenschaften für das ausgewählte Element werden im Eigenschaftenbereich angezeigt.  
  
2.  Geben Sie im Textfeld neben **Lesezeichen**eine Zeichenfolge ein, die als Bezeichnung für dieses Lesezeichen dienen soll. Sie können z. B. für ein Bild im Bericht **BikePhoto** als Lesezeichen eingeben. Alternativ können Sie auf die Ausdrucksschaltfläche (**fx**) klicken, um das Dialogfeld **Ausdruck** zu öffnen, und einen Ausdruck angeben, der zu einer Bezeichnung ausgewertet wird. Für eine Gruppe muss der angegebene Ausdruck der Gruppierungsausdruck sein.  
  
    > [!NOTE]  
    >  Sie können für das Lesezeichen eine beliebige Zeichenfolge wählen, sie muss jedoch im Bericht eindeutig sein. Wenn das Lesezeichen nicht eindeutig ist, verweist der Lesezeichenlink auf das erste übereinstimmende Lesezeichen.  
  
### So fügen Sie einen Lesezeichenlink hinzu  
  
1.  Klicken Sie in der Entwurfssicht mit der rechten Maustaste auf das Textfeld, das Bild oder das Diagramm, dem Sie einen Link hinzufügen möchten, und klicken Sie dann auf **Eigenschaften**.  
  
2.  Klicken Sie im Dialogfeld **Eigenschaften** für dieses Berichtselement auf **Aktion**.  
  
3.  Wählen Sie **Gehe zu Lesezeichen**. Im Dialogfeld für diese Option wird ein zusätzlicher Abschnitt angezeigt.  
  
4.  Geben Sie im Feld **Lesezeichen auswählen** ein Lesezeichen oder einen zu einem Lesezeichen ausgewerteten Ausdruck ein, oder wählen Sie ein Lesezeichen bzw. einen Ausdruck aus. Im vorhergehenden Beispiel geben Sie z. B. **BikePhoto** ein, um im Bericht einen Link zum Bild zu erstellen.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  (Optional) Der Text wird nicht automatisch als Link formatiert. Es empfiehlt sich, die Farbe und den Effekt des Texts zu ändern, um zu verdeutlichen, dass es sich um einen Link handelt. Ändern Sie im Abschnitt **Schriftart** auf der Registerkarte "Home" des Menübands z. B. die Farbe in Blau und den Effekt in "Unterstrichen".  
  
7.  Klicken Sie zum Testen des Links auf **Ausführen** , um eine Vorschau des Berichts anzuzeigen, und klicken Sie dann auf das Berichtselement, für das Sie den Link festgelegt haben.  
  
## Siehe auch  
 [Interaktive Sortierung, Dokumentstrukturen und Links &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Filtern, Gruppieren und Sortieren von Daten &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  