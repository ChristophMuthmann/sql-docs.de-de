---
title: "Objekte löschen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.deleteobjects.f1
helpviewer_keywords: Delete Objects dialog box
ms.assetid: 49541441-179c-40d3-ba0c-01bcae545984
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2f4fdde3b074596301e42cf557c8cfb641963b8e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="delete-objects"></a>Objekte löschen
In diesem Dialogfeld können Sie eine Datenbank oder ein Datenbankobjekt löschen.  
  
## <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
**Zu löschendes Objekt**  
Zeigt die Namen, Typen, Besitzer und den Status von zu löschenden Objekten sowie Fehlermeldungen während der Ausführung an.  
  
> [!NOTE]  
> Das Ausführen von **Löschen** für eine Datenbank entspricht der Verwendung von DROP DATABASE in [!INCLUDE[tsql](../../includes/tsql_md.md)].  
  
**Abhängigkeiten anzeigen**  
Klicken Sie hier, um sowohl die vom gerade ausgewählten Objekt abhängigen Objekte als auch die Objekte anzuzeigen, von denen das aktuelle Objekt abhängt (Aufwärts- und Abwärtsabhängigkeit). Die im Dialogfeld **Abhängigkeiten anzeigen** angezeigten Informationen sind schreibgeschützt.  
  
> [!NOTE]  
> Die Schaltfläche **Abhängigkeiten anzeigen** wird nicht für alle Datenbankobjekttypen angezeigt. Wenn Sie die Abhängigkeiten anzeigen möchten und die Schaltfläche **Abhängigkeiten anzeigen** nicht verfügbar ist, klicken Sie im Objekt-Explorer mit der rechten Maustaste auf das Objekt, und klicken Sie dann auf **Abhängigkeiten anzeigen**.  
  
**Sicherungs- und Wiederherstellungsverlaufsinformationen für Datenbanken löschen**  
Wird nur angezeigt, wenn eine Datenbank gelöscht wird. Bei Aktivierung dieses Kontrollkästchens wird der Sicherungs- und Wiederherstellungsverlauf für die betroffene Datenbank aus der **msdb** -Datenbank gelöscht.  
  
**Bestehende Verbindungen schließen**  
Wird nur angezeigt, wenn eine Datenbank gelöscht wird. Bei Aktivierung dieses Kontrollkästchens werden die Verbindungen zur betreffenden Datenbank beendet.  
  
