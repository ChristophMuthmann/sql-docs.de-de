---
title: CDC Instance Deployment Script | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: change-data-capture
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8fa82822-ac99-48ef-a18d-f4f3a77105b4
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eaa5e76954f4ad9f694128d72fb647ee72395610
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="cdc-instance-deployment-script"></a>CDC Instance Deployment Script
  In diesem Abschnitt wird das Dialogfeld CDC Instance Deployment Script beschrieben, in dem das Bereitstellungsskript der CDC-Instanz angezeigt wird. Dieses Skript kann verwendet werden, um die CDC-Datenbank mit ihren Artefakten auf einer anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz neu zu erstellen.  
  
 Nach Abschluss des Bereitstellungsskripts sollten Sie Folgendes sicherstellen:  
  
-   Das Bereitstellungsskript setzt voraus, dass die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Zielinstanz für Oracle CDC mit der Oracle CDC Service Configuration Console oder mit dem vom Programm erstellten **prepare script** (Vorbereitungsskript) vorbereitet wurde.  
  
-   Der Teil des Skripts, der zum Aktivieren der Datenbank für CDC verwendet wird, muss von einem `sysadmin`ausgeführt werden.  
  
-   Das Skript behält das Oracle Log Mining-Kennwort nicht bei. Das Kennwort muss manuell festgelegt werden, nachdem das Skript ausgeführt und der Oracle CDC Service gestartet wurde.  
  
 Aktivieren Sie im Dialogfeld **CDC Instance Deployment Script** die folgenden Optionen.  
  
 **Speichern unter**  
 Speichert das Skript in einer Textdatei, die Sie an einem beliebigen Speicherort ablegen können. Sie können die Datei mit dem Skript auf einen beliebigen anderen Server kopieren, um es dort auszuführen.  
  
 **Kopieren**  
 Kopiert das Skript in die Zwischenablage. Sie können das Skript dann in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder einen beliebigen Texteditor einfügen, um die Skripts später auszuführen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Vorbereiten von SQL Server für CDC](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md)  
  
  
