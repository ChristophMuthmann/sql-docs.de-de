---
title: Find-Methode (ADO) | Microsoft Docs
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
- Recordset15::raw_Find
- Recordset15::Find
helpviewer_keywords:
- Find method [ADO]
ms.assetid: 55c9810a-d8ca-46c2-a9dc-80e7ee7aa188
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9ee7c7feb630040fce10311335f414213bba4ada
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="find-method-ado"></a>Find-Methode (ADO)
Sucht eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) für die Zeile, die die angegebenen Kriterien erfüllt. Optional kann die Richtung der Suche, Startzeile und Offset von der Startzeile angegeben werden. Wenn die Kriterien erfüllt sind, wird die aktuelle Zeilenposition bei dem gefundenen Datensatz festgelegt. Andernfalls wird die Position festgelegt, Ende (oder Start) von der **Recordset**.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Find (Criteria, SkipRows, SearchDirection, Start)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Kriterien*  
 Ein **Zeichenfolge** Wert, der eine Anweisung zu verwendenden Spaltennamen, Vergleichsoperator und-Wert angeben, in die Suche enthält.  
  
 *SkipRows*  
 Optionale*.* Ein **lange** Wert, dessen Standardwert ist 0 (null), der angibt, das Zeilenoffset wurde aus der aktuellen Zeile oder *starten* Lesezeichen, um die Suche zu starten. Standardmäßig wird die Suche für die aktuelle Zeile gestartet.  
  
 *SearchDirection*  
 Optionale*.* Ein [SearchDirectionEnum](../../../ado/reference/ado-api/searchdirectionenum.md) Wert, der angibt, ob die Suche auf der aktuellen Zeile oder die nächste verfügbare Zeile in die Richtung der Suche beginnen soll. Eine Suche nicht erfolgreiche beendet wird, am Ende der **Recordset** ist der Wert **AdSearchForward**. Eine Suche nicht erfolgreiche beendet wird, am Anfang der **Recordset** ist der Wert **AdSearchBackward**.  
  
 *Starten*  
 Optional. Ein **Variant** Lesezeichen, das als die Startposition für die Suche funktioniert.  
  
## <a name="remarks"></a>Hinweise  
 Kann nur ein einzelner Spaltennamen angegeben werden, *Kriterien*. Diese Methode unterstützt keine Suche nach mehreren Spalten.  
  
 Der Vergleichsoperator im *Kriterien* möglicherweise "**>**"(größer als),"**\<**" (kleiner als), "=" (gleich), "> =" (größer als oder gleich) "< =" (kleiner oder gleich), "<>" (ungleich) oder "like" (Mustervergleich).  
  
 Der Wert in *Kriterien* kann eine Zeichenfolge, eine Gleitkommazahl oder ein Datum sein. Zeichenfolgenwerte werden in einfache Anführungszeichen oder "#" (Nummernzeichen) gesetzt (z. B. "State ="WA"" oder "Status = #WA #"). Datumswerte in ein "#" (Nummernzeichen) als Trennzeichen (z. B. "Start_date > #7/22/&#97;"). Diese Werte enthalten können, Stunden, Minuten und Sekunden Zeitstempel an, jedoch dürfen nicht für Millisekunden oder Fehlermeldungen angezeigt.  
  
 Wenn der Vergleichsoperator "wie" ist, kann der Zeichenfolgenwert ein Sternchen (*), um ein oder mehr Vorkommen eines beliebigen Zeichens oder einer Teilzeichenfolge gefunden enthalten. Z. B. "Zustand wie bin\*" "Maine und Massachusetts. Führende und nachfolgende Sternchen können auch um eine Teilzeichenfolge innerhalb der Werte zu suchen. Z. B. "State wie"\*als\*"" Alaska, Arkansas und Massachusetts übereinstimmt.  
  
 Sternchen können nur am Ende einer Zeichenfolge der Suchkriterien oder am Anfang und Ende einer Kriterienzeichenfolge verwendet werden, wie oben gezeigt. Sie können nicht mithilfe des Sternchens als führenden Platzhalter ("* str'), oder als eine eingebettete Platzhalter ('s\*R"). Dies verursacht einen Fehler.  
  
> [!NOTE]
>  Wenn eine aktuelle Zeilenposition vor dem Aufrufen nicht festgelegt ist, wird eine Fehlermeldung angezeigt **suchen**. Jede Methode, die Position der Zeile, z. B. legt [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), sollte aufgerufen werden, bevor **suchen**.  
  
> [!NOTE]
>  Beim Aufrufen der **suchen** Methode in einem Recordset, und die aktuelle Position im Recordset auf dem letzten Datensatz oder das Ende der Datei (EOF) ist, wird dort nicht alles. Aufrufen, müssen Sie die **MoveFirst** Methode, um die aktuelle Position/Cursor auf den Anfang des Recordsets einzurichten.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Find Methodenbeispiel (VB)](../../../ado/reference/ado-api/find-method-example-vb.md)   
 [Index-Eigenschaft](../../../ado/reference/ado-api/index-property.md)   
 [Optimieren Sie die Eigenschaft dynamisch (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [Seek-Methode](../../../ado/reference/ado-api/seek-method.md)
