---
title: Entwerfen gespeicherter Prozeduren | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
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
ms.openlocfilehash: 4fa8e3b4bf7a5fcd7817a662a5e4c4d6b5db59cc
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="designing-stored-procedures"></a>Entwerfen von gespeicherten Prozeduren
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Sowohl das administrative Objektmodell Analysis Management Objects (AMO) und das clientorientierte Objektmodell [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX® Data Objects (Multidimensional) (ADO MD) stehen in gespeicherten Prozeduren.  
  
 Gespeicherte Prozeduren müssen sich in ihrem Gültigkeitsbereich (entweder der Server oder die Datenbank) befinden, um auf der aufzurufenden MDX-Ebene (Multidimensional Expressions) sichtbar zu sein. Nachdem eine gespeicherte Prozedur aufgerufen wurde, ist ihr Gültigkeitsbereich jedoch nicht auf Aktionen unter dem übergeordneten Element begrenzt. Eine gespeicherte Prozedur kann überall auf dem Server Änderungen vornehmen. Dabei müssen lediglich die Sicherheitseinschränkungen des Benutzerprozesses, der sie aufruft, oder die Einschränkungen der Transaktion beachtet werden, in der sie ausgeführt wird.  
  
 Serverbereichsprozeduren sind in allen Kontexten auf dem Server verfügbar. Gespeicherte Datenbankbereichsprozeduren sind nur im Datenbankkontext der Datenbank sichtbar, in der sie definiert sind.  
  
 Wie jede andere MDX-Funktion muss eine gespeicherte Prozedur aufgelöst werden, bevor eine MDX-Sitzung fortgesetzt werden kann. Während ihrer Ausführung sperren gespeicherte Prozeduren MDX-Sitzungen. Sofern nicht spezielle Gründe für das Anhalten einer MDX-Sitzung bei wartenden Benutzerinteraktionen vorliegen, wird von Benutzerinteraktionen (z. B. Dialogfeldern) abgeraten.  
  
## <a name="dependent-assemblies"></a>Abhängige Assemblys  
 Alle abhängigen Assemblys müssen in eine Instanz von [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] geladen werden, um von der Common Language Runtime (CLR) gefunden zu werden. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] speichert die abhängigen Assemblys im gleichen Ordner wie die Hauptassembly, damit alle Verweise auf Funktionen in den Assemblys von der CLR automatisch aufgelöst werden können.  
  
## <a name="see-also"></a>Siehe auch  
 [Mehrdimensionales Modell Assemblys-Verwaltung](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definieren gespeicherter Prozeduren](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
