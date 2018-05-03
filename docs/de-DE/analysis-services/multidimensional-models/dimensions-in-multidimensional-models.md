---
title: Dimensionen in mehrdimensionalen Modellen | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f2a58f5db400792b09cabafc12ae2a521e0f1776
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="dimensions-in-multidimensional-models"></a>Dimensionen in mehrdimensionalen Modellen
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
  
 [Verwenden Sie Business Intelligence-Assistenten zum Erweitern von Dimensionen](http://msdn.microsoft.com/library/12d995d1-75ca-4890-bf4b-a2656910b8d0)  
 Beschreibt das Verbessern einer Datenbankdimension mithilfe des Business Intelligence-Assistenten.  
  
## <a name="see-also"></a>Siehe auch  
 [Cubes in mehrdimensionalen Modellen](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
  
  
