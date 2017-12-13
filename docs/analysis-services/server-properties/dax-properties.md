---
title: DAX-Eigenschaften | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: aa928dc5-d00d-4f8a-80b9-7e6973d2196c
caps.latest.revision: "6"
author: HeidiSteen
ms.author: heidist
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a8a94cb71ab8625a2a546e62f5dc828b605aeaa2
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="dax-properties"></a>DAX-Eigenschaften
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Der DAX-Abschnitt von "Msmdsrv.ini" enthält Einstellungen zur Steuerung der Abfrage Verhalten in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], z. B. die Obergrenze für die Anzahl der Zeilen im Resultset eine DAX-Abfrage zurückgegeben. 
  
  Bei sehr großen Rowsets – etwa den in DirectQuery-Modellen zurückgegebenen – ist der Standardwert von einer Million Zeilen möglicherweise nicht ausreichend. Wissen Sie, ob die Grenze anpassen benötigt, wenn Sie diesen Fehler erhalten: Das Resultset einer Abfrage einer externen Datenquelle hat die maximal zulässige Größe von ‚1000000' Zeilen überschritten.
 
Um die Obergrenze zu erhöhen, legen Sie die Konfigurationseinstellung **MaxIntermediateRowSize** fest. Sie müssen das gesamte Element manuell in den DAX-Abschnitt der Konfigurationsdatei einfügen. Die Einstellung ist in der Datei erst dann vorhanden, wenn Sie sie hinzufügen.
  
## <a name="configuration-snippet"></a>Konfigurationscodeausschnitt

```
<ConfigurationSettings>
. . .
<DAX>   
  <PredicateCheckSpoolCardinalityThreshold>5000
  </PredicateCheckSpoolCardinalityThreshold>
  <DQ>
     <MaxIntermediateRowsetSize>1000000
     </MaxIntermediateRowsetSize>
  </DQ>
</DAX>
. . . 
```

## <a name="property-descriptions"></a>Eigenschaftsbeschreibungen

Einstellung |Wert |Description
--------|-------|-----------
MaxIntermediateRowsetSize | 1000000 | Maximale Anzahl von in einer DAX-Abfrage zurückgegebenen Zeilen. Fügen Sie diesen Eintrag manuell zur Datei „msmdsrv.ini“ hinzu, und erhöhen Sie den Wert, wenn die Standardeinstellung zu niedrig ist. 
PredicateCheckSpoolCardinalityThreshold| 5000 | Eine erweiterte Eigenschaft, die nur unter Anleitung des Microsoft-Supports geändert werden sollte.

Weitere Informationen zu zusätzlichen Servereigenschaften und zum Festlegen dieser Eigenschaften finden Sie unter [Servereigenschaften in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md). 
