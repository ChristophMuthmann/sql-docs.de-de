---
title: Server-Element (DTA) | Microsoft Docs
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
ms.assetid: 9fe0bfb4-3aa6-4eb2-a83e-c0d0e7d4e9f6
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a70751047dec6fb9f5826ce23bf81381cba828cf
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="server-element-dta"></a>Server-Element (DTA)
  Enthält die Identifikationsinformationen für den Server, auf dem sich die zu optimierenden Datenbanken befinden.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
<DTAInput>  
    <Server>  
    ...code removed here...  
    </Server>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|**Datentyp und -länge**|Keine.|  
|**Standardwert**|Keine.|  
|**Vorkommen**|Einmal pro **DTAInput** -Element erforderlich.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|[DTAInput-Element &#40; DTA &#41;](../../tools/dta/dtainput-element-dta.md)|  
|**Untergeordnete Elemente**|[Name-Element für Server &#40; DTA &#41;](../../tools/dta/name-element-for-server-dta.md)<br /><br /> [Database-Element für Server &#40; DTA &#41;](../../tools/dta/database-element-for-server-dta.md)|  
  
## <a name="remarks"></a>Hinweise  
 Sie können nur ein **Server** -Element für das **DTAInput** -Element angeben. Dieses Element hat im DTA-XML-Schema den Namen **ServerDetailsTypecomplexType** . Dieses **Server** -Element ist nicht mit dem untergeordneten Element für das **Configuration** -Element identisch. Weitere Informationen finden Sie unter [Server-Element für Konfiguration &#40;DTA&#41;](../../tools/dta/server-element-for-configuration-dta.md).  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird veranschaulicht, wie die **Sales.SalesPerson** -Tabelle in der **AdventureWorks** -Datenbank auf SERVER001 angegeben wird:  
  
```xml  
<Server>  
  <Name>SERVER001</Name>  
  <Database>  
    <Name>AdventureWorks</Name>  
    <Schema>  
      <Name>Sales</Name>  
      <Table>  
        <Name>SalesPerson</Name>  
      </Table>  
    </Schema>  
  </Database>  
</Server  
```  
  
## <a name="see-also"></a>Siehe auch  
 [XML-Eingabedateireferenz &#40;Datenbankoptimierungsratgeber&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  

