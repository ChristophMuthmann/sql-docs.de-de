---
title: "Verbindung mit Server herstellen (Oracle), Anmeldename | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.oracleconnection.login.f1"
helpviewer_keywords: 
  - "Dialogfeld "Verbindung mit Server herstellen", Replikation"
ms.assetid: 86ed91a1-a07c-46f2-a913-67317ef2255e
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Verbindung mit Server herstellen (Oracle), Anmeldename
  Auf der Registerkarte **Anmeldename** des Dialogfelds **Verbindung mit Server herstellen** können Sie das Konto angeben, unter dem der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Verteiler Verbindungen mit dem Oracle-Verleger herstellt. Sie müssen dafür dasselbe Konto verwenden wie für das Schema des administrativen Replikationsbenutzers, das Sie bei der Konfiguration des Verlegers angegeben haben. Weitere Informationen finden Sie unter [Konfigurieren eines Oracle-Verlegers](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## Optionen  
 **Serverinstanz**  
 Der TNS-Name (Transparent Network Substrate) des Oracle-Verlegers, der bei Konfiguration der auf dem Verteiler installierten Oracle-Clientsoftware angegeben wurde.  
  
 **Authentifizierung**  
 Wählen Sie **Oracle-Standardauthentifizierung** (empfohlen) oder **Windows-Authentifizierung**. Bei Auswahl von **Windows-Authentifizierung**:  
  
-   Der Oracle-Server muss so konfiguriert sein, dass mit den Windows-Anmeldeinformationen Verbindungen hergestellt werden können. Weitere Informationen finden Sie in der Oracle-Dokumentation.  
  
-   Sie müssen dazu auf demselben [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Konto angemeldet sein, wie für das Schema des administrativen Replikationsbenutzers angegeben wurde.  
  
 **Anmeldung** und **Kennwort**  
 Bei Auswahl von **Oracle-Standardauthentifizierung** für die **Authentifizierung** aktivieren, geben Sie den Anmeldenamen und das Kennwort zu verwenden, die identisch mit denen für das Schema des administrativen replikationsbenutzers angegeben sein muss.  
  
## Siehe auch  
 [Begriffe im Zusammenhang mit dem Veröffentlichen von Oracle-Daten](../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)  
  
  