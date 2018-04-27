---
title: Sortierung (Dialogfeld) (Visual Database Tools) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vdt.dlgbox.definecolumncollation
- vdtsql.chm:65561
ms.assetid: e4020f79-7abf-4839-b9b2-984ef7049817
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3f5efc3b29f6ecf3f66b170524eeba41d235f39e
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="collation-dialog-box-visual-database-tools"></a>Sortierreihenfolge (Dialogfeld) (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Mit diesem Dialogfeld können Sie eine Sortierreihenfolge für die Spalte angeben. Die Sortierreihenfolge einer Spalte wird bei jedem Vorgang verwendet, bei dem die Werte der Spalte mit einer anderen Spalte oder mit konstanten Werten verglichen werden. Gleichzeitig wird dadurch das Verhalten einiger Zeichenfolgenfunktionen beeinflusst, z. B. SUBSTRING und CHARINDEX. Eine vollständige Liste der Auswirkungen der Einstellung der Sortierreihenfolge einer Spalte finden Sie in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Dokumentation.  
  
Das Dialogfeld wird in den folgenden Fällen angezeigt:  
  
-   Wenn Sie auf der Registerkarte **Spalteneigenschaften** im Feld **Sortierung** einen ungültigen Sortierungsnamen eingeben.  
  
-   Wenn Sie im Feld **Sortierreihenfolge** auf der Registerkarte **Spalteneigenschaften** klicken, und dann auf die Schaltfläche mit den Auslassungspunkten (**…**) rechts neben dem Feld klicken.  
  
## <a name="options"></a>Tastatur  
**SQL-Sortierung**  
Wählen Sie aus der Dropdownliste eine in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] definierte Sortierreihenfolge.  
  
**Windows-Sortierreihenfolge**  
Wählen Sie aus den Sortierreihenfolgen, die in Windows in der Dropdownliste definiert sind.  
  
**Binäre Sortierung**  
Verwenden Sie die Binärcodes der Zeichenwerte für Vergleiche. Wenn Sie diese Option auswählen, sind bestimmte Optionen der alphabetischen Vergleiche nicht verfügbar. Beispielsweise ist das Vergleichen ohne Unterscheidung von Groß- und Kleinschreibung nicht möglich, da Groß- und Kleinbuchstaben eine unterschiedliche binäre Codierung aufweisen. Diese Option wird nur verwendet, wenn Sie **Windows-Sortierreihenfolge**ausgewählt haben.  
  
**Lexikalische Sortierung**  
Verwenden Sie alphabetische Vergleichsoptionen. Diese Option wird nur verwendet, wenn Sie **Windows-Sortierreihenfolge**ausgewählt haben. Zu den alphabetischen Vergleichsoptionen gehören folgende:  
  
-   **Groß-/Kleinschreibung beachten** Aktivieren Sie diese Option, wenn beim Vergleichen die Groß- und Kleinschreibung berücksichtigt werden soll.  
  
-   **Akzente berücksichtigen** Aktivieren Sie diese Option, wenn beim Vergleichen zwischen Buchstaben mit Akzent und Buchstaben ohne Akzent unterschieden werden soll. Wenn Sie diese Option aktivieren, werden beim Vergleichen außerdem gleiche Buchstaben mit unterschiedlichen Akzenten unterschieden.  
  
-   **Kana berücksichtigen** Aktivieren Sie diese Option, wenn beim Vergleichen Unterschiede zwischen Katakana- und Hiragana-Japanisch berücksichtigt werden sollen.  
  
-   **Breite berücksichtigen** Aktivieren Sie diese Option, wenn beim Vergleichen der Unterschied zwischen Zeichen halber Breite und Zeichen normaler Breite berücksichtigt werden soll.  
  
**Schaltfläche Standard wiederherstellen**  
Wenden Sie die Standardsortierreihenfolge für die Datenbank auf die Spalte an.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Verwenden von Spalten in Aggregatabfragen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-columns-in-aggregate-queries-visual-database-tools.md)  
  
