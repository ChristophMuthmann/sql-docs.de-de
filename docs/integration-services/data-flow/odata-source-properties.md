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
ms.sourcegitcommit: ee79d0f1b31963b7d13aa07bf4603246139c3a7c
ms.openlocfilehash: 64e297a37c3b6449551968b5788f8c2c0ddd4ab6
ms.contentlocale: de-de
ms.lasthandoff: 08/23/2017

---
# <a name="odata-source-properties"></a>OData-Quelleneigenschaften
Wenn Sie mit der rechten Maustaste **OData-Quelle** im Datenfluss und auf **Eigenschaften**, Sie finden Sie unter Eigenschaften für die **OData-Quelle** -Komponente in den **Eigenschaften** Fenster.  

## <a name="properties"></a>Eigenschaften 
|Eigenschaft|Description|  
|-|-|  
|CollectionName|Der Name der Auflistung, um vom OData-Dienst abrufen. Die Eigenschaft **CollectionName** wird verwendet, wenn **UseResourcePath** FALSE ist.<br /><br /> Diese Eigenschaft ist Expressionable, die Sie den Wert zur Laufzeit festlegen kann. Jedoch, wenn die Metadaten der Auflistung nicht den Metadaten, der zur Entwurfszeit vorhanden waren übereinstimmen, tritt ein Validierungsfehler, datenflussausführung fehlschlägt.|  
|DefaultStringLength|Dieser Wert gibt die Standardlänge für Zeichenfolgenspalten an, die keine maximale Länge aufweisen.<br /><br /> **Standardwert:** 4000|  
|Abfrage|Die OData-Abfrageparameter. Diese Eigenschaft ist Expressionable und kann zur Laufzeit festgelegt werden.|  
|ResourcePath|Verwenden Sie diese Eigenschaft, wenn Sie einen vollständigen Ressourcenpfad angeben müssen, anstatt nur einen Auflistungsnamen auszuwählen. Diese Eigenschaft wird verwendet, wenn **UseResourcePath** TRUE ist.|  
|UseResourcePath|Beim Wert TRUE wird der **ResourcePath** -Wert an die Basis-URL angefügt, um den Speicherort des OData-Feeds zu bestimmen. Bei FALSE wird der **CollectionName** -Wert verwendet.<br /><br /> **Standardwert:** False|  
  
## <a name="see-also"></a>Siehe auch
[OData-Quelle](odata-source.md)

