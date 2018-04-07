---
title: Konfigurieren der externes Windows-System zum Abrufen der Remotetabelle Kopien InfiniBand-PDW
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f866890b-cad5-49ac-bbeb-848bfb26c2d5
caps.latest.revision: 11
ms.openlocfilehash: 32875c5c7b93f47dbf9dbcc01c621df402ab782d
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband"></a>Konfigurieren Sie eine externe Windows-System zum Empfangen der Remotetabelle Kopien mit InfiniBand
Beschreibt, wie erwerben und Konfigurieren von einem nicht-Appliance-Windows-Betriebssystem mit dem InfiniBand-Netzwerk für die Verwendung mit der Funktion zum Kopieren von Remotetabelle in SQL Server PDW verbunden. Das Windows-System hostet der SQL Server-Datenbank, die die Remotetabelle Kopie aus einer SQL Server PDW-Datenbank empfängt. Es ist auf dem Gerät separat verkauft und mit dem Gerät InfiniBand-Netzwerk verbunden.  
  
> [!NOTE]  
> Herstellen einer Verbindung über das InfiniBand-Netzwerk ist nicht erforderlich für die Verwendung von remote-Tabelle kopieren. Herstellen einer Verbindung über das Ethernet-Netzwerk kann erfolgen, wenn die Ethernet-Bandbreite, die Ihren Anforderungen entspricht.  
  
Dieses Thema beschreibt eine der Konfigurationsschritte zum Konfigurieren von remote-Tabelle kopieren. Eine Übersicht über die Konfigurationsschritte finden Sie unter [Remotekopie-Tabelle](remote-table-copy.md)  
  
## <a name="before-you-begin"></a>Vorbereitungen  
Bevor Sie die externe Windows-System konfigurieren, müssen Sie folgende Schritte ausführen:  
  
1.  Erwerben Sie, oder geben Sie ein WindowsSystem, das die remote-Kopien erhält.  
  
2.  Schienenkits für das Windows-System in das Gestell Steuerelement (sofern genügend Speicherplatz vorhanden ist), oder schließen Sie genug, um das Gerät, damit Sie die Appliance InfiniBand-Netzwerk hergestellt werden können.  
  
3.  Erwerben Sie vom Hardwarehersteller Appliance InfiniBand-Kabel und einem InfiniBand-Netzwerkadapter. Es wird empfohlen, einen Netzwerkadapter mit zwei Ports für die Fehlertoleranz erwerben, wenn Sie die exportierten Daten zu empfangen. Ein Netzwerkadapter für die zwei Ports wird empfohlen, aber es ist keine Voraussetzung.  
  
## <a name="HowToWindows"></a>Konfigurieren Sie eine externe Windows-System um Remotetabelle Kopien zu erhalten.  
Um das externe Windows-System zu konfigurieren, verwenden Sie die folgenden Schritte aus:  
  
1.  Installieren Sie den InfiniBand-Netzwerkadapter in das Windows-System.  
  
2.  Verbinden Sie InfiniBand-Netzwerkadapter mit dem main InfiniBand-Switch in das Steuerelement Rack mit InfiniBand-Kabel.  
  
3.  Installieren Sie und konfigurieren Sie den entsprechenden Windows-Treiber für den InfiniBand-Netzwerkadapter.  
  
    InfiniBand-Treiber für Windows sind von der OpenFabrics Alliance, einer Branche Consortium InfiniBand-Hersteller entwickelt.  Der richtige Treiber möglicherweise mit Ihrem Adapter InfiniBand verteilt wurden. Wenn dies nicht der Fall ist, wird der Treiber kann von www.openfabrics.org heruntergeladen werden.  
  
4.  Konfigurieren Sie die IP-Adresse für jeden Port auf dem Adapter. SMP-Systemen sind erforderlich, um die statische IP-Adressen aus einem reservierten Adressbereich für diesen Zweck zu verwenden. Konfigurieren Sie den ersten Port gemäß den folgenden Parametern:  
  
    -   IP-Netzwerkadresse: 172.16.132.x  
  
    -   IP-Subnetzmaske: 255.255.128.0  
  
    -   IP-Host-Bereich: 1-254  
  
    Konfigurieren Sie für InfiniBand-Netzwerkadapter mit zwei Ports des zweite Ports gemäß den folgenden Parametern aus:  
  
    -   IP-Netzwerkadresse: 172.16.132.x  
  
    -   IP-Subnetzmaske: 255.255.128.0  
  
    -   IP-Host-Bereich: 1-254  
  
5.  Wenn zwei Portadapter verwendet wird, oder mehrere externe Windows-Systemen in einer Anwendung verbunden sind, weisen Sie jedes System einen anderen Host Anzahl in jedem IP-Subnetz.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
