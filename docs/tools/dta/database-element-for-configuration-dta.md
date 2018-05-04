---
title: Database-Element für Konfiguration (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: e91ba243-6cc9-457a-8f5a-134f3c71ae69
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eaa4205ecec50a446b9a3cac2d1d14f4b7290f07
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="database-element-for-configuration-dta"></a>Database-Element für Konfiguration (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Gibt die Datenbank an, für die der Datenbankoptimierungsratgeber die hypothetische Konfiguration auswerten soll (wird durch das **Configuration** -Element angegeben).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Description|  
|--------------------|-----------------|  
|**Datentyp und -länge**|Keine.|  
|**Standardwert**|Keine.|  
|**Vorkommen**|Einmal oder mehrfach pro **Server** -Element erforderlich.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|[Server-Element für Konfiguration &#40;DTA&#41;](../../tools/dta/server-element-for-configuration-dta.md)|  
|**Untergeordnete Elemente**|[Name-Element für Datenbank &#40;DTA&#41;](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [Schema-Element für Datenbank &#40;DTA&#41;](../../tools/dta/schema-element-for-database-dta.md)<br /><br /> [Recommendation-Element &#40;DTA&#41;](../../tools/dta/recommendation-element-dta.md)|  
  
## <a name="remarks"></a>Remarks  
 Dieses Element hat den Namen **DatabaseTypecomplexType** im XML-Schema des Datenbankoptimierungsratgebers. Dieses **Database** -Element ist nicht mit dem Element identisch, dessen übergeordnetes Stammelement das **Server** -Element ist. Dieses Element wird oben in der XML-Eingabedatei angezeigt. Weitere Informationen finden Sie unter [Database-Element für Server &#40;DTA&#41;](../../tools/dta/database-element-for-server-dta.md).  
  
## <a name="example"></a>Beispiel  
 Ein Beispiel für die Verwendung dieses **Database**-Elements finden Sie unter [Beispiel für eine XML-Eingabedatei mit benutzerdefinierter Konfiguration &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
