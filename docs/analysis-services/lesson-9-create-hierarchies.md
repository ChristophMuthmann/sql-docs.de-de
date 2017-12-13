---
title: 'Lektion 10: Erstellen von Hierarchien | Microsoft Docs'
ms.custom: 
ms.date: 04/10/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 1e2561d3-4890-4495-a9cd-84eb88508938
caps.latest.revision: "23"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: d154519f39c17d1bdee4cf2a96ddb18f96ac3444
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/08/2017
---
# <a name="lesson-9-create-hierarchies"></a>Lektion 9: Erstellen von Hierarchien
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

In dieser Lektion erstellen Sie Hierarchien. Hierarchien sind Gruppen von Spalten, die in Ebenen angeordnet werden. Beispielsweise könnte eine Geografiehierarchie Unterebenen für Land, Status, Landkreis und Stadt beinhalten. Hierarchien können getrennt von anderen Spalten in der Feldliste einer Clientanwendung zur Berichtserstellung angezeigt werden, sodass Clientbenutzer einfacher darin navigieren und sie in einen Bericht aufnehmen können. Weitere Informationen finden Sie unter [Hierarchien](../analysis-services/tabular-models/hierarchies-ssas-tabular.md).  
  
Verwenden Sie zum Erstellen von Hierarchien im Modell-Designer in *Diagrammsicht*. Erstellen und Verwalten von Hierarchien wird in der Datensicht nicht unterstützt.  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **20 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Dieses Thema ist Teil eines Lernprogramms zur Tabellenmodellierung, das in der entsprechenden Reihenfolge bearbeitet werden sollte. Vor dem Ausführen der Aufgaben in dieser Lektion, Sie sollten haben die vorherige Lektion abgeschlossen: [Lektion 8: Erstellen von Perspektiven](../analysis-services/lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Erstellen von Hierarchien  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a>So erstellen Sie eine Kategoriehierarchie in der DimProduct-Tabelle  
  
1.  Im Modell-Designer (Diagrammsicht), mit der Maustaste die **DimProduct** Tabelle > **Hierarchie erstellen**. Eine neue Hierarchie wird am unteren Rand des Tabellenfensters angezeigt. Benennen Sie die Hierarchie **Kategorie**.  
  
2.  Klicken Sie auf, und ziehen Sie die **"productcategoryname"** Spalte mit dem neuen **Kategorie** Hierarchie.  
  
3.  In der **Kategorie** Hierarchie mit der rechten Maustaste die **"productcategoryname"** > **umbenennen**, und geben Sie dann **Kategorie**.  
  
    > [!NOTE]  
    > Durch das Umbenennen einer Spalte in einer Hierarchie wird die betreffende Spalte in der Tabelle nicht umbenannt. Eine Spalte in einer Hierarchie ist nur eine Darstellung der Spalte in der Tabelle.  
  
4.  Klicken Sie auf, und ziehen Sie die **ProductSubcategoryName** Spalte die **Kategorie** Hierarchie. Benennen Sie sie **Subcategory**. 
  
5.  Mit der rechten Maustaste die **ModelName** Spalte > **Hierarchie hinzufügen**, und wählen Sie dann **Kategorie**. Führen Sie dieselben Aktionen für **EnglishProductName**. Benennen Sie diese Spalten in der Hierarchie **Modell** und **Produkt**.  

    ![als tabellarische-lesson9-Kategorie](../analysis-services/media/as-tabular-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a>Zum Erstellen von Hierarchien in der DimDate-Tabelle  
  
1.  In der **DimDate** Tabelle, erstellen Sie eine neue Hierarchie, die mit dem Namen **Kalender**.  
  
3.  Fügen Sie die folgenden Spalten in Ordnung hinzu:

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  In der **DimDate** Tabelle, erstellen Sie eine **Geschäftskalender** Hierarchie. Unter anderem die folgenden Spalten:  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  Schließlich wird in der **DimDate** Tabelle, erstellen Sie eine **ProductionCalendar** Hierarchie. Unter anderem die folgenden Spalten:  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>Wie geht es weiter?
Wechseln Sie zur nächsten Lektion: [Lektion 10: Erstellen von Partitionen](../analysis-services/lesson-10-create-partitions.md). 
  
  
