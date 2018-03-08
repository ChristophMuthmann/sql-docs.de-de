---
title: "Vorbereiten von SQL Server für CDC | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a327fa18-58f4-4e69-bb87-44faf47e20ef
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d48e2cd3e7c8d8c97b3b18f514a481696dabad6c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="how-to-prepare-sql-server-for-cdc"></a>Vorbereiten von SQL Server für CDC
  Der Oracle CDC Service erfordert, dass alle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zielinstanzen die MSXDBCDC-Datenbank enthalten. Sie erstellen diese Datenbank mithilfe der Aktion Prepare SQL Server in der CDC Service Configuration Console. Dieser Task wird für jede [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zielinstanz nur einmal ausgeführt.  
  
 Unten wird beschrieben, wie Sie eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank mithilfe der CDC Service Configuration Console auf Oracle Change Data Capture vorbereiten. Bei diesem Prozess wird die MSXDBCDC-Datenbank erstellt, und die erforderlichen Tabellen, gespeicherten Prozeduren und anderen erforderlichen Artefakte werden definiert.  
  
 Das Vorbereiten von SQL Server for Oracle CDC wird vom Oracle CDC Service-Administrator durchgeführt. Weitere Informationen zur Rolle des CDC Service-Administrators finden Sie unter [User Roles](../../integration-services/change-data-capture/user-roles.md).  
  
### <a name="to-enable-sql-server-for-cdc"></a>So aktivieren Sie SQL Server für CDC  
  
1.  Wählen Sie im Menü **Start** die Option **CDC Service Configuration for Oracle**.  
  
2.  Wählen Sie im linken Bereich die Option **Local CDC Services** , und klicken Sie dann im **Aktionsbereich** auf **Prepare SQL Server**.  
  
     Sie können auch mit der rechten Maustaste auf **Local CDC Services** (Lokale CDC-Dienste) klicken und **Prepare SQL Server**(SQL Server vorbereiten) auswählen.  
  
3.  Geben Sie die erforderlichen Informationen im Dialogfeld Preparing SQL Server Instance for Oracle CDC ein. Informationen zum Eingeben der erforderlichen Informationen in dieses Dialogfeld finden Sie unter [Prepare SQL Server for CDC](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md).  
  
     Um die SQL Server-Instanz für Oracle CDC vorzubereiten, muss die Anmeldung über die Schreibberechtigung für die MSXDBCDC-Datenbank verfügen. Geben Sie die Anmeldeinformationen für eine Anmeldung ein, die über die Schreibberechtigung für die MSXDBCDC-Datenbank verfügt, z. B. als Mitglied der Rolle `sysasmin` .  
  
 **Hinweis**: Sie können auf **Skript anzeigen** klicken, um eine schreibgeschützte Version des Setupskripts anzuzeigen. Ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Systemadministrator kann dieses Skript bei Bedarf in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Console kopieren, um sie zu bearbeiten und auszuführen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Vorbereiten von SQL Server für CDC](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md)  
  
  
