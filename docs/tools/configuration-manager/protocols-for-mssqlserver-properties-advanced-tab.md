---
title: Protokolle für MSSQLSERVER-Eigenschaften (Registerkarte „Erweitert“) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: configuration-manager
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: abd5ca68-825f-4c07-b27c-3b3a79d03d74
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4aeaeb623e10074a22d3712e460dcca7d4ce5993
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="protocols-for-mssqlserver-properties-advanced-tab"></a>Protokolle für MSSQLSERVER-Eigenschaften (Registerkarte "Erweitert")
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  Mit der Registerkarte **Erweitert** im Dialogfeld **Protokolle für MSSQLSERVER-Eigenschaften** können Sie für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]**Erweiterter Schutz für die Authentifizierung** konfigurieren. **Erweiterter Schutz** ist eine Funktion der vom Betriebssystem implementierten Netzwerkkomponenten. **Erweiterter Schutz** ist in Windows 7 und Windows Server 2008 R2 verfügbar und in Service Packs für ältere Betriebssysteme enthalten. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist sicherer, wenn Verbindungen möglichst mithilfe des **erweiterten Schutzes**hergestellt werden. Einige Funktionen von **Erweiterter Schutz** setzen die Auswahl von **Verschlüsselung erzwingen** auf der Registerkarte **Flags** voraus.  
  
> [!IMPORTANT]  
>  **Erweiterter Schutz** ist in Windows standardmäßig nicht aktiviert. Informationen zum Aktivieren von **Erweiterter Schutz** in Windows finden Sie im Knowledge Base-Artikel [Erweiterter Schutz für die Authentifizierung](http://go.microsoft.com/fwlink/?LinkId=178431).  
  
 Weitere Informationen zum Konfigurieren anderer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienste und eine vollständige Beschreibung von **Erweiterter Schutz**finden Sie auf [Microsoft.com](http://go.microsoft.com/fwlink/?LinkId=177752).  
  
 **Erweiterter Schutz** wird von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ab [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]vollständig unterstützt. Für andere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Clientanbieter wird **Erweiterter Schutz** derzeit nicht unterstützt.  
  
## <a name="options"></a>Tastatur  
 **Erweiterter Schutz**  
 Es gibt drei mögliche Werte:  
  
-   Bei der Einstellung **Aus**ist **Erweiterter Schutz** deaktiviert. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanz akzeptiert Verbindungen von jedem beliebigen Client, unabhängig davon, ob er geschützt ist oder nicht. **Aus** ist mit älteren und nicht gepatchten Betriebssystemen kompatibel, bietet aber weniger Sicherheit. Verwenden Sie diese Einstellung nur, wenn Sie wissen, dass die Clientbetriebssysteme keinen erweiterten Schutz unterstützen.  
  
-   Bei der Einstellung **Zulässig**wird **Erweiterter Schutz** für Verbindungen von Betriebssystemen vorausgesetzt, die die Funktion **Erweiterter Schutz**unterstützen. Verbindungen von ungeschützten Clientanwendungen, die auf geschützten Clientbetriebssystemen ausgeführt werden, werden abgelehnt. **Erweiterter Schutz** wird für Verbindungen von ungeschützten Betriebssystemen ignoriert. Diese Einstellung ist sicherer als **Aus**, bietet jedoch nicht die höchste Sicherheit. Verwenden Sie diese Einstellung in gemischten Umgebungen, in denen einige Betriebssysteme oder Anwendungen die Funktion **Erweiterter Schutz** unterstützen, andere jedoch nicht.  
  
-   Bei der Einstellung **Erforderlich**werden nur Verbindungen von geschützten Anwendungen auf geschützten Betriebssystemen akzeptiert. Diese Einstellung ist die sicherste der drei Optionen. Von Betriebssystemen, die die Funktion **Erweiterter Schutz** nicht unterstützen, können jedoch keine Verbindungen mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]hergestellt werden.  
  
 **Akzeptierte NTLM-SPNs**  
 Wenn die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durch mehr als einen NTLM-Dienstprinzipalnamen (SPN) identifiziert wird, listen Sie die SPNs hier als eine Reihe von Zeichenfolgen auf, die von Semikolons getrennt wird. Der Wert **MSSQLSvc/HostName1.Contoso.com;MSSQLSvc/HostName2.Contoso.com**zeigt beispielsweise an, dass Clients, die versuchen, eine Verbindung mit SPNs mit dem Namen **MSSQLSvc/HOST1.Contoso.com** und **MSSQLSvc/HOST2.Contoso.com** herzustellen, zulässig sind. Die maximale Länge der Variablen beträgt 2048 Zeichen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erweiterter Schutz für die Authentifizierung mit Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)  
  
  
