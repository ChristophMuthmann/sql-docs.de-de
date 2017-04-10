---
title: "SQL Server, Benutzerdefinierbar-Objekt | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Benutzerdefinierbar-Objekt"
  - "SQLServer:Benutzerdefinierbar"
ms.assetid: 633de3ef-533c-4f0c-9c7b-c105129d8e94
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# SQL Server, Benutzerdefinierbar-Objekt
  Das **Benutzerdefinierbar** -Objekt in Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ermöglicht Ihnen das Erstellen von benutzerdefinierten Leistungsindikatorinstanzen. Verwenden Sie benutzerdefinierte Leistungsindikatorinstanzen zum Überwachen von Aspekten des Servers, die nicht von vorhandenen Leistungsindikatoren überwacht werden. Beispielsweise Komponenten, die ausschließlich in Ihrer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank vorkommen (z. B. für die Anzahl der protokollierten Kundenbestellungen oder das Produktverzeichnis).  
  
 Das **Benutzerdefinierbar** -Objekt enthält 10 Instanzen des Abfragleistungsindikators: **Benutzerindikator 1** bis **Benutzerindikator 10**. Diese Leistungsindikatoren werden den gespeicherten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Prozeduren **sp_user_counter1** bis **sp_user_counter10** zugeordnet. Da diese gespeicherten Prozeduren von Benutzeranwendungen ausgeführt werden, werden die von den gespeicherten Prozeduren festgelegten Werte im Systemmonitor angezeigt. Ein Leistungsindikator kann einen einzelnen ganzzahligen Wert überwachen, wie z. B. eine gespeicherte Prozedur, die zählt, wie viele Bestellungen für ein bestimmtes Produkt an einem Tag eingegangen sind.  
  
> [!NOTE]  
>  Die gespeicherten Benutzerleistungsindikator-Prozeduren werden nicht automatisch vom Systemmonitor abgerufen. Sie müssen explizit von einer Benutzeranwendung ausgeführt werden, damit die Leistungsindikatorwerte aktualisiert werden. Verwenden Sie einen Trigger für das automatische Update des Leistungsindikatorwerts. Wenn Sie z. B. einen Leistungsindikator erstellen möchten, der die Anzahl von Zeilen in einer Tabelle überwacht, erstellen Sie einen INSERT- und DELETE-Trigger für die Tabelle, der folgende Anweisung ausführt: `SELECT COUNT(*) FROM table`. Wenn der Trigger aufgrund einer INSERT- oder DELETE-Operation in der Tabelle ausgelöst wird, wird der Leistungsindikator des Systemmonitors automatisch aktualisiert.  
  
 In dieser Tabelle wird das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Benutzerdefinierbar** beschrieben.  
  
|Benutzerdefinierbar-Leistungsindikatoren von SQL Server|Beschreibung|  
|---------------------------------------|-----------------|  
|**Abfrage**|Das **Benutzerdefinierbar** -Objekt enthält den Abfrageleistungsindikator. Die Benutzer konfigurieren die **User counter** innerhalb des Abfrageobjekts.|  
  
 In dieser Tabelle werden die **Instanzen** des **Abfrage** -Leistungsindikators beschrieben.  
  
|Instanzen des Abfrageleistungsindikators|Beschreibung|  
|-----------------------------|-----------------|  
|**User counter 1**|Definiert mithilfe von **sp_user_counter1**.|  
|**User counter 2**|Definiert mithilfe von **sp_user_counter2**.|  
|**User counter 3**|Definiert mithilfe von **sp_user_counter3**.|  
|…||  
|**User counter 10**|Definiert mithilfe von **sp_user_counter10**.|  
  
 Wenn Sie die gespeicherten Benutzerleistungsindikator-Prozeduren verwenden möchten, führen Sie sie von Ihrer eigenen Anwendung mit einem einzelnen ganzzahligen Parameter, der den neuen Wert für den Leistungsindikator darstellt, aus. Um beispielsweise den Wert 10 für **User counter 1** festzulegen, führen Sie die folgende Transact-SQL-Anweisung aus:  
  
```  
EXECUTE sp_user_counter1 10  
```  
  
 Die gespeicherten Benutzerleistungsindikator-Prozeduren können von jeder beliebigen Stelle aufgerufen werden, von der andere gespeicherte Prozeduren, wie etwa Ihre eigenen gespeicherten Prozeduren, auch aufgerufen werden können. Sie können beispielsweise die folgende gespeicherte Prozedur erstellen, um die Anzahl von Verbindungen und Verbindungsversuchen seit dem Starten einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zu zählen:  
  
```  
DROP PROC My_Proc  
GO  
CREATE PROC My_Proc  
AS   
   EXECUTE sp_user_counter1 @@CONNECTIONS  
GO  
```  
  
 Die @@CONNECTIONS-Funktion gibt die Anzahl von Verbindungen und Verbindungsversuchen seit dem Starten einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zurück. Dieser Wert wird an die gespeicherte Prozedur **sp_user_counter1** als Parameter übergeben.  
  
> [!IMPORTANT]  
>  Die in den gespeicherten Benutzerleistungsindikator-Prozeduren definierten Abfragen sollten so einfach wie möglich sein. Arbeitsspeicherintensive Abfragen mit umfangreichen Sortier- oder Hashvorgängen oder Abfragen, die viele E/A-Vorgänge ausführen, sind bezüglich der Ausführung aufwendig und können die Leistung beeinträchtigen.  
  
## Berechtigungen  
 **sp_user_counter** ist für alle Benutzer verfügbar, kann jedoch für jeden Abfrageleistungsindikator eingeschränkt werden.  
  
## Siehe auch  
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  