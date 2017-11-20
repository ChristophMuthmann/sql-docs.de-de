---
title: Veraltete Funktionen von Master Data Services | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d8506bda-66dd-45a4-bfc9-3a10fa665acc
caps.latest.revision: 18
author: smartysanthosh
ms.author: nagavo
manager: erikre
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 37ba9531f4b4a2ba9b5831f5d7e8e121f5d3ad7d
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="deprecated-master-data-services-features"></a>Veraltete Funktionen von Master Data Services
  In diesem Thema werden die als veraltet markierten Funktionen von [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] beschrieben, die in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]noch verfügbar sind. Diese Funktionen werden voraussichtlich in einer zukünftigen Version von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]entfernt. Als veraltet markierte Funktionen sollten in neuen Anwendungen nicht verwendet werden.  
  
## <a name="explicit-hierarchies-collections-and-related-components"></a>Explizite Hierarchien, Sammlungen und zugehörige Komponenten  
 Explizite Hierarchien, Sammlungen und zugehörige Komponenten sind veraltet. Elemente, die als konsolidierte Elemente modelliert wurden (übergeordnetes Element in einer expliziten Hierarchie), und Elementtypen aus Sammlungen werden in abgeleiteten Hierarchien als Blattelemente gestaltet. Die folgenden neuen Funktionen aktivieren abgeleitete Hierarchien, sodass diese an die Stelle der expliziten Hierarchien treten.  
  
-   Rekursive abgeleitete Hierarchien können nun auch verwendet werden, um Elementsicherheitsberechtigungen zuzuweisen.  
  
     Eine explizite Hierarchie entspricht einer rekursiven abgeleiteten Hierarchie mit einer einzelnen, nicht rekursiven Ebene unterhalb der rekursiven Ebene. Eine rekursive abgeleitete Hierarchie kann komplex sein und eine oder mehrere Ebenen unterhalb und/oder unterhalb einer rekursiven Ebene beinhalten.  
  
-   Die Seite „Abgeleitete Hierarchie“ im Explorer zeigt nun die nicht zugewiesenen (nicht verwendeten) Elemente für jede Ebene der Hierarchie. Nicht verwendete Knoten sind nach Hierarchieebene gruppiert. Elemente können per Drag & Drop oder Ausschneiden und Einfügen zwischen den nicht verwendeten Knoten und den Stammknoten verschoben werden.  
  
     In der Systemverwaltung werden nicht verwendete Knoten im Bereich **Vorschau** angezeigt. Im Bereich „Sicherheit“ werden die nicht verwendeten Knoten in den **Hierarchieelementberechtigungen** angezeigt. Jedem Element unter dem **Stammknoten** oder dem Knoten **Nicht verwendet** kann eine Berechtigung zugewiesen werden. Sowohl den **Stammelementen**, als auch den **nicht verwendeten**Elementen und den **nicht verwendeten** Pseudoelementen können ebenfalls Berechtigungen zugewiesen werden.  
  
-   Die gespeicherte Prozedur „mdm.udpConvertCollectionAndConsolidatedMembersToLeaf“ konvertiert explizite Hierarchien in abgeleitete rekursive Hierarchien. Außerdem konvertiert sie konsolidierte Elemente und Sammlungselemente in Blattelemente.  
  
     Explizite Hierarchien, konsolidierte Elementtypen und Sammlungselementtypen werden immer noch unterstützt. Die Ausführung der Prozedur ist daher optional. Wenn Sie diese Elemente verwenden, sollten Sie die gespeicherte Prozedur ausführen, da die Elemente veraltet sind.  
  
 Informationen zu expliziten Hierarchien, Sammlungen und konsolidierten Elementen finden Sie in den folgenden Themen.  
  
-   [Explizite Hierarchien &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
-   [Sammlungen &#40;Master Data Services&#41;](../master-data-services/collections-master-data-services.md)  
  
-   [Elemente &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)  
  
## <a name="attribute-entity-transaction-log-type"></a>Transaktionsprotokolltyp von Entitäten  
Der Transaktionsprotokolltyp von Entitäten „Attribut“ ist veraltet, bitte migrieren Sie zum Transaktionsprotokolltyp von Entitäten „Element“. Informationen zu Transaktionsprotokolltypen von Entitäten finden Sie in folgendem Thema:
* [Ändern des Transaktionsprotokolltyps von Entitäten (Master Data Services)](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)
* [Elementrevisionsverlauf](../master-data-services/member-revision-history-master-data-services.md)
  
## <a name="external-resources"></a>Externe Ressourcen  
 Blogbeitrag [Deprecated: Explicit Hierarchies and Collections](http://go.microsoft.com/fwlink/p/?LinkId=615373)(Veraltet: explizite Hierarchien und Sammlungen) auf msdn.com.  
  
## <a name="see-also"></a>Siehe auch  
 [Eingestellte Master Data Services-Funktionen](../master-data-services/discontinued-master-data-services-features.md)  
  
  

