---
title: DAX-Eigenschaften | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: aa928dc5-d00d-4f8a-80b9-7e6973d2196c
caps.latest.revision: 6
author: HeidiSteen
ms.author: heidist
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 225c4aea79b880fd85f118d89bae1339e370aa40
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="dax-properties"></a>DAX-Eigenschaften
   Der DAX-Abschnitt von „msmdsrv.ini“ enthält Einstellungen zur Steuerung bestimmter Verhaltensweisen von Abfragen in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], wie z.B. die maximale Anzahl von Zeilen, die in einem DAX-Abfrageresultset zurückgegeben werden. 
  
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

