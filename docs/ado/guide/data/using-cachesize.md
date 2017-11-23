---
title: CacheSize mit | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- locks [ADO], CacheSize property
- CacheSize property [ADO]
ms.assetid: ca1c3422-b6a4-4ba6-af55-54f975b698b1
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 72ef02bfcf8e5392d23cd90f0ad0d49fe4d87122
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="using-cachesize"></a>Verwenden von CacheSize
Verwenden der **CacheSize** Eigenschaft steuern, wie viele Datensätze gleichzeitig in den lokalen Arbeitsspeicher vom Anbieter abzurufen. Z. B. wenn die **CacheSize** ist 10, nach dem ersten Öffnen der **Recordset** -Objekt, der Anbieter Ruft die ersten 10 Datensätze in den lokalen Speicher ab. Beim Navigieren durch die **Recordset** Objekt, gibt der Anbieter die Daten aus dem lokalen Speicherpuffer zurück. Sobald Sie hinter dem letzten Datensatz in den Cache verschieben, ruft die nächsten 10 Datensätze aus der Datenquelle mit der Anbieter in den Cache ab.  
  
> [!NOTE]
>  **CacheSize** basiert auf der **maximale Anzahl geöffneter Zeilen** -anbieterspezifische Datenquelleneigenschaft (in der **Eigenschaften** Auflistung von der **Recordset** Objekt). Sie können nicht festgelegt **CacheSize** auf einen Wert größer als **maximale Anzahl geöffneter Zeilen.** Legen Sie zum Ändern der Anzahl der Zeilen, die vom Anbieter geöffnet werden können, **maximale Anzahl geöffneter Zeilen**.  
  
 Der Wert der **CacheSize** angepasst werden kann, während der Lebensdauer der **Recordset** Objekt, aber durch Ändern dieses Werts wirkt sich nur auf die Anzahl der Datensätze im Cache nach nachfolgendem Abrufen aus der Datenquelle. Ändern den Wert der Eigenschaft allein ändert sich nicht auf den aktuellen Inhalt des Caches aus.  
  
 Wenn weniger Datensätze als abrufen **CacheSize** gibt, gibt der Anbieter die übrigen Datensätze zurück, und kein Fehler auftritt.  
  
 Ein **CacheSize** Einstellung von 0 (null) ist nicht zulässig, und gibt einen Fehler zurück.  
  
 Datensätze, die aus dem Cache abgerufene spiegeln nicht gleichzeitige Änderungen, die anderen Benutzern an den Quelldaten vorgenommen. Um ein Update aller zwischengespeicherten Daten zu erzwingen, verwenden Sie die [Resync](../../../ado/reference/ado-api/resync-method.md) Methode.  
  
 Wenn **CacheSize** auf einen Wert größer als 1 ist, die Navigationsmethoden festgelegt ist ([verschieben](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst, MoveLast, MoveNext und MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) kann in der Navigation zu einer gelöschten führen Datensatz gelöscht, nachdem die Datensätze abgerufen wurden. Nach dem Abrufen werden nachfolgende Löschvorgänge nicht in Ihrem Datencache berücksichtigt werden, bis Sie versuchen, einen Datenwert aus einer gelöschten Zeile zugreifen. Allerdings festlegen **CacheSize** wird auf 1 dieses Problem beseitigt, da der gelöschte Zeilen nicht abgerufen werden können.
