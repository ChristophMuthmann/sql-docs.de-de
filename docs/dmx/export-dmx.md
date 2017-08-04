---
title: EXPORT (DMX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- EXPORT
dev_langs:
- DMX
helpviewer_keywords:
- exporting mining models
- exporting mining structures
- mining structures [DMX], exporting
- EXPORT statement
ms.assetid: 97617071-e560-4080-81af-a80276fc0823
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bfc3e8344d1c6967185979c0970be6d49b572500
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="export-dmx"></a>EXPORT (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Extrahiert ein Miningmodell- oder Miningstrukturobjekt aus dem Server in eine ABF-Datei (Analysis Services Backup File).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
EXPORT <object type> <object name>[, <object name>] [<object type> <object name>[, <object name] ] TO <filename> [WITH DEPENDENCIES]  
```  
  
## <a name="arguments"></a>Argumente  
 *Objekttyp*  
 Optional den Typ des Objekts (entweder Miningmodell oder Miningstruktur) exportieren.  
  
 *Objektname*  
 Optional. Der Name des zu exportierenden Objekts.  
  
 *Dateiname*  
 Die Zeichenfolge, die den Namen und den Speicherort der Datei angibt, in die exportiert werden soll.  
  
## <a name="remarks"></a>Hinweise  
 Ist in der Anweisung ein Miningmodell angegeben, enthält die sich ergebende Datei auch eine zugeordnete Miningstruktur. Wenn die Anweisung gibt **WITH DEPENDENCIES**, alle Objekte, die zum Verarbeiten des Objekts (z. B. die Datenquelle und Datenquellensicht) erforderlich sind, sind in die ABF-Datei enthalten.  
  
 Müssen Sie eine Datenbank oder Administrator zum Exportieren oder Importieren von Objekten aus einer [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Datenbank.  
  
## <a name="export-mining-structure-example"></a>Beispiel zum Exportieren einer Miningstruktur  
 Im folgenden Beispiel werden die Miningstrukturen Targeted Mailing und Forecasting sowie das Association-Miningmodell in eine Datei exportiert. Da das Association-Modell zur Market Basket-Miningstruktur gehört, wird in dem Beispiel auch die Market Basket-Struktur exportiert. Alle anderen Miningmodelle, die möglicherweise vorhanden, als Teil der Market Basket-Miningstruktur wird nicht exportiert werden, da das Association-Modell mit exportiert wurde **MININGMODELL**, nicht **MININGSTRUKTUR**.  
  
```  
EXPORT MINING STRUCTURE [Targeted Mailing], [Forecasting] MINING MODEL Association TO 'C:\TM_NEW.abf'  
```  
  
## <a name="export-mining-model-example"></a>Beispiel zum Exportieren eines Miningmodells  
 Im folgenden Beispiel wird das Association-Miningmodell in die angegebene Datei exportiert. Da die Anweisung gibt **WITH DEPENDENCIES**, die Datenquelle und Datenquellensicht-Objekte auch in die ABF-Datei enthalten sind.  
  
```  
EXPORT MINING MODEL [Association] TO 'C:\Association_NEW.abf' WITH DEPENDENCIES  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40; DMX &#41; Datendefinitionsanweisungen](../dmx/dmx-statements-data-definition.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Datenbearbeitungsanweisungen](../dmx/dmx-statements-data-manipulation.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)   
 [-IMPORT &#40; DMX &#41;](../dmx/import-dmx.md)   
 [Exportieren und Importieren von Datamining-Objekte](../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
  

