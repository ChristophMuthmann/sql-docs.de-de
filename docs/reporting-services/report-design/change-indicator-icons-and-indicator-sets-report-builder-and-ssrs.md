---
title: "&#196;ndern von Indikatorsymbolen und Indikators&#228;tzen (Berichts-Generator und SSRS) | Microsoft Docs"
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
ms.assetid: 8a056adf-4473-473d-9b0c-314675af7bfd
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# &#196;ndern von Indikatorsymbolen und Indikators&#228;tzen (Berichts-Generator und SSRS)
  Möglicherweise stellen die vorkonfigurierten Indikatorsätze, die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] für paginierte Berichte bereitstellt, die Daten nicht immer effektiv dar und können im übermittelten Bericht nicht optimal verwendet werden. Dieses Thema enthält Vorgehensweisen, um die Darstellung von Indikatorsymbolen zu ändern und die Indikatorsätze anzupassen, sodass andere, mehr oder weniger Indikatorsymbole enthalten sind.  
  
 Optionen wie Farben können mit Ausdrücken festgelegt werden. Weitere Informationen finden Sie unter [Ausdrücke &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
## So ändern Sie die Farbe eines Indikatorsymbols  
  
1.  Klicken Sie mit der rechten Maustaste auf den Indikator, der geändert werden soll, und klicken Sie auf **Indikatoreigenschaften**.  
  
2.  Klicken Sie im linken Bereich auf **Wert und Status** .  
  
3.  Klicken Sie in der Spalte **Farbe** neben dem Symbol, das geändert werden soll, auf den Nach-unten-Pfeil, und wählen Sie dann die gewünschte Farbe, **Keine Farbe**oder **Weitere Farben**.  
  
     Klicken Sie optional auf die Schaltfläche **Ausdruck** (*fx*), um einen Ausdruck zu bearbeiten, mit dem der Wert der Option **Farbe** festgelegt wird.  
  
     Wenn Sie auf **Weitere Farben**geklickt haben, wird das Dialogfeld **Farbe auswählen** geöffnet, in dem Sie zwischen vielen verschiedenen Farben auswählen können. Weitere Informationen zu den zugehörigen Optionen finden Sie unter [Farbe auswählen (Dialogfeld) &#40;Berichts-Generator und SSRS&#41;](../Topic/Select%20Color%20Dialog%20Box%20\(Report%20Builder%20and%20SSRS\).md). Klicken Sie auf **OK** , um das Dialogfeld **Farbe auswählen** zu schließen.  
  
4.  Klicken Sie auf **OK**.  
  
## So ändern Sie das Symbol  
  
1.  Klicken Sie mit der rechten Maustaste auf den Indikator, der geändert werden soll, und klicken Sie auf **Indikatoreigenschaften**.  
  
2.  Klicken Sie im linken Bereich auf **Wert und Status** .  
  
3.  Klicken Sie auf den Nach-unten-Pfeil neben dem Symbol, das Sie ändern möchten, und wählen Sie ein anderes Symbol aus.  
  
     Klicken Sie optional auf die Schaltfläche **Ausdruck** (*fx*), um einen Ausdruck zu bearbeiten, der den Wert der Option **Symbol** festlegt.  
  
4.  Klicken Sie auf **OK**.  
  
## So verwenden Sie ein benutzerdefiniertes Bild als Indikatorsymbol  
  
1.  Klicken Sie mit der rechten Maustaste auf den Indikator, der geändert werden soll, und klicken Sie auf **Indikatoreigenschaften**.  
  
2.  Klicken Sie im linken Bereich auf **Wert und Status** .  
  
3.  Klicken Sie auf den Nach-unten-Pfeil neben dem Symbol, das Sie ändern möchten, und wählen Sie **Bild**aus.  
  
4.  Klicken Sie in der Liste **Bildquelle auswählen** auf **Extern**, **Eingebettet**oder **Datenbank**.  
  
5.  Führen Sie abhängig von der Bildquelle eine der folgenden Aktionen aus:  
  
    -   Wenn Sie ein Bild verwenden, das außerhalb des Berichts gespeichert ist, klicken Sie auf **Durchsuchen** , und navigieren Sie zu dem Bild. Der Bericht enthält einen Verweis auf das Bild.  
  
    -   Wenn Sie ein Bild verwenden möchten, das in den Bericht eingebettet ist, klicken Sie auf **Importieren** , und navigieren Sie zu dem Bild. Das Bild wird der Berichtsdefinition hinzugefügt und zusammen damit gespeichert.  
  
    -   Wenn Sie ein Bild verwenden möchten, das sich in einer Datenbank in der Liste **Dieses Feld verwenden** befindet, wählen Sie das Feld aus der Liste aus. Wählen Sie danach in der Liste **Diesen MIME-Typ verwenden** den MIME-Typ des Bilds aus.  
  
6.  Klicken Sie auf **OK**.  
  
## So fügen Sie dem Indikatorsatz ein Symbol hinzu  
  
1.  Klicken Sie mit der rechten Maustaste auf den Indikator, der geändert werden soll, und klicken Sie auf **Indikatoreigenschaften**.  
  
2.  Klicken Sie im linken Bereich auf **Wert und Status** .  
  
3.  Klicken Sie auf **Hinzufügen**. Ein Indikator wird mithilfe des Standardsymbols und der Option **Keine Farbe** hinzugefügt.  
  
     Konfigurieren Sie den indictor, um das gewünschte Symbol und die gewünschte Farbe zu verwenden. In den Vorgehensweisen weiter oben in diesem Thema werden die entsprechenden Schritte erläutert.  
  
4.  Klicken Sie auf **OK**.  
  
## So löschen Sie ein Symbol im Indikatorsatz  
  
1.  Klicken Sie mit der rechten Maustaste auf den Indikator, der geändert werden soll, und klicken Sie auf **Indikatoreigenschaften**.  
  
2.  Klicken Sie im linken Bereich auf **Wert und Status** .  
  
3.  Wählen Sie den Indikator aus, der gelöscht werden soll, und klicken Sie dann auf **Löschen**.  
  
4.  Klicken Sie auf **OK**.  
  
## Siehe auch  
 [Indikatoren &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  