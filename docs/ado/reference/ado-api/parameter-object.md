---
title: Parameterobjekt | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Parameter
helpviewer_keywords:
- Parameter object [ADO]
ms.assetid: e010e794-7f0f-4026-8b5b-37328e437d63
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ec8556b03b2f0d3a3d7d439ae223385860040c63
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="parameter-object"></a>Parameter-Objekt
Stellt einen Parameter oder das zugeordnete Argument eine [Befehl](../../../ado/reference/ado-api/command-object-ado.md) -Objekt auf Grundlage einer parametrisierten Abfrage oder gespeicherte Prozedur.  
  
## <a name="remarks"></a>Hinweise  
 Viele Anbieter unterstützen parametrisierte Befehle. Hierbei handelt es sich um Befehle, die in denen die gewünschte Aktion einmal definiert ist, aber Variablen (oder der Typparameter) werden verwendet, um einige Details des Befehls alter. Beispielsweise könnte eine SQL SELECT-Anweisung mithilfe eines Parameters definieren Sie die Übereinstimmungskriterien für eine WHERE-Klausel und eine andere, um den Spaltennamen für eine SORT BY-Klausel definieren.  
  
 **Parameter** Objekte darstellen, Parameter, die parametrisierte Abfragen zugeordnet sind, oder in/Out-Argumente und Rückgabewerte der gespeicherten Prozeduren. Abhängig von den Funktionen der Anbieter, einige Auflistungen, Methoden oder Eigenschaften eine **Parameter** Objekt möglicherweise nicht zur Verfügung.  
  
 Mit den Auflistungen, Methoden und Eigenschaften von einer **Parameter** -Objekts können Sie folgende Möglichkeiten:  
  
-   Festlegen oder Zurückgeben der Name eines Parameters mit der [Namen](../../../ado/reference/ado-api/name-property-ado.md) Eigenschaft.  
  
-   Festlegen oder Zurückgeben der Wert eines Parameters mit der [Wert](../../../ado/reference/ado-api/value-property-ado.md) Eigenschaft. **Wert** ist die Standardeigenschaft eines der **Parameter** Objekt.  
  
-   Festlegen oder Zurückgeben von Parametereigenschaften mit der [Attribute](../../../ado/reference/ado-api/attributes-property-ado.md), [Richtung](../../../ado/reference/ado-api/direction-property.md), [Genauigkeit](../../../ado/reference/ado-api/precision-property-ado.md), [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md), [ Größe](../../../ado/reference/ado-api/size-property-ado-parameter.md), und [Typ](../../../ado/reference/ado-api/type-property-ado.md) Eigenschaften.  
  
-   Übergeben von langen Binär-oder Zeichendatentypen an einen Typparameter mit der [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) Methode.  
  
-   Zugreifen auf anbieterspezifische Attribute mithilfe der [Eigenschaften](../../../ado/reference/ado-api/properties-collection-ado.md) Auflistung.  
  
 Wenn Sie wissen, dass die Namen und zugeordnete Eigenschaften der Parameter der gespeicherten Prozedur oder eine parametrisierte Abfrage, die Sie aufrufen möchten, können Sie die [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) Methode zum Erstellen der **Parameter** Objekte mit dem entsprechenden eigenschafteneinstellungen und Verwenden der [Anfügen](../../../ado/reference/ado-api/append-method-ado.md) Methode sie zum Hinzufügen der [Parameter](../../../ado/reference/ado-api/parameters-collection-ado.md) Auflistung. Auf diese Weise können Sie festlegen und Zurückgeben von Parameterwerten ohne Aufruf der [aktualisieren](../../../ado/reference/ado-api/refresh-method-ado.md) Methode für die **Parameter** Auflistung abzurufenden die Parameterinformationen vom Anbieter, eine potenziell ressourcenintensiver Vorgang.  
  
 Die **Parameter** Objekt ist nicht sicher für Skripting.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [Parameter-Objekteigenschaften, Methoden und Ereignisse](../../../ado/reference/ado-api/parameter-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Command-Objekt (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [CreateParameter-Methode (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Parameters-Auflistung (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Properties-Collection (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
