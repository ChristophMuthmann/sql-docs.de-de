---
title: "Änderungsskript speichern (Dialogfeld) (Visual Database Tools) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdt.dlgbox.generatechangescript
- vdtsql.chm:65544
ms.assetid: fc9d1639-5efa-44fe-a04f-4d4d0def2833
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5a10e76496a5dfcb781c6153cfb787b6e3232de1
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="save-change-script-dialog-box-visual-database-tools"></a>Änderungsskript speichern (Dialogfeld) (Visual Database Tools)
Dieses Dialogfeld zeigt das [!INCLUDE[tsql](../../includes/tsql_md.md)] -Skript für die Änderungen an, die Sie seit der letzten Speicherung der Tabelle vorgenommen haben. Außerdem können Sie in diesem Dialogfeld das Skript an einem auszuwählenden Speicherort als Textdatei speichern.  
  
Sie können auf dieses Dialogfeld nach dem Vornehmen nicht gespeicherter Änderungen einer Tabelle im Tabellen-Designer zugreifen. Klicken Sie im Menü **Tabellen-Designer** auf **Änderungsskript generieren**.  
  
> [!NOTE]  
> Änderungsskripts, die von Visual Database Tools zur Verfügung gestellt werden, enthalten keine Fehlerbehandlung. Dabei wird angenommmen, dass seit dem Öffnen des Tools keine Datenbankobjekte geändert wurden, und dass deshalb keine änderungsbezogenen Probleme auftreten werden. Vor dem Ausführen des Änderungsskripts sollten Sie die entsprechenden Fehlerbehandlungsanweisungen einschließen.  
  
## <a name="options"></a>enthalten  
**Änderungsskript automatisch nach jedem Speichern erstellen**  
Ist dieses Kontrollkästchen aktiviert, wird das Dialogfeld **Änderungsskript speichern** jedes Mal angezeigt, wenn Sie Änderungen an einer Tabelle speichern.  
  
**Ja**  
Öffnen Sie das Dialogfeld **Speichern** , mit dem Sie den Speicherort für die Textdatei auswählen können.  
  
**Nein**  
Brechen Sie die Erstellung des Änderungsskripts ab.  
  
