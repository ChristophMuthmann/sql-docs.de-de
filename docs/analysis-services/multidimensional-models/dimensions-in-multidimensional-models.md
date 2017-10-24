---
title: Dimensionen in mehrdimensionalen Modellen | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OLAP [Analysis Services], dimensions
- dimensions [Analysis Services], about dimensions
- OLAP objects [Analysis Services], dimensions
ms.assetid: 2b62b05c-00fd-4e60-b77f-f707ba83a19b
caps.latest.revision: 46
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3e98c77a6b243bd5890aac6612db663377bd1bb3
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dimensions-in-multidimensional-models"></a>Dimensionen in mehrdimensionalen Modellen
  Eine Datenbankdimension ist eine Auflistung verknüpfter Objekte, Attribute genannt, mit deren Hilfe Informationen zu Faktendaten in einem oder mehreren Cubes zur Verfügung gestellt werden können. Typische Attribute in einer Produktdimension können z. B. Produktname, Produktkategorie, Produktlinie, Produktgröße und Produktpreis sein. Diese Objekte sind an eine oder mehrere Spalten in einer oder mehreren Tabellen in einer Datenquellensicht gebunden. Standardmäßig sind diese Attribute als Attributhierarchien sichtbar und dienen zum besseren Verständnis der Faktdaten in einem Cube. Attribute können in Form von benutzerdefinierten Hierarchien organisiert werden, die Navigationspfade bereitstellen, um Benutzer beim Durchsuchen der Daten in einem Cube zu unterstützen.  
  
 Cubes enthalten alle Dimensionen, auf die Benutzer ihre Analysen von Faktendaten stützen. Eine Instanz einer Datenbankdimension in einem Cube wird Cubedimension genannt. Sie bezieht sich auf eine oder mehrere Measuregruppen in einem Cube. Eine Datenbankdimension kann mehrere Male in einem Cube verwendet werden. Eine Faktentabelle kann z. B. mehrere zeitbezogene Fakten aufweisen, und es kann eine separate Cubedimension definiert werden, die die Analyse der einzelnen zeitbezogenen Fakten unterstützt. Es muss jedoch nur eine zeitbezogene Datenbankdimension vorhanden sein, was auch bedeutet, dass nur eine zeitbezogene relationale Datenbanktabelle vorhanden sein muss, um mehrere zeitbasierte Cubedimensionen zu unterstützen.  
  
> [!NOTE]  
>  Informationen zu Leistungsproblemen im Zusammenhang mit dem Dimensionsentwurf finden Sie im [Leistungsleitfaden zu SQL Server 2008 R2 Analysis Services](http://go.microsoft.com/fwlink/?LinkId=306717).  
  
## <a name="defining-dimensions-attributes-and-hierarchies"></a>Definieren von Dimensionen, Attributen und Hierarchien  
 Die einfachste Möglichkeit, Datenbank- und Cubedimensionen, Attribute und Hierarchien zu definieren, besteht darin, den Cube-Assistenten zu verwenden, um Dimensionen zur gleichen Zeit zu erstellen, zu der Sie den Cube definieren. Der Cube-Assistent erstellt Dimensionen auf der Basis der Dimensionstabellen in der Datenquellensicht, die der Assistent identifiziert, oder die Sie für die Verwendung in dem Cube angeben. Der Assistent erstellt daraufhin die Datenbankdimensionen und fügt sie dem neuen Cube hinzu, wodurch Cubedimensionen erstellt werden.  
  
 Wenn Sie einen Cube erstellen, können Sie dem neuen Cube zudem jede beliebige Dimension hinzufügen, die bereits in der Datenbank vorhanden ist. Diese wurde zuvor möglicherweise schon für einen anderen Cube oder vom Dimensions-Assistenten definiert. Nachdem eine Datenbankdimension definiert wurde, können Sie sie im Dimensions-Designer ändern und konfigurieren. Sie können auch mithilfe des Cube-Designers begrenzte benutzerdefinierte Einstellungen an der Cubedimension vornehmen.  
  
> [!NOTE]  
>  Mithilfe von XMLA oder Analysis Management Objects (AMO) können Sie Dimensionen, Attribute und Hierarchien auch programmgesteuert entwerfen und konfigurieren. Weitere Informationen finden Sie unter [Analysis Services Scripting Language &#40;ASSL for XMLA&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md) (Analysis Services Scripting Language (ASSL für XMLA)) und [Entwickeln mit Analysis Management Objects &#40;AMO&#41;](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 In der folgenden Tabelle werden die Themen in diesem Abschnitt beschrieben.  
  
 [Definieren von Datenbankdimensionen](../../analysis-services/multidimensional-models/define-database-dimensions.md)  
 Beschreibt das Ändern und Konfigurieren einer Datenbankdimension mithilfe des Dimensions-Designers.  
  
 [Dimensionsattributeigenschaftenverweis](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
 Beschreibt das Definieren, Ändern und Konfigurieren eines Datenbankdimensionsattributs mithilfe des Dimensions-Designers.  
  
 [Definieren von Attributbeziehungen](../../analysis-services/multidimensional-models/attribute-relationships-define.md)  
 Beschreibt das Definieren, Ändern und Konfigurieren einer Attributbeziehung mithilfe des Dimensions-Designers.  
  
 [Erstellen von benutzerdefinierten Hierarchien](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md)  
 Beschreibt das Definieren, Ändern und Konfigurieren einer aus Dimensionsattributen bestehenden benutzerdefinierten Hierarchie mithilfe des Dimensions-Designers.  
  
 [Verwenden des Business Intelligence-Assistenten zum Erweitern von Dimensionen](http://msdn.microsoft.com/library/12d995d1-75ca-4890-bf4b-a2656910b8d0)  
 Beschreibt das Verbessern einer Datenbankdimension mithilfe des Business Intelligence-Assistenten.  
  
## <a name="see-also"></a>Siehe auch  
 [Cubes in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
  
  

