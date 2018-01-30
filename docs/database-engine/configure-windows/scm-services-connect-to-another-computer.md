---
title: Herstellen einer Verbindung mit einem anderen Computer (SQL Server-Konfigurations-Manager) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connections [SQL Server], other computers
ms.assetid: c4c1e94f-4f5f-431e-8b5b-d5ff97baf723
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d8e4014206abb4c84201724744ec30f1f39f4243
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="scm-services---connect-to-another-computer"></a>SCM-Dienste: Verbinden mit einem anderen Computer
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] In diesem Thema wird beschrieben, wie Sie in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] eine Verbindung mit einem anderen Computer herstellen können. Befolgen Sie die erste Prozedur, um die Computerverwaltung von Windows, MMC ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console) zu öffnen, stellen Sie eine Verbindung zu dem Computer her, und erweitern die Struktur "Dienste und Anwendungen". Führen Sie das zweite Verfahren zum Erstellen einer Datei mit einem Link zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager auf einem Remotecomputer aus.  
  
> [!NOTE]  
>  Bei einer Remoteverbindung können einige Aktionen nicht von Configuration Manager ausgeführt werden.  
  
 Zum Starten, Stoppen, Anhalten oder Fortsetzen von Diensten auf einem anderen Computer können Sie auch mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung zu dem Server herstellen, mit der rechten Maustaste auf den Server oder den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent und anschließend auf die gewünschte Aktion klicken.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-connect-to-another-computer-with-windows-computer-management"></a>So stellen Sie eine Verbindung mit einem anderen Computer mit der Computerverwaltung von Windows her  
  
1.  Klicken Sie im Menü **Start** mit der rechten Maustaste auf **Arbeitsplatz**, und klicken Sie dann auf **Verwalten**.  
  
2.  Klicken Sie in **Computerverwaltung**mit der rechten Maustaste auf **Computerverwaltung (lokal)**, und klicken Sie dann auf **Verbindung mit anderem Computer herstellen**.  
  
3.  Geben Sie im Dialogfeld **Computer auswählen** in das Textfeld **Anderen Computer** den Namen des Computers ein, den Sie verwalten möchten, und klicken Sie dann auf **OK**.  
  
     Die Computerverwaltung zeigt die Dienste an, die auf dem Remotecomputer ausgeführt werden. Der Knoten der obersten Ebene wird in **Computerverwaltung**\<*Remotecomputer*> geändert.  
  
4.  Erweitern Sie in der Konsolenstruktur **Dienste und Anwendungen**, und erweitern Sie dann **SQL Server-Konfigurations-Manager** , um die Dienste des Remotecomputers zu verwalten.  
  
#### <a name="to-save-a-link-to-sql-server-configuration-manager-for-another-computer"></a>So sichern Sie einen Link zu SQL Server-Konfigurations-Manager für einen anderen Computer  
  
1.  Klicken Sie im Menü **Start** auf **Ausführen**.  
  
2.  Geben Sie im Feld **Öffnen** die Zeichenfolge **mmc -a** ein, um die [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console im Autorenmodus zu öffnen.  
  
3.  Klicken Sie im Menü **Datei** auf **Snap-In hinzufügen/entfernen**.  
  
4.  Klicken Sie im Fenster **Snap-In hinzufügen/entfernen** auf **Hinzufügen**.  
  
5.  Klicken Sie im Dialogfeld **Eigenständiges Snap-In hinzufügen** auf **Computerverwaltung** , und klicken Sie dann auf **Hinzufügen**.  
  
6.  Klicken Sie im Dialogfeld **Computerverwaltung** auf **Anderen Computer**, geben Sie den Namen des zu verwaltenden Remotecomputers ein, und klicken Sie dann auf **Fertig stellen**.  
  
7.  Klicken Sie im Dialogfeld **Eigenständiges Snap-In hinzufügen** auf **Schließen**.  
  
8.  Klicken Sie im Fenster **Snap-In hinzufügen/entfernen** auf **OK**.  
  
9. Erweitern Sie **Computerverwaltung (***\<Computername>***)** und **Dienste und Anwendungen**.  
  
10. Klicken Sie mit der rechten Maustaste auf **SQL Server-Konfigurations-Manager**, und klicken Sie dann auf **Neues Fenster**.  
  
11. Klicken Sie im Menü **Fenster** auf **Konsolenstamm**, um zum ersten Fenster zurückzuwechseln, und löschen Sie das Fenster.  
  
12. Klicken Sie im Menü **Datei** auf **Speichern unter**, und speichern Sie die Datei im gewünschten Ordner. Geben Sie der Datei dabei einen passenden Namen mit der Erweiterung **.msc** . Schließen Sie das Fenster [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console.  
  
13. Doppelklicken Sie auf die Datei, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager auf dem Zielcomputer zu öffnen. Speichern Sie gegebenenfalls einen Link zu der Datei auf dem Desktop oder im Menü **Start** .  
  
> [!CAUTION]  
>  Wenn Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager auf einem Remotecomputer verwenden, ist der Computername nicht offensichtlich, und es ist möglich, versehentlich den falschen Computer zu stoppen oder zu konfigurieren. Überprüfen Sie auf der Registerkarte **Dienst** das Feld **Hostname** , um den Computernamen zu überprüfen, bevor Sie einen Dienst ändern.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Konfigurieren von WMI zum Anzeigen des Serverstatus in SQL Server-Tools](http://msdn.microsoft.com/library/7e97197b-ed4d-40d1-9a52-9ab1d92401d7)  
  
  
