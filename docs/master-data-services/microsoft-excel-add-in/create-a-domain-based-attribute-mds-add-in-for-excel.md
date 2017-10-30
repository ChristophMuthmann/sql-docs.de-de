---
title: "Erstellen eines domänenbasierten Attributs (MDS-Add-In für Excel) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7b3e30dc-8f41-4a5d-8009-ae5a4426a64b
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 0183ba6f178fbc9f392b4e711ccaba49220ffa3e
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="create-a-domain-based-attribute-mds-add-in-for-excel"></a>Erstellen eines domänenbasierten Attributs (MDS-Add-In für Excel)
  Im [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]können Administratoren ein domänenbasiertes Attribut erstellen, wenn sie die Werte in einer Spalte auf einen bestimmten Satz von Werten beschränken möchten.  
  
 Die Werte können sich bereits im Arbeitsblatt befinden oder aus einer vorhandenen Entität stammen.  
  
> [!NOTE]  
>  Wenn Benutzer einen Wert in die eingeschränkte Spalte eingeben, anstatt diesen in der Liste auszuwählen, werden Fehler nach der Veröffentlichung in der Spalte **$InputStatus$** angezeigt.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf die Funktionsbereiche **Systemverwaltung** und **Explorer** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../../master-data-services/administrators-master-data-services.md).  
  
-   Das Modell und die Entität müssen bereits vorhanden sein.  
  
### <a name="to-perform-this-procedure"></a>So führen Sie diese Prozedur aus  
  
1.  Laden Sie in Excel die Entität, in der die Spalte (Attribut) enthalten ist, die Sie einschränken möchten. Weitere Informationen finden Sie unter [Export Data to Excel from Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)(Exportieren von Daten nach Excel aus Master Data Services).  
  
2.  Klicken Sie in der Spalte, die Sie einschränken möchten, auf eine beliebige Zelle.  
  
3.  Klicken Sie in der Gruppe **Modell erstellen** auf **Attributeigenschaften**.  
  
4.  Wählen Sie im Dialogfeld **Attributeigenschaften** in der Liste **Attributtyp** die Option **Eingeschränkte Liste (domänenbasiert)**.  
  
5.  In der Liste **Attribut mit Werten auffüllen aus** :  
  
    -   Um Werte aus dem Arbeitsblatt zu verwenden, wählen Sie **die ausgewählte Spalte**aus. Mit den Werten der ausgewählten Spalte wird eine neue Entität und eine neue Stagingtabelle erstellt.  
  
    -   Wählen Sie den Namen der Entität aus, um Werte einer vorhandenen Entität zu verwenden.
    
    Wenn mehr als 50 Entitäten vorhanden sind, können Sie diese filtern und nach einer Entität suchen. Wählen Sie andernfalls eine Entität aus der Dropdownliste aus.  
  
6.  Wenn Sie im vorherigen Schritt **die ausgewählte Spalte** gewählt haben, geben Sie im Feld **Neuer Entitätsname** einen Namen für die neue Entität ein. Dies kann der gleiche Name wie der Spaltenname (Attribut) sein.  
  
7.  Klicken Sie auf **OK**. Jede Zelle in der Spalte verfügt jetzt über eine Liste mit Werten, unter denen Benutzer wählen können.  
  
## <a name="next-steps"></a>Nächste Schritte  
  
-   Um Werte der eingeschränkten Liste hinzuzufügen und daraus zu löschen, laden Sie die Entität, auf der das Attribut basiert. Weitere Informationen zum Laden von Entitäten finden Sie unter [Export Data to Excel from Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)(Exportieren von Daten nach Excel aus Master Data Services).  
  
## <a name="see-also"></a>Siehe auch  
 [Domänenbasierte Attribute &#40;Master Data Services&#41;](../../master-data-services/domain-based-attributes-master-data-services.md)   
 [Erstellen einer Entität (MDS-Add-In für Excel)](../../master-data-services/microsoft-excel-add-in/create-an-entity-mds-add-in-for-excel.md)   
 [Erstellen eines Modells &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/building-a-model-mds-add-in-for-excel.md)  
  
  

