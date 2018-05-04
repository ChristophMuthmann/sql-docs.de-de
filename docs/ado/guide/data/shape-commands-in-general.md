---
title: Shape-Befehle im Allgemeinen | Microsoft Docs
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
- shape commands [ADO]
- data shaping [ADO], shape commands
ms.assetid: 1fac7831-a187-4b15-9b43-aad380c5556c
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6af36fbf7a3b60067c94f0d21aa6e7514df1a098
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="shape-commands-in-general"></a>Shape-Befehle im Allgemeinen
Datenstrukturierung definiert die Spalten von einer geformten **Recordset**, die Beziehungen zwischen den Entitäten dargestellt durch die Spalten und die Art und Weise, in dem die **Recordset** mit Daten aufgefüllt wird.  
  
 Eine geformten **Recordset** kann die folgenden Typen von Spalten bestehen.  
  
|Spaltentyp|Description|  
|-----------------|-----------------|  
|data|Felder aus einem **Recordset** durch einen Abfragebefehl zurückgegeben wird für einem Datenanbieter, Tabelle oder zuvor geformten **Recordset**.|  
|Kapitel|Ein Verweis auf eine andere **Recordset**Namens eine *Kapitel*. Kapitelspalten stellen das Definieren einer *über-/* Beziehung, in dem die *übergeordneten* ist die **Recordset** der Kapitelspalte sowie die enthält*untergeordneten* ist die **Recordset** durch das Kapitel dargestellt.|  
|Aggregat (aggregate)|Der Wert der Spalte wird abgeleitet, durch das Ausführen einer *Aggregatfunktion* für alle Zeilen oder eine Spalte aller Zeilen einer untergeordneten **Recordset**. (Im folgenden Thema finden Sie in Aggregatfunktionen [Aggregatfunktionen, die CALC-Funktion und das NEW-Schlüsselwort](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md).)|  
|berechneter Ausdruck|Der Wert der Spalte wird durch Berechnen eines Visual Basic für Applikationen-Ausdrucks auf Spalten in der gleichen Zeile abgeleitet der **Recordset**. Der Ausdruck ist das Argument für die CALC-Funktion. (Finden Sie unter berechneter Ausdruck im folgenden Thema [Aggregatfunktionen, die CALC-Funktion und das NEW-Schlüsselwort](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md) und [Visual Basic für Applikationen-Funktionen](../../../ado/guide/data/visual-basic-for-applications-functions.md).)|  
|new|Leere erstellte Felder, die zu einem späteren Zeitpunkt mit Daten aufgefüllt werden können. Die Spalte ist mit dem neuen Schlüsselwort definiert. (Siehe NEW-Schlüsselwort in das folgende Thema [Aggregatfunktionen, die CALC-Funktion und das NEW-Schlüsselwort](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md).)|  
  
 Shape-Befehl darf eine Klausel, die einen Abfragebefehl eines zugrunde liegenden Datenanbieters gibt an, der zurückgegeben wird ein **Recordset** Objekt. Die Abfrage die Syntax richtet sich nach den Anforderungen des zugrunde liegenden Datenanbieters. Dies wird in der Regel "SQL" oder ADO die Verwendung von bestimmte Abfragesprache nicht notwendig.  
  
 Form Befehle ausgeben können, indem Sie **Recordset** Objekte oder durch Festlegen der [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) Eigenschaft von der [Befehl](../../../ado/reference/ado-api/command-object-ado.md) Objekt und dem anschließenden Aufrufen der [ausführen ](../../../ado/reference/ado-api/execute-method-ado-command.md) Methode.  
  
 Eine SQL-JOIN-Klausel können Sie zwei Tabellen beziehen; allerdings eine hierarchische **Recordset** können die Informationen noch effizienter darstellen. Jede Zeile eine **Recordset** durch einen JOIN wiederholt Informationen Dokumentkopien aus einer der Tabellen erstellt. Eine hierarchische **Recordset** hat nur ein übergeordnetes Element **Recordset** für jede mit mehreren untergeordneten **Recordset** Objekte.  
  
 Shape-Befehle können geschachtelt werden. D. h. die *übergeordneten-Befehl* oder *untergeordnete Befehl* selbst ist möglicherweise ein anderes Shape-Befehl.  
  
 Shape-Anbieter immer einem Clientcursor wird zurückgibt, selbst wenn der Benutzer eine Cursorposition des angibt **AdUseServer**.  
  
 Sie erreichen die **Recordset** Bestandteile der geformten **Recordset** programmgesteuert oder über eine entsprechende visual-Steuerelement.  
  
 Microsoft bietet ein visuelles Tool, das Shape-Befehle generiert (finden Sie unter der [Daten Umgebung Designer](http://go.microsoft.com/fwlink/?LinkId=5689) in der Dokumentation zu Visual Basic 6) und ein anderes, das hierarchische Cursor angezeigt (siehe "mithilfe der Microsoft hierarchische Flex-Tabelle-Steuerelement"in der Dokumentation zu Visual Basic 6).  
  
 Informationen zum Navigieren in einer hierarchischen **Recordset**, finden Sie unter [zugreifen auf Zeilen in einem hierarchischen Recordset](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
 Genaue Informationen zu syntaktisch korrekte Form-Befehlen finden Sie unter [formale Grammatik für Formen](../../../ado/guide/data/formal-shape-grammar.md).  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Aggregatfunktionen, die CALC-Funktion und das NEW-Schlüsselwort](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)  
  
-   [Ausgeben von Befehlen an den zugrunde liegenden Datenanbieter](../../../ado/guide/data/issuing-commands-to-the-underlying-data-provider.md)
