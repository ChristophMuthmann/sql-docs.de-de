---
title: Entwerfen gespeicherter Prozeduren | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- stored procedures [Analysis Services], designing
- dependent assemblies [Analysis Services]
- assemblies [Analysis Services]
ms.assetid: af4e7bd5-041b-4a40-9942-0ef6a3af46c6
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e768747452fbdae3d4e839c48bd52954528b6559
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="designing-stored-procedures"></a>Entwerfen von gespeicherten Prozeduren
  In gespeicherten Prozeduren ist sowohl das administrative Objektmodell "Analysis Management Objects" (AMO) als auch das clientorientierte Objektmodell "[!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX® Data Objects (Multidimensional)" (ADO MD) verfügbar.  
  
 Gespeicherte Prozeduren müssen sich in ihrem Gültigkeitsbereich (entweder der Server oder die Datenbank) befinden, um auf der aufzurufenden MDX-Ebene (Multidimensional Expressions) sichtbar zu sein. Nachdem eine gespeicherte Prozedur aufgerufen wurde, ist ihr Gültigkeitsbereich jedoch nicht auf Aktionen unter dem übergeordneten Element begrenzt. Eine gespeicherte Prozedur kann überall auf dem Server Änderungen vornehmen. Dabei müssen lediglich die Sicherheitseinschränkungen des Benutzerprozesses, der sie aufruft, oder die Einschränkungen der Transaktion beachtet werden, in der sie ausgeführt wird.  
  
 Serverbereichsprozeduren sind in allen Kontexten auf dem Server verfügbar. Gespeicherte Datenbankbereichsprozeduren sind nur im Datenbankkontext der Datenbank sichtbar, in der sie definiert sind.  
  
 Wie jede andere MDX-Funktion muss eine gespeicherte Prozedur aufgelöst werden, bevor eine MDX-Sitzung fortgesetzt werden kann. Während ihrer Ausführung sperren gespeicherte Prozeduren MDX-Sitzungen. Sofern nicht spezielle Gründe für das Anhalten einer MDX-Sitzung bei wartenden Benutzerinteraktionen vorliegen, wird von Benutzerinteraktionen (z. B. Dialogfeldern) abgeraten.  
  
## <a name="dependent-assemblies"></a>Abhängige Assemblys  
 Alle abhängigen Assemblys müssen in eine Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] geladen werden, um von der Common Language Runtime (CLR) gefunden zu werden. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] speichert die abhängigen Assemblys im gleichen Ordner wie die Hauptassembly, damit alle Verweise auf Funktionen in den Assemblys von der CLR automatisch aufgelöst werden können.  
  
## <a name="see-also"></a>Siehe auch  
 [Mehrdimensionales Modell Assemblys-Verwaltung](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definieren gespeicherter Prozeduren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
