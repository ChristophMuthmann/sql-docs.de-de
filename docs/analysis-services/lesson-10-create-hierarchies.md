---
title: "Lektion 10: Erstellen von Hierarchien | Microsoft Docs"
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
ms.assetid: 1e2561d3-4890-4495-a9cd-84eb88508938
caps.latest.revision: 23
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Lektion 10: Erstellen von Hierarchien
In dieser Lektion erstellen Sie Hierarchien. Hierarchien sind Gruppen von Spalten, die in Ebenen angeordnet werden. Beispielsweise könnte eine Geografiehierarchie Unterebenen für Land, Status, Landkreis und Stadt beinhalten. Hierarchien können getrennt von anderen Spalten in der Feldliste einer Clientanwendung zur Berichtserstellung angezeigt werden, sodass Clientbenutzer einfacher darin navigieren und sie in einen Bericht aufnehmen können. Weitere Informationen finden Sie unter [Hierarchien &#40;SSAS – tabellarisch&#41;](../analysis-services/tabular-models/hierarchies-ssas-tabular.md).  
  
Verwenden Sie zum Erstellen von Hierarchien den Modell-Designer in der *Diagrammsicht*. Das Erstellen und Verwalten von Hierarchien in der Datensicht des Modell-Designers wird nicht unterstützt.  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **20 Minuten**  
  
## Erforderliche Komponenten  
Dieses Thema ist Teil eines Lernprogramms zur Tabellenmodellierung, das in der entsprechenden Reihenfolge bearbeitet werden sollte. Sie sollten vor dem Ausführen der Aufgaben in dieser Lektion die vorherige, [Lektion 9: Erstellen von Perspektiven](../Topic/Lesson%209:%20Create%20Perspectives.md), abgeschlossen haben.  
  
## Erstellen von Hierarchien  
  
#### So erstellen Sie in der Product-Tabelle eine Kategoriehierarchie  
  
1.  Klicken Sie im Modell-Designer auf das Menü **Modell**, zeigen Sie auf **Modellansicht**, und klicken Sie anschließend auf **Diagrammsicht**.  
  
  
  
2.  Klicken Sie mit der rechten Maustaste auf die Tabelle **Produkt** und anschließend auf **Hierarchie erstellen**. Eine neue Hierarchie wird am unteren Rand des Tabellenfensters angezeigt.  
  
3.  Benennen Sie im Bereich für den Hierarchienamen die Hierarchie um, indem Sie **Category** (Kategorie) eingeben und anschließend die EINGABETASTE drücken.  
  
4.  Klicken Sie in der Tabelle **Product** auf die Spalte **Product Category Name** (Name der Produktkategorie), ziehen Sie sie in die Hierarchie **Category**, und legen Sie sie anschließend oberhalb des Namens **Category** ab.  
  
5.  Klicken Sie in der Hierarchie **Category** mit der rechten Maustaste auf die Spalte **Product Category Name**, klicken Sie auf **Umbenennen**, und geben Sie anschließend **Category** ein.  
  
    > [!NOTE]  
    > Durch das Umbenennen einer Spalte in einer Hierarchie wird die betreffende Spalte in der Tabelle nicht umbenannt. Eine Spalte in einer Hierarchie ist nur eine Darstellung der Spalte in der Tabelle.  
  
6.  Klicken Sie in der Tabelle **Product** auf die Spalte **Product Subcategory Name** (Name der Produktunterkategorie), und ziehen Sie sie in die Hierarchie **Category**.  
  
7.  Benennen Sie **Product Subcategory Name** in **Subcategory** um.  
  
8.  Klicken Sie auf die Spalten **Model Name** (Modellname) und **Product Name** (Produktname) (in dieser Reihenfolge), und ziehen Sie die Spalten in den Bereich unterhalb der Spalte **Product Subcategory Name**. Benennen Sie die jeweiligen Spalten in **Model** und **Product** um.  
  
#### So erstellen Sie Hierarchien in der Date-Tabelle  
  
1.  Klicken Sie im Modell-Designer mit der rechten Maustaste auf die Tabelle **Date** und anschließend auf **Hierarchie erstellen**.  
  
2.  Benennen Sie die Hierarchie in **Calendar** (Kalender) um.  
  
3.  Fügen Sie die folgenden Spalten in der entsprechenden Reihenfolge hinzu, und benennen Sie sie dann um:  
  
    |Column|Umbenennen in:|  
    |----------|--------------|  
    |Calendar Year|Year|  
    |Calendar Semester|Semester|  
    |Calendar Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
4.  Wiederholen Sie in der Tabelle **Date** die oben genannten Schritte, und erstellen Sie die Hierarchie **Fiscal**, einschließlich der folgenden Spalten:  
  
    |Column|Umbenennen in:|  
    |----------|--------------|  
    |Fiscal Year|Year|  
    |Fiscal Semester|Semester|  
    |Fiscal Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
5.  Wiederholen Sie abschließend in der Tabelle **Date** die oben genannten Schritte, und erstellen Sie die Hierarchie **Production Calendar** (Produktionskalender), einschließlich der folgenden Spalten:  
  
    |Column|Umbenennen in:|  
    |----------|--------------|  
    |Calendar Year|Year|  
    |Week Number Of Year|Week|  
    |Day Of Week|Day|  
  
## Nächste Schritte  
Wenn Sie mit diesem Tutorial fortfahren möchten, wechseln Sie zur nächsten Lektion: [Lektion 11: Erstellen von Partitionen](../analysis-services/lesson-11-create-partitions.md).  
  
  
  
