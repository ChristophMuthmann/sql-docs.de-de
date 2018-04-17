---
title: NULL-Zulässigkeit und Vergleiche mit Dreiwertiger Logik | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- precision [CLR integration]
- overflow detections [CLR integration]
- null values [CLR integration]
- three-value logic comparisons [CLR integration]
- data types [CLR integration]
- SqlBoolean data type
ms.assetid: 13da4c7f-1010-4b2d-a63c-c69b6bfd96f1
caps.latest.revision: 38
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f2765043127179ee7578cd4258e909351198e727
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="nullability-and-three-value-logic-comparisons"></a>Zulässigkeit von NULL-Werten und Vergleiche mit dreiwertiger Logik
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Wenn Sie kennen die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentypen finden Sie ähnliche Semantik und Genauigkeit in die **System.Data.SqlTypes** Namespace in der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Es gibt jedoch einige Unterschiede, und die wichtigsten dieser Unterschiede werden in diesem Thema behandelt.  
  
## <a name="null-values"></a>NULL-Werte  
 Ein Hauptunterschied zwischen den systemeigenen CLR (Common Language Runtime)-Datentypen und den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datentypen besteht darin, dass Erstere keine NULL-Werte zulassen, Letztere dagegen die uneingeschränkte NULL-Semantik bereitstellen.  
  
 Vergleiche werden durch NULL-Werte beeinflusst. Wenn die beiden Werte x und y verglichen werden und x oder y NULL ist, dann ergeben einige logische Vergleiche den Wert UNKNOWN statt true oder false.  
  
## <a name="sqlboolean-data-type"></a>SqlBoolean-Datentyp  
 Zur Darstellung dieser dreiwertigen Logik wurde im **System.Data.SqlTypes** -Namespace der **SqlBoolean** -Typ eingeführt. Vergleiche zwischen beliebigen Werten des Typs **SqlTypes** ergeben einen Wert des **SqlBoolean** -Typs. Der UNKNOWN-Wert wird durch den NULL-Wert des **SqlBoolean** -Typs dargestellt. Die Eigenschaften **IsTrue**, **IsFalse**und **IsNull** dienen zur Überprüfung des Werts eines **SqlBoolean** -Typs.  
  
## <a name="operations-functions-and-null-values"></a>Vorgänge, Funktionen und NULL-Werte  
 Alle arithmetischen Operatoren (+, -, \*, /, %), bitweisen Operatoren (~, & und |), und die meisten Funktionen NULL zurück, wenn einer der Operanden oder Argumente des **SqlTypes** NULL sind. Die **IsNull** -Eigenschaft gibt stets den Wert true oder false zurück.  
  
## <a name="precision"></a>Genauigkeit  
 Für Dezimaldatentypen in der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -CLR gelten andere Maximalwerte als für die numerischen Datentypen und Dezimaldatentypen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Außerdem wird bei den Dezimaldatentypen der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -CLR die maximale Genauigkeit angenommen. In der CLR für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], allerdings **SqlDecimal** bietet die gleiche maximale Genauigkeit und Dezimalstellenanzahl sowie die gleiche Semantik wie die decimal-Datentyp in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="overflow-detection"></a>Überlauferkennung  
 In der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -CLR wird durch die Addition von zwei sehr großen Zahlen möglicherweise keine Ausnahme ausgelöst. Wenn kein Prüfvorgang verwendet wurde, dann wird das zurückgegebene Ergebnis möglicherweise als negative Ganzzahl dargestellt. In **System.Data.SqlTypes**werden Ausnahmen für alle Überlauf- und Unterlauffehler sowie Fehler aufgrund einer Division durch 0 ausgelöst.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Datentypen in .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
