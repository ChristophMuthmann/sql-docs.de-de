---
title: "Lektion 3: Entwerfen des übergeordneten Berichts mithilfe des Berichts-Assistenten | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 2f69dcd3-cd6d-45a9-a62a-ba6f5f3179d8
caps.latest.revision: 9
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b491008866649087e050b04261bfde7a3ad82e92
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="lesson-3-design-the-parent-report-using-the-report-wizard"></a>Lektion 3: Entwerfen des übergeordneten Berichts mithilfe des Berichts-Assistenten
Nachdem Sie eine Datenverbindung und eine Datentabelle für den übergeordneten Bericht erstellt haben, entwerfen Sie im nächsten Schritt den übergeordneten Bericht mithilfe des Berichts-Assistenten im Berichts-Designer. Weitere Informationen zum Berichts-Designer finden Sie unter [Entwerfen von Berichten mithilfe des Berichts-Designers &#40;SSRS&#41;](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md).  
  
### <a name="to-design-the-parent-report-using-the-report-wizard"></a>So entwerfen Sie den übergeordneten Bericht mithilfe des Berichts-Assistenten  
  
1.  Stellen Sie sicher, dass die Website der obersten Ebene im **Projektmappen-Explorer**ausgewählt ist.  
  
2.  Klicken Sie mit der rechten Maustaste auf die Website, und wählen Sie **Neues Element hinzufügen**aus.  
  
3.  Wählen Sie im Dialogfeld **Neues Element hinzufügen** die Option **Berichts-Assistent**aus, geben Sie einen Namen für die Berichtsdatei ein, und wählen Sie anschließend **Hinzufügen**aus.  
  
    Daraufhin wird der Berichts-Assistent gestartet.  
  
4.  Wählen Sie auf der Seite **Dataseteigenschaften** im Feld **Datenquelle** das **DataSet1** aus, das Sie in [Lektion 2: Definieren einer Datenverbindung und einer Datentabelle für den übergeordneten Bericht](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)erstellt haben.  
  
    Das Feld **Verfügbare Datasets** wird automatisch anhand der oben erstellten **DataTable** aktualisiert.  
  
5.  Wählen Sie **Weiter**aus.  
  
6.  Gehen Sie auf der Seite **Felder anordnen** wie folgt vor:  
  
    1.  Ziehen Sie **ProductID**, **Name**, **ProductNumber**, **SafetyStockLevel**und **ReorderLevel** vom Feld **Verfügbare Felder** auf das Feld **Werte** .  
  
    2.  Klicken Sie auf den Pfeil neben **Sum(ProductID)**, **Sum(SafetyStockLevel)**und **Sum(ReorderLevel)** , und löschen Sie die Auswahl **Sum** .  
  
7.  Klicken Sie zweimal auf **Weiter** und anschließend auf **Fertig stellen** , um den **Berichts-Assistenten**zu schließen.  
  
    Die RDLC-Datei ist jetzt erstellt. Die Datei wird im Berichts-Designer geöffnet. Die entworfene Tablix wird jetzt auf der Entwurfsoberfläche angezeigt.  
  
8.  Speichern Sie die RDLC-Datei.  
  
## <a name="next-task"></a>Nächste Aufgabe  
Sie haben erfolgreich den übergeordneten Bericht mithilfe des Berichts-Assistenten entworfen. Als Nächstes erstellen Sie eine Datenverbindung und eine Datentabelle für den untergeordneten Bericht. Siehe [Lektion 4: Definieren einer Datenverbindung und einer Datentabelle für den untergeordneten Bericht](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md).  
  
  
  


