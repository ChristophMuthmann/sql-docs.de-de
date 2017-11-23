---
title: Konfigurieren von RDS unter Windows 2000 | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: RDS configuration [ADO], Windows 2000
ms.assetid: ef37e858-c05f-4f52-a65f-3ce6037e0d03
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 831608a7930f9fae1bef31132ee11f22654a8b5c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="configuring-rds-on-windows-2000"></a>Konfigurieren von RDS unter Windows 2000
Wenn erste RDS, um ordnungsgemäß zu funktionieren nach dem upgrade auf Windows 2000 Probleme auftreten, führen Sie diese Schritte aus, um das Problem zu beheben:  
  
1.  Stellen Sie sicher, dass der WWW-Publishingdienst zuerst ausgeführt wird, durch Navigieren zu http:// Server mithilfe von Internet Explorer. Wenn Sie den Webserver auf diese Weise zugreifen können, öffnen Sie ein Eingabeaufforderungsfenster, und geben Sie den folgenden Befehl "NET START W3SVC".  
  
2.  Wählen Sie im Startmenü ausführen. Geben Sie "Msdfmap.ini", und klicken Sie dann auf OK, um die Datei "Msdfmap.ini" im Editor zu öffnen. Überprüfen Sie im Abschnitt [CONNECT DEFAULT], und wenn der Parameter für den Zugriff auf NOACCESS festgelegt ist, ändern Sie ihn auf schreibgeschützt.  
  
3.  Navigieren Sie zu "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DataFactory\HandlerInfo" und stellen Sie sicher, dass mit dem Hilfsprogramm RegEdit **HandlerRequired** auf 0 festgelegt ist und **DefaultHandler** ist "" (leere Zeichenfolge).  
  
     **Hinweis** , wenn Sie Änderungen an diesem Abschnitt der Registrierung vornehmen, müssen beenden und Neustarten der WWW-Publishingdienst durch die folgenden Befehle an der Eingabeaufforderung eingeben: "NET STOP W3SVC" und "NET START W3SVC".  
  
4.  Navigieren Sie in der Registrierung auf "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch" und stellen Sie sicher, dass ein Schlüssel mit dem Namen vorhanden ist mit dem Hilfsprogramm RegEdit **RDSServer.Datafactory**. Wenn dies nicht der Fall ist, erstellen Sie ihn.  
  
5.  Mit Internetdienste-Manager, suchen Sie die Standardwebsite, und zeigen Sie die Eigenschaften des virtuellen Stammverzeichnisses MSADC. Überprüfen Sie die Sicherheit bzw. die IP-Adresse des Verzeichnisses und Einschränkungen nach Domänenname. Wählen Sie "Zugewiesen", wenn die "Zugriff verweigert" aktiviert ist.  
  
 Achten Sie darauf, dass Sie versuchen, einen Neustart des Servers ein, wenn die Änderungen nicht zur Behebung des Problems zuerst angezeigt werden.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565). Ab Windows 8 und Windows Server 2012, sind RDS-Serverkomponenten nicht mehr in der Windows-Betriebssystems enthalten. Migrieren von Anwendungen, mit denen RDS [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


