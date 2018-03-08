---
title: "Erstellen der Tabelle Anweisung Einschränkungen | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CREATE TABLE statement limitations [ODBC]
- ODBC SQL grammar, CREATE TABLE statement limitations
ms.assetid: c5067855-20c9-456f-8d63-f375b4297f2e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0d8f73082a87978bf735e2e44f97987ba34ffbb5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="create-table-statement-limitations"></a>Erstellen von Einschränkungen für Tabelle-Anweisung
Wenn der Microsoft Access, Microsoft Excel oder Paradoxdriver verwendet wird, und die Länge einer Spalte Text- oder Binärformat nicht angegeben ist (oder als 0 angegeben ist), wird die Länge der Spalte auf 255 festgelegt.  
  
 Wenn der Treiber dBASE verwendet wird, und die Länge einer Spalte Text- oder Binärformat nicht angegeben ist (oder als 0 angegeben ist), werden die Spaltenlänge und 254 festgelegt.  
  
 Maximal 255 Spalten wird unterstützt.  
  
 Wenn der Microsoft Excel-Treiber verwendet wird, auf einer 97 Datenquelle, einem Arbeitsblatt oder keine Microsoft Excel 5.0, 7.0, kann nicht mit dem gleichen Namen wie einem Arbeitsblatt erstellt werden, die zuvor gelöscht wurde. Der Microsoft Excel-Treiber verwendet wird, auf einem Arbeitsblatt, Version 5.0, 7.0 oder 97 zuzugreifen, DROP TABLE-Anweisung löscht das Arbeitsblatt, aber löscht nicht den Arbeitsblattnamen.  
  
 Wenn Paradox-Treiber verwendet wird, können keine Spalten hinzugefügt werden, nachdem ein Index für eine Tabelle definiert wurde. Wenn die erste Spalte der Argumentliste einer CREATE TABLE-Anweisung ein Index erstellt wird, kann keine zweite Spalte in der Argumentliste enthalten.
