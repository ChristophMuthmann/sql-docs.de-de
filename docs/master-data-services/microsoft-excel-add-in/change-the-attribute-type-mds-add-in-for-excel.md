---
title: "&#196;ndern des Attributtyps (MDS-Add-in f&#252;r Excel) | Microsoft Docs"
ms.custom: ""
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9d3001d9-8d0f-4e4a-8e04-4f666bf0df69
caps.latest.revision: 8
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 8
---
# &#196;ndern des Attributtyps (MDS-Add-in f&#252;r Excel)
  Im [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] können Administratoren den Attributtyp ändern, wenn der Datentyp oder die Anzahl zulässiger Zeichen falsch ist.  
  
 Wenn Sie den Attributtyp ändern möchten, um eine eingeschränkte Liste (domänenbasiertes Attribut) zu erstellen, finden Sie weitere Informationen unter [Erstellen eines domänenbasierten Attributs &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/create-a-domain-based-attribute-mds-add-in-for-excel.md).  
  
> [!NOTE]  
>  Sie können den Typ oder die Länge der Spalten **Name** oder **Code** nicht aktualisieren.  
  
## Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf die Funktionsbereiche **Systemverwaltung** und **Explorer** zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../../master-data-services/administrators-master-data-services.md).  
  
-   Modell, Entität und Attribut müssen vorhanden sein.  
  
### So ändern Sie den Attributtyp  
  
1.  Laden Sie in Excel die Entität, die die Spalte (Attribut) enthält, die Sie ändern möchten. Weitere Informationen finden Sie unter [Export Data to Excel from Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md) (Exportieren von Daten nach Excel aus Master Data Services).  
  
2.  Klicken Sie in der Spalte, die Sie ändern möchten, auf eine beliebige Zelle.  
  
3.  Klicken Sie in der Gruppe **Modell erstellen** auf **Attributeigenschaften**.  
  
4.  Aktualisieren Sie im Dialogfeld **Attributeigenschaften** je nach Bedarf die Einstellungen.  
  
5.  Klicken Sie auf **OK**.  
  
## Was geschieht, wenn Sie den Attributtyp ändern?  
 Wenn eine Abhängigkeit von dem Attribut besteht, weil beispielsweise eine MDS-Geschäftsregel oder eine abgeleitete Hierarchie auf das Attribut verweist, können Sie den Datentyp des Attributs nicht ändern. Sie erhalten eine Fehlermeldung, dass der Typ des Attributs nicht geändert werden kann, da ein Objekt damit verknüpft ist.  
  
 Wenn während der Datentypkonvertierung für die Attributwerte ein Fehler auftritt, führt MDS Folgendes aus.  
  
-   Der Datentyp des Attributs wird geändert.  
  
-   Es wird eine Kopie des Attributs mit dem Suffix "_old" generiert, das die vorherigen Werte enthält. Dies wird als veraltetes Attribut bezeichnet.  
  
## Siehe auch  
 [Attribute &#40;Master Data Services&#41;](../../master-data-services/attributes-master-data-services.md)   
 [Erstellen eines Modells &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/building-a-model-mds-add-in-for-excel.md)  
  
  