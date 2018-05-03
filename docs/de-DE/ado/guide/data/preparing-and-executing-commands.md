---
title: Vorbereiten und Ausführen von Befehlen | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], preparing and executing commands
ms.assetid: 7448d9ee-7f4b-47e3-be54-2df8c9bbac32
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 53d81f2e944954715246f98959567cb9e02fe0be
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="preparing-and-executing-commands"></a>Vorbereiten und Ausführen von Befehlen
Befehle sind Anweisungen zu einem Anbieter ausgestellt Eingriffe für die zugrunde liegenden Datenquelle. Eine SQL-Anweisung ist z. B. ein Befehl für den Microsoft SQL-Datenanbieter. In ADO werden Befehle in der Regel durch dargestellt **Befehl** Objekte aufweist, obwohl der einfache Befehle auch ausgegeben werden können, können Sie über **Verbindung** oder **Recordset** Objekte.  
  
 Sie können die **Befehl** Objekt zum Anfordern des Vorgangs alle unterstützten Typen vom Anbieter, vorausgesetzt, dass der Anbieter die Befehlszeichenfolge ordnungsgemäß interpretiert werden kann. Ein allgemeiner Vorgang für Datenanbieter ist, um eine Datenbank abzufragen und Zurückgeben von Datensätzen in einer **Recordset** -Objekt, das, die als Container für das Ergebnis und ein Tool zum Anzeigen des Ergebnisses vorstellen können. Wie bei vielen ADO-Objekten, einige **Befehl** Auflistungen, Methoden oder Eigenschaften möglicherweise Fehler auf, wenn referenziert werden, abhängig von den Funktionen des Anbieters generieren.  
  
 Zusätzlich zur Verwendung von **Befehl** Objekte aufweist, können Sie die **Execute** Methode für die **Verbindung** Objekt oder die **öffnen** Methode für die  **Recordset** Objekt, das einen Befehl ausgeben und ausführen lassen. Allerdings sollten Sie verwenden eine **Befehl** -Objekt, wenn Sie einen Befehl in Ihrem Code wiederverwenden müssen oder detaillierte Parameterinformationen mit dem Befehl übergeben werden sollen. Diese Szenarien werden weiter unten in diesem Abschnitt ausführlicher behandelt.  
  
> [!NOTE]
>  Bestimmte **Befehl**s kann ein Resultset als binärer Stream oder ein einzelner zurückgeben **Datensatz** sondern als eine **Recordset**, wenn dies vom Anbieter unterstützt wird. Darüber hinaus einige **Befehl**s dürfen keine Resultset überhaupt (z. B. eine SQL Update-Abfrage) zurückgegeben. Dieser Abschnitt befasst sich das häufigste Szenario jedoch: Ausführen von **Befehl**s, die als Ergebnisse zurückgeben einer **Recordset** Objekt. Weitere Informationen zum Zurückgeben von Ergebnissen in **Datensatz**s oder **Stream**s, finden Sie unter [Datensätze und Datenströme](../../../ado/guide/data/records-and-streams.md).  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Command-Objekte (Übersicht)](../../../ado/guide/data/command-object-overview.md)  
  
-   [Erstellen und Ausführen eines einfachen Befehls](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Befehlsobjekt-Parameter](../../../ado/guide/data/command-object-parameters.md)  
  
-   [Aufrufen einer gespeicherten Prozedur mit einem Befehl](../../../ado/guide/data/calling-a-stored-procedure-with-a-command.md)  
  
-   [Aufrufen einer gespeicherten Prozedur als Methode für ein Verbindungsobjekt](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
-   [Benannte Befehle](../../../ado/guide/data/named-commands.md)  
  
-   [Übergeben von Parametern an einen benannten Befehl](../../../ado/guide/data/passing-parameters-to-a-named-command.md)
