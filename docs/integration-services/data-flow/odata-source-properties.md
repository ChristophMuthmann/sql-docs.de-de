---
title: OData-Quelleneigenschaften | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4fde5bb0-6d78-4ec4-8f0b-67f91c53fe99
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4abbcdc6e39836bdabd3737f1bd8872df47d4f52
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="odata-source-properties"></a>OData-Quelleneigenschaften
Wenn Sie im Datenfluss mit der rechten Maustaste auf **OData-Quelle** und anschließend auf **Eigenschaften**klicken, werden die Eigenschaften der Komponente **OData-Quelle** im Fenster **Eigenschaften** angezeigt.  

## <a name="properties"></a>Eigenschaften 
|Eigenschaft|Description|  
|-|-|  
|CollectionName|Der Name der Auflistung, die Sie vom OData-Dienst abrufen. Die Eigenschaft **CollectionName** wird verwendet, wenn **UseResourcePath** FALSE ist.<br /><br /> Diese Eigenschaft ist ausdrucksfähig, sodass Sie den Wert zur Laufzeit festlegen können. Wenn die Metadaten der Auflistung jedoch nicht mit den Metadaten übereinstimmen, die zur Entwurfszeit verwendet wurden, tritt ein Überprüfungsfehler auf, der zum Abbruch der Datenflussausführung führt.|  
|DefaultStringLength|Dieser Wert gibt die Standardlänge für Zeichenfolgenspalten an, die keine maximale Länge aufweisen.<br /><br /> **Standardwert:** 4000|  
|Dataseteigenschaften|Die OData-Abfrageparameter. Diese Eigenschaft ist ausdrucksfähig und kann zur Laufzeit festgelegt werden.|  
|ResourcePath|Verwenden Sie diese Eigenschaft, wenn Sie einen vollständigen Ressourcenpfad angeben müssen, anstatt nur einen Auflistungsnamen auszuwählen. Diese Eigenschaft wird verwendet, wenn **UseResourcePath** TRUE ist.|  
|UseResourcePath|Beim Wert TRUE wird der **ResourcePath** -Wert an die Basis-URL angefügt, um den Speicherort des OData-Feeds zu bestimmen. Bei FALSE wird der **CollectionName** -Wert verwendet.<br /><br /> **Standardwert:** False|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter
[OData-Quelle](odata-source.md)
