---
title: Verwenden von DRILLTHROUGH zum Abrufen von Quelldaten (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: af0ab4491a2ba57521e77723480a8e18850f56ee
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-manipulation---retrieve-source-data-using-drillthrough"></a>MDX - Datenbearbeitung: Abrufen von Quelldaten verwenden von DRILLTHROUGH
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Die [DRILLTHROUGH](../../../mdx/mdx-data-manipulation-drillthrough.md)-Anweisung wird in MDX (Multidimensional Expressions) dazu verwendet, ein Rowset aus den Quelldaten für eine Cubezelle abzurufen.  
  
 Damit eine **DRILLTHROUGH** -Anweisung für einen Cube ausgeführt werden kann, muss für diesen Cube eine Drillthroughaktion definiert sein. Um eine Drillthroughaktion zu definieren, klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]im Cube-Designer im **Aktionsbereich** auf der Symbolleiste auf **Neue Drillthroughaktion**. In der neuen Drillthroughaktion geben Sie den Aktionsnamen, das Ziel, die Bedingung und die Spalten an, die von der **DRILLTHROUGH** -Anweisung zurückgegeben werden sollen.  
  
## <a name="drillthrough-statement-syntax"></a>Syntax der DRILLTHROUGH-Anweisung  
 Die **DRILLTHROUGH** -Anweisung hat folgende Syntax:  
  
```  
<drillthrough> ::= DRILLTHROUGH [<Max_Rows>] [<First_Rowset>] <MDX select> [<Return_Columns>]  
   < Max_Rows> ::= MAXROWS <positive number>  
   <First_Rowset> ::= FIRSTROWSET <positive number>  
   <Return_Columns> ::= RETURN <member or attribute> [, <member or attribute>]  
```  
  
 Die **SELECT** -Klausel kennzeichnet die Cubezelle, die die Quelldaten enthält, die abgerufen werden sollen. Diese **SELECT** -Klausel ist mit einer normalen MDX- **SELECT** -Anweisung identisch, mit dem einen Unterschied, dass in der **SELECT** -Klausel nur ein Element auf jeder Achse angegeben werden kann. Wenn mehr als ein Element auf einer Achse angegeben wird, tritt ein Fehler auf.  
  
 Die `<Max_Rows>` -Syntax gibt die maximale Anzahl der Zeilen in jedem zurückgegebenen Rowset an. Wenn der OLE DB-Anbieter, der für die Verbindung mit der Datenquelle verwendet wird, **DBPROP_MAXROWS**nicht unterstützt, wird die `<Max_Rows>` -Einstellung ignoriert.  
  
 Die `<First_Rowset>` -Syntax identifiziert die Partition, deren Rowset zuerst zurückgegeben wird.  
  
 Die `<Return_Columns>` -Syntax identifiziert die zugrunde liegenden Datenbankspalten, die zurückgegeben werden sollen.  
  
## <a name="drillthrough-statement-example"></a>Beispiel für die DRILLTHROUGH-Anweisung  
 Das folgende Beispiel zeigt die Verwendung der **DRILLTHROUGH** -Anweisung: In diesem Beispiel fragt die DRILLTHROUGH-Anweisung die Blätter der Dimensionen Store, Product und Time entlang der Stores-Dimension (die Slicerachse) ab und gibt dann die Department-Measuregruppe, die Abteilungs-ID (Department ID) und den Vornamen der/des Angestellten zurück.  
  
```  
DRILLTHROUGH  
Select {Leaves(Store), Leaves(Product), Leaves(Time),*} on 0  
From Stores  
RETURN [Department MeasureGroup].[Department Id], [Employee].[First Name]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Bearbeiten von Daten & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)  
  
  
