---
title: "Protokollversand-&#220;berwachungseinstellungen | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.databaseproperties.logshipping.settings.monitor.f1"
ms.assetid: 45e2ba7d-b3aa-4643-9451-bcb991572314
caps.latest.revision: 17
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 17
---
# Protokollversand-&#220;berwachungseinstellungen
  Mithilfe dieser Seite können Sie die Eigenschaften des Protokollversand-Überwachungsservers konfigurieren und ändern.  
  
 Eine Erklärung zu den Konzepten des Protokollversands finden Sie unter [Informationen zum Protokollversand &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
## Optionen  
 **Überwachungsserverinstanz**  
 Zeigt den Namen der Serverinstanz an, die zurzeit als Überwachungsserver für die Protokollversandkonfiguration konfiguriert ist.  
  
 **Connect**  
 Wählen Sie eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aus, die als Überwachungsserver verwendet werden soll, und stellen Sie die entsprechende Verbindung her. Das zum Verbinden verwendete Konto muss Mitglied der festen Serverrolle sysadmin auf der sekundären Serverinstanz sein.  
  
 **Identität des Auftragsproxykontos annehmen (normalerweise ist dies das Dienstkonto des SQL Server-Agents der Serverinstanz, in der der Auftrag ausgeführt wird)**  
 Legt fest, dass der Protokollversand beim Verbinden mit der Überwachungsserverinstanz die Identität des vom SQL Server-Agent verwendeten Proxykontos annimmt. Stellen Sie sicher, dass Sicherungs-, Kopier- und Wiederherstellungsprozesse eine Verbindung mit dem Überwachungsserver herstellen können, damit der Status der Protokollversandvorgänge aktualisiert werden kann.  
  
 **Folgende SQL Server-Anmeldung verwenden**  
 Ermöglichen Sie dem Protokollversand beim Herstellen der Verbindung mit der Überwachungsserverinstanz die Verwendung einer bestimmten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung. Stellen Sie sicher, dass Sicherungs-, Kopier- und Wiederherstellungsprozesse eine Verbindung mit dem Überwachungsserver herstellen können, damit der Status der Protokollversandvorgänge aktualisiert werden kann. Wählen Sie diese Option aus, wenn der Protokollversand eine bestimmte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung verwenden soll, und geben Sie dann den Anmeldenamen und das Kennwort an.  
  
 **Verlauf löschen nach**  
 Geben Sie an, für welchen Zeitraum die Verlaufsinformationen des Protokollversands auf dem Überwachungsserver aufbewahrt werden, bevor sie gelöscht werden.  
  
 **Auftragsname**  
 Gibt den Namen des vom SQL Server-Agent bereitgestellten Warnungsauftrags an, mit dem der Protokollversand Warnungen auslöst, wenn beim Sichern oder Wiederherstellen Schwellenwerte überschritten werden. Wenn Sie den Auftrag erstmalig erstellen, können Sie den Namen durch Eingabe in das entsprechende Feld ändern.  
  
 **Zeitplan**  
 Gibt den aktuellen Zeitplan des vom SQL Server-Agent bereitgestellten Warnungsauftrags an.  
  
 **Bearbeiten**  
 Ändert die Parameter des vom SQL Server-Agent bereitgestellten Warnungsauftrags.  
  
 **Diesen Auftrag deaktivieren**  
 Hält den vom SQL Server-Agent bereitgestellten Warnungsauftrag an.  
  
  