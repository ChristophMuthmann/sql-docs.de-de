---
title: Datenbankobjekt (TMSL) | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: ae5c046b-8242-4046-ae76-2c070503fd93
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 65672af9d00dc4b9058c59a656989df7c6a32638
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="database-object-tmsl"></a>Datenbankobjekt (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Definiert eine tabellarische Datenbank mit Kompatibilitätsgrad 1200 oder höher, auf Grundlage eines Modells der gleichen Ebene. In diesem Thema werden die Objektdefinition von einer Datenbank, die Nutzlast für Anforderungen, die erstellen, ändern, löschen und Ausführen von Verwaltungsaufgaben für die Datenbank bereitstellen.  
  
> [!NOTE]  
>  In jedem Skript kann nur eine Datenbank zum Zeitpunkt verwiesen werden. Für jedes Objekt als die Datenbank selbst ist die Datenbankeigenschaft optional, wenn Sie das Modell anzugeben. Es ist 1: 1-Zuordnung zwischen einem Modell und eine Datenbank, die verwendet werden kann, um den Datenbanknamen abzuleiten, wenn diese nicht explizit angegeben wird.   
> Auf ähnliche Weise können Sie out-Modell, lassen die Eigenschaften für die Datenbank festlegen.  
  
## <a name="object-definition"></a>Objektdefinition  
 Alle Objekte verfügen über einen gemeinsamen Satz von Eigenschaften, einschließlich Name, Typ, Beschreibung, eine eigenschaftsauflistung und Anmerkungen. **Datenbank** Objekte verfügen außerdem über die folgenden Eigenschaften.  
  
 CompatibilityLevel  
 Gültige Werte sind derzeit 1200, 1400. Niedrigere Kompatibilitätsgraden verwenden verschiedene Metadatenmodul.  
  
 readwritemode  
 Listet den Modus der Datenbank an. Es ist üblich, eine Datenbank schreibgeschützt in Konfigurationen mit hoher Verfügbarkeit oder Skalierbarkeit machen. Gültige Werte sind ReadWrite,  
                ReadOnly,  
                oder ReadOnlyExclusive. Finden Sie unter [hohe Verfügbarkeit und Skalierbarkeit in Analysis Services](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md) und [Umschalten in einer Analysis Services-Datenbank zwischen Schreib-und Lesemodus](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md) für Weitere Informationen, wenn diese Eigenschaft verwendet wird.  
  
## <a name="usage"></a>Verwendung  
 **Datenbank** Objekte sind in fast jeder Befehl verwendet. Finden Sie unter [Befehle in Tabular Model Scripting Language &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md) eine Liste. Ein **Datenbank** Objekt ist ein untergeordnetes Element eines Serverobjekts.  
  
 Beim Erstellen, ersetzen oder ändern ein Datenbankobjekt, geben Sie alle Lese-/ Schreibzugriff Eigenschaften der Objektdefinition. Eine Lese-/ Schreibzugriff-Eigenschaft nicht angegeben, gilt einen Löschvorgang.  
  
## <a name="partial-syntax"></a>Teilweise-Syntax  
 Da diese Objektdefinition so umfangreich ist, sind nur direkte Eigenschaften aufgelistet. Die **Modell** -Objekt ermöglicht den Großteil der Datenbankdefinition. Finden Sie unter [Modellobjekt &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/model-object-tmsl.md) , wie das Objekt definiert ist.  
  
```  
    "database": {  
      "type": "object",  
      "properties": {  
        "name": {  
          "type": "string"  
        },  
        "id": {  
          "type": "string"  
        },  
        "description": {  
          "type": "string"  
        },  
        "compatibilityLevel": {  
          "type": "integer"  
        },  
        "readWriteMode": {  
          "enum": [  
            "readWrite",  
            "readOnly",  
            "readOnlyExclusive"  
          ]  
        },  
        "model": {  
          "type": "object",  
          ...  
        }  
    }  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Tabular Model Scripting Language &#40;TMSL&#41; – Referenz](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Hohe Verfügbarkeit und Skalierbarkeit in Analysis Services](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)  
  
  
