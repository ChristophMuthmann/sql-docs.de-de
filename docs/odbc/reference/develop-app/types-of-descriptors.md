---
title: Typen von Deskriptoren | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], types
ms.assetid: ec20e446-e540-41ad-8559-d9c0a5b8358f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9a5d5caf63abd6b9800ee6e65b7f6c30de108703
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="types-of-descriptors"></a>Typen von Deskriptoren
Ein Deskriptor wird verwendet, um einen der folgenden beschreiben:  
  
-   Ein Satz von NULL oder mehr Parameter. Eine Parameterdeskriptor kann verwendet werden, um zu beschreiben:  
  
    -   Die *Anwendung Parameterpuffer* enthält entweder die Eingabeargumente dynamische als Satz von der Anwendung oder die dynamische Ausgabeargumente nach der Ausführung einer **Aufrufen** SQL-Anweisung.  
  
    -   Die *Implementierung Parameterpuffer*. Für dynamische Eingabeargumente enthält diese Spalte die gleichen Argumente wie die Anwendung Parameterpuffer nach der Datenkonvertierung, die die Anwendung angeben kann. Für dynamische Ausgabeargumente enthält diese Spalte zurückgegebene Argumente, bevor jede Datenkonvertierung, die die Anwendung angeben kann.  
  
     Für dynamische Eingabeargumente muss die Anwendung ausgeführt werden, auf einem anwendungsparameterdeskriptor vor der Ausführung einer SQL-Anweisung, die Marker dynamischer Parameter enthält. Für Eingabe- und dynamische Argumente kann die Anwendung unterschiedliche Datentypen aus Implementation Parameter Descriptor, um die Datenkonvertierung zu erreichen angeben.  
  
-   Eine einzelne Zeile von Datenbankdaten. Eine Zeilendeskriptor kann verwendet werden, um zu beschreiben:  
  
    -   Die *Implementierung Zeilenpuffer,* enthält die Zeile aus der Datenbank. (Diese Puffer konzeptionell Daten enthalten, geschrieben oder aus der Datenbank gelesen. Die gespeicherten Form von Datenbankdaten ist jedoch nicht angegeben. Eine Datenbank kann zusätzliche Konvertierung in die Daten aus der Form im Puffer Implementierung ausführen.)  
  
    -   Die *Anwendung Zeilenpuffer,* dargestellt, die an die Anwendung, die nach der Datenkonvertierung, die die Anwendung angeben, kann die Zeile der Daten enthält.  
  
     Die Anwendung arbeitet mit der Anwendung Zeilendeskriptor in jedem Fall, in dem Spaltendaten aus der Datenbank in Anwendungsvariablen angezeigt werden müssen. Um der Datenkonvertierung von Spaltendaten zu erreichen, kann die Anwendung unterschiedliche Datentypen von den in den Implementierungszeilendeskriptor angeben.  
  
 Der Deskriptor-Typen werden in der folgenden Tabelle zusammengefasst.  
  
|Puffertyp|Zeilen|Dynamische Parameter|  
|-----------------|----------|------------------------|  
|**Anwendungspuffer**|Zeile Anwendungsdiensts (ARD)|Anwendungsparameterdeskriptor (APD)|  
|**Implementierung Puffer**|Implementierungszeilendeskriptor (IRD)|Implementation Parameter Descriptor, (IPD)|  
  
 Für den Parameter oder den Zeilenpuffer Wenn die Anwendung in den entsprechenden Datensätzen der Implementierung und Deskriptoren gibt unterschiedliche Datentypen an, führt der Treiber Datenkonvertierung, wenn sie die Deskriptoren verwendet. Es kann z. B. numerische und "DateTime" in-Zeichenfolge-Format konvertieren. (Gültige Konvertierungen finden Sie unter [Anhang D: Datentypen](../../../odbc/reference/appendixes/appendix-d-data-types.md).)  
  
 Ein Deskriptor kann verschiedene Rollen ausführen. Verschiedene Anweisungen können Deskriptor freigeben, die die Anwendung explizit reserviert. Ein Zeilendeskriptor in einer einzelnen Anweisung kann als eine Parameterdeskriptor in einer anderen Anweisung dienen.  
  
 Es ist immer, ob ein angegebener Deskriptor ein Anwendungsdiensts oder einen Deskriptor Implementierung ist bekannt, selbst wenn der Deskriptor noch nicht in einem Datenbankvorgang verwendet wurde. Für die Deskriptoren, die die Implementierung implizit zuordnet, zeichnet die Implementierung der vordefinierten Zeile relativ zur das Anweisungshandle verwenden. Der Deskriptor, der die Anwendung durch Aufrufen von zuordnet **SQLAllocHandle** ist ein Deskriptor für die Anwendung.
