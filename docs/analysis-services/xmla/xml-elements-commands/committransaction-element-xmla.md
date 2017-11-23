---
title: CommitTransaction-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: CommitTransaction Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#CommitTransaction
- urn:schemas-microsoft-com:xml-analysis#CommitTransaction
- microsoft.xml.analysis.committransaction
helpviewer_keywords: CommitTransaction command
ms.assetid: 1cd814dc-a0be-4305-b44d-faf15e843f7d
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 98c2a6ffaa4949b4eaaf45291ed854090a78f135
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="committransaction-element-xmla"></a>CommitTransaction-Element (XMLA)
  Führt einen Commit für eine Transaktion für die aktuelle Sitzung mit einem [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Instanz.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Command>  
   <CommitTransaction />  
</Command>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|0-n: Optionales Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[Befehl](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Untergeordnete Elemente|Keine|  
  
## <a name="remarks"></a>Hinweise  
 Der **CommitTransaction** -Befehl führt für die aktuelle Sitzung einen Commit für eine aktive Transaktion aus, die explizit durch das **BeginTransaction** -Element definiert ist. Wenn keine aktive Transaktion vorhanden ist, tritt ein Fehler auf. Besteht bereits eine aktive Transaktion, reduziert die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Instanz den Verweiszähler der Transaktionen für die aktuelle Sitzung. Wenn der Verweiszähler explizit definierter aktiver Transaktionen den Wert Null erreicht die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] -Instanz einen Commit für die Transaktion.  
  
## <a name="see-also"></a>Siehe auch  
 [BeginTransaction-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)   
 [Cancel-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)   
 [RollbackTransaction-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)   
 [Befehle &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
