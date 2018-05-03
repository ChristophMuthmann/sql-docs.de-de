---
title: Anzeigen des Cubeschemas | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8e6ff9162eb9a72596b3f5dc43ef86cd00d287e4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="view-the-cube-schema"></a>Anzeigen des Cubeschemas
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Im **Cube-Designer** auf der Registerkarte **Cubestruktur** im Bereich **Datenquellensicht** wird das Cubeschema angezeigt. Das Schema entspricht der Tabellengruppe, aus der die Measures und Dimensionen für einen Cube abgeleitet werden. Jedes Cubeschema besteht aus mindestens einer Faktentabelle und Dimensionstabelle, auf denen die Measures und Dimensionen im Cube basieren.  
  
 Auf der Registerkarte **Cubestruktur** im Bereich **Datenquellensicht** wird ein Diagramm der Datenquellensicht angezeigt, die die Grundlage für den Cube bildet. Dieses Diagramm stellt eine Teilmenge des Hauptdiagramms der Datenquellensicht dar. Im Bereich **Datenquellensicht** können Tabellen ein- und ausgeblendet und beliebige vorhandene Diagramme angezeigt werden. Änderungen am zugrunde liegenden Schema (z. B. durch Hinzufügen neuer Beziehungen oder benannter Abfragen) sind jedoch nicht möglich. Um Änderungen am Schema vorzunehmen, verwenden Sie den Datenquellensicht-Designer.  
  
 Wenn Sie einen Cube erstellen, ist das im Bereich **Datenquellensicht** auf der Registerkarte **Cubestruktur** angezeigte Diagramm anfänglich identisch mit dem Diagramm **Alle Tabellen anzeigen** in der Datenquellensicht für das Projekt oder die Datenbank. Sie können dieses Diagramm durch jedes vorhandene Diagramm in der Datenquellensicht ersetzen und im Bereich **Datenquellensicht** Anpassungen vornehmen.  
  
 Während Sie das Diagramm im **Cube-Designer**bearbeiten, sind im Menü **Datenquellensicht** Befehle verfügbar, die auf die Registerkarte oder auf beliebige ausgewählte Objekte auf der Registerkarte angewendet werden. Sie können auch mit der rechten Maustaste auf den Diagrammhintergrund oder auf ein Objekt im Diagramm klicken, um Befehle für das Diagramm oder ausgewählte Objekt auszuführen. Folgende Aktionen sind möglich:  
  
-   Umschalten zwischen Diagramm- und Strukturformat.  
  
-   Anordnen, Suchen, Anzeigen und Ausblenden von Tabellen.  
  
-   Anzeigen von Anzeigenamen.  
  
-   Umschalten zwischen Layouts.  
  
-   Ändern der Vergrößerung.  
  
-   Anzeigen von Eigenschaften.  
  
 Darüber hinaus können Sie die in der folgenden Tabelle aufgeführten Aktionen ausführen:  
  
|Aktion|Aktion|  
|--------|-------------|  
|Verwenden eines Diagramms aus der Datenquellensicht des Cubes|Zeigen Sie im Menü **Datenquellensicht** auf **Diagramm kopieren von**, und klicken Sie dann auf das Diagramm für die Datenquellensicht, das Sie verwenden möchten.<br /><br /> - oder -<br /><br /> Klicken Sie mit der rechten Maustaste auf den Hintergrund des Bereichs **Datenquellensicht** , zeigen Sie auf **Diagramm kopieren von**, und klicken Sie dann in der Datenquellensicht auf das gewünschte Diagramm. Da durch diese Methode eine unabhängige Kopie des Diagramms erstellt wird, werden Änderungen, die Sie auf der Registerkarte **Cube-Generator** vornehmen, im ursprünglichen Diagramm nicht angezeigt.|  
|Ausschließliches Anzeigen der im Cube verwendeten Tabellen|Klicken Sie im Menü **Datenquellensicht** auf **Nur verwendete Tabellen anzeigen**.<br /><br /> - oder -<br /><br /> Klicken Sie mit der rechten Maustaste auf den Hintergrund des Bereichs **Datenquellensicht** , und klicken Sie dann auf **Nur verwendete Tabellen anzeigen**.|  
|Bearbeiten des Schemas der Datenquellensicht|Klicken Sie im Menü **Datenquellensicht** auf **Datenquellensicht bearbeiten**.<br /><br /> - oder -<br /><br /> Klicken Sie mit der rechten Maustaste auf den Hintergrund des Bereichs **Datenquellensicht** , und klicken Sie dann auf **Datenquellensicht bearbeiten**.|  
  
  
