---
title: Clientprotokolle-Eigenschaften (Registerkarte Reihenfolge) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: configuration-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- client protocols [SQL Server]
ms.assetid: 64fd7135-1756-4885-bed9-9ab8997ecc6c
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5ae4db3ad7f7589fd95711dbe5667d1cc73d4164
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="client-protocols-properties-order-tab"></a>Eigenschaften der Clientprotokolle (Registerkarte Reihenfolge)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  Verwenden Sie die Seite **Reihenfolge** im Dialogfeld **Eigenschaften der Clientprotokolle**, um die Clientprotokolle anzuzeigen und zu aktivieren.  
  
 Klicken Sie auf ein Protokoll, und klicken Sie dann auf **Aktivieren** oder **Deaktivieren** , um das ausgewählte Protokoll in die Liste **Deaktivierte Protokolle** oder **Aktivierte Protokolle** zu verschieben.  
  
 Protokolle werden in der Reihenfolge verwendet, in der sie aufgelistet sind, wobei zunächst das erste Protokoll in der Liste, dann das zweite Protokoll usw. verwendet wird. Verschieben Sie Protokolle in der Liste **Aktivierte Protokolle** nach oben oder nach unten, indem Sie auf die Schaltfläche mit dem Aufwärtspfeil bzw. Abwärtspfeil klicken. Beim Herstellen einer Verbindung zu [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] von einem Client auf diesem Computer wird immer zuerst das **Shared Memory** -Protokoll versucht, falls dieses aktiviert ist.  
  
> [!NOTE]  
>  Diese Einstellungen werden nicht von [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET SqlClient verwendet. In der Protokollreihenfolge für .NET SqlClient steht TCP an der ersten Stelle, dann folgen Named Pipes. Dies kann nicht geändert werden.  
  
## <a name="options"></a>Tastatur  
 **Deaktivierte Protokolle**  
 Listet die Protokolle, die installiert sind, aber derzeit nicht verwendet.  
  
 **Aktivierte Protokolle**  
 Listet die Protokolle, die für die verfügbaren [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Clients auf diesem Computer.  
  
 **>**  
 Aktiviert das aktuell hervorgehobene Protokoll im Feld **Deaktivierte Protokolle** und verschiebt es in das Feld **Aktivierte Protokolle** .  
  
 **\<**  
 Deaktiviert das aktuell hervorgehobene Protokoll im Feld **Aktivierte Protokolle** und verschiebt es in das Feld **Deaktivierte Protokolle** .  
  
 Pfeil nach oben  
 Verschiebt das markierte Protokoll in der Liste nach oben. Damit wird die Priorität erhöht, nach der von der Netzwerkbibliothek versucht wird, das ausgewählte Protokoll für Verbindungen zu verwenden.  
  
 Pfeil nach unten  
 Verschiebt das markierte Protokoll in der Liste nach unten. Damit wird die Priorität herabgesetzt, nach der von der Netzwerkbibliothek versucht wird, das ausgewählte Protokoll für Verbindungen zu verwenden.  
  
 **Shared Memory-Protokoll aktivieren**  
 Aktiviert das Shared Memory-Protokoll. Dieses wird (falls aktiviert) immer zuerst herangezogen, wenn von einem Client eine Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] auf diesem Computer hergestellt wird.  
  
> [!NOTE]  
>  Wenn das Protokoll mithilfe eines Präfix oder als Teil der Verbindungszeichenfolge angegeben ist, wird nur das angegebene Protokoll versucht.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Auswählen eines Netzwerkprotokolls](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)  
  
  
