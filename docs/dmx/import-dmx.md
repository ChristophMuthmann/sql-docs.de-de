---
title: IMPORTIEREN (DMX) | Microsoft Docs
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
f1_keywords:
- IMPORT
dev_langs:
- DMX
helpviewer_keywords:
- IMPORT statement
- mining structures [DMX], importing
ms.assetid: c053bc88-2daf-4ebb-81d7-5a330250536d
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 5510631430ed75a04dd9685d1197f60c64a85aa8
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="import-dmx"></a>IMPORT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Lädt ein Miningmodell oder eine Miningstruktur aus einer ABF-Datei (Analysis Services Backup File) auf den Server.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
IMPORT FROM <filename>  
```  
  
## <a name="arguments"></a>Argumente  
 *Dateiname*  
 Eine Zeichenfolge, die den Namen und den Speicherort der Datei angibt, die importiert werden soll.  
  
## <a name="remarks"></a>Hinweise  
 Wenn keine Objekte angegeben sind, wird der gesamte Inhalt der DMB-Datei geladen. Wenn die DMB-Datei eine Datenbank enthält, die auf dem Server nicht vorhanden ist, wird die Datenbank erstellt.  
  
 Sie müssen Datenbank- oder Serveradministrator sein, damit Sie Objekte exportieren bzw. importieren können.  
  
## <a name="import-from-file-example"></a>Beispiel für das Importieren aus einer Datei  
 Im folgenden Beispiel wird der gesamte Inhalt der Datei, die das Zuordnungsmodell und die Struktur enthält, auf den aktuellen Server importiert.  
  
```  
IMPORT FROM 'C:\TEMP\Association_NEW.dmb'  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datamining-Erweiterungen &#40; DMX &#41; Datendefinitionsanweisungen](../dmx/dmx-statements-data-definition.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; Datenbearbeitungsanweisungen](../dmx/dmx-statements-data-manipulation.md)   
 [Datamining-Erweiterungen &#40; DMX &#41; -Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)   
 [EXPORT &#40; DMX &#41;](../dmx/export-dmx.md)   
 [Exportieren und Importieren von Datamining-Objekte](../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
  

