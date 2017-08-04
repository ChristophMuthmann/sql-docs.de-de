---
title: Modelle (Master Data Services) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- models [Master Data Services], about models
- models [Master Data Services]
ms.assetid: 9f862a3d-25ab-41e9-b833-1db99959e825
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 635cb271e49ec96f889fdbba508e0374b186a8c9
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="models-master-data-services"></a>Modelle (Master Data Services)
  Modelle stellen die höchste Ebene der Datenorganisation in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]dar. Ein Modell definiert die Struktur der Daten in der Masterdaten-Verwaltungslösung. Ein Modell enthält die folgenden Objekte:  
  
-   Entitäten  
  
-   Attribute und Attributgruppen  
  
-   Explizite und abgeleitete Hierarchien  
  
-   Auflistungen  
  
 In Modellen wird die Struktur der Masterdaten organisiert. Ihre [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Implementierung kann über ein Modell oder viele Modelle verfügen, von denen jedes Daten ähnlichen Typs gruppiert. Die Masterdaten werden im Allgemeinen in vier Kategorien unterteilt: Personen, Orte, Gegenstände oder Begriffe. Sie können z. B. ein Produktmodell erstellen, das produktbezogene Daten enthält, oder ein Kundenmodell, das kundenbezogene Daten enthält.  
  
 Sie können Benutzern und Gruppen Berechtigungen für die Anzeige und Aktualisierung von Objekten innerhalb des Modells zuweisen. Wenn Sie keine Berechtigung für das Modell gewähren, wird es nicht angezeigt.  
  
 Zu einem beliebigen Zeitpunkt können Sie Kopien der Masterdaten innerhalb eines Modells erstellen. Diese Kopien werden als Versionen bezeichnet.  
  
 Nachdem Sie ein Modell in einer Testumgebung definiert haben, können Sie es mit oder ohne die entsprechenden Daten von der Testumgebung aus in einer Produktionsumgebung bereitstellen. Auf diese Weise erübrigt sich die Neuerstellung der Modelle in der Produktionsumgebung.  
  
## <a name="how-models-relate-to-other-objects"></a>Zusammenhang zwischen Modellen und anderen Objekten  
 Ein Modell enthält Entitäten. Entitäten enthalten Attribute, explizite Hierarchien und Auflistungen. Attribute können in Attributgruppen enthalten sein. Domänenbasierte Attributesind vorhanden, wenn eine Entität für eine andere Entität als Attribut verwendet wird.  
  
 Dieses Bild zeigt die Beziehung zwischen den Objekten in einem Modell an.  
  
 ![Objekte in einem Master Data Services-Modell](../master-data-services/media/mds-conc-model-circles.gif "Objekte in einem Master Data Services-Modell")  
  
> [!NOTE]  
>  Abgeleitete Hierarchien sind ebenfalls Modellobjekte, sie werden jedoch nicht im Bild angezeigt. Abgeleitete Hierarchien werden von den domänenbasierten Attributbeziehungen abgeleitet, die zwischen Entitäten vorhanden sind. Finden Sie unter [abgeleitete Hierarchien &#40; Master Data Services &#41; ](../master-data-services/derived-hierarchies-master-data-services.md) für Weitere Informationen.  
  
 Masterdaten sind die Daten, die in den Modellobjekten enthalten sind. In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]werden Masterdaten als Elemente in einer Entität gespeichert.  
  
 Modellobjekte werden im Funktionsbereich **Systemverwaltung** der [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] -Benutzeroberfläche verwaltet.  
  
## <a name="model-example"></a>Modellbeispiel  
 Im folgenden Beispiel gruppieren die Objekte im Produktmodell logisch produktbezogene Daten.  
  
 ![Product Model Master beispielhafte](../master-data-services/media/mds-conc-model.gif "Product Model Master Data-Beispiel")  
  
 Weitere allgemeine Modelle:  
  
-   Konten: Mögliche Entitäten sind Bilanzkonten, Gewinn- und Verlustrechnungen, Statistiken und Kontotyp.  
  
-   Kunde: Mögliche Entitäten sind Geschlecht, Ausbildung, Beruf und Familienstand.  
  
-   Geografie: Mögliche Entitäten sind Postleitzahlen, Städte, Landkreise, Staaten, Provinzen, Regionen, Gebiete, Länder und Kontinente.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Erstellen Sie ein Modell, um die Masterdaten zu organisieren.|[Erstellen Sie ein Modell &#40; Master Data Services &#41;](../master-data-services/create-a-model-master-data-services.md)|  
|Ändern Sie den Namen eines vorhandenen Modells.|[Bearbeiten Sie Modell &#40; Master Data Services &#41;](../master-data-services/edit-model-master-data-services.md)|  
|Löschen Sie ein vorhandenes Modell.|[Löschen eines Modells &#40; Master Data Services &#41;](../master-data-services/delete-a-model-master-data-services.md)|  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   [Übersicht über Master Data Services &#40;MDS&#41;](../master-data-services/master-data-services-overview-mds.md)  
  
-   [Entitäten &#40;Master Data Services&#41;](../master-data-services/entities-master-data-services.md)  
  
-   [Attribute &#40; Master Data Services &#41;](../master-data-services/attributes-master-data-services.md)  
  
-   [Bereitstellen von Modellen &#40; Master Data Services &#41;](../master-data-services/deploying-models-master-data-services.md)  
  
-   [Modellierung von Objektberechtigungen &#40; Master Data Services &#41;](../master-data-services/model-object-permissions-master-data-services.md)  
  
  
