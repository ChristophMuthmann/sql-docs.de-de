---
title: "Auswählen des richtigen SQL Server-Agent-Dienstkontos für Multiserverumgebungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, service accounts
- multiserver environments [SQL Server], SQL Server Agent service account behavior
ms.assetid: a07e2f38-281c-495b-965b-13fad03ba548
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 86d85a50ab48b48c25610def1d2d1816a5856255
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="choose-the-right-sql-server-agent-service-account-for-multiserver-environments"></a>Auswählen des richtigen SQL Server-Agent-Dienstkontos für Multiserverumgebungen
Das Windows-Konto, das Sie für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-Agent-Dienst auswählen, kann sich wie im Folgenden beschrieben auf das Verhalten einer Multiserverumgebung auswirken:  
  
-   Wenn Sie den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst unter einem Konto ausführen, das nicht Mitglied der lokalen Windows-Administratorengruppe ist, treten beim Eintragen von Zielservern bei Masterservern u. U. Fehler auf. In diesem Fall wird die folgende Fehlermeldung zurückgegeben:  
  
    "Fehler beim Eintragungsvorgang."  
  
    Starten Sie die Dienste von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent neu, um das Problem zu beheben.  
  
-   Wenn der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst unter dem Konto LocalSystem ausgeführt wird, werden Vorgänge zwischen Masterservern und Zielservern nur unterstützt, wenn sich Masterserver und Zielserver auf demselben Computer befinden. Wenn Sie diese Konfiguration verwenden, wird beim Eintragen von Zielservern bei einem Masterserver die folgende Meldung zurückgegeben:  
  
    „Stellen Sie sicher, dass das Agentstartkonto für *<Zielserver-Computername>* Rechte zur Anmeldung als Zielserver besitzt.“  
  
    Sie können diese zu Informationszwecken ausgegebene Meldung ignorieren. Der Eintragungsvorgang wird dennoch erfolgreich abgeschlossen.  
  
Weitere Informationen zum Auswählen eines Kontos für den [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Agent-Dienst finden Sie unter [Auswählen eines Kontos für den SQL Server-Agent-Dienst](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md).  
  

