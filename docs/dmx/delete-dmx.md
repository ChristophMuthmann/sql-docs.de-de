---
title: "LÖSCHEN (DMX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: DELETE
dev_langs: DMX
helpviewer_keywords:
- DELETE statement [DMX]
- mining structures [DMX], clearing
- clearing mining models
- deleting mining models
- mining models [Analysis Services], clearing
- deleting mining structures
ms.assetid: 5a8204c3-a3df-4d97-9c1d-d997d24c70e3
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 35c908eaed7147a454d02c5bf6620e274e45df18
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="delete-dmx"></a>DELETE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  LGöscht abhängig von den verwendeten DMX-Klauseln (Data Mining-Erweiterungen) ein Miningmodell, eine Miningstruktur oder eine Miningstruktur samt allen ihr zugeordneten Miningmodellen.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DELETE FROM [MINING MODEL] <model>[.CONTENT]  
DELETE FROM [MINING STRUCTURE] <structure>[.CONTENT]|[.CASES]  
```  
  
## <a name="arguments"></a>Argumente  
 *model*  
 Ein Modellbezeichner.  
  
 *Struktur*  
 Ein Strukturbezeichner.  
  
## <a name="remarks"></a>Hinweise  
 Wenn Sie keinen angeben **MININGMODELL** oder **MININGSTRUKTUR**, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] sucht nach den Objekttyp basierend auf den Namen und das richtige Objekt verarbeitet. Wenn der Server eine Miningstruktur und ein Miningmodell enthält, die denselben Namen haben, wird ein Fehler zurückgegeben.  
  
 In der folgenden Tabelle sind die Ergebnisse beschrieben, die sich ergeben, wenn verschiedene Formen der Syntax verwendet werden.  
  
|-Anweisung.|Ergebnis|  
|---------------|------------|  
|DELETE FROM MINING STRUCTURE*\<Struktur >*<br /><br /> oder<br /><br /> DELETE FROM MINING STRUCTURE*\<Struktur >*. INHALT|Führt ProcessClear für die Miningstruktur an. Der gesamte Inhalt wird aus der Miningstruktur sowie aus den dieser zugeordneten Miningmodellen gelöscht.|  
|DELETE FROM MINING STRUCTURE*\<Struktur >*. FÄLLE|Führt ' ProcessClearStructureOnly ' für die Miningstruktur an. Der gesamte Inhalt wird aus der Miningstruktur gelöscht, wogegen die der Struktur zugeordneten Miningmodelle erhalten bleiben. Drillthrough für die zugeordneten Miningmodelle erzeugt einen Fehler, nachdem der Inhalt der Miningstruktur gelöscht wurde.|  
|Löschen von MINING MODEL*\<Modell >*<br /><br /> oder<br /><br /> Löschen von MINING MODEL*\<Modell >*. INHALT|Führt ProcessClear für das Miningmodell, aber die Statuswerte intakt bleibt. Statuswerte sind die möglichen Status einer Spalte. Beispielsweise sind die Statuswerte für eine Geschlecht-Spalte die Werte männlich und weiblich.|  
  
 Weitere Informationen zur Verarbeitung von Typen finden Sie unter [Type-Element &#40; XMLA &#41; ](../analysis-services/xmla/xml-elements-properties/type-element-xmla.md).  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der gesamte Inhalt aus dem NB_Sample-Modell entfernt.  
  
```  
DELETE FROM NB_Sample.CONTENT  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40; DMX &#41; Datendefinitionsanweisungen](../dmx/dmx-statements-data-definition.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Datenbearbeitungsanweisungen](../dmx/dmx-statements-data-manipulation.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
