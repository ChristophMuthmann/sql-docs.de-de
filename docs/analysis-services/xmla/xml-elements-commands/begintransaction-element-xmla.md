---
title: BeginTransaction-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- BeginTransaction Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#BeginTransaction
- microsoft.xml.analysis.begintransaction
- http://schemas.microsoft.com/analysisservices/2003/engine#BeginTransaction
helpviewer_keywords:
- BeginTransaction command
ms.assetid: fca122fc-b57c-4ba6-849b-ca8c93cf64e9
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 677ad07e9ce6206bbc4e7946ec111f8865bcfcce
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="begintransaction-element-xmla"></a>BeginTransaction-Element (XMLA)
  Startet eine Transaktion für die aktuelle Sitzung mit einer Instanz von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<Command>  
   <BeginTransaction />  
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
 Der **BeginTransaction** -Befehl startet eine aktive Transaktion auf der aktuellen Sitzung. Besteht bereits eine aktive Transaktion, inkrementiert die [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Instanz den Verweiszähler der Transaktionen für die aktuelle Sitzung. Wenn nicht, startet die Instanz eine neue Transaktion und setzt den Verweiszähler der aktuellen Sitzung auf 1. Wenn eine aktive Transaktion explizit über den **BeginTransaction** -Befehl angegeben wird, werden alle folgenden Befehle innerhalb der explizit angegebenen Transaktion ausgeführt.  
  
 Wenn die aktuelle Sitzung beendet wird und der Verweiszähler der Transaktionen höher als null ist, wird für alle aktiven Transaktionen ein Rollback ausgeführt.  
  
 Wenn es in der aktuellen Sitzung keine explizit angegebenen aktiven Transaktionen gibt, wird jeder in der aktuellen Sitzung ausgegebene Befehl innerhalb einer implizit definierten Transaktion ausgeführt. Ein Commit wird für die implizite Transaktion ausgeführt, wenn der Befehl erfolgreich ist; bei einem Fehlschlagen des Befehls wird ein Rollback ausgeführt.  
  
## <a name="see-also"></a>Siehe auch  
 [Cancel-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)   
 [CommitTransaction-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)   
 [RollbackTransaction-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)   
 [Befehle &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  

