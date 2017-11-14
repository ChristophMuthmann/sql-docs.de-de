---
title: Model-Objekts (TMSL) | Microsoft Docs
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 9382d0d6-2d4b-49ad-a0eb-35970f0f3afb
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 369bf544360d50c061314f45c04e8fb55784184c
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="model-object-tmsl"></a>Model-Objekts (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Definiert ein tabellarisches Modell. Es ist ein Modell pro Datenbank und nur eine Datenbank, die in einem Befehl angegeben werden kann. Ein Datenbankobjekt ist das übergeordnete Objekt.  
  
 Modelldefinitionen sind zu groß für die gesamte Syntax in einem Thema zu reproduzieren. Aus diesem Grund kann eine partielle syntaxhervorhebung, mit die Hauptbestandteile unten mit Links zu untergeordneten Objekten gefunden werden.  
  
 Möglicherweise ist die beste Möglichkeit, eine Modelldefinition zu verstehen, mit einem tabellarischen Modell zu starten, mit denen Sie vertraut. Verwenden der **Code anzeigen** Option in SQL Server Data Tools, um seine Definition anzuzeigen. Vergessen Sie nie einen JSON-Editor zu installieren, sodass Sie den Code anzeigen können. Sie erhalten einen JSON-Editor in Visual Studio durch [Herunterladen von der Community Edition](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) oder eine andere Edition von Visual Studio.  
  
> [!NOTE]  
>  In jedem Skript kann nur eine Datenbank zum Zeitpunkt verwiesen werden. Für jedes Objekt als die Datenbank selbst ist die Datenbankeigenschaft optional, wenn Sie das Modell anzugeben. Es ist 1: 1-Zuordnung zwischen einem Modell und eine Datenbank, die verwendet werden kann, um den Datenbanknamen abzuleiten, wenn diese nicht explizit angegeben wird.   
> Auf ähnliche Weise können Sie out-Modell, lassen die Eigenschaften für die Datenbank festlegen.  
  
## <a name="object-definition"></a>Objektdefinition  
 Alle Objekte verfügen über einen gemeinsamen Satz von Eigenschaften, einschließlich Name, Typ, Beschreibung, eine eigenschaftsauflistung und Anmerkungen. **Modell** Objekte verfügen außerdem über die folgenden Eigenschaften.  
  
 StorageLocation  
 Der Speicherort auf dem Datenträger, um das Modell zu platzieren.  
  
 defaultMode  
 Die Standardmethode zum Bereitstellen von Daten in der Partition.  
  
 defaultDataView  
 Für Modelle im DirectQuery-Modus bestimmt diese Eigenschaft an, welche Partitionen verwendet werden, um Abfragen für das Modell auszuführen.  Gültige Werte sind vollständige Installation und Beispiel.  
  
 culture  
 Die Kultur, für die Formatierung.  
  
 collation  
 Die Sortierreihenfolge. Finden Sie unter [globalisierungsszenarien für Analysis Services](../../analysis-services/globalization-scenarios-for-analysis-services.md) für Weitere Informationen.  
  
 Tabellen  
 Die vollständige Auflistung der Tabellen im Modell, einschließlich der Partitionen, Spalten, Measures, KPIs und Anmerkungen. Finden Sie unter [Object &#40; Tabellen TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md) für Details.  
  
 Beziehungen  
 Gibt die Beziehung zwischen jedem Tabellenpaar, einschließlich Eigenschaften, die filterrichtung und die Sicherheit festlegen. Finden Sie unter [Beziehungen Object &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/relationships-object-tmsl.md) für Details.  
  
 Datenquellen  
 Eine oder mehrere Verbindungen mit externen Datenbanken Daten für das Modell bereitstellt, oder zum pass-through-Abfragen. Finden Sie unter [DataSources Object &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md) für Details.  
  
 Rollen  
 Objekte, die Datenbankberechtigung, Benutzerkonten und optional von Sicherheitsfiltern in DAX, für die benutzerdefinierte Zugriffssteuerung zuordnen.  
  
## <a name="usage"></a>Verwendung  
 **Modell** Objekte enthalten ein gesamtes Modell. Sie müssen ein Modell und/oder seine übergeordnete Datenbankobjekt in die meisten Befehle angeben.  
  
 Beim Erstellen, ersetzen oder Ändern eines Model-Objekts geben Sie alle Lese-/ Schreibzugriff Eigenschaften der Objektdefinition. Eine Lese-/ Schreibzugriff-Eigenschaft nicht angegeben, gilt einen Löschvorgang.  
  
## <a name="partial-syntax"></a>Teilweise-Syntax  
 Da diese Objektdefinition so umfangreich ist, werden nur die erste Ebenen Eigenschaften aufgeführt. Finden Sie unter [Definitionen von Systemobjekten im tabellarischen Modell Scripting Language &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/tmsl-reference-tabular-objects.md) eine Liste der untergeordneten Objekte.  
  
```  
    "model": {  
      "description": "Model object of a Tabular database",  
      "type": "object",  
      "properties": {  
          "name": {  },  
          "description": {  },  
         "storageLocation": {  },  
         "defaultMode":  {  },  
         "defaultDataView": {  },  
         "culture": {  },  
         "collation": {  },  
         "annotations": {  },  
         "tables": {  },  
         "relationships": {  },  
         "dataSources": {  },  
         "perspectives": {  },  
            "cultures": {  },  
         "roles": {  }  
    }  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Kompatibilitätsgrad für tabellarische Modelle in Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  

