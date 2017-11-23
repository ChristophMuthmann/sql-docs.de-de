---
title: AccountType-Element (ASSL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: AccountType Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: AccountType
helpviewer_keywords: AccountType element
ms.assetid: 4fdf17d3-cd84-4bf6-9baf-21e15d4bf71e
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e59eeeebc216840a62266cda57da8bdf2838eeba
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="accounttype-element-assl"></a>AccountType-Element (ASSL)
  Enthält den Namen des definierten Kontotyps ein [Datenbank](../../../analysis-services/scripting/objects/database-element-assl.md) Element.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Account>  
   ...  
   <AccountType>...</AccountType>  
   ...  
</Account>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Zeichenfolge (Enumeration)|  
|Standardwert|Keine|  
|Kardinalität|1-1: Erforderliches Element, das nur einmal auftritt.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Konto](../../../analysis-services/scripting/objects/account-element-assl.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der Wert dieses Elements ist auf eine der in der folgenden Tabelle aufgelisteten Zeichenfolgen beschränkt.  
  
|Wert|Description|  
|-----------|-----------------|  
|*Einkommen*|Das Konto ist ein Einnahmenkonto.|  
|*Ausgaben*|Das Konto ist ein Ausgabenkonto.|  
|*Datenfluss*|Das Konto ist ein Cashflowkonto.|  
|*Lastenausgleich*|Das Konto ist ein Bilanzkonto.|  
|*Anlage*|Das Konto ist ein Bestandskonto.|  
|*Haftung*|Das Konto ist ein Passivkonto.|  
|*Statistische*|Das Konto ist ein statistisches Konto.|  
  
 Die Enumeration, die den zulässigen Werten für die entsprechende **AccountType** im Objekt Analysis Management Objects (AMO) Modell ist <xref:Microsoft.AnalysisServices.AccountTypes>.  
  
## <a name="see-also"></a>Siehe auch  
 [Accounts-Element &#40; ASSL &#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)   
 [Datenbankeigenschaften &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
