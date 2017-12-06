---
title: Issue-Element (Ssbdiagnose) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssbdiagnose
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- issue element
- XML output file format [ssbdiagnose], issue element
- ssbdiagnose
ms.assetid: 2246a886-686b-44ca-9771-b155cedad8be
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 370b4d10d7a0b7bb9407ad6867d2c81de3ecda61
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="issue-element-ssbdiagnose"></a>Issue-Element (ssbdiagnose)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Meldet ein Problem, das durch gefunden wurde die **Ssbdiagnose** Hilfsprogramm. Die XML-Ausgabedatei von **ssbdiagnose** enthält für jedes gemeldete Problem ein Issue-Element.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
<Issue  
    type="..."   
    code="..."   
    server="..."   
    database="..."   
    object="...">   
    ...   
</Issue>  
```  
  
## <a name="element-attributes"></a>Elementattribute  
  
|Attribut|Beschreibung|  
|---------------|-----------------|  
|**Typ**|Identifiziert die Kategorie des vom Issue-Element gemeldeten Problems:<br /><br /> **„Diagnose“** meldet ein bei der Analyse einer [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Konfiguration „gefundenes Konfigurationsproblem.<br /><br /> **„Problem“** meldet ein Problem, aufgrund dessen **ssbdiagnose** die Analyse nicht abschließen konnte. Beheben Sie das Problem, und führen Sie **ssbdiagnose**erneut aus.<br /><br /> **„Event“** meldet ein [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] -Ereignis, das bei der Ausführung einer **-RUNTIME** -Überprüfung gefunden wurde. Ereignisse werden nur gemeldet, wenn **-SHOWEVENTS** angegeben ist.|  
|**Code**|Gibt die Fehlernummer für die Meldung an.|  
|**server**|Identifiziert die Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] , in der das Problem gefunden wurde. Wenn das Problem in einer Standardinstanz gefunden wurde, enthält das Serverattribut nur den Computernamen. Wenn das Problem in einer benannten Instanz gefunden wurde, weist das Serverattribut das Format Computername\Instanzname auf.|  
|**database**|Identifiziert den Namen der Datenbank, in der das Problem gefunden wurde.|  
|**Objekt (object)**|Identifiziert den Namen des Objekts, in dem das Problem gefunden wurde. Wenn das Problem auf der Ebene einer Instanz oder Datenbank aufgetreten ist, wird im Objektattribut der Name der Instanz bzw. Datenbank wiederholt.|  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|**Datentyp und -länge**|**string**, unbegrenzte Länge.|  
|**Wert**|Gibt den Text der Fehlermeldung zurück.|  
|**Vorkommen**|Einmal pro gemeldeten Fehler.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Elemente|  
|------------------|--------------|  
|**Übergeordnetes Element**|[DiagnosticInformation-Element &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)|  
|**Untergeordnete Elemente**|Keine|  
  
## <a name="example"></a>Beispiel  
 Dieses Element meldet einen 1102-Fehler für eine Datenbank ohne Hauptschlüssel, wobei der Fehler bei der Analyse einer [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Konfiguration gefunden wurde.  
  
```  
<Issue type="Diagnosis" code="1102" server="TestComputer" database="TargetDB" object="TargetDB">The master key was not found</diagnostic>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ssbdiagnose-Hilfsprogramm &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  
