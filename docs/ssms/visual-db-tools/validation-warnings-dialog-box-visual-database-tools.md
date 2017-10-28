---
title: "Gültigkeitswarnungen (Dialogfeld) (Visual Database Tools) | Microsoft-Dokumentation"
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
- vdtsql.chm:65556
- vdt.dlgbox.validationwarnings
ms.assetid: fc76e234-ec9c-4a19-a65b-cb558ec8268e
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 78aac0124cb34ac7699907df89c3251559bb79f8
ms.contentlocale: de-de
ms.lasthandoff: 08/18/2017

---
# <a name="validation-warnings-dialog-box-visual-database-tools"></a>Gültigkeitswarnungen (Dialogfeld) (Visual Database Tools)
Dieses Dialogfeld wird angezeigt, wenn Sie Änderungen zu speichern versuchen, die u. U. Schaden anrichten, oder wenn der Commit für die Datenbank vermutlich fehlschlägt. In diesem Dialogfeld werden die möglichen Nebeneffekte bzw. die Gründe für das Fehlschlagen des Commitvorgangs angegeben. Sie können dann entweder mit der Änderung fortfahren oder den Vorgang abbrechen.  
  
> [!NOTE]  
> Dieses Dialogfeld wird angezeigt, wenn Sie versuchen, vorgenommene Änderungen an die Datenbank zu übermitteln, oder wenn Sie ein Änderungsskript speichern.  
  
Das Dialogfeld kann aus folgenden Gründen angezeigt werden:  
  
-   Sie besitzen möglicherweise nicht die Datenbankberechtigungen zum Ausführen eines Commits für alle Änderungen.  
  
-   Die Änderungen würden falsch formatierte abgeleitete Spalten, Standardeinschränkungen oder CHECK-Einschränkungen zur Folge haben.  
  
-   Die Änderung des Datentyps für eine Spalte könnte zu Datenverlusten führen.  
  
-   Eine Änderung hätte einen Index von mehr als 900 Byte zur Folge.  
  
-   Eine Änderung würde eine Tabelle bzw. Spalte ändern und würde dadurch zu einer an ein Schema gebundenen Sicht oder einer benutzerdefinierten Funktion führen.  
  
-   Eine Änderung würde zur Neuerstellung einer Tabelle mit mindestens einem verschlüsselten Trigger führen, wobei die Trigger gelöscht werden würden.  
  
-   Die Änderungen ergeben besondere Einstellungen von ANSI_NULLS und/oder ANSI_PADDING für die Spalten innerhalb einer Tabelle.  
  
## <a name="options"></a>enthalten  
**Ja**  
Setzen Sie den Vorgang fort, und generieren Sie das Änderungsskript, oder übermitteln Sie die Änderungen an die Datenbank. Der Commitvorgang kann trotzdem noch fehlschlagen, wenn Sie nicht über die Berechtigungen zum Ändern der Datenbank verfügen, wenn die Änderungen bewirken, dass der Index größer als 900 Bytes wird, oder wenn die Änderungen eine falsch formatierte berechnete Spalte, Standardeinschränkungen oder CHECK-Einschränkungen zur Folge haben.  
  
**Nein**  
Brechen Sie den Speichervorgang ab.  
  
**Textdatei speichern**  
Zeigen Sie das Dialogfeld **Speichern unter** an, in dem Sie einen Speicherort für eine Textdatei angeben können, die eine Liste der Warnungen enthält.  
  
## <a name="see-also"></a>Siehe auch  
[Entwerfen von Tabellen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-tables-visual-database-tools.md)  
[Themen zur Vorgehensweise: Entwerfen von Abfragen und Sichten &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  

