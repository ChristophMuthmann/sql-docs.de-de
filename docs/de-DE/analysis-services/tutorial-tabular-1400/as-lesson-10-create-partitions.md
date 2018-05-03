---
title: 'Analysis Services Tutorial Lektion 10: Erstellen von Partitionen | Microsoft Docs'
description: Beschreibt, wie Partitionen in Analysis Services Tutorial-Projekt zu erstellen.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: ff8058439cc4ad1f567573267b88f07340f56409
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="create-partitions"></a>Erstellen von Partitionen

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In dieser Lektion erstellen Sie Partitionen, um die FactInternetSales-Tabelle in kleinere logische Teile aufzuteilen, die verarbeitet werden können (aktualisiert) unabhängig von anderen Partitionen. Standardmäßig verfügt jede Tabelle, die Sie in Ihr Modell einschließen eine Partition, die alle der Tabelle Spalten und Zeilen enthält. Die FactInternetSales-Tabelle möchten die Daten nach Jahr unterteilen. eine Partition für jeden der fünf Jahren der Tabelle. Jede Partition kann dann unabhängig verarbeitet werden. Weitere Informationen finden Sie unter [Partitionen](../tabular-models/partitions-ssas-tabular.md). 
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **15 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  

Dieser Artikel ist Teil eines Lernprogramms zur tabellenmodellierung, das in Reihenfolge absolviert werden sollte. Vor dem Ausführen der Aufgaben in dieser Lektion, Sie sollten haben die vorherige Lektion abgeschlossen: [Lektion 9: Erstellen von Hierarchien](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md).  
  
## <a name="create-partitions"></a>Erstellen von Partitionen  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a>Zum Erstellen von Partitionen in der FactInternetSales-Tabelle  
  
1.  Erweitern Sie im tabellarischen Modell-Explorer **Tabellen**, und klicken Sie dann mit der rechten Maustaste **FactInternetSales** > **Partitionen**.  
  
2.  Klicken Sie im Partitions-Manager auf **Kopie**, und ändern Sie dann den Namen in **FactInternetSales2010**.
  
    Da die Partition nur die Zeilen innerhalb eines bestimmten Zeitraums für das Jahr 2010 eingeschlossen werden soll, müssen Sie den Abfrageausdruck ändern.
  
4.  Klicken Sie auf **Entwurf** Abfrage-Editor zu öffnen, und klicken Sie auf die **FactInternetSales2010** Abfrage.

5.  Klicken Sie in der Vorschau auf den Pfeil nach unten in der **OrderDate** Spaltenüberschrift, und klicken Sie dann auf **Datum/Uhrzeit-Filter** > **zwischen**.

    ![als-lesson10-Abfrage-editor](../tutorial-tabular-1400/media/as-lesson10-query-editor.png)

6.  Klicken Sie im Dialogfeld Filterzeilen im **Reihen anzeigen: OrderDate**, lassen Sie **ist nach oder gleich**, und geben Sie dann in das Feld Date **1/1/2010**. Lassen Sie die **und** Operator ausgewählt ist, wählen Sie dann **ist, bevor Sie**, geben Sie dann in das Feld Date **1/1/2011**, und klicken Sie dann auf **OK**.

    ![als-lesson10-Filter-Zeilen](../tutorial-tabular-1400/media/as-lesson10-filter-rows.png)
    
    Beachten Sie im Abfrage-Editor in ANGEWENDETE Schritte finden Sie einen weiteren Schritt mit dem Namen Zeilen gefiltert. Dieser Filter ist nur für die Bestelldaten 2010 aus.

8.  Klicken Sie auf **Importieren**.

    Im Partitions-Manager bemerkt haben, dass es sich bei der Abfrageausdruck jetzt zusätzliche Zeilen gefiltert Klausel hat.

    ![Abfrage als lesson10](../tutorial-tabular-1400/media/as-lesson10-query.png)
  
    Diese Anweisung gibt an, dass diese Partition nur die Daten in diesen Zeilen enthalten soll, in denen der OrderDate in Kalenderjahres 2010 wie in der gefilterten Rows-Klausel angegeben ist.  
  
  
#### <a name="to-create-a-partition-for-the-2011-year"></a>So erstellen Sie eine Partition für das Jahr 2011  
  
1.  Klicken Sie in der Liste auf die **FactInternetSales2010** Partitionieren Sie erstellt haben, und klicken Sie dann auf **Kopie**.  Ändern Sie den Partitionsnamen zu **FactInternetSales2011**. 

    Sie müssen keine Abfrage-Editor verwenden, um eine neue Klausel für gefilterten Zeilen zu erstellen. Alles, was Sie tun müssen, da Sie eine Kopie der Abfrage für 2010 erstellt haben, ist eine geringfügige Änderung in der Abfrage für 2011 vornehmen.
  
2.  In **Abfrageausdruck**, Reihenfolge für diese Partition, um nur die Zeilen für das Jahr 2011 enthalten, ersetzen Sie die Jahren in der Zeilen gefiltert-Klausel mit **2011** und **2012**, z. B.:  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="to-create-partitions-for-2012-2013-and-2014"></a>Zum Erstellen von Partitionen für 2012, 2013 und 2014.  
  
- Führen Sie die vorherigen Schritte, und Erstellen von Partitionen für 2012, 2013 und 2014, Ändern der Jahre in der Zeilen gefiltert-Klausel, um nur Zeilen für dieses Jahr einzuschließen. 
  

## <a name="delete-the-factinternetsales-partition"></a>Löschen Sie die FactInternetSales-partition

Nun, da Sie Partitionen für jedes Jahr haben, können Sie die FactInternetSales-Partition löschen; verhindert die Überlappung bei der Auswahl von Prozess alle beim Verarbeiten von Partitionen.

#### <a name="to-delete-the-factinternetsales-partition"></a>So löschen Sie die FactInternetSales-partition

-  Klicken Sie auf die **FactInternetSales** partitionieren, und klicken Sie dann auf **löschen**.



## <a name="process-partitions"></a>Partitionen verarbeiten  

Beachten Sie im Partitions-Manager die **letzten verarbeitet** Spalte für jede der neuen erstellten Partitionen zeigt diese Partitionen nie verarbeitet wurden. Wenn Sie Partitionen erstellen, sollten Sie einen Partitionsverarbeitungs- bzw. tabellenverarbeitungsvorgang aus, um die Daten dieser Partitionen zu aktualisieren ausführen.  
  
#### <a name="to-process-the-factinternetsales-partitions"></a>So verarbeiten Sie die FactInternetSales-Partitionen  
  
1.  Klicken Sie auf **OK** Partitions-Manager zu schließen.  
  
2.  Klicken Sie auf die **FactInternetSales** Tabelle, und klicken Sie auf die **Modell** Menü > **Prozess** > **Partitionen verarbeiten**.  
  
3.  Überprüfen Sie im Dialogfeld Partitionen verarbeiten **Modus** festgelegt ist, um **Standard verarbeiten**.  
  
4.  Aktivieren Sie das Kontrollkästchen in der Spalte **Verarbeiten** für jede der fünf von Ihnen erstellten Partitionen, und klicken Sie anschließend auf **OK**.  

    ![als-lesson10-Prozess-Partitionen](../tutorial-tabular-1400/media/as-lesson10-process-partitions.png)
  
    Wenn Sie für Identitätswechsel-Anmeldeinformationen aufgefordert werden, geben Sie den Windows-Benutzernamen und Kennwort an, das Sie in Lektion 2 angegeben.  
  
    Das Dialogfeld **Datenverarbeitung** wird daraufhin angezeigt. Es zeigt die Verarbeitungsdetails für jede Partition an. Beachten Sie, dass eine unterschiedliche Anzahl an Zeilen für jede Partition übertragen wird. Jede Partition enthält nur die Zeilen für das Jahr in der WHERE-Klausel in der SQL-Anweisung angegeben. Wenn die Verarbeitung abgeschlossen ist, fahren Sie fort und schließen Sie das Dialogfeld „Datenverarbeitung“.  
  
    ![als lesson10-Prozess-Vervollständigung](../tutorial-tabular-1400/media/as-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>Wie geht es weiter?

Wechseln Sie zur nächsten Lektion: [Lektion 11: Erstellen von Rollen](../tutorial-tabular-1400/as-lesson-11-create-roles.md). 
