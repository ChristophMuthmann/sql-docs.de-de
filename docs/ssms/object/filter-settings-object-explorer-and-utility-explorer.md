---
title: Filtereinstellungen (Objekt-Explorer und Hilfsprogramm-Explorer) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-objects
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.common.filtersettings.f1
- sql13.ag.job.filtersettings.f1
ms.assetid: 4aab04bc-e1ab-4d4b-ab74-b287fc805bc2
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6ebfd7d638615b68d02da5b01c33ce4719cd162b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="filter-settings-object-explorer-and-utility-explorer"></a>Filtereinstellungen (Objekt-Explorer und Hilfsprogramm-Explorer)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Mithilfe dieses Dialogfelds können Sie einen Filter angeben. Mit einem Filter können Sie Objekt-Explorer und Hilfsprogramm-Explorer so konfigurieren, dass nur Elemente angezeigt werden, die bestimmte Kriterien erfüllen. So können Sie mit einem Filter beispielsweise nur Aufträge mit Namen anzeigen lassen, die das Wort "Wartung" enthalten. Die Kopfzeile für das Dialogfeld **Filtereinstellungen** enthält den Namen des Servers und kann den Namen der Datenbank enthalten.  
  
## <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
**Eigenschaft**  
Zeigt die Eigenschaft an, nach der gefiltert werden soll.  
  
**Ist gleich**  
Wählen Sie die Art aus, in der der Filter den Wert auf die Eigenschaft anwendet. Folgende Optionen stehen zur Verfügung:  
  
-   **Ist gleich**  
  
    Der Filter zeigt Elemente an, bei denen die Eigenschaft und der Wert genau übereinstimmen.  
  
-   **Enthält**  
  
    Der Filter zeigt die Elemente an, bei denen die Eigenschaft den Wert enthält. Die Eigenschaft kann noch weiteren Text enthalten.  
  
-   **Enthält nicht**  
  
    Der Filter zeigt die Elemente an, bei denen die Eigenschaft den Wert nicht enthält.  
  
-   **Kleiner als**  
  
    Verfügbar für Datumsangaben. Dieser Filter zeigt Elemente an, deren Datum vor dem eingegebenen Wert liegt.  
  
-   **Kleiner oder gleich**  
  
    Verfügbar für Datumsangaben. Dieser Filter zeigt Elemente an, deren Datum vor dem eingegebenen Wert liegt bzw. genau dem Wert entspricht.  
  
-   **Größer als**  
  
    Verfügbar für Datumsangaben. Dieser Filter zeigt Elemente an, deren Datum nach dem eingegebenen Wert liegt.  
  
-   **Größer oder gleich**  
  
    Verfügbar für Datumsangaben. Dieser Filter zeigt Elemente an, deren Datum nach dem eingegebenen Wert liegt bzw. genau dem Wert entspricht.  
  
-   **Zwischen**  
  
    Verfügbar für Datumsangaben. Dieser Filter zeigt Elemente an, deren Datum zwischen den eingegebenen Datumsangaben liegt. Wählen Sie **Zwischen** aus, und drücken Sie TAB, um eine weitere Zeile für die Eingabe des zweiten Datums hinzuzufügen.  
  
-   **Nicht zwischen**  
  
    Verfügbar für Datumsangaben. Dieser Filter zeigt Elemente an, deren Datum vor oder nach den beiden eingegebenen Datumsangaben liegt. Wählen Sie **Nicht zwischen** aus, und fügen Sie der **Operator** -Spalte mit TAB eine neue Zeile für die Eingabe des zweiten Datums hinzu.  
  
**ReplTest1**  
Geben Sie den Wert ein, mit dem die Eigenschaft verglichen werden soll. Bei Datumsangaben klicken Sie auf den nach unten zeigenden Pfeil, um einen Kalender für die Auswahl des Datums anzuzeigen.  
  
**Filter löschen**  
Entfernt alle aktuellen Filtereinstellungen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Verwenden von SQL Server Management Studio](../../ssms/use-sql-server-management-studio.md)  
[Übersicht über das SQL Server-Hilfsprogramm](http://msdn.microsoft.com/en-us/6e6cbd25-6b1c-4e21-9ade-4584e243fd8f)  
  
