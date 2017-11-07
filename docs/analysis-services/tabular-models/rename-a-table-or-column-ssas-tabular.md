---
title: "Umbenennen einer Tabelle oder Spalte (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: 
ms.date: 05/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.bidtoolset.renametableorcolumn.f1
ms.assetid: 88061a39-c5aa-403d-a52b-7fdb365fc235
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5a560b70416ed73945db053249a51508635b50ac
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="rename-a-table-or-column-ssas-tabular"></a>Umbenennen einer Tabelle oder Spalte (SSAS – tabellarisch)
  Sie können während des Importvorgangs den Namen einer Tabelle ändern, indem Sie im **Tabellenimport-Assistenten** auf der Seite **Tabellen und Sichten auswählen** einen **Anzeigenamen**eingeben. Sie können während des Datenimports auch Tabellen- und Spaltennamen ändern, indem Sie im **Tabellenimport-Assistenten** auf der Seite **SQL-Abfrage angeben**eine Abfrage angeben.  
  
 Nachdem dem Modell die Daten hinzugefügt wurden, wird der Name (oder Titel) einer Tabelle auf der Tabellenregisterkarte im unteren Bereich des Modell-Designers angezeigt. Sie können den Namen einer Tabelle ändern, um ihr einen geeigneteren Namen zu geben. Sie können eine Spalte auch umbenennen, nachdem die Daten dem Modell hinzugefügt wurden. Diese Option ist insbesondere dann wichtig, wenn Sie Daten aus mehreren Quellen importiert haben und sicherstellen möchten, dass Spalten in anderen Tabellen Namen haben, die leicht zu unterscheiden sind.  
  
### <a name="to-rename-a-table"></a>So benennen Sie eine Tabelle um  
  
1.  Klicken Sie im Modell-Designer mit der rechten Maustaste auf die Registerkarte der Tabelle, die Sie umbenennen möchten, und klicken Sie auf **Umbenennen**.  
  
2.  Geben Sie den neuen Namen ein.  
  
    > [!NOTE]  
    >  Sie können mit dem Dialogfeld **Tabelleneigenschaften bearbeiten** andere Eigenschaften einer Tabelle bearbeiten, einschließlich der Verbindungsinformationen und Spaltenzuordnungen. Den Namen können Sie in diesem Dialogfeld jedoch nicht ändern.  
  
### <a name="to-rename-a-column"></a>So benennen Sie eine Spalte um  
  
1.  Doppelklicken Sie im Modell-Designer auf die Kopfzeile der Spalte, die Sie umbenennen möchten, oder klicken Sie mit der rechten Maustaste auf die Kopfzeile, und wählen Sie im Kontextmenü **Spalte umbenennen** aus.  
  
2.  Geben Sie den neuen Namen ein.  
  
## <a name="naming-requirements-for-columns-and-tables"></a>Anforderungen für die Benennung von Spalten und Tabellen  
 Die folgenden Wörter und Zeichen können nicht im Namen einer Tabelle oder einer Spalte verwendet werden:  
  
-   Führende oder nachfolgende Leerzeichen  
  
-   Steuerzeichen  
  
-   Die folgenden Zeichen (die in den Namen für Analysis Services-Objekte nicht zulässig sind): .,;':/\\*|?&%$!+=()[]{}<>  
  
-   Von Analysis Services reservierte Schlüsselwörter, einschließlich Funktionsnamen und Operatoren von Multidimensional Expressions (MDX) und Data Mining Extensions (DMX)  
  
## <a name="effect-of-renaming-on-existing-tables-columns-and-calculations"></a>Auswirkung des Umbenennungsvorgangs auf vorhandene Tabellen, Spalten und Berechnungen  
 Jedes Mal, wenn Sie den Namen einer Tabelle ändern, ändern Sie den Namen des zugrunde liegenden Tabellenobjekts, der möglicherweise mehrere Spalten oder Measures enthält. Alle Spalten in der Tabelle und alle Beziehungen, die verwenden die Tabelle, müssen aktualisiert werden, um den neuen Namen in ihren Definitionen zu verwenden. Dieses Update kann in den meisten Fällen automatisch durchgeführt werden.
  
 Alle Berechnungen, die die umbenannte Tabelle oder Spalten in der umbenannten Tabelle verwenden, müssen ebenfalls aktualisiert werden, und die von diesen Berechnungen abgeleiteten Daten müssen aktualisiert und neu berechnet. Je nach Anzahl der betroffenen Tabellen und Berechnungen kann dies einige Zeit in Anspruch nehmen. Der beste Zeitpunkt zum Umbenennen von Tabellen ist daher entweder während des Importvorgangs oder bevor Sie komplexe Beziehungen und Berechnungen erstellen.  
  
## <a name="see-also"></a>Siehe auch  
 [Tabellen und Spalten](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [Importieren aus PowerPivot](../../analysis-services/tabular-models/import-from-power-pivot-ssas-tabular.md)   
 [Importieren aus Analysis Services](../../analysis-services/tabular-models/import-from-analysis-services-ssas-tabular.md)  
  
  

