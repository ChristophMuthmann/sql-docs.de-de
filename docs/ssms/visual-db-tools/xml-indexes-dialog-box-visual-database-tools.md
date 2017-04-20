---
title: "Dialogfeld „XML-Indizes“ (Visual Database Tools) | Microsoft-Dokumentation"
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
- vdt.dlgbox.xmlindexes
ms.assetid: eef38310-4498-4ccc-bb77-5bbd1c7cc477
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 88cb1d98e64580b53af2587c431430d91615d0b6
ms.lasthandoff: 04/11/2017

---
# <a name="xml-indexes-dialog-box-visual-database-tools"></a>XML-Indizes (Dialogfeld) (Visual Database Tools)
Verwenden Sie das Dialogfeld **XML-Indizes**, um Indizes für Spalten vom Datentyp XML zu erstellen, denn diese können nicht mithilfe des Dialogfelds **Index/Schlüssel** indiziert werden. Jede XML-Spalte kann mehrere XML-Indizes aufweisen, aber der zuerst erstellte Index (der primäre Index) bildet die Basis für alle weiteren Indizes (die sekundären Indizes). Wenn Sie den primären XML-Index löschen, werden auch die sekundären Indizes gelöscht.  
  
## <a name="options"></a>enthalten  
**Ausgewählter XML-Index**  
Listet vorhandene XML-Indizes auf. Wird ausgewählt, um die zugehörigen Eigenschaften im rechten Datenblatt anzuzeigen. Falls die Liste leer ist, sind für die Tabelle Indizes definiert worden.  
  
**Hinzufügen**  
Erstellen Sie einen neuen XML-Index.  
  
**Delete**  
Löschen Sie den in der Liste **Ausgewählter XML-Index** ausgewählten XML-Index. Beim Löschen des primären XML-Indexes wird eine Meldung ausgegeben, dass dadurch auch alle sekundären Indizes gelöscht werden, und Sie können entweder den Vorgang fortsetzen oder die Aktion abbrechen.  
  
**Kategorie Allgemein**  
Wenn die Kategorie erweitert ist, werden die Eigenschaftenfelder für **Spalten**, **Ist Primary**und **Typ**angezeigt.  
  
**Spalten**  
Zeigt an, dass dieser Index in aufsteigender Reihenfolge sortiert ist.  
  
**Ist Primary**  
Gibt an, ob dies der primäre Index ist. Der erste für die Spalte erstellte XML-Index stellt die Basis für die anderen Indizes dar.  
  
**Primärverweisname**  
Zeigt für einen sekundären Index den Namen des primären Indexes an. Nur verfügbar, wenn es sich um einen sekundären Index handelt.  
  
**Sekundärer Typ**  
Zeigt den Typ des sekundären Indexes an. Nur verfügbar, wenn es sich um einen sekundären Index handelt.  
  
**Typ**  
Zeigt an, dass dies ein XML-Index ist.  
  
**Kategorie Identität**  
Wenn die Kategorie erweitert ist, werden die Eigenschaftenfelder für **Name** und **Beschreibung** angezeigt.  
  
**Name**  
Zeigt den Namen des XML-Indexes an. Wenn ein neuer Index erstellt wird, erhält dieser einen Standardnamen, der auf der Tabelle im aktiven Fenster des Tabellen-Designers basiert. Sie können den Namen jederzeit ändern.  
  
**Beschreibung**  
Beschreiben Sie den Index. Klicken Sie zum Erstellen einer detaillierteren Beschreibung auf **Beschreibung** , und klicken Sie dann auf die Schaltfläche mit den Auslassungspunkten (**…**) rechts neben dem Eigenschaftenfeld. Dadurch wird ein größerer Bereich verfügbar, in den Sie Text eingeben können.  
  
**Kategorie Tabellen-Designer**  
Wenn die Kategorie erweitert ist, werden Informationen zu den Eigenschaften dieses XML-Indexes angezeigt.  
  
**Füllspezifikation**  
Wenn dieses Element erweitert ist, werden Informationen für **Füllfaktor** und **Index mit Leerstellen auffüllen**angezeigt.  
  
**Füllfaktor**  
Geben Sie an, zu welchem Prozentsatz die Indexseite vom System gefüllt werden kann. Sobald eine Seite gefüllt ist, müssen beim Hinzufügen neuer Daten die Seite vom System geteilt werden, wobei die Leistung beeinträchtigt wird.  
  
-   Ein Wert von 100 bedeutet, dass die Seiten gefüllt werden. Diese Einstellung erfordert den geringsten Aufwand an Speicherplatz, ist aber auch am wenigsten effektiv. Diese Einstellung sollte nur verwendet werden, wenn keine Änderungen an den Daten vorgenommen werden, zum Beispiel in einer schreibgeschützten Tabelle.  
  
-   Durch einen niedrigeren Wert bleibt auf den Datenseiten ein größerer Bereich leer. Dadurch müssen die Datenseiten seltener geteilt werden, wenn Indizes größer werden. Dies erfordert allerdings mehr Speicherplatz. Diese Einstellung empfiehlt sich eher, wenn Änderungen an den Daten in der Tabelle vorgenommen werden.  
  
**Index mit Leerstellen auffüllen**  
Stellen Sie Seiten in diesem Index mit demselben Prozentsatz leeren Platzes (Auffüllung) zur Verfügung, wie in **Füllfaktor**angegeben.  
  
**Ist deaktiviert**  
Geben Sie an, ob der Index deaktiviert ist. Deaktivierte Indizes unterstützen weder Suchvorgänge noch werden sie aktualisiert, wenn der Tabelle neue Elemente hinzugefügt werden. Sie können die Leistung für Masseneinfügungen und -updates verbessern, indem Sie einen Index deaktivieren.  
  
**Seitensperren sind zulässig**  
Geben Sie an, ob Sperren auf Seitenebene für diesen Index zugelassen sind. Das Zulassen oder Untersagen von Sperren auf Seitenebene wirkt sich auf die Datenbankleistung aus.  
  
**Statistiken neu berechnen**  
Berechnen Sie beim Erstellen des Indexes neue Statistiken. Durch das Neuberechnen von Statistiken wird die Erstellung der Indizes verlangsamt, die Abfrageleistungen werden allerdings verbessert.  
  
**Zeilensperren sind zulässig**  
Geben Sie an, ob das Sperren auf Zeilenebene für diesen Index zugelassen ist. Das Zulassen oder Untersagen von Sperren auf Zeilenebene wirkt sich auf die Datenbankleistung aus.  
  
## <a name="see-also"></a>Siehe auch  
[Erstellen von XML-Indizes](http://msdn.microsoft.com/en-us/6ecac598-355d-4408-baf7-1b2e8d4cf7c1)  
  

