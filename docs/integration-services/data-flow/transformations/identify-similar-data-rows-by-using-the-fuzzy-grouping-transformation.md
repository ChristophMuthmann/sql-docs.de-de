---
title: "Identifizieren ähnlicher Datenzeilen mithilfe der Transformation für Fuzzygruppierung | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- Fuzzy Grouping transformation
- match similar data [Integration Services]
- similar data rows [Integration Services]
- fuzzy matches
ms.assetid: ffcb41a6-e23d-49ea-8c32-ac980e3dc495
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d6d11c2474853586930e5cd46fde8f61526cd6ed
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation"></a>Identifizieren ähnlicher Datenzeilen mithilfe der Transformation für Fuzzygruppierung
  Das Paket muss bereits mindestens einen Datenflusstask und eine Quelle enthalten, damit Sie eine Transformation für Fuzzygruppierung hinzufügen und konfigurieren können.  
  
### <a name="to-implement-fuzzy-grouping-transformation-in-a-data-flow"></a>So implementieren Sie eine Transformation für Fuzzygruppierung in einem Datenfluss  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Projekt mit dem gewünschten Paket.  
  
2.  Doppelklicken Sie im Projektmappen-Explorer auf das Paket, um es zu öffnen.  
  
3.  Klicken Sie auf die Registerkarte **Datenfluss** , und ziehen Sie dann aus dem Fenster **Toolbox**die Transformation für Fuzzygruppierung auf die Entwurfsoberfläche.  
  
4.  Verbinden Sie die Transformation für Fuzzygruppierung mit dem Datenfluss, indem Sie den Konnektor von der Datenquelle oder einer vorherigen Transformation auf die Transformation für Fuzzygruppierung ziehen.  
  
5.  Doppelklicken Sie auf die Transformation für Fuzzygruppierung.  
  
6.  Wählen Sie im Dialogfeld **Transformations-Editor für Fuzzygruppierung** auf der Registerkarte **Verbindungs-Manager** einen OLE DB-Verbindungs-Manager aus, der eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank herstellt.  
  
    > [!NOTE]  
    >  Für die Transformation muss eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Datenbank vorhanden sein, damit temporäre Tabellen und Indizes erstellt werden können.  
  
7.  Klicken Sie auf die Registerkarte **Spalten** , und aktivieren Sie in der Liste **Verfügbare Eingabespalten** die Kontrollkästchen der Eingabespalten, die zum Identifizieren ähnlicher Zeilen im Dataset verwendet werden sollen.  
  
8.  Aktivieren Sie das Kontrollkästchen in der **Pass-Through** -Spalte, um die Eingabespalten für das Pass-Through an die Transformationsausgabe zu identifizieren. Pass-Through-Spalten werden nicht in die Identifizierung doppelter Zeilen eingeschlossen.  
  
    > [!NOTE]  
    >  Eingabespalten, die zum Gruppieren verwendet werden, werden automatisch als Pass-Through-Spalten ausgewählt. Die Auswahl dieser Spalten kann nicht aufgehoben werden, während sie zum Gruppieren verwendet werden.  
  
9. Aktualisieren Sie optional die Namen von Ausgabespalten in der **Ausgabealias** -Spalte.  
  
10. Aktualisieren Sie optional die Namen von bereinigten Spalten in der **Gruppenausgabealias** -Spalte.  
  
    > [!NOTE]  
    >  Die Standardnamen von Spalten sind die Namen der Eingabespalten mit dem Suffix "_clean".  
  
11. Aktualisieren Sie optional den zu verwendenden Übereinstimmungstyp in der **Übereinstimmungstyp** -Spalte.  
  
    > [!NOTE]  
    >  Mindestens eine Spalte muss die Fuzzyübereinstimmung verwenden.  
  
12. Geben Sie die minimale Ähnlichkeit von Spalten in der **Minimale Ähnlichkeit** -Spalte an. Der Wert muss zwischen 0 und 1 liegen. Je näher der Wert an 1 liegt, desto ähnlicher müssen die Werte in den Eingabespalten sein, um eine Gruppe zu bilden. Eine minimale Ähnlichkeit von 1 bedeutet eine genaue Übereinstimmung.  
  
13. Aktualisieren Sie optional die Namen von Ähnlichkeitsspalten in der **Ähnlichkeitsausgabealias** -Spalte.  
  
14. Aktualisieren Sie die Werte in der **Zahlen** -Spalte, um die Behandlung von Zahlen in Datenwerten anzugeben.  
  
15. Um anzugeben, wie die Transformation die Zeichenfolgendaten in einer Spalte vergleicht, ändern Sie die Standardauswahl von Vergleichsoptionen in der **Vergleichsflags** -Spalte.  
  
16. Klicken Sie auf die Registerkarte **Erweitert** , um die Namen der Spalten zu ändern, die die Transformation der Ausgabe für den eindeutigen Zeilenbezeichner (_key_in), den doppelten Zeilenbezeichner (_key_out) und den Ähnlichkeitswert (_score) hinzufügt.  
  
17. Passen Sie optional den Schwellenwert für die Ähnlichkeit mithilfe des Schiebereglers an.  
  
18. Deaktivieren Sie optional die Kontrollkästchen für Tokentrennzeichen, um Trennzeichen in den Daten zu ignorieren.  
  
19. Klicken Sie auf **OK**.  
  
20. Klicken Sie im Menü **Datei** auf **Ausgewählte Elemente speichern** , um das aktualisierte Paket zu speichern.  
  
## <a name="see-also"></a>Siehe auch  
 [Transformation für Fuzzygruppierung](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)   
 [Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Integration Services-Pfade](../../../integration-services/data-flow/integration-services-paths.md)   
 [Datenflusstask](../../../integration-services/control-flow/data-flow-task.md)  
  
  

