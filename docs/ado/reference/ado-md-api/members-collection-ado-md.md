---
title: Members-Auflistung (ADO MD) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Level::Members
- Members
- Position::Members
helpviewer_keywords:
- Members collection [ADO MD]
ms.assetid: 3a647cde-efdc-4394-b1b9-8cbb1b9d689f
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d72b7b87507e13ae4aa103a6333e7e2caaf581ae
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="members-collection-ado-md"></a>Members-Auflistung (ADO MD)
Enthält die [Member](../../../ado/reference/ado-md-api/member-object-ado-md.md) Objekte aus einer Ebene oder einer Position auf einer Achse.  
  
## <a name="remarks"></a>Hinweise  
 Ein **Elemente** Auflistung wird verwendet, um die folgenden Elemente enthalten:  
  
-   Die Elemente, aus denen eine Ebene in einem Cube besteht. Diese sind in enthalten die **Elemente** Auflistung von einer [Ebene](../../../ado/reference/ado-md-api/level-object-ado-md.md) Objekt. Beispiel für die Verwendung aus des Beispiels [Übersicht über multidimensionale Schemas und Daten](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md), sind die vier Elemente der Ebene Ländern, Kanada, USA, Großbritannien und Deutschland.  
  
-   Die Elemente, die die untergeordneten Elemente eines bestimmten Elements in einer Hierarchie sind. Diese Elemente werden zurückgegeben, durch die [Kinder](../../../ado/reference/ado-md-api/children-property-ado-md.md) Eigenschaft des übergeordneten Elements **Member** Objekt. Beispielsweise sind die erneut mit demselben Beispiel, die zwei untergeordneten Elemente des dem Kanada-Element Kanada-Ostküste und Canada-Westküste.  
  
-   Die Elemente, die eine bestimmte Position entlang der Achse definieren eine [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md). Mittels Cellset aus [arbeiten mit mehrdimensionalen Daten](../../../ado/guide/multidimensional/working-with-multidimensional-data.md) beispielsweise sind die beiden Elemente der ersten Position auf der x-Achse Mein Schatz und Seattle. Diese Elemente enthalten sind die **Elemente** Auflistung von einem [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md) Objekt.  
  
 **Mitglieder** ist eine standard-ADO-Auflistung. Mit den Eigenschaften und Methoden einer Auflistung können Sie Folgendes tun:  
  
-   Abrufen der Anzahl von Objekten in der Auflistung mit den [Anzahl](../../../ado/reference/ado-api/count-property-ado.md) Eigenschaft.  
  
-   Ein Objekt aus der Auflistung hat den Standardwert zurückgeben [Element](../../../ado/reference/ado-api/item-property-ado.md) Eigenschaft.  
  
-   Aktualisieren Sie die Objekte in der Auflistung über den Anbieter mit der [aktualisieren](../../../ado/reference/ado-api/refresh-method-ado.md) Methode.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Eigenschaften, Methoden und Ereignisse](../../../ado/reference/ado-md-api/members-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Member-Beispiel (VBScript)](../../../ado/reference/ado-md-api/members-example-vbscript.md)   
 [Member-Objekt (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)
