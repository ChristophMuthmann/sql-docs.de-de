---
title: "Übersicht: Importieren von Daten aus Excel (MDS-Add-In für Excel) | Microsoft-Dokumentation"
ms.custom: SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ea84a9aa-aeec-411b-ab8d-bc1b14f864a3
caps.latest.revision: "13"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 53da4593acf085e0bcaf8423aee411d71f5c2ee4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="overview-importing-data-from-excel-mds-add-in-for-excel"></a>Übersicht: Importieren von Daten aus Excel (MDS-Add-In für Excel)
  Veröffentlichen Sie in [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]im MDS-Repository Daten, wenn Sie diese für andere Benutzer freigeben möchten. Sobald die Daten veröffentlicht werden, stehen sie anderen Benutzern des Add-Ins zum Herunterladen zur Verfügung.  
  
 Wenn Sie Daten veröffentlichen, werden alle Daten, die Sie hinzugefügt oder aktualisiert haben, im MDS-Repository veröffentlicht. Gelöschte Daten werden nicht veröffentlicht. Sie müssen Daten separat löschen. Weitere Informationen finden Sie unter [Löschen einer Zeile &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/delete-a-row-mds-add-in-for-excel.md).  
  
> [!NOTE]  
>  Die Veröffentlichung kann nicht zum Erstellen einer neuen Entität verwendet werden. Weitere Informationen zum Erstellen von Entitäten finden Sie unter [Erstellen einer Entität &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/create-an-entity-mds-add-in-for-excel.md).  
  
## <a name="when-multiple-users-publish-at-the-same-time"></a>Wenn mehrere Benutzer gleichzeitig veröffentlichen  
 Mehrere Benutzer können Updates zu den gleichen Daten veröffentlichen. Sobald jeder Benutzer veröffentlicht hat, wird das Update in der Datenbank gespeichert. Dies bedeutet, dass ein Benutzer, der nicht mit den zuletzt aktualisierten Daten gearbeitet hat, immer noch den Wert ändern kann, wenn er oder sie veröffentlicht.  
  
 Nur die Updates, die Sie vornehmen, werden in der Datenbank veröffentlicht. Alle veraltete Daten im Arbeitsblatt werden nicht veröffentlicht.  
  
## <a name="transactions-and-annotations"></a>Transaktionen und Anmerkungen  
 Jede veröffentlichte Änderung wird als Transaktion gespeichert. Wenn Sie möchten, können Sie einer Transaktion Anmerkungen (Kommentare) hinzufügen, um zu erklären, warum Sie die Änderung vorgenommen haben.  
  
-   Sie können keine Löschungen kommentieren, obwohl Löschungen als Transaktionen gespeichert werden, die von einem Administrator umgekehrt werden können.  
  
-   Wenn Sie den **Code** -Wert für ein Element ändern, sind alle vorherigen Transaktionen für das Element nicht verfügbar. Durch die Änderung des **Code** -Werts auf den ursprünglichen Wert können Sie auf die vorherigen Transaktionen zugreifen.  
  
-   Sie können Transaktionen anzeigen, die von anderen Benutzern an einem Element vorgenommen wurden. Sie können auch alle Transaktionen anzeigen, die Sie an einem Element vorgenommen haben, auch wenn Sie nicht mehr über die Berechtigung für bestimmte Attribute verfügen. Nicht angezeigt werden Transaktionen, die Attribute enthalten, für die Sie keine Berechtigung erhalten haben.  
  
 Sie können alle an einem Element vorgenommenen Transaktionen anzeigen. Weitere Informationen finden Sie unter [Anzeigen aller Anmerkungen oder Transaktionen für ein Element &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md).  
  
> [!IMPORTANT]  
>  Wenn Sie eine Anmerkung von mehr als 500 Zeichen eingeben, wird die Anmerkung automatisch abgeschnitten.  
  
## <a name="business-rule-and-other-validation"></a>Geschäftsregel und andere Überprüfung  
 Wenn Sie Daten veröffentlichen, wird eine Überprüfung ausgeführt, um sicherzustellen, dass die Daten exakt sind, bevor sie dem MDS-Repository hinzugefügt werden. Wenn die Daten die angegebenen Kriterien nicht erfüllen, werden sie nicht im Repository veröffentlicht. Weitere Informationen finden Sie unter [Überprüfen von Daten &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/validating-data-mds-add-in-for-excel.md).  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Veröffentlichen Sie Daten vom aktiven Arbeitsblatt zurück zum MDS-Repository.|[Importieren von Daten aus Excel in Master Data Services &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|Löschen Sie eine Zeile aus dem MDS-Repository und vom Arbeitsblatt zur gleichen Zeit.|[Löschen einer Zeile &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/delete-a-row-mds-add-in-for-excel.md)|  
|Zeigen Sie Anmerkungen (Kommentare) und Transaktionen für Datenzeilen (Elemente) an, wenn Sie die Updates der Daten im Zeitverlauf anzeigen möchten.|[Anzeigen aller Anmerkungen oder Transaktionen für ein Element &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
|Kombinieren Sie Daten aus zwei Arbeitsblättern, wenn Sie Daten vor der Veröffentlichung vergleichen möchten.|[Kombinieren von Daten &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/combine-data-mds-add-in-for-excel.md)|  

  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   [Aktualisieren von Daten &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/refreshing-data-mds-add-in-for-excel.md)  
  
-   [Master Data Services-Add-In für Microsoft Excel](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)  
  
  
