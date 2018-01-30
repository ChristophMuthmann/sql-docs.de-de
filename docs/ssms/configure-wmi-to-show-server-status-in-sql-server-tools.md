---
title: Konfigurieren von WMI zum Anzeigen des Serverstatus in SQL Server-Tools | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms
ms.reviewer: 
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- WMI Provider for Server Events, setting permissions
- WMI permissions [SQL Server]
ms.assetid: 7e97197b-ed4d-40d1-9a52-9ab1d92401d7
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 654dfff830fa18a1a38a3ecb3454cfa824e097c9
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="configure-wmi-to-show-server-status-in-sql-server-tools"></a>Konfigurieren von WMI zum Anzeigen des Serverstatus in SQL Server-Tools
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)] In diesem Thema wird beschrieben, wie WMI konfiguriert wird, um den Serverstatus in SQL Server-Tools in [!INCLUDE[ssCurrent](../includes/sscurrent_md.md)] anzuzeigen. Bei der Verbindungsherstellung mit Servern wird von den Komponenten Registrierte Server und Objekt-Explorer von [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull_md.md)]sowie auch vom [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] -Konfigurations-Manager Windows Management Instrumentation (WMI) zum Abrufen des Status der [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] -Dienste (MSSQLSERVER) und [!INCLUDE[ssNoVersion](../includes/ssnoversion_md.md)] -Agent-Dienste (MSSQLSERVER) verwendet. Zum Anzeigen des Dienststatus muss der Benutzer über Remotezugriffsrechte für das WMI-Objekt verfügen. Zum Konfigurieren dieser Berechtigung muss auf dem Server WMI installiert sein.  
  
## <a name="SSMSProcedure"></a>So konfigurieren Sie die WMI-Berechtigung  
  
1.  Klicken Sie auf dem Remoteserver im Menü **Start** auf **Ausführen**.  
  
2.  Geben Sie im Feld **Öffnen** die Zeichenfolge **wmimgmt.msc**ein, und klicken Sie dann auf **OK**.  
  
3.  Klicken Sie im Programm **Windows-Verwaltungsinfrastruktur** mit der rechten Maustaste auf **WMI-Steuerung (Lokal)**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Erweitern Sie im Dialogfeld **Eigenschaften von WMI-Steuerung (Lokal)** auf der Registerkarte **Sicherheit** den Eintrag **Root**, und klicken Sie dann auf **CIMV2**.  
  
5.  Klicken Sie auf **Sicherheit** , um das Dialogfeld **Sicherheit für ROOT\CIMV2** zu öffnen.  
  
6.  Fügen Sie zum Feld **Gruppen- oder Benutzernamen** eine Gruppe oder einen Benutzer hinzu, und markieren Sie die Gruppe bzw. den Benutzer.  
  
7.  Wählen Sie im Feld **Berechtigungen für***<group or user>* die Spalte **Zulassen** für die Berechtigung **Remoteaktivierung** für Benutzer aus, durch die der Dienststatus remote erkannt werden soll.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Starten, Beenden oder Anhalten des SQL Server-Agent-Dienstes](../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
