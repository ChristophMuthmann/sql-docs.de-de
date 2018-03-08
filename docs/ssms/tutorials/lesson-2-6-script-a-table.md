---
title: "Erstellen eines Skriptes für eine Tabelle | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ea88d736-849e-4368-b55d-06aeee097bf3
caps.latest.revision: "31"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c047fd16f30998d831977ae422b68d40ab50513b
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="lesson-2-6---script-a-table"></a>Lektion 2-6: Erstellen eines Skriptes für eine Tabelle
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] können Skripts für das Auswählen, Einfügen, Aktualisieren und Löschen von Tabellen und das Anlegen, Ändern, Löschen und Ausführen von gespeicherten Prozeduren erstellt werden.  
  
Möglicherweise benötigen Sie in einigen Fällen ein Skript mit mehreren Optionen, wie z. B. zum Löschen einer Prozedur und dann zum Anlegen einer Prozedur oder zum Anlegen einer Tabelle und dann zum Ändern einer Tabelle. Zum Anlegen kombinierter Skripts speichern Sie das erste Skript in einem Abfrage-Editorfenster und das zweite in der Zwischenablage, sodass Sie es im Fenster nach dem ersten Skript einfügen können.  
  
 
1.  Erweitern Sie im Objekt-Explorer Ihren Server, erweitern Sie **Datenbanken**, erweitern Sie [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]und **Tabellen**, klicken Sie mit der rechten Maustaste auf **HumanResources.Employee**, und zeigen Sie anschließend auf **Skript für Tabelle als**.  
  
2.  Das Kontextmenü umfasst sieben Optionen für Skripts: **CREATE in**, **DROP in**, **DROP und CREATE in**, **SELECT in**, **INSERT in**, **UPDATE in**und **DELETE in**. Zeigen Sie auf **UPDATE in**, und klicken Sie dann auf **Neues Abfrage-Editorfenster**.  
  
3.  Ein neues Abfrage-Editorfenster wird geöffnet, eine Verbindung wird hergestellt, und die gesamte Update-Anweisung wird angezeigt.  
  
    Diese Übung zeigt Ihnen, dass die Funktion zur Skripterstellung mehr bietet als das Schreiben eines Skripts zum Anlegen einer Tabelle oder gespeicherten Prozedur. Diese neue Funktion unterstützt Sie, wenn Sie Ihrem Projekt schnell Skripts für Datenänderungen hinzufügen möchten. Es hilft Ihnen beim einfachen Erstellen von Skripts für die Ausführung gespeicherter Prozeduren. So können Sie in vielen Bereichen viel Zeit bei der Arbeit mit Tabellen und Prozeduren sparen.  
  
 
  
  
  
