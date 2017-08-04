---
title: OData-Quelleneigenschaften | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4fde5bb0-6d78-4ec4-8f0b-67f91c53fe99
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b4f3283de9e26ce05849a34c8906a3095c229680
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="odata-source-properties"></a>OData-Quelleneigenschaften
  Wenn Sie im Datenfluss mit der rechten Maustaste auf **OData-Quelle** und anschließend auf **Eigenschaften**klicken, werden die Eigenschaften der Komponente **OData-Quelle** im Fenster **Eigenschaften** angezeigt.  
  
|||  
|-|-|  
|Eigenschaft|Description|  
|CollectionName|Der Name der Auflistung, die Sie vom OData-Dienst abrufen möchten. Die Eigenschaft **CollectionName** wird verwendet, wenn **UseResourcePath** FALSE ist.<br /><br /> Diese Eigenschaft ist ausdrucksfähig, d. h., der Wert kann zur Laufzeit festgelegt werden. Wenn die Metadaten der Auflistung jedoch nicht mit den Metadaten übereinstimmen, die zur Entwurfszeit verwendet wurden, tritt ein Überprüfungsfehler auf, der zum Abbruch der Datenflussausführung führt.|  
|DefaultStringLength|Dieser Wert gibt die Standardlänge für Zeichenfolgenspalten an, die keine maximale Länge aufweisen.<br /><br /> **Standardwert:** 4000|  
|Abfrage|Die OData-Abfrageparameter. Diese Eigenschaft ist ausdrucksfähig und kann zur Laufzeit festgelegt werden.|  
|ResourcePath|Verwenden Sie diese Eigenschaft, wenn Sie einen vollständigen Ressourcenpfad angeben müssen, anstatt nur einen Auflistungsnamen auszuwählen. Diese Eigenschaft wird verwendet, wenn **UseResourcePath** TRUE ist.|  
|UseResourcePath|Beim Wert TRUE wird der **ResourcePath** -Wert an die Basis-URL angefügt, um den Speicherort des OData-Feeds zu bestimmen. Bei FALSE wird der **CollectionName** -Wert verwendet.<br /><br /> **Standardwert:** False|  
  
  
