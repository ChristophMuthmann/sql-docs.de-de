---
title: "Übersicht über die Strukturierung Daten | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data shaping [ADO], overview
ms.assetid: 4cb5fd29-4e56-46ac-ae48-a6771c321c0c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f885a8585d3665efcc39bfe979b501d779c35c00
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="data-shaping-overview"></a>Daten strukturieren (Übersicht)
*Strukturieren von Daten* bedeutet hierarchische Beziehungen zwischen mindestens zwei logische Entitäten in einer Abfrage zu erstellen. Die Hierarchie sehen in über-/ unterordnungsbeziehungen zwischen einem Datensatz einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), und einen oder mehrere Datensätze (auch bekannt als Kapitel) eines anderen **Recordset**. In einer über-/ unterordnungsbeziehung, die das übergeordnete Element **Recordset** enthält das untergeordnete Element **Recordset**. Ein Beispiel für eine hierarchische Beziehung ist Customers und Orders. Für jeden Kunden in einer Datenbank können NULL oder mehr Aufträge vorhanden sein. Die hierarchische Beziehung kann rekursiv sein, was bedeutet, dass zwei Ebenen untergeordneten Datensätze in einen untergeordneten Datensatz geschachtelt werden können. Im Prinzip kann ein hierarchischer Datensatz Anzeigetiefe geschachtelt werden. In der Praxis ADO schränkt die Rekursion bis maximal 512 **Recordset**s.  
  
 In Allgemein Spalten von einer geformten **Recordset** kann Daten von einem Datenanbieter wie Microsoft® SQL Server, Verweise auf eine andere enthalten **Recordset**, Werte aus einer Berechnung in eine einzelne Zeile mit einem abgeleitet **Recordset**, oder Werte abgeleitet aus einem Vorgang für eine Spalte eine gesamte **Recordset**. Eine Spalte kann auch neu erstellt wurde und leer sein.  
  
 Beim Abrufen des Wert einer Spalte, die einen Verweis auf eine andere enthält **Recordset**, ADO gibt automatisch den tatsächlichen **Recordset** durch den Verweis dargestellt. Der Verweis auf eine **Recordset** ist tatsächlich ein Verweis auf eine Teilmenge der das untergeordnete Element wird aufgerufen, eine *Kapitel*. Ein einzelnes übergeordnetes Element kann mehr als ein untergeordnetes Element verweisen **Recordset**.  
  
 ADO-Unterstützung für das Strukturieren von Daten ermöglicht es Ihnen, Abfragen einer Datenquelle und Zurückgeben einer **Recordset** in der ein Datensatz (übergeordneten) stellt ein (untergeordnetes) **Recordset**. In der Customer-Order-Szenario können Sie Daten, die zum Abrufen von Informationen für Kunden sowie die von einzelnen Kunden in einer einzelnen Abfrage aufgegebenen Bestellungen strukturieren. Die resultierenden **Recordset** ist auch bekannt als geformten **Recordset**.  
  
 Darüber hinaus Daten in ADO strukturiert werden, können Sie zum Erstellen neuer **Recordset** Objekte ohne eine zugrunde liegende Datenquelle mithilfe der **neu** Schlüsselwort, um die Felder von der übergeordneten und untergeordneten beschreiben  **Recordsets**. Die neue **Recordset** Objekt kann anschließend mit Daten gefüllt und persistent gespeichert. Entwickler können auch verschiedene Berechnungen oder Aggregationen auszuführen (z. B. **Summe**, **AVG**, und **MAX**) für untergeordnete Felder. Strukturieren von Daten kann auch ein übergeordnetes Element erstellen **Recordset** von einem untergeordneten **Recordset** durch Gruppieren von Datensätzen in der untergeordneten und eine Zeile in das übergeordnete Element für jede Gruppe in das untergeordnete Element platzieren.  
  
 Reguläre SQL ermöglicht es Ihnen, Daten mithilfe von **JOIN** Syntax, aber dies kann ineffizient sein und unhandlich da redundante übergeordneten Daten in jedem Datensatz für einen angegebenen über-/ unterordnungsbeziehung zurückgegebenen wiederholt werden. Strukturieren von Daten kann einen einzelnen übergeordneten Datensatz im übergeordneten Element verknüpft **Recordset** mit mehreren untergeordneten Datensätzen in der untergeordneten **Recordset**, vermeiden die redundante eine **verknüpfen**. Die meisten Personen suchen, die über-/ mehrere **Recordset** Programmiermodell besser natürliche und einfacher zu verwenden als die einzelnen **Recordset JOIN** Modell.

