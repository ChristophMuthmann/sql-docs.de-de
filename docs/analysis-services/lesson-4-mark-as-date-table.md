---
title: "Lektion 4: Markieren als Datumstabelle | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: c32cc336-b7d8-4122-9d62-4936344d2315
caps.latest.revision: 18
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Lektion 4: Markieren als Datumstabelle
In „Lektion 2: Hinzufügen von Daten“ haben Sie eine Dimensionstabelle mit dem Namen „DimDate“ importiert und in „Date“ umbenannt. In Ihrem Modell lautet der Name dieser Tabelle jetzt „Date“, sie kann jedoch auch als *Datumstabelle* bezeichnet werden, da sie Datums- und Uhrzeitdaten enthält.  
  
Immer wenn Sie in Berechnungen Zeitintelligenzfunktionen verwenden, z.B. in Kürze beim Erstellen von Measures, müssen Sie Eigenschaften von Datentabellen angeben, die eine *Datumstabelle* und als eindeutigen Bezeichner die *Datumsspalte* in dieser Tabelle enthalten. Sie können dann gültige Beziehungen zwischen anderen Tabellen und der Datumstabelle erstellen. Dies ist für Berechnungen mit DAX-Zeitintelligenzfunktionen erforderlich.  
  
In dieser Lektion kennzeichnen Sie die importierte und umbenannte Date-Tabelle als *Datumstabelle* und die Date-Spalte (in der Date-Tabelle) als *Datumsspalte* (eindeutiger Bezeichner). Diese Verwendung des Namens "Date" bzw. "Datum" kann verwirrend sein, Sie werden jedoch bald das Prinzip begreifen.  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **3 Minuten**  
  
## Erforderliche Komponenten  
Dieses Thema ist Teil eines Lernprogramms zur Tabellenmodellierung, das in der entsprechenden Reihenfolge bearbeitet werden sollte. Sie sollten vor dem Ausführen der Aufgaben in dieser Lektion die vorherige Lektion abgeschlossen haben: [Lektion 3: Umbenennen von Spalten](../analysis-services/lesson-3-rename-columns.md).  
  
### So legen Sie "Als Datumstabelle markieren" fest  
  
1.  Klicken Sie im Modell-Designer auf die Tabelle (Registerkarte) **Date**.  
  
2.  Wählen Sie die **Datum**-Spalte und stellen Sie anschließend im Fenster **Eigenschaften** unter **Datentyp** sicher, dass **Datum** ausgewählt ist.  
  
3.  Klicken Sie im Menü **Tabelle** auf **Datum** und anschließend auf **Als Datumstabelle markieren**.  
  
4.  Wählen Sie im Dialogfeld **Als Datumstabelle markieren** im Listenfeld **Datum** die Spalte **Datum** als eindeutigen Bezeichner aus.  
  
## Nächste Schritte  
Wenn Sie mit diesem Tutorial fortfahren möchten, wechseln Sie zur nächsten Lektion: [Lektion 5: Erstellen von Beziehungen](../analysis-services/lesson-5-create-relationships.md).  
  
  
  
