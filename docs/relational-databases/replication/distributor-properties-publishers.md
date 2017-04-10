---
title: "Verteilereigenschaften (Verleger) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.configdistwizard.distproperties.publishers.f1"
helpviewer_keywords: 
  - "Verteilereigenschaften (Dialogfeld)"
ms.assetid: 31c81898-11ca-4d2f-afea-2fbc71e19ce4
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# Verteilereigenschaften (Verleger)
  Mithilfe der Seite **Verleger** des Dialogfelds **Verteilereigenschaften** können Sie es Verlegern ermöglichen, diesen Verteiler zu verwenden. Sie können auch zu diesen Verlegern gehörige Eigenschaften festlegen. Beachten Sie, dass dieser Server nicht zu einem Verleger wird, wenn Sie es einem Verleger ermöglichen, diesen Server als Verteiler zu verwenden. Sie müssen eine Verbindung mit dem Verleger herstellen, ihn für das Veröffentlichen konfigurieren und diesen Server als Verteiler auswählen. Sie können den Verleger konfigurieren und mithilfe des Assistenten für neue Veröffentlichung einen Verteiler auswählen.  
  
## Optionen  
 **Verleger**  
 Wählen Sie die Server aus, die diesen Verteiler verwenden dürfen. Klicken Sie auf die Schaltfläche Eigenschaften **(...)** neben einem Verleger, um zusätzliche Eigenschaften anzuzeigen und festzulegen.  
  
 **Hinzufügen**  
 Wenn der Server, die Sie zulassen möchten, nicht aufgeführt ist, klicken Sie auf **Hinzufügen** Hinzufügen eine [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Herausgeber oder Oracle-Verleger zur Liste der verfügbaren Verleger. Wenn der von Ihnen hinzugefügte Server der erste Server ist, der diesen Verteiler als Remoteverteiler verwendet, werden Sie aufgefordert, ein Kennwort für administrative Verbindungen einzugeben.  
  
 **Kennwort für administrative Verbindung**  
 Verwendung angeben oder aktualisieren, können das Kennwort für die Replikation für die Verbindung zwischen dem Verleger und dem Remoteverteiler mithilfe, der **Distributor_admin** Anmeldung:  
  
-   Wenn der Verteiler nur als lokaler Verteiler dient, wird dieses Kennwort per Zufallsgenerator erstellt und automatisch konfiguriert.  
  
-   Wenn der Verteiler bereits einen Remoteverleger besitzt, wurde ein Kennwort bereits ursprünglich auf dieser Seite oder auf der Seite **Verteilerkennwort** des Verteilungskonfigurations-Assistenten angegeben.  
  
-   Wenn Sie den ersten Remoteverleger für diesen Verleger aktivieren, werden Sie aufgefordert, ein Kennwort einzugeben.  
  
 Weitere Informationen zur Sicherheit für Verteiler finden Sie unter [Schützen des Verteilers](../../relational-databases/replication/security/secure-the-distributor.md).  
  
## Siehe auch  
 [Konfigurieren der Verteilung](../../relational-databases/replication/configure-distribution.md)   
 [Konfigurieren der Veröffentlichung und der Verteilung](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Erstellen einer Veröffentlichung](../../relational-databases/replication/publish/create-a-publication.md)   
 [Anzeigen und Ändern der Verteiler- und Verlegereigenschaften](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  