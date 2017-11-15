---
title: "Wartungsplan (Dialogfeld „Berichterstellung und Protokollierung“) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.maint.reportinglogging.f1
ms.assetid: 3a30b17a-3deb-446f-900a-62f88934a90f
caps.latest.revision: "22"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b94a7b05ebe694c668bfb9e8763e1be479cddf51
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="maintenance-plan-reporting-and-logging-page"></a>Wartungsplan (Dialogfeld 'Berichterstellung und Protokollierung')
  Mit dem Dialogfeld **Berichterstellung und Protokollierung** können Sie die Berichte und Protokolle konfigurieren, die beim Ausführen von Wartungsplänen generiert werden.  
  
## <a name="options"></a>Optionen  
 **Textdateibericht generieren**  
 Geben Sie an, ob von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein Textdateibericht geschrieben werden soll.  
  
 **Neue Datei erstellen**  
 Erstellt eine neue Berichtsdatei für jede Ausführung des Wartungsplans. Standardmäßig werden die Berichtsdateien auf den Computer geschrieben, der als Host der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fungiert, die diesen Wartungsplan enthält. Die Dateien werden in dem während des Setups von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] festgelegten Standardprotokollordner gespeichert. Wenn Sie einen anderen Ordner angeben möchten, geben Sie im Textfeld **Ordner** den vollständigen Ordnerpfad ein, oder klicken Sie auf die Schaltfläche zum Durchsuchen (**...**), und navigieren Sie zum gewünschten Ordner.  
  
 **An Datei anfügen**  
 Fügt die jeweiligen Berichte der einzelnen Planausführungen an die Datei an, die im Textfeld **Dateiname** angegeben wurde. Sie können auch eine Datei angeben, indem Sie auf die Schaltfläche zum Durchsuchen klicken und im angezeigten Dialogfeld eine Datei auswählen.  
  
 **Bericht an einen E-Mail-Empfänger senden**  
 Übermittelt das Ergebnis einer Wartungsplanausführung per E-Mail. Diese Option ist nur verfügbar, wenn Datenbank-E-Mail aktiviert und ordnungsgemäß konfiguriert ist.  
  
 **Agentoperator**  
 Wählen Sie einen Agentoperator aus der Liste aus, der als E-Mail-Empfänger festgelegt werden soll. Diese Option ist nur verfügbar, wenn Datenbank-E-Mail aktiviert und ordnungsgemäß konfiguriert ist.  
  
 **Erweiterte Informationen protokollieren**  
 Mit dieser Option enthält das Protokoll mehr Informationen. Durch Verwenden dieser Option wird der gespeicherte Wartungsplanverlauf umfangreicher.  
  
 **Auf Remoteserver protokollieren**  
 Protokolliert den Wartungsplanverlauf auf einem Remoteserver.  
  
 **Verbindung**  
 Gibt die Verbindungsinformationen an, die beim Protokollieren auf einem Remoteserver verwendet werden sollen.  
  
 **Neu**  
 Zeigt das Dialogfeld **Verbindungseigenschaften** an. Dient dem Konfigurieren neuer Verbindungsinformationen zum Protokollieren auf einem Remoteserver.  
  
## <a name="see-also"></a>Siehe auch  
 [Wartungspläne](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Datenbank-E-Mail](../../relational-databases/database-mail/database-mail.md)  
  
  
