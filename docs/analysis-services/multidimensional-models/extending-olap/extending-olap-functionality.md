---
title: "Erweitern von OLAP-Funktionalität | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 49a17ff3-94e9-4969-84fc-37d49e63933b
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c41d406152efc89e097398d89c9a149dd6a5eb93
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="extending-olap-functionality"></a>Erweiterte von OLAP-Funktionalität
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Als Programmierer können Sie Analysis Services erweitern, indem das Schreiben von Assemblys, personalisierte Erweiterungen und gespeicherten Prozeduren, die Funktionen bereitstellen, die Sie in mehreren datenbankanwendungen verwenden oder wiederverwenden möchten. Assemblys werden verwendet, um durch Hinzufügen von neuen Prozeduren und Funktionen zur MDX-Sprache oder mittels des Personalisierungs-Add-Ins die mehrdimensionale Modelle-Funktionalität zu erweitern.  
  
 Gespeicherte Prozeduren können verwendet werden, um externe Routinen aufzurufen, und vereinfachen so die Entwicklung und Implementierung von Analysis Services-Datenbanken, da gemeinsamer Code nur einmal entwickelt werden muss und an einem einzelnen Ort gespeichert werden kann. Mit gespeicherten Prozeduren kann Anwendungen Geschäftsfunktionalität hinzugefügt werden, die von der systemeigenen Funktionalität von MDX nicht bereitgestellt wird.  
  
 Personalisierungen sind benutzerdefinierte Objekte, die Sie einem Cube hinzufügen, um ein Verhalten bereitzustellen, das sich je nach Benutzer ändert. Personalisierungen sind keine permanenten Objekte im Cube, sondern Objekte, die von der Clientanwendung während der Sitzung des Benutzers dynamisch angewendet werden. Beispiele umfassen das Ändern der Währung von einem Währungswert abhängig von der Person, die auf die Daten zugreift, Bereitstellen von individualisierten KPIs oder eine gezielte Vorschlagsliste für Stammkunden, die online kaufen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Erweitern von OLAP durch Personalisierungen](../../../analysis-services/multidimensional-models/extending-olap/extending-olap-through-personalizations.md)  
  
 [Personalisierungserweiterungen für Analysis Services](../../../analysis-services/multidimensional-models/extending-olap/analysis-services-personalization-extensions.md)  
  
 [Definieren gespeicherter Prozeduren](../../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
