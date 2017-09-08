---
title: "Ändern von Tabellen-, Spalten- oder zeilenfilterzuordnungen (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2124c526-5772-4f84-a019-9dd3e906e8dd
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b80323e5aaf1dd6c469ddffefb5d92542e9d3a19
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="change-table-column-or-row-filter-mappings-ssas-tabular"></a>Ändern von Tabellen-, Spalten- oder Zeilenfilterzuordnungen (SSAS – tabellarisch)
  In diesem Thema wird beschrieben, wie Tabellen-, Spalten- oder Zeilenfilterzuordnungen im Dialogfeld **Tabelleneigenschaften bearbeiten** in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]geändert werden.  
  
 Die Optionen im Dialogfeld **Tabelleneigenschaften bearbeiten** variieren, je nachdem, ob Daten ursprünglich durch Auswahl von Tabellen aus einer Liste oder mithilfe einer SQL-Abfrage importiert wurden. Wenn die Daten ursprünglich durch Auswahl aus einer Liste importiert wurden, wird das Dialogfeld **Tabelleneigenschaften bearbeiten** im Tabellenvorschaumodus angezeigt. In diesem Modus wird nur eine Teilmenge angezeigt, die auf die ersten 50 Zeilen der Quelltabelle beschränkt ist. Wenn die Daten ursprünglich durch Verwendung einer SQL-Anweisung importiert wurden, wird im Dialogfeld **Tabelleneigenschaften bearbeiten** nur eine SQL-Anweisung angezeigt. Mithilfe einer SQL-Abfrageanweisung können Sie eine Teilmenge der Zeilen abrufen, indem Sie entweder einen Filter entwerfen oder die SQL-Anweisung manuell bearbeiten.  
  
 Wenn Sie die Quelle in eine Tabelle ändern, die andere Spalten als die aktuelle Tabelle enthält, wird eine entsprechende Warnmeldung angezeigt. Sie müssen dann die Spalten auswählen, die Sie in die aktuelle Tabelle einfügen möchten, und auf **Speichern**klicken. Sie können die gesamte Tabelle ersetzen, indem Sie das Kontrollkästchen links von der Tabelle aktivieren.  
  
> [!NOTE]  
>  Wenn die Tabelle über mehrere Partitionen verfügt, können Sie die Zeilenfilterzuordnungen nicht im Dialogfeld Tabelleneigenschaften bearbeiten ändern. Verwenden Sie zum Ändern der Zeilenfilterzuordnungen für Tabellen mit mehreren Partitionen den Partitions-Manager. Weitere Informationen finden Sie unter [Partitionen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
#### <a name="to-change-table-column-or-row-filter-mappings"></a>So ändern Sie Tabellen-, Spalten- oder Zeilenfilterzuordnungen  
  
1.  Klicken Sie im Modell-Designer auf die Tabelle und dann auf das Menü **Tabelle** und auf **Tabelleneigenschaften**.  
  
2.  Suchen Sie im Dialogfeld **Tabelleneigenschaften bearbeiten** nach der Spalte, die die Filterkriterien enthält, und klicken Sie dann rechts von der Spaltenüberschrift auf den Pfeil nach unten.  
  
3.  Führen Sie im Menü **AutoFilter** einen der folgenden Schritte aus:  
  
    -   Wählen Sie in der Liste der Spaltenwerte mindestens einen Wert aus, nach dem gefiltert werden soll, bzw. heben Sie die Auswahl auf, und klicken Sie auf OK.  
  
         Wenn die Anzahl der Werte sehr groß ist, kann es sein, dass einzelne Elemente nicht in der Liste angezeigt werden. Stattdessen wird eine Meldung angezeigt, dass zu viele Elemente zum Anzeigen vorhanden sind.  
  
    -   Klicken Sie je nach Typ der Spalte auf **Zahlenfilter** oder **Textfilter** , und klicken Sie anschließend auf einen der Vergleichsoperatorbefehle (wie „Ist gleich“), oder klicken Sie auf „Benutzerdefinierter Filter“. Erstellen Sie im Dialogfeld **Benutzerdefinierter Filter** den Filter, und klicken Sie dann auf **OK**.  
  
         Falls Sie erneut beginnen möchten, klicken Sie auf **Zeilenfilter löschen**.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabelleneigenschaften bearbeiten (Dialogfeld) &#40;SSAS&#41;](http://msdn.microsoft.com/library/8d913e83-7246-44cc-8fc7-31729023c0d8)  
  
  
