---
title: "Überprüfen einer SQL Server-Installation | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: setup-install
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: validating installations [SQL Server]
ms.assetid: 1689af50-d2b8-4aa6-8f27-cc7127157fc8
caps.latest.revision: "31"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: acff32fa933ca2e2b0832f5d79c33d2c67355677
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="validate-a-sql-server-installation"></a>Überprüfen einer SQL Server-Installation
  Mithilfe des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Ermittlungsberichts können Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Version sowie die auf dem Computer installierten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Funktionen überprüfen. Der **Bericht zur Ermittlung installierter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Funktionen** zeigt einen Bericht aller [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]-, [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]-, [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]-, [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]-, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]-, [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]-, [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] -und [!INCLUDE[ssSQL15](../../includes/sssqlv14-md.md)]-Produkte und -Funktionen an, die auf dem lokalen Server installiert sind. Der Bericht zur Ermittlung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Funktionen steht im **-Installationscenter auf der Seite** Tools [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereit.  
  
 ## <a name="run-includessnoversionincludesssnoversion-mdmd-features-discovery-report"></a>Ausführen des Bericht zur Ermittlung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Funktionen  
  
 Rufen Sie das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Installationscenter auf. Zeigen Sie dazu im **Startmenü** auf **Alle Programme**, **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \<Versionsname>**, **Konfigurationstools**, und klicken Sie auf **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Installationscenter**. Klicken Sie im linken Navigationsbereich des **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Installationscenter** auf **Tools** und anschließend auf **Bericht zur Ermittlung installierter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Funktionen**, um den Bericht zur Ermittlung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Funktionen auszuführen.  
  
 Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Ermittlungsbericht wird unter %Programme%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<letzte Setupsitzung\> gespeichert.  
  
 Sie können den Ermittlungsbericht auch über die Befehlszeile generieren. Führen Sie „Setup.exe /Action=RunDiscovery“ über eine Eingabeaufforderung aus. Wenn Sie der oben stehenden Befehlszeile den Schalter „/q“ hinzufügen, wird keine Benutzeroberfläche angezeigt, sondern unter %Programme%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<letzte Setupsitzung\> der entsprechende Bericht erstellt.  
  
## <a name="see-also"></a>Siehe auch  
 [Lesen und Anzeigen der Setupprotokolldateien von SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
