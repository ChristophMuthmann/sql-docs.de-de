---
title: "Master Data Services-Add-In für Microsoft Excel | Microsoft-Dokumentation"
ms.custom: SQL2016_New_Updated
ms.date: 07/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 33d9c8fc-9602-494d-b9ab-8f0f42785974
caps.latest.revision: "30"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: db24fe315bbb87b2ae730eca497038763e28d63a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="master-data-services-add-in-for-microsoft-excel"></a>Master Data Services-Add-In für Microsoft Excel
  Mit dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] können Sie gefilterte Listen der Daten von MDS in Excel laden, wo Sie damit genauso arbeiten können, wie Sie es mit beliebigen anderen Daten auch tun würden. Wenn Sie fertig sind, können Sie die Daten in MDS veröffentlichen, wo sie zentral gespeichert werden. Mit Sicherheit wird festgelegt, welche Daten Sie anzeigen und aktualisieren können.  
  
 Wenn Sie Administrator sind, verwenden Sie [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] , um Entitäten und Attribute zu erstellen und sie mit Daten zu laden. Dadurch ist es nicht mehr erforderlich, beliebige andere Tools zum Laden von Daten in die Modelle zu verwenden.  
  
 In [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]können Sie mithilfe von Data Quality Services (DQS) Daten vor dem Laden in MDS zuordnen. Dadurch werden doppelte Daten in MDS verhindert.  

## <a name="downloads"></a>Downloads 
>*  Sie können das Master Data Services Add-In für Excel und SQL Server 2016 SP1 von [dieser Microsoft Download Center-Seite](https://go.microsoft.com/fwlink/?linkid=836866) herunterladen. 
>* Laden Sie das [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] für SQL Server 2017 CTP1 von [dieser Microsoft Download Center-Seite](https://go.microsoft.com/fwlink/?linkid=836867)herunter. Dieses Add-In funktioniert auch für SQL Server 2017 RC1.

 
  
## <a name="terms"></a>Begriffe  
 Wenn Sie mit dem Add-In arbeiten, stoßen Sie möglicherweise auf die folgenden Begriffe. Weitere Informationen über diese Konzepte finden Sie unter [Übersicht über Master Data Services &#40;MDS&#41;](../../master-data-services/master-data-services-overview-mds.md).  
  
-   Das *MDS repository* ist, wo alle Masterdaten gespeichert sind. Es ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank, die zum Speichern von MDS-Daten konfiguriert ist. Um mit Daten aus dem Repository zu arbeiten, laden Sie die Daten in Excel. Wenn Sie mit der Arbeit fertig sind, veröffentlichen Sie die Änderungen im Repository. Administratoren können dem Repository neue Entitäten und Attribute hinzufügen.  
  
-   *Von MDS verwaltete Daten* sind Daten, die im MDS-Repository gespeichert sind und die Sie in Excel laden, wo die Daten als markierte Zeilen angezeigt werden. Sie können Daten hinzufügen, die nicht von MDS verwaltet werden und die nicht davon betroffen sind, wenn Sie die von MDS verwalteten Daten aktualisieren.  
  
-   Ein *model* ist ein Container mit Daten. Versionen dieser Container können erstellt werden, und normalerweise ist die neueste Version die aktuellste. Weitere Informationen finden Sie unter [Modelle &#40;Master Data Services&#41;](../../master-data-services/models-master-data-services.md).  
  
-   Eine *entity* ist eine Liste mit Daten. Sie können sich eine Entität als Tabelle in einer Datenbank vorstellen. Die Entität **Farbe** könnte z. B. eine Liste mit Farben enthalten. Weitere Informationen finden Sie unter [Entitäten &#40;Master Data Services&#41;](../../master-data-services/entities-master-data-services.md).  
  
-   Ein *Element* ist eine Zeile mit Daten (ein Datensatz). Jede Entität enthält Elemente. Ein Beispiel für ein Element ist **Blau**. Weitere Informationen finden Sie unter [Elemente &#40;Master Data Services&#41;](../../master-data-services/members-master-data-services.md).  
  
-   Ein *attribute* ist eine Spalte mit Daten. Jedes Element verfügt über Attribute. Das Attrribut **Code** für das Element **Blau** ist z.B. **B**. Weitere Informationen zu Attributen finden Sie unter [Attribute &#40;Master Data Services&#41;](../../master-data-services/attributes-master-data-services.md).  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Erstellen Sie eine Verbindung zu einem [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] -Repository.|[Herstellen einer Verbindung mit einem MDS-Repository &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md)|  
|Laden Sie von MDS verwaltete Daten in Excel.|[Exportieren von Daten nach Excel aus Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)|  
|Speichern Sie eine Shortcutabfrage, die Sie zum Öffnen der gerade angezeigten, von MDS verwalteten Daten verwenden können.|[Speichern einer Shortcutabfragedatei &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/save-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|Geben Sie Verknüpfungen für andere frei.|[Senden einer Shortcutabfragedatei &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/email-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|Zeigen Sie alle Änderungen an, die an einem Element vorgenommen wurden.|[Anzeigen aller Anmerkungen oder Transaktionen für ein Element &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
|Ermitteln Sie vor dem Veröffentlichen von neuen Daten, ob doppelte Werte vorhanden sind.|[Abgleichen ähnlicher Daten &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)|  
|Veröffentlichen Sie Daten eines Arbeitsblatts im MDS-Repository.|[Importieren von Daten aus Excel in Master Data Services &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|Erstellen Sie im Arbeitsblatt eine neue Entität mit Daten. (Nur Administratoren)|[Erstellen einer Entität &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/create-an-entity-mds-add-in-for-excel.md)|  
|Erstellen Sie ein domänenbasiertes Attribut, das auch als eingeschränkte Liste bezeichnet wird. (Nur Administratoren)|[Erstellen eines domänenbasierten Attributs &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/create-a-domain-based-attribute-mds-add-in-for-excel.md)|  
|Legen Sie Eigenschaften zum Laden und dem Veröffentlichen von Daten im Master Data Services-Add-In für Excel fest. (Nur Administratoren)|[Festlegen von Eigenschaften für das Master Data Services-Add-In für Microsoft Excel](../../master-data-services/microsoft-excel-add-in/setting-properties-for-master-data-services-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   [Verbindungen &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/connections-mds-add-in-for-excel.md)  
  
-   [Übersicht: Exportieren von Daten nach Excel &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
-   [Shortcutabfragedateien &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [Aktualisieren von Daten &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/refreshing-data-mds-add-in-for-excel.md)  
  
-   [Übersicht: Importieren von Daten aus Excel &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
-   [Überprüfen von Daten &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/validating-data-mds-add-in-for-excel.md)  
  
-   [Data Quality-Abgleich im MDS-Add-In für Excel](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)  
  
-   [Erstellen eines Modells &#40;MDS-Add-In für Excel&#41;](../../master-data-services/microsoft-excel-add-in/building-a-model-mds-add-in-for-excel.md)  
  
-   [Festlegen von Eigenschaften für das Master Data Services-Add-In für Microsoft Excel](../../master-data-services/microsoft-excel-add-in/setting-properties-for-master-data-services-add-in-for-excel.md)  
  
-   [Sicherheit &#40;Master Data Services&#41;](../../master-data-services/security-master-data-services.md)  
  
  
