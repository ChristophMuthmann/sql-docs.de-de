---
title: "Aktivieren, Deaktivieren und Löschen von Breakpoints | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: ssms
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 357b5874-273f-43a9-8e30-83872bdea5dc
caps.latest.revision: "5"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 38a596f36d68cc6efd8b21450aaddf5f0a293ab0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="enable-disable-and-delete-breakpoints"></a>Aktivieren, Deaktivieren und Löschen von Breakpoints
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Zum Anzeigen und Verwalten aller offenen Breakpoints können Sie das Fenster **Breakpoints** verwenden. Mithilfe des Fensters können Sie Informationen zu Breakpoints anzeigen und Aktionen ausführen, z. B. Löschen, Deaktivieren und Aktivieren von Breakpoints.  
  
## <a name="the-breakpoints-window"></a>Fenster "Breakpoints"  
 Das Fenster **Breakpoints** enthält Informationen, z. B. auf welcher Codezeile sich der Breakpoint befindet. Außerdem können Sie im Fenster **Breakpoints** Breakpoints löschen, deaktivieren und aktivieren. Weitere Informationen zum Fenster **Breakpoints** finden Sie unter [Breakpoints Window](../../relational-databases/scripting/transact-sql-debugger-breakpoints-window.md).  
  
 Durch das Deaktivieren von Breakpoints wird verhindert, dass der Breakpoint die Ausführung anhält, wobei die Definition jedoch beibehalten wird, falls Sie den Breakpoint später aktivieren möchten. Durch das Löschen von Breakpoints werden sie endgültig gelöscht. Sie müssen einen neuen Breakpoint umschalten, um die Ausführung für die Anweisung anzuhalten.  
  
## <a name="to-open-the-breakpoints-window"></a>So öffnen Sie das Fenster "Breakpoints"  
 **To open the Breakpoints window**  
  
 Zum Öffnen des Fensters **Breakpoints** haben Sie folgende Möglichkeiten:  
  
-   Klicken Sie im Menü **Debuggen** auf **Fenster**und dann auf **Breakpoints**.  
  
-   Klicken Sie auf der Symbolleiste **Debuggen** auf die Schaltfläche **Breakpoints** .  
  
-   Drücken Sie STRG+ALT+B.  
  
## <a name="to-disable-a-single-breakpoint"></a>So deaktivieren Sie einen einzelnen Breakpoint  
 **To disable a single breakpoint**  
  
 Sie können einen einzelnen Breakpoint folgendermaßen deaktivieren:  
  
-   Klicken Sie im Fenster „Abfrage-Editor“ mit der rechten Maustaste auf den Breakpoint, und klicken Sie anschließend auf **Breakpoint deaktivieren**.  
  
-   Deaktivieren Sie im Fenster "Breakpoints" das Kontrollkästchen links neben dem Breakpoint.  
  
## <a name="to-disable-all-breakpoints"></a>So deaktivieren Sie alle Breakpoints  
 **To disable all breakpoints**  
  
 Sie können alle Breakpoints folgendermaßen deaktivieren:  
  
-   Klicken Sie im Menü **Debuggen** auf **Alle Breakpoints deaktivieren**.  
  
-   Klicken Sie auf der Symbolleiste des Fensters **Breakpoints** auf die Schaltfläche **Alle Breakpoints deaktivieren** .  
  
## <a name="to-enable-a-single-breakpoint"></a>So aktivieren Sie einen einzelnen Breakpoint  
 **To enable a single breakpoint**  
  
 Sie können einen einzelnen Breakpoint folgendermaßen aktivieren:  
  
-   Klicken Sie im Fenster „Abfrage-Editor“ mit der rechten Maustaste auf den Breakpoint, und klicken Sie anschließend auf **Breakpoint aktivieren**.  
  
-   Aktivieren Sie im Fenster "Breakpoints" das Kontrollkästchen links neben dem Breakpoint.  
  
## <a name="to-enable-all-breakpoints"></a>So aktivieren Sie alle Breakpoints  
 **To enable all breakpoints**  
  
 Sie können alle Breakpoints folgendermaßen aktivieren:  
  
-   Klicken Sie im Menü **Debuggen** auf **Alle Breakpoints aktivieren**.  
  
-   Klicken Sie auf der Symbolleiste des Fensters **Breakpoints** auf die Schaltfläche **Alle Breakpoints aktivieren** .  
  
## <a name="to-delete-a-single-breakpoint"></a>So löschen Sie einen einzelnen Breakpoint  
 **To delete a single breakpoint**  
  
 Sie können einen einzelnen Breakpoint folgendermaßen löschen:  
  
-   Klicken Sie im Fenster „Abfrage-Editor“ mit der rechten Maustaste auf den Breakpoint, und klicken Sie anschließend auf **Breakpoint löschen**.  
  
-   Klicken Sie im Fenster „Breakpoints“ mit der rechten Maustaste auf den Breakpoint, und klicken Sie anschließend im Kontextmenü auf **Löschen** .  
  
-   Wählen Sie im Fenster "Breakpoints" den Breakpoint aus, und drücken Sie dann ENTF.  
  
## <a name="to-delete-all-breakpoints"></a>So löschen Sie alle Breakpoints  
 **To delete all breakpoints**  
  
 Sie können alle Breakpoints folgendermaßen löschen:  
  
-   Klicken Sie im Menü **Debuggen** auf **Alle Breakpoints löschen**.  
  
-   Klicken Sie auf der Symbolleiste des Fensters **Breakpoints** auf die Schaltfläche **Alle Breakpoints löschen** .  
  
## <a name="see-also"></a>Siehe auch  
 [Ein- und Ausschalten eines Breakpoints](../../relational-databases/scripting/toggle-a-breakpoint.md)  
  
  
