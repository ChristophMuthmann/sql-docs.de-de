---
title: 'Analysis Services Tutorial Lektion 3: Markieren als Datumstabelle | Microsoft Docs'
description: Beschreibt die Vorgehensweise beim Markieren einer Date-Tabelle in der Analysis Services Tutorial-Projekt.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
ms.openlocfilehash: b747791b4e33683c2eaad73b3d19d80e7c10f601
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2018
---
# <a name="mark-as-date-table"></a>Als Datumstabelle markieren

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In Lektion 2: Abrufen von Daten, Sie importiert eine Dimensionstabelle, die mit dem Namen **DimDate**. Während in Ihrem Modell in dieser Tabelle DimDate heißt, sie können auch bekannt sein als eine *Datumstabelle*, insofern, dass es sich um Datums-und Uhrzeitdaten enthält.  
  
Wenn Sie DAX-zeitintelligenzfunktionen verwenden, z. B. Wenn Sie später Measures erstellen müssen, geben Sie Eigenschaften darunter ein *Datumstabelle* und einen eindeutigen Bezeichner *Datumsspalte* in dieser Tabelle.
  
In dieser Lektion kennzeichnen Sie die **DimDate** als Tabelle der *Datumstabelle* und die **Datum** Spalte (in der Date-Tabelle) als die *Datumsspalte* (eindeutig Bezeichner).  

Bevor Sie die Datumstabelle und Datumsspalte kennzeichnen, ist es ein guter Zeitpunkt, führen Sie ein wenig Housekeeping um Ihr Modell um verständlicher zu machen. Beachten Sie in der Tabelle DimDate eine Spalte mit dem Namen **FullDateAlternateKey**. Diese Spalte enthält eine Zeile für jeden Tag in jedes Kalenderjahr in der Tabelle enthalten. Sie verwenden diese Spalte viel in measureformeln und in Berichten. Allerdings FullDateAlternateKey ist eigentlich eine gute Bezeichner für diese Spalte. Sie benennen Sie sie um **Datum**, leichter zu identifizieren und in Formeln enthalten. Wann immer möglich, ist es eine gute Idee, Umbenennen von Objekten wie Tabellen und Spalten, um sie zu vereinfachen, SSDT und Clientanwendungen zur berichterstellung zu ermitteln. 
  
Geschätzte Zeit zum Abschließen dieser Lektion: **drei Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  

Dieser Artikel ist Teil eines Lernprogramms zur tabellenmodellierung, das in Reihenfolge absolviert werden sollte. Vor dem Ausführen der Aufgaben in dieser Lektion, Sie sollten haben die vorherige Lektion abgeschlossen: [Lektion 2: Abrufen von Daten](../tutorial-tabular-1400/as-lesson-2-get-data.md). 

### <a name="to-rename-the-fulldatealternatekey-column"></a>Umbenennen der FullDateAlternateKey-Spalte

1.  Klicken Sie im Modell-Designer auf die **DimDate** Tabelle.

2.  Doppelklicken Sie auf die Header für die **FullDateAlternateKey** Spalte, und benennen Sie sie um **Datum**.

  
### <a name="to-set-mark-as-date-table"></a>So legen Sie "Als Datumstabelle markieren" fest  
  
1.  Wählen Sie die **Datum** -Spalte und stellen Sie anschließend im Fenster **Eigenschaften** unter **Datentyp**sicher, dass  **Datum** ausgewählt ist.  
  
2.  Klicken Sie im Menü **Tabelle** auf **Datum**und anschließend auf **Als Datumstabelle markieren**.  
  
3.  Wählen Sie im Dialogfeld **Als Datumstabelle markieren** im Listenfeld **Datum** die Spalte **Datum** als eindeutigen Bezeichner aus. Es ist in der Regel standardmäßig aktiviert. Klicken Sie auf **OK**. 

    ![als-lesson3-Date-Tabelle](../tutorial-tabular-1400/media/as-lesson3-date-table.png)
  

## <a name="whats-next"></a>Wie geht es weiter?

[Lektion 4: Erstellen von Beziehungen](../tutorial-tabular-1400/as-lesson-4-create-relationships.md).
  
