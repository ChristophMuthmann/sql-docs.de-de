---
title: Attribute (Master Data Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- free-form attributes [Master Data Services]
- attributes [Master Data Services], about attributes
- attributes [Master Data Services], file attributes
- file attributes [Master Data Services]
- attributes [Master Data Services], free-form attributes
- attributes [Master Data Services]
ms.assetid: 95ecb75f-c559-41c3-933c-40ae60a4c2fd
caps.latest.revision: "13"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ca7a31974a26dfe6b8f38ea3e17c480a74526518
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="attributes-master-data-services"></a>Attribute (Master Data Services)
  Attribute sind Objekte, die in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Entitäten enthalten sind. Attributwerte beschreiben die Elemente der Entität. Ein Attribut kann verwendet werden, um ein Blattelement, ein konsolidiertes Element oder eine Auflistung zu beschreiben.  
  
## <a name="how-attributes-relate-to-other-model-objects"></a>Zusammenhang zwischen Attributen und anderen Modellobjekten  
 Sie können sich ein Attribut als Spalte in einer Entitätstabelle vorstellen. Ein Attributwert dient zur Beschreibung eines bestimmten Elements.  
  
 ![Als Tabelle dargestellte Master Data Services-Entität](../master-data-services/media/mds-conc-entity-table.gif "Master Data Services Entity Represented as Table")  
  
 Wenn Sie eine Entität erstellen, die viele Attribute enthält, können Sie die Attribute in Attributgruppen organisieren. Weitere Informationen finden Sie unter [Attributgruppen &#40;Master Data Services&#41;](../master-data-services/attribute-groups-master-data-services.md).  
  
## <a name="required-attributes"></a>Erforderliche Attribute.  
 Wenn Sie eine Entität erstellen, werden die Attribute Name und Code automatisch erstellt. Code erfordert einen Wert und muss innerhalb der Entität eindeutig sein. Sie können das Name-Attribut und das Code-Attribut nicht entfernen.  
  
## <a name="attribute-types"></a>Attributtypen  
 Es gibt drei Typen von Attributen:  
  
-   Freiformattribute, die Freiformeingabe für Text, Zahlen, Datumsangaben oder Links ermöglichen.  
  
-   Domänenbasierte Attribute, die von Entitäten aufgefüllt werden. Weitere Informationen finden Sie unter [Domänenbasierte Attribute &#40;Master Data Services&#41;](../master-data-services/domain-based-attributes-master-data-services.md).  
  
-   Dateiattribute, die zum Speichern von Dateien, Dokumenten oder Bildern verwendet werden. Dateiattribute tragen zur Konsistenz der Daten bei, indem bestimmte Erweiterungen für Dateien vorausgesetzt werden. Dateiattribute können jedoch nicht zuverlässig verhindern, dass ein böswilliger Benutzer eine Datei eines anderen Typs hochlädt.  
  
### <a name="numeric-free-form-attributes"></a>Numerische Freiformattribute  
 Die Werte von numerischen Freiformattributen erfordern eine besondere Behandlung, da diese Werte auf den Werttyp **SqlDouble** beschränkt sind.  
  
 Standardmäßig enthält ein **SqlDouble** -Wert 15 Dezimalstellen, obwohl intern ein Maximum von 17 Ziffern gespeichert wird. Die Genauigkeit einer Gleitkommazahl hat mehrere Folgen:  
  
-   Zwei Gleitkommazahlen, die für eine bestimmte Genauigkeit identisch zu sein scheinen, können sich als unterschiedlich erweisen, wenn sich die zwei letzten Ziffern unterscheiden.  
  
-   Eine mathematische oder Vergleichsoperation, die eine Gleitkommazahl verwendet, ergibt möglicherweise ein anderes Ergebnis, wenn eine Dezimalzahl verwendet wird, da die Gleitkommazahl ggf. nicht hundertprozentig mit der Dezimalzahl übereinstimmt.  
  
-   Bei einem mithilfe von Gleitkommazahlen berechneten Wert liefert eine *Gegenprobe* möglicherweise ein abweichendes Ergebnis. Der Begriff Roundtrip wird in Bezug auf einen Wert verwendet, wenn ein Vorgang eine ursprüngliche Gleitkommazahl in ein anderes Format konvertiert, ein umgekehrter Vorgang das konvertierte Format zurück zu einer Gleitkommazahl überträgt und die endgültige Gleitkommazahl mit der ursprünglichen Gleitkommazahl übereinstimmt. Der Roundtrip kann fehlschlagen, wenn eine oder mehrere Ziffern am Ende des Werts bei der Konvertierung verloren gehen oder geändert werden.  
  
## <a name="attribute-examples"></a>Attributbeispiele  
 Im folgenden Beispiel verfügt die Entität über folgende Attribute: Name, Code, Subcategory, StandardCost, ListPrice und FilePhoto. Diese Attribute beschreiben die Elemente. Jedes Element wird durch eine einzelne Zeile mit Attributwerten dargestellt.  
  
 ![Entitätstabelle für Fahrradprodukte](../master-data-services/media/mds-conc-entity-table-w-data.gif "Bike Product Entity Table")  
  
 Im folgenden Beispiel stellt die Entität Product Folgendes:  
  
-   Die Freiformattribute Name, Code, StandardCost und ListPrice  
  
-   Das domänenbasierte Attribut Subcategory  
  
-   Das Dateiattribut FilePhoto  
  
 Die Entität Subcategory wird als domänenbasiertes Attribut der Entität Product verwendet. Die Entität Category wird als domänenbasiertes Attribut der Entität Subcategory verwendet. Die Entitäten Category und Subcategory enthalten genauso wie die Entität Product jeweils die Standardattribute Name und Code.  
  
 ![Produktentitätsbaumstruktur](../master-data-services/media/mds-conc-entity-ui.gif "Product Entity Tree Structure")  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Erstellen Sie ein neues Freiformtextattribut.|[Erstellen eines Textattributs &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)|  
|Erstellen Sie ein neues numerisches Freiformattribut.|[Erstellen eines numerischen Attributs &#40;Master Data Services&#41;](../master-data-services/create-a-numeric-attribute-master-data-services.md)|  
|Erstellen Sie ein neues Freiformlinkattribut.|[Erstellen eines Linkattributs &#40;Master Data Services&#41;](../master-data-services/create-a-link-attribute-master-data-services.md)|  
|Erstellen Sie ein neues Dateiattribut.|[Erstellen eines Dateiattributs &#40;Master Data Services&#41;](../master-data-services/create-a-file-attribute-master-data-services.md)|  
|Erstellen Sie ein neues domänenbasiertes Attribut.|[Erstellen eines domänenbasierten Attributs &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)|  
|Ändern Sie den Namen eines vorhandenen Attributs.|[Ändern eines Attributnamens und Datentyps &#40;Master Data Services&#41;](../master-data-services/change-an-attribute-name-and-data-type-master-data-services.md)|  
|Fügen Sie einer Änderungsnachverfolgungsgruppe vorhandene Attribute hinzu.|[Hinzufügen von Attributen zu einer Änderungsnachverfolgungsgruppe &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md)|  
|Löschen Sie ein vorhandenes Attribut.|[Löschen eines Attributs &#40;Master Data Services&#41;](../master-data-services/delete-an-attribute-master-data-services.md)|  
|Ändern Sie die Reihenfolge der Attribute.|[Ändern der Reihenfolge von Attributen](../master-data-services/change-the-order-of-attributes.md)|  
|Erstellen Sie ein Datenattribut|[Erstellen eines Datenattributs &#40;Master Data Services&#41;](../master-data-services/create-a-date-attribute-master-data-services.md)|  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   [Domänenbasierte Attribute &#40;Master Data Services&#41;](../master-data-services/domain-based-attributes-master-data-services.md)  
  
-   [Attributgruppen &#40;Master Data Services&#41;](../master-data-services/attribute-groups-master-data-services.md)  
  
-   [Elemente &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)  
  
-   [Blattberechtigungen &#40;Master Data Services&#41;](../master-data-services/leaf-permissions-master-data-services.md)
  
