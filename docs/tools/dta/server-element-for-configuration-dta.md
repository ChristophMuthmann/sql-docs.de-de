---
title: "Server-Element für Konfiguration (DTA) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Server element
ms.assetid: da9ff870-9cfd-42fe-994b-7b9292681f7d
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 548c08ab2bb5a12cade464305fa1ac0969c26bca
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="server-element-for-configuration-dta"></a>Server-Element für Konfiguration (DTA)
  Enthält die Identifikationsinformationen für den Server, auf dem der Datenbankoptimierungsratgeber die hypothetische Konfiguration auswerten soll (wird durch das **Configuration** -Element angegeben).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
<Configuration>  
    <Server>  
...code removed here...  
    </Server>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|**Datentyp und -länge**|Keine.|  
|**Standardwert**|Keine.|  
|**Vorkommen**|Einmal pro **Configuration** -Element erforderlich.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|[Configuration-Element &#40; DTA &#41;](../../tools/dta/configuration-element-dta.md)|  
|**Untergeordnete Elemente**|[Name-Element für Server &#40; DTA &#41;](../../tools/dta/name-element-for-server-dta.md)<br /><br /> [Database-Element für Konfiguration &#40; DTA &#41;](../../tools/dta/database-element-for-configuration-dta.md)|  
  
## <a name="remarks"></a>Hinweise  
 Sie können nur ein **Server** -Element für das **Configuration** -Element angeben. Dieses Element hat den Namen **ServerTypecomplexType** im [XML-Schema des Datenbankoptimierungsratgebers](http://go.microsoft.com/fwlink/?linkid=43100). Dieses **Server** -Element ist nicht mit dem untergeordneten Element für das **DTAInput** -Element identisch. Weitere Informationen finden Sie unter [Server-Element &#40;DTA&#41;](../../tools/dta/server-element-dta.md).  
  
## <a name="example"></a>Beispiel  
 Ein Beispiel für die Syntax finden Sie unter [Beispiel für eine XML-Eingabedatei mit benutzerdefinierter Konfiguration &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
