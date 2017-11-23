---
title: "Database-Element für Server (DTA) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: Database element
ms.assetid: 5cd9a87a-af4b-45f3-8c18-f7fd7e7d3064
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f1988ac62e5a19d235915a95f27e03562f00c31b
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="database-element-for-server-dta"></a>Database-Element für Server (DTA)
  Gibt die Datenbank an, die Sie auf einem bestimmten Server optimieren möchten.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine.|  
|Standardwert|Keine.|  
|Vorkommen|Einmal oder mehrfach pro **Server** -Element erforderlich.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|Übergeordnetes Element|[Server-Element &#40;DTA&#41;](../../tools/dta/server-element-dta.md)|  
|Untergeordnete Elemente|[Name-Element für Datenbank &#40;DTA&#41;](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [Schema-Element für Datenbank &#40;DTA&#41;](../../tools/dta/schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>Hinweise  
 Dieses Element hat den Namen **DatabaseDetailsTypecomplexType** im XML-Schema des Datenbankoptimierungsratgebers. Dieses **Database** -Element ist nicht mit dem identisch, dessen übergeordnetes Stammelement das **Configuration** -Element ist. Weitere Informationen finden Sie unter [Database-Element für Konfiguration &#40;DTA&#41;](../../tools/dta/database-element-for-configuration-dta.md).  
  
## <a name="example"></a>Beispiel  
 Ein Beispiel für die Verwendung des **Database** -Elements finden Sie unter [Server-Element &#40;DTA&#41;](../../tools/dta/server-element-dta.md).  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
