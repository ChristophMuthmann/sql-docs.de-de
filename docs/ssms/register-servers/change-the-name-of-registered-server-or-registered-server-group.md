---
title: "Ändern des Namens eines registrierten Servers bzw. einer registrierte Servergruppe | Microsoft-Dokumentation"
ms.custom: 
ms.date: 08/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying registered server or server group names
- server groups [SQL Server]
- Registered Servers [SQL Server], names
- renaming registered server or server group
- names [SQL Server], registered server or server group
ms.assetid: 10e1546b-9edb-400c-8676-2ea1192d6134
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 5db067d5a2fe5bbf9953484c9a999ed7b1fcddae
ms.openlocfilehash: b99eea0ee5988ce791948c2fa7340271b74e7ec4
ms.contentlocale: de-de
ms.lasthandoff: 07/31/2017

---
# <a name="change-the-name-of-registered-server-or-registered-server-group"></a>Ändern des Namens eines registrierten Servers oder einer Servergruppe
  In diesem Thema wird beschrieben, wie Sie den Namen eines registrierten Servers oder einer Servergruppe mithilfe von [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ändern. Dieser Name kann jedoch jederzeit geändert werden. Bei einer Änderung des Namens eines registrierten Servers wird nur die Anzeige des Namens geändert. Um die Verbindung zu einem anderen Server herzustellen, müssen Sie die Verbindungseigenschaften des registrierten Servers bearbeiten.  
  
##  <a name="SSMSProcedure"></a> Verwendung von SQL Server Management Studio  
Navigieren Sie über das Menü zu **Ansicht\\Registrierte Server**, um den Bereich **Registrierte Server** zu öffnen.  
#### <a name="to-change-the-name-of-a-server"></a>So ändern Sie den Namen eines Servers  
  
1.  Erweitern Sie in **Registrierte Server**die Option **Datenbankmodul** und anschließend **Lokale Servergruppen**.  

2.  Klicken Sie mit der rechten Maustaste zum Auswählen auf **Eigenschaften** , um das Dialogfeld **Serverregistrierungseigenschaften bearbeiten** zu öffnen.
  
3.  Geben Sie im Textfeld **Name des registrierten Servers** den neuen Namen für die Serverregistrierung ein, und klicken Sie anschließend auf **Speichern**.  
  
#### <a name="to-change-the-name-of-a-server-group"></a>So ändern Sie den Namen einer Servergruppe  
  
1.  Erweitern Sie in **Registrierte Server**die Option **Datenbankmodul** und anschließend **Lokale Servergruppen**.  

2.  Klicken Sie mit der rechten Maustaste auf eine Servergruppe, und wählen Sie **Eigenschaften** aus, um das Dialogfeld **Servergruppeneigenschaften bearbeiten** zu öffnen. 
  
3.  Geben Sie im Textfeld **Gruppenname** den neuen Namen für die Servergruppe ein, und klicken Sie anschließend auf **Speichern**.  
  
## <a name="see-also"></a>Siehe auch  
 [Ändern der Registrierung eines Servers &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/change-a-server-s-registration-sql-server-management-studio.md)  
  
  

