---
title: Mithilfe von Seiten | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- PageSize property [ADO]
- pages [ADO]
- Recordset object [ADO]
- AbsolutePage property [ADO]
- PageCount property [ADO]
ms.assetid: 442b08c5-ccc7-4192-a1cc-22f250867782
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4e6b067e98d45fb515b8a4334d1a14936c0d0504
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="using-pages"></a>Mithilfe von Seiten
Verwenden der **"PageCount"** -Eigenschaft können Sie bestimmen, wie viele Seiten der Daten werden die **Recordset** Objekt. *Seiten* sind Gruppen von Datensätzen, dessen Größe gleich, der **PageSize** Einstellung der Eigenschaft. Auch wenn die letzte Seite unvollständig ist, da weniger als Datensätze die **PageSize** Wert, zählt als eine zusätzliche Seite in der **"PageCount"** Wert. Wenn die **Recordset** Objekt unterstützt diese Eigenschaft nicht **"PageCount"** beträgt-1, um anzugeben, dass die **"PageCount"** Maskierungsstufe ist.  
  
 Verwenden der **PageSize** -Eigenschaft können Sie bestimmen, wie viele Datensätze eine logische Seite der Daten bilden. Einrichten einer Seitengröße können Sie mit der **AbsolutePage** Eigenschaft auf den ersten Eintrag in einer bestimmten Seite verschoben. Dies ist nützlich in Szenarien, Webserver, soll, wenn der Benutzer seitenweise durch Daten, kann eine bestimmte Anzahl von Datensätzen zu einem Zeitpunkt anzuzeigen.  
  
 Diese Eigenschaft kann zu einem beliebigen Zeitpunkt festgelegt werden, und sein Wert wird zum Berechnen der Position des ersten Datensatzes, der eine bestimmte Seite verwendet werden.  
  
 Verwenden der **AbsolutePage** Eigenschaft, um die Seitenzahl zu identifizieren, auf dem der aktuelle Datensatz gespeichert ist. Der Anbieter muss erneut, die entsprechende Funktionalität für diese Eigenschaft verfügbar sein unterstützen.  
  
 **AbsolutePage** ist 1-basiert und entspricht 1, wenn der aktuelle Datensatz der erste Datensatz im ist die **Recordset**. Legen Sie diese Eigenschaft auf den ersten Eintrag in einer bestimmten Seite verschoben. Abrufen der Gesamtanzahl von Seiten aus der **"PageCount"** Eigenschaft.
