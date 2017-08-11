---
title: "Hinzufügen, verschieben oder Löschen einer Tabelle, Matrix oder Liste (Berichts-Generator und SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b97c470-cde0-4bb1-a46e-5f5f5553feaa
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 52df1c4404f761f58189e5bfc05e23359f053808
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="add-move-or-delete-a-table-matrix-or-list-report-builder-and-ssrs"></a>Hinzufügen, Verschieben oder Löschen einer Tabelle, Matrix oder Liste (Berichts-Generator und SSRS)
  In einem paginierten [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Bericht zeigt ein Datenbereich Daten aus einem Berichtsdataset an. Zu den Datenbereichen gehören Tabelle, Matrix, Liste, Diagramm und Messgerät. Um einen Datenbereich in einen anderen Datenbereich zu schachteln, fügen Sie die Datenbereiche getrennt hinzu, und ziehen Sie dann den Datenbereich, den Sie schachteln möchten, auf den anderen Datenbereich.  
  
 Am einfachsten können Sie einen Tabellen- oder Matrixdatenbereich einem Bericht hinzufügen, indem Sie den Assistenten Neue Tabelle oder Neue Matrix ausführen. Diese Assistenten führen Sie durch die einzelnen Schritte bei der Auswahl einer Verbindung mit einer Datenquelle, dem Anordnen von Feldern und der Auswahl von Layout und Stil. Die Assistenten sind nur im Berichts-Generator verfügbar.  
  
## <a name="to-add-a-table-or-matrix-to-a-report-by-using-the-new-table-or-new-matrix-wizard"></a>So fügen Sie einem Bericht mit den Assistenten "Neue Tabelle" oder "Neue Matrix" eine Tabelle oder Matrix hinzu  
  
1.  Klicken Sie auf der Registerkarte **Einfügen** auf **Tabelle** oder **Matrix**und dann auf **Tabellen-Assistent** oder **Matrix-Assistent**.  
  
2.  Befolgen Sie die Schritte im Assistenten **Neue Tabelle** oder **Neue Matrix** .  
  
3.  Klicken Sie auf der Registerkarte **Home** auf **Ausführen** , um den gerenderten Bericht anzuzeigen.  
  
4.  Klicken Sie auf der Registerkarte **Ausführen** auf **Entwurf** , um den Bericht weiter zu bearbeiten.  
  
## <a name="to-add-a-data-region"></a>So fügen Sie einen Datenbereich hinzu  
  
1.  Klicken Sie auf dem **Menüband**in der Gruppe **Datenbereiche** auf den hinzuzufügenden Datenbereich.  
  
2.  Klicken Sie auf die Entwurfsoberfläche, und erstellen Sie dann durch Ziehen ein Feld mit der gewünschten Datenbereichsgröße.  
  
3.  Ziehen Sie ein Berichtsdataset-Feld aus dem Berichtsdatenbereich auf eine Datenbereichszelle. Jetzt ist der Datenbereich an Daten im Berichtsdataset gebunden.  
  
## <a name="to-select-a-data-region"></a>So wählen Sie einen Datenbereich aus  
  
-   Klicken Sie für einen Tablix-Datenbereich mit der rechten Maustaste auf den Eckziehpunkt. Klicken Sie für einen Diagramm- oder Messgerät-Datenbereich in den Datenbereich.  
  
     Ein Auswahlkästchen und acht Ziehpunkte werden angezeigt.  
  
     Klicken Sie für geschachtelte Datenbereiche mit der rechten Maustaste in den geschachtelten Datenbereich, klicken Sie auf **Auswählen**, und wählen Sie anschließend das gewünschte Berichtselement aus. Im Eigenschaftenbereich können Sie überprüfen, welches Berichtselement ausgewählt ist. Der Name des auf der Entwurfsoberfläche ausgewählten Elements wird in der Symbolleiste des Eigenschaftenbereichs angezeigt.  
  
## <a name="to-move-a-data-region"></a>So verschieben Sie einen Datenbereich  
  
-   Um einen Datenbereich zu verschieben, klicken Sie auf das Auswahlkästchen des Datenbereichs, und ziehen Sie ihn an die gewünschte Position. Verwenden Sie Ausrichtungslinien, um den Bereich an vorhandenen Berichtselementen auszurichten.  
  
     Wenn das Lineal nicht sichtbar ist, klicken Sie auf die Registerkarte Ansicht, und wählen Sie die Option **Lineal** aus.  
  
     Sie können den ausgewählten Datenbereich auf der Entwurfsoberfläche auch mit den Pfeiltasten verschieben.  
  
## <a name="to-delete-a-data-region"></a>So löschen Sie einen Datenbereich  
  
-   Wählen Sie den Datenbereich aus, klicken Sie mit der rechten Maustaste in den Datenbereich, und klicken Sie anschließend auf **Löschen**.  
  
## <a name="see-also"></a>Siehe auch  
 [Tablix-Datenbereich &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Tabellen, Matrizen und Listen &#40; Berichts-Generator und SSRS &#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
