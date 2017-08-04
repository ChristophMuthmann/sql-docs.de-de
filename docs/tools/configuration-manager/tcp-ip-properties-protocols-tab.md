---
title: TCP/IP-Eigenschaften (Registerkarte "Protokolle") | Microsoft Docs
ms.custom: 
ms.date: 08/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- TCP/IP [SQL Server], configuration options
ms.assetid: 007638fc-3a24-4460-adbe-545ded5d6f88
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c1a3d4995d3cc79f9a31533b918268f14204d511
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# TCP/IP-Eigenschaften (Registerkarte Protokoll)
  Verwenden Sie das Dialogfeld **TCP/IP-Eigenschaften** zum Konfigurieren der Optionen für das TCP/IP-Protokoll. Klicken Sie im linken Bereich auf **TCP/IP** , um die einzelnen IP-Adresskonfigurationen im Detailbereich anzuzeigen.  
  
 Microsoft SQL Server muss neu gestartet werden, damit die Änderungen in Kraft treten.  
  
## enthalten  
 **Enabled**  
 Mögliche Werte sind **Yes** und **No**.  
  
 **Keep Alive**  
 Geben Sie das Intervall (in Millisekunden) an, in dem Erhaltungspakete übertragen werden, die die Verfügbarkeit des Computers an der Remoteseite der Verbindung sicherstellen.  
  
 **Listen All**  
 Specify whether SQL Server will listen on all the IP addresses that are bound to network cards on the computer. Wenn für diese Option **Nein**festgelegt ist, müssen Sie jede IP-Adresse einzeln mithilfe des Dialogfeldes „Eigenschaften“ für jede IP-Adresse konfigurieren. Wenn für diese Option **Ja**festgelegt ist, gelten die Einstellungen des Eigenschaftenfeldes **IPAll** für alle IP-Adressen. Der Standardwert ist **Ja**.  
  
 **No Delay**  
 SQL Server implementiert keine Änderungen an dieser Eigenschaft.  
  
## Siehe auch  
 [Auswählen eines Netzwerkprotokolls](https://msdn.microsoft.com/library/ms187892(v=sql.130).aspx)   
 [Erstellen einer gültigen Verbindungszeichenfolge mithilfe von TCP / IP-](https://msdn.microsoft.com/library/ms191260.aspx)  
  
  

