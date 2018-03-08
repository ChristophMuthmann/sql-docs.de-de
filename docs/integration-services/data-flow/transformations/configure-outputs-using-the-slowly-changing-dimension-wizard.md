---
title: "Konfiguration von Ausgaben mithilfe des Assistenten für langsam veränderliche Dimensionen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Slowly Changing Dimension transformation
- slowly changing dimensions
- Slowly Changing Dimension Wizard
ms.assetid: da111731-1ffa-49b9-bcaa-3c93fd0eb619
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0aa62acd9470c1d1d5e2764046ab3302f8edc46a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="configure-outputs-using-the-slowly-changing-dimension-wizard"></a>Konfiguration von Ausgaben mithilfe des Assistenten für langsam veränderliche Dimensionen
  Der Assistent für langsam veränderliche Dimensionen dient als Editor für die Transformation für langsam veränderliche Dimensionen. Das Erstellen und Konfigurieren des Datenflusses für langsam veränderliche Dimensionen kann eine komplexe Aufgabe sein. Der Assistent für langsam veränderliche Dimensionen bietet die einfachste Methode zum Erstellen des Datenflusses für die Ausgaben der Transformation für langsam veränderliche Dimensionen und führt durch die Schritte zum Zuordnen von Spalten, Auswählen von Geschäftsschlüsselspalten, Festlegen von Spaltenänderungsattributen und Konfigurieren der Unterstützung für abgeleitete Dimensionselemente.  
  
 Sie müssen mindestens eine Geschäftsschlüsselspalte in der Dimensionstabelle auswählen und einer Eingabespalte zuordnen. Der Wert des Geschäftsschlüssels verlinkt einen Datensatz in der Quelle mit einem Datensatz in der Dimensionstabelle. Die Transformation verwendet diese Zuordnung, um den Datensatz in der Dimensionstabelle zu finden und um zu ermitteln, ob ein Datensatz neu ist oder geändert wird. Der Geschäftsschlüssel ist im Allgemeinen der Primärschlüssel in der Quelle, es kann sich jedoch auch um einen alternativen Schlüssel handeln, wenn dieser einen Datensatz eindeutig identifiziert und sein Wert unverändert bleibt. Bei dem Geschäftsschlüssel kann es sich auch um einen zusammengesetzten Schlüssel aus mehreren Spalten handeln. Der Primärschlüssel in der Dimensionstabelle ist im Allgemeinen ein Ersatzschlüssel und damit ein numerischer Wert, der automatisch durch eine Identitätsspalte oder durch eine benutzerdefinierte Lösung wie ein Skript generiert wird.  
  
 Bevor Sie den Assistenten für langsam veränderliche Dimensionen ausführen können, müssen Sie dem Datenfluss eine Quelle und eine Transformation für langsam veränderliche Dimensionen hinzufügen, und dann die Ausgabe von der Quelle mit der Eingabe der Transformation für langsam veränderliche Dimensionen verbinden. Optional kann der Datenfluss andere Transformationen zwischen der Datenquelle und der Transformation für langsam veränderliche Dimensionen einschließen.  
  
 Doppelklicken Sie auf die Transformation für langsam veränderliche Dimensionen, um den Assistenten für langsam veränderliche Dimensionen im [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer zu öffnen.  
  
## <a name="creating-slowly-changing-dimension-outputs"></a>Erstellen von Ausgaben für die Transformation für langsam veränderliche Dimensionen  
  
#### <a name="to-create-slowly-changing-dimension-transformation-outputs"></a>So erstellen Sie Ausgaben für die Transformation für langsam veränderliche Dimensionen  
  
1.  Wählen Sie den Verbindungs-Manager für den Zugriff auf die Datenquelle aus, die die zu aktualisierende Dimensionstabelle enthält.  
  
     Eine Liste von Verbindungs-Managern, die im Paket enthalten sind, steht zur Auswahl.  
  
2.  Wählen Sie die Dimensionstabelle oder die Sicht aus, die Sie aktualisieren möchten.  
  
     Nachdem Sie den Verbindungs-Manager ausgewählt haben, können Sie die Tabelle oder Sicht in der Datenquelle auswählen.  
  
3.  Legen Sie Schlüsselattribute für Spalten fest, und ordnen Sie Eingabespalten Spalten in der Dimensionstabelle zu.  
  
     Sie müssen mindestens eine Geschäftsschlüsselspalte in der Dimensionstabelle auswählen und einer Eingabespalte zuordnen. Andere Eingabespalten können Spalten in der Dimensionstabelle als Nichtschlüsselzuordnungen zugeordnet werden.  
  
4.  Wählen Sie den Änderungstyp für jede Spalte aus.  
  
    -   **Veränderliches Attribut** überschreibt vorhandene Werte in Datensätzen.  
  
    -   **Verlaufsattribut** erstellt neue Datensätze, statt vorhandene Datensätze zu aktualisieren.  
  
    -   **Festes Attribut** gibt an, dass der Spaltenwert nicht geändert werden darf.  
  
5.  Legen Sie die Optionen für feste und veränderliche Attribute fest  
  
     Wenn Sie für Spalten die Verwendung des Änderungstyps **Festes Attribut** konfigurieren, können Sie angeben, ob bei der Transformation für langsam veränderliche Dimensionen ein Fehler auftritt, wenn Änderungen an diesen Spalten erkannt werden. Wenn Sie für Spalten die Verwendung des Änderungstyps **Veränderliches Attribut** konfigurieren, können Sie angeben, ob alle übereinstimmenden Datensätze, einschließlich veralteter Datensätze, aktualisiert werden.  
  
6.  Legen Sie die Optionen für Verlaufsattribute fest.  
  
     Wenn Sie für Spalten die Verwendung des Änderungstyps **Verlaufsattribut** konfigurieren, müssen Sie auswählen, wie zwischen aktuellen und abgelaufenen Datensätzen unterschieden werden soll. Sie können eine aktuelle Zeilenindikatorspalte oder zwei Datenspalten zum Identifizieren aktueller und abgelaufener Zeilen verwenden. Wenn Sie die aktuelle Zeilenindikatorspalte verwenden, können Sie sie auf **Aktuell**, **Wahr** , wenn die Daten aktuell sind, und **Abgelaufen** oder **Falsch** festlegen, wenn die Zeilen abgelaufen sind. Sie können auch benutzerdefinierte Werte eingeben. Wenn Sie zwei Datenspalten verwenden, ein Startdatum und ein Enddatum, können Sie das zu verwendende Datum zum Festlegen der Datenspaltenwerte angeben, indem Sie ein Datum eingeben oder eine Systemvariable auswählen und dann deren Wert verwenden.  
  
7.  Geben Sie die Unterstützung für abgeleitete Elemente an, und wählen Sie die Spalten aus, die der Datensatz für das abgeleitete Element enthält.  
  
     Beim Laden von Measures in eine Faktentabelle können Sie minimale Datensätze für abgeleitete Elemente erstellen, die noch nicht vorhanden sind. Wenn später aussagekräftige Daten vorhanden sind, können die Dimensionsdatensätze aktualisiert werden. Die folgenden Typen minimaler Datensätze können erstellt werden:  
  
    -   Ein Datensatz, in dem alle Spalten mit Änderungstypen NULL sind.  
  
    -   Ein Datensatz, in dem eine boolesche Spalte anzeigt, dass der Datensatz ein abgeleitetes Element ist.  
  
8.  Überprüfen Sie die Konfigurationen, die der Assistent für langsam veränderliche Dimensionen erstellt. In Abhängigkeit von den unterstützten Änderungstypen werden dem Paket unterschiedliche Datenflusskomponenten hinzugefügt.  
  
     Im folgenden Diagramm wird ein Beispiel eines Datenflusses dargestellt, der Änderungen für feste Attribute, veränderliche Attribute und Verlaufsattribute sowie abgeleitete Elemente und Änderungen an übereinstimmenden Datensätzen unterstützt.  
  
     ![Datenfluss vom Assistenten für langsam veränderliche Dimensionen](../../../integration-services/data-flow/transformations/media/dimensionwizard.gif "Datenfluss vom Assistenten für langsam veränderliche Dimensionen")  
  
## <a name="updating-slowly-changing-dimension-outputs"></a>Aktualisieren von Ausgaben für die Transformation für langsam veränderliche Dimensionen  
 Die einfachste Methode, um die Konfiguration von Ausgaben für die Transformation für langsam veränderliche Dimensionen zu aktualisieren, ist die erneute Ausführung des Assistenten für langsam veränderliche Dimensionen und das Ändern der Eigenschaften auf den Seiten des Assistenten. Sie können die Transformation für langsam veränderliche Dimensionen auch im Dialogfeld **Erweiterter Editor** oder programmgesteuert aktualisieren.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)  
  
  
