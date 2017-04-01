---
title: "Startprogramm f&#252;r SQL-Volltextfilterdaemon (Registerkarte Anmelden) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 13e260f9-a75f-430b-88a3-959ddcead8fe
caps.latest.revision: 9
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 9
---
# Startprogramm f&#252;r SQL-Volltextfilterdaemon (Registerkarte Anmelden)
  Ab [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] wird der Dienst SQL-Volltextfilterdaemon (FDHOST-Startprogramm) von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Volltextsuche verwendet. Dieser Dienst muss ausgeführt werden, wenn Sie die Volltextsuche verwenden. Informationen über die Prozesse des Filterdaemonhosts finden Sie unter "Architektur der Volltextsuche" in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Onlinedokumentation.  
  
 Verwenden der **Anmelden** Registerkarte der **SQL Volltext-Eigenschaften-Volltextfilterdaemon** Dialogfeld an, das von verwendete Konto der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Volltextdienst, das Kennwort des Kontos zu ändern und zu starten und beenden Sie den Dienst. Das Ändern eines Kennworts für ein Konto wird nach einem Neustart des Diensts wirksam.  
  
> [!NOTE]  
>  Beim Ändern des Kontonamens, der von einem Dienst auf einer gruppierten Instanz verwendet wird, muss das neue Konto Mitglied der Domänengruppe sein, die während des Setups für den zu ändernden Dienst angegeben wird, oder Sie müssen die Berechtigung zum Hinzufügen von Mitgliedern zu dieser Gruppe besitzen. Wenden Sie sich an Ihren Domänenadministrator, falls Sie keine Berechtigung zum Ändern der Gruppenmitgliedschaft haben.  
>   
>  Weitere Informationen über das Auswählen eines Kontos zum Ausführen des Dienstes finden Sie unter "Einrichten von Windows-Dienstkonten" in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation.  
  
## Optionen  
 **Integriertes Konto**  
 **Lokales System**  
 Geben Sie das lokale Systemkonto an. Dieses Konto erfordert kein Kennwort. Das lokale Systemkonto kann die Zusammenarbeit mit anderen Servern verhindern. Dies hängt von den Privilegien ab, die dem Konto erteilt wurden.  
  
 **Lokaler Dienst**  
 Geben Sie das lokale Dienstkonto an. Dieses Konto erfordert kein Kennwort. Das lokale Dienstkonto kann die Zusammenarbeit mit anderen Servern verhindern. Dies hängt von den Privilegien ab, die dem Konto erteilt wurden.  
  
 **Netzwerkdienst**  
 Es wird empfohlen, dass Sie nicht das Netzwerkdienstkonto für verwenden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Dienste oder die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienste. Lokale Benutzerkonten oder Domänenbenutzerkonten sind für die Dienste besser geeignet.  
  
 **Dieses Konto**  
 Geben Sie ein lokales oder ein Domänenbenutzerkonto an, das die Windows-Authentifizierung verwendet. Das Verwenden eines Domänenbenutzerkontos mit minimalen Berechtigungen für Dienste wird empfohlen.  
  
 **Kontoname**  
 Geben Sie den Kontonamen des lokalen oder Domänenbenutzers an.  
  
 **Kennwort**  
 Geben Sie das Kennwort des Kontos ein.  
  
 **Kennwort bestätigen**  
 Geben Sie das Kennwort des Kontos erneut ein.  
  
 **Start**  
 Starten Sie den Dienst.  
  
 **Beenden**  
 Beenden Sie den Dienst.  
  
 **Anhalten**  
 Halten Sie den Dienst an. Für diesen Dienst nicht verfügbar.  
  
 **Fortsetzen**  
 Setzen Sie einen angehaltenen Dienst fort.  
  
  