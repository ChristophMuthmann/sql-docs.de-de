---
title: "Erstellen einer Entität (MDS-Add-In für Excel) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: microsoft-excel-add-in
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d354abb3-88fe-4b40-a374-f6256b84ffae
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a344f047e914a798ec34053100f474c7aabcde76
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/05/2018
---
# <a name="create-an-entity-mds-add-in-for-excel"></a>Erstellen einer Entität (MDS-Add-In für Excel)
  In [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]können Administratoren neue Entitäten erstellen, um Daten zu speichern. Wenn Sie eine Entität erstellen, sollten Sie mindestens eine Stichprobenentnahme der Daten laden, die Sie speichern möchten.  
  
## <a name="prerequisites"></a>Voraussetzungen  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf die Funktionsbereiche **Systemverwaltung** und **Explorer** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../../master-data-services/administrators-master-data-services.md).  
  
-   Sie müssen über ein vorhandenes Modell verfügen, in dem die Entität erstellt werden kann. Weitere Informationen finden Sie unter [Erstellen eines Modells &#40;Master Data Services&#41;](../../master-data-services/create-a-model-master-data-services.md).  
  
-   Stellen Sie sicher, dass die Daten die folgenden Anforderungen erfüllen:  
  
    -   Die Daten sollten eine Kopfzeile haben.  
  
    -   Es ist hilfreich, wenn die Spalten **Name** und **Code** vorhanden sind. Der**Code** ist ein eindeutiger Bezeichner für jede Zeile.  
  
    -   Außer der Kopfzeile sollte mindestens eine Zeile mit Daten vorhanden sein. Nicht in allen Spalten müssen Werte enthalten sein, aber die Daten sollten repräsentativ für die Daten sein, die in der Entität enthalten sein sollen.  
  
    -   Wenn Sie eine Spalte verwenden, die einen eindeutigen Bezeichner enthält (unter MDS als **Code**bezeichnet), sollten Sie sicherstellen, dass die Werte eindeutig sind. Falls keine Spalte Bezeichner enthält, können Sie diese beim Erstellen der Entität automatisch generieren lassen.  
  
    -   Stellen Sie sicher, dass keine Zellen Formeln enthalten.  
  
    -   Stellen Sie sicher, dass keine Zellen Zeitwerte enthalten. Datumswerte können unter MDS gespeichert werden, aber für Zeitwerte ist dies nicht möglich.  
  
### <a name="to-create-an-entity-and-load-data"></a>So erstellen Sie eine Entität und laden Daten  
  
1.  Öffnen oder erstellen Sie ein Excel-Arbeitsblatt, das die zu ladenden Daten enthält.  
  
2.  Wählen Sie die Zellen aus, die Sie in die neue Entität laden möchten.  
  
3.  Klicken Sie auf der Registerkarte **Masterdaten** in der Gruppe **Modell erstellen** auf **Entität erstellen**.  
  
4.  Stellen Sie eine Verbindung mit einem MDS-Repository her, wenn Sie dazu aufgefordert werden.  
  
5.  Lassen Sie den Standardbereich im Dialogfeld **Entität erstellen** unverändert, oder passen Sie ihn an die zu ladenden Daten an.  
  
6.  Deaktivieren Sie nicht das Kontrollkästchen **Meine Daten besitzen Kopfzeilen** .  
  
7.  Wählen Sie aus der Liste **Modell** ein Modell aus.  
  
8.  Wählen Sie aus der Liste **Version** eine Version aus.  
  
9. Geben Sie im Feld **Neuer Entitätsname** einen Namen für die Entität ein.  
  
10. Wählen Sie in der Liste **Code** die Spalte aus, die eindeutige Bezeichner enthält, oder lassen Sie die Codes automatisch generieren.  
  
11. Optional. Wählen Sie in der Liste **Name** eine Spalte aus, die Namen für jedes Element enthält.  
  
12. Klicken Sie auf **OK**. Nachdem die Entität erfolgreich erstellt wurde, wird eine neue Kopfzeile angezeigt, die Zellen werden hervorgehoben, und der Blattname wird an den Entitätsnamen angepasst.  
  
## <a name="next-steps"></a>Next Steps  
  
-   Um Fehler anzuzeigen, die in der Gruppe **Veröffentlichen und Überprüfen** aufgetreten sind, klicken Sie auf **Status anzeigen**. Die Spalten ValidationStatus und InputStatus werden angezeigt. Weitere Informationen finden Sie unter [Überprüfen von Daten &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/validating-data-mds-add-in-for-excel.md).  
  
-   Bestätigen Sie, dass die Attribute mit dem gewünschten Datentyp erstellt wurden.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen eines domänenbasierten Attributs &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/create-a-domain-based-attribute-mds-add-in-for-excel.md)  
  
  
