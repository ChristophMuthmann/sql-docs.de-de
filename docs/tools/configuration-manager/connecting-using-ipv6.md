---
title: "Herstellen einer Verbindung über IPv6 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Internet Protocol
- IPv4
- IPv6
ms.assetid: 2669098c-f5f1-43da-aec6-e91003ac89f6
caps.latest.revision: "18"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f7d6f507497d79bbf3bb71f7c0d6f406a37402da
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="connecting-using-ipv6"></a>Herstellen von Verbindungen über IPv6
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client unterstützen das Internetprotokoll, Version 4 (IPv4), und das Internetprotokoll, Version 6 (IPv6), vollständig. Wenn Windows mit IPv6 konfiguriert ist, erkennen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Komponenten automatisch das Vorhandensein von IPv6. Eine spezielle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfiguration ist nicht erforderlich.  
  
 Umfang der Unterstützung:  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] und die anderen Serverkomponenten können gleichzeitig an IPv4- und IPv6-Adressen lauschen. Wird sowohl IPv4 als auch IPv6 verwendet, können Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit dem [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Konfigurations-Manager so konfigurieren, dass nur auf IPv4-Adressen oder nur auf IPv6-Adressen gelauscht werden.  
  
-   Wenn der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Browserdienst auf einem Computer ausgeführt wird, der sowohl IPv4 als auch IPv6 unterstützt, wird beim Abfragen einer IPv4-Adresse eine IPv4-Adresse sowie der erste IPv4t-TCP-Port in der Liste zurückgegeben. Beim Abfragen einer IPv6-Adresse antwortet der Dienst mit einer IPv6-Adresse und dem ersten IPv6-TCP-Port in seiner Liste. Zur Vermeidung von Inkonsistenzen wird empfohlen, den IPv4- und IPv6-Listener so zu konfigurieren, dass er auf demselben Port lauscht.  
  
-   Tools wie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Konfigurations-Manager akzeptieren bei IP-Adressen sowohl das IPv4- als auch das IPv6-Format. In den meisten Fällen die Verbindungszeichenfolge muss nicht geändert werden, wenn die \< *Computer_name*>\\<*Instance_name*> mit dem Serverhostnamen oder den vollqualifizierten Domänennamen (FQDN) angegeben. Verwendet der Servercomputer sowohl IPv4 als auch IPv6, wird sein Hostname oder FQDN in mehrere IP-Adressen aufgelöst, d. h. in mindestens eine IPv4-Adresse und mehrere IPv6-Adressen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client versucht, Verbindungen mithilfe dieser IP-Adressen herzustellen, und verwendet die erste Verbindung, die erfolgreich hergestellt werden kann. Die IP-Adressen werden dabei in der Reihenfolge verwendet, wie sie aus TCP/IP empfangen werden. Da die Reihenfolge von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client nicht vorhergesagt werden kann, muss sie als zufällige Reihenfolge betrachtet werden. Wenn sowohl IPv4- als auch IPv6-Adressen vorhanden sind, werden die IPv4-Adressen zuerst versucht. Diese Logik ist für die Benutzer von ODBC, OLE DB oder ADO.NET transparent.  
  
    > [!NOTE]  
    >  Wenn [!INCLUDE[ssDE](../../includes/ssde-md.md)] auf IPv4 nicht lauscht, wird erst nach Ablauf der Timeoutspanne für die IPv4-Verbindung versucht, die Verbindung über die IPv6-Adresse herzustellen. Um diese Verzögerung zu vermeiden, müssen Sie die Verbindung direkt mit der IPv6-Adresse herstellen oder auf dem Client einen Alias mit der IPv6-Adresse konfigurieren.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Konfigurations-Manager](../../relational-databases/sql-server-configuration-manager.md)  
  
  
