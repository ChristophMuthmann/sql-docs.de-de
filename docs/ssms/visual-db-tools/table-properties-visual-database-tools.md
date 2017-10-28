---
title: Tabelleneigenschaften (Visual Database Tools) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdt.tabledesigner
- vdt.designers.properties.Table
ms.assetid: cc392987-1aab-45f5-b5af-a26be53409bf
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3773ad2f9b1ba26af775d70146e17740eed828ad
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="table-properties-visual-database-tools"></a>Tabelleneigenschaften (Visual Database Tools)
Diese Eigenschaften werden im Eigenschaftenfenster angezeigt, wenn Sie mit der rechten Maustaste in den Tabellen-Designer klicken und Eigenschaften auswählen. Wenn nicht anders beschrieben, können Sie diese Eigenschaften im Eigenschaftenfenster bearbeiten, wenn die Tabelle markiert ist.  
  
> [!NOTE]  
> Wenn die Tabelle zur Replikation veröffentlicht ist, müssen Sie mit der Transact-SQL-Anweisung [ALTER TABLE](http://msdn.microsoft.com/en-us/f1745145-182d-4301-a334-18f799d361d1) oder mit SMO (SQL Server Management Objects) Schemaänderungen ausführen. Wenn die Schemaänderungen mit dem Tabellen-Designer oder dem Datenbankdiagramm-Designer ausgeführt werden, wird versucht, die Tabelle zu entfernen und erneut zu erstellen. Da veröffentlichte Objekte nicht gelöscht werden können, schlägt die Schemaänderung fehl.  
  
## <a name="show-table-properties-in-table-designer"></a>Anzeigen von Tabelleneigenschaften im Tabellen-Designer  
  
> [!NOTE]  
> Die in diesem Thema behandelten Eigenschaften sind nicht alphabetisch, sondern nach Kategorie angeordnet.  
  
**Kategorie Identität**  
Wenn die Kategorie erweitert ist, werden die Eigenschaften für **Name**, **Beschreibung**und **Schema**angezeigt.  
  
**Name**  
Zeigt den Namen der Tabelle an. Bearbeiten Sie das Textfeld, um den Namen zu ändern.  
  
> [!CAUTION]  
> Alle Abfragen, Sichten, benutzerdefinierten Funktionen, gespeicherten Prozeduren und Programme, die auf die Tabelle verweisen, werden durch die Namensänderung ungültig.  
  
**Datenbankname**  
Zeigt den Namen der Datenquelle der ausgewählten Tabelle an.  
  
**Beschreibung**  
Zeigt eine Beschreibung der ausgewählten Tabelle an. Klicken Sie auf die Beschreibung, und klicken Sie anschließend auf die Auslassungspunkte **(...)** rechts neben der Eigenschaft, um die ganze Beschreibung anzuzeigen oder sie zu bearbeiten.  
  
**Schema**  
Zeigt den Namen des Schemas an, zu dem die Tabelle gehört. (Gilt nur für Microsoft SQL Server.)  
  
**Servername**  
Zeigt den Namen des Servers für diese Datenquelle an.  
  
**Kategorie Tabellen-Designer**  
Wenn die Kategorie erweitert ist, werden Eigenschaften für **Identitätsspalte**, **Ist indizierbar**und **Ist repliziert**angezeigt.  
  
**Identitätsspalte**  
Zeigt die Spalte an, die als Identitätsspalte der Tabelle verwendet wird. Wenn Sie die Identitätsspalte ändern möchten, wählen Sie einen Eintrag in der Dropdownliste aus. In der Liste werden nur Spalten mit einem numerischen Datentyp aufgeführt.  
  
**Ist indizierbar**  
Zeigt an, ob die Tabelle indiziert werden kann. Wenn die Tabelle nicht indiziert werden kann, liegt dies unter Umständen daran, dass Sie nicht der Besitzer der Tabelle sind, oder dass die Tabelle Spalten mit den Datentypen text, ntext oder image enthält.  
  
**Ist repliziert**  
Zeigt an, ob die Tabelle in einem anderen Speicherort repliziert wird.  
  
**Kategorie Reguläre Datenbereichsspezifikation**  
Wenn die Kategorie erweitert ist, werden Eigenschaften für **(Datenbereichstyp)**, **Schemaname der Dateigruppe oder Partition**und **Partitionsspaltenliste**angezeigt.  
  
**(Datenbereichstyp)**  
Zeigt an, ob die Tabelle mit einem Dateigruppen- oder einem Partitionsschema gespeichert wird.  
  
**Schemaname der Dateigruppe oder Partition**  
Zeigt den Namen des Dateigruppen- oder Partitionsschemas an.  
  
**Partitionsspaltenliste**  
Ermöglicht den Zugriff auf das Dialogfeld **Partitionsspaltenliste** .  
  
**Zeilen-GUID-Spalte**  
Zeigt die Spalte an, die von Microsoft SQL Server als ROWGUID-Spalte der Tabelle verwendet wird. Wenn Sie die ROWGUID-Spalte ändern möchten, wählen Sie einen Eintrag in der Dropdownliste aus. (Gilt nur für SQL Server 7.0 oder höher.)  
  
**Text/Image-Dateigruppe**  
Stellt eine Dropdownliste bereit, in der die Dateigruppe für Spalten mit dem Datentyp text oder image ausgewählt werden kann. Wenn die Tabelle mit einem Partitionsschema gespeichert wird, lassen Sie dieses Feld leer.  
  
## <a name="see-also"></a>Siehe auch  
[Entwerfen von Tabellen (Visual Database Tools)](../../ssms/visual-db-tools/design-tables-visual-database-tools.md)  
  

