---
title: "Ändern einer partitionsquelle Verwendung eine anderen Faktentabelle | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- fact tables [Analysis Services]
- partitions [Analysis Services], fact tables
ms.assetid: 5508312f-8e46-4802-9362-6688ca03d098
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ded060a7f5451e7bf0907f40da78d9fb9e95b8dc
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/15/2018
---
# <a name="change-a-partition-source-to-use-a-different-fact-table"></a>Ändern einer Partitionsquelle für die Verwendung einer anderen Faktentabelle
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Bei der Erstellung von Partitionen können Sie für Cubes unterschiedliche Faktentabellen verwenden. Die unterschiedlichen Tabellen können dabei aus einer einzelnen Datenquellensicht, aus verschiedenen Datenquellensichten oder aus verschiedenen Datenquellen stammen. Eine Datenquellensicht kann auch unterschiedliche Tabellen aus mehreren Datenquellen enthalten.  
  
 Alle Faktentabellen und Dimensionen für die Partitionen eines Cubes müssen dieselbe Struktur wie die Faktentabelle und die Dimensionen des Cubes besitzen. Unterschiedliche Faktentabellen können z. B. dieselbe Struktur besitzen, aber Daten für verschiedene Jahre oder verschiedene Produktlinien enthalten.  
  
 Eine Faktentabelle geben Sie auf der Seite **Quellinformationen angeben** des Partitions-Assistenten an. Geben Sie auf dieser Seite im Gruppenfeld Partitionsquelle neben **Suchen in**an, in welcher Datenquelle bzw. Datenquellensicht gesucht werden soll. Klicken Sie als Nächstes auf **Tabellen suchen**, und wählen Sie dann unter **Verfügbare Tabellen**die zu verwendende Tabelle aus.  
  
 Wenn Sie unterschiedliche Faktentabellen verwenden, sollten Sie sicherstellen, dass in den Partitionen keine Daten doppelt auftreten. Wenn eine Faktentabelle z. B. Transaktionen nur für das Jahr 2012 und eine andere Faktentabelle Transaktionen nur für das Jahr 2013 enthält, weisen diese Tabellen unabhängige Daten auf. Ebenso sind Faktentabellen für verschiedene Produktlinien oder verschiedene geografische Gebiete unabhängig voneinander.  
  
 Es ist möglich, aber nicht empfehlenswert, dass Sie unterschiedliche Faktentabellen verwenden, die doppelte Daten enthalten. In diesem Fall müssen Sie Filter in den Partitionen verwenden, um sicherzustellen, dass die von einer Partition verwendeten Daten nicht von einer anderen Partition verwendet werden. Weitere Informationen finden Sie unter [Create and Manage a Local Partition &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen Sie und verwalten Sie einer lokalen Partition &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)  
  
  
