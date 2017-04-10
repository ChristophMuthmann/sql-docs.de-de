---
title: "Sicherheits&#252;berwachung-Ereigniskategorie (SQL Server Profiler) | Microsoft Docs"
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
  - "Sicherheitsüberwachung-Ereigniskategorie [SQL Server]"
  - "Ereignisklassen [SQL Server Profiler], Sicherheitsüberwachung (Ereigniskategorie)"
  - "SQL Server-Ereignisklassen, Sicherheitsüberwachung (Ereigniskategorie)"
ms.assetid: e64f7695-2f23-4adb-b83d-52f147cc1a2f
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Sicherheits&#252;berwachung-Ereigniskategorie (SQL Server Profiler)
  Die **Sicherheitsüberwachung** -Ereigniskategorie enthält Sicherheitsüberwachungsereignisse.  
  
## In diesem Abschnitt  
  
|Thema|Beschreibung|  
|-----------|-----------------|  
|[Audit Add DB User (Ereignisklasse)](../../relational-databases/event-classes/audit-add-db-user-event-class.md)|Gibt an, dass eine Anmeldung hinzugefügt oder entfernt wurde, wie ein Datenbankbenutzer zu einer Datenbank.|  
|[Audit Add Login to Server Role (Ereignisklasse)](../../relational-databases/event-classes/audit-add-login-to-server-role-event-class.md)|Gibt an, dass eine Annmeldung von einer festen Serverrolle hinzugefügt oder entfernt wurde.|  
|[Audit Add Member to DB Role (Ereignisklasse)](../../relational-databases/event-classes/audit-add-member-to-db-role-event-class.md)|Gibt an, dass eine Anmeldung von einer Rolle hinzugefügt oder entfernt wurde.|  
|[Audit Add Role-Ereignisklasse](../../relational-databases/event-classes/audit-add-role-event-class.md)|Gibt an, dass eine Datenbankrolle von einer Datenbank hinzugefügt oder entfernt wurde.|  
|[Audit Addlogin (Ereignisklasse)](../../relational-databases/event-classes/audit-addlogin-event-class.md)|Gibt an, dass eine Anmeldung hinzugefügt oder entfernt wurde.|  
|[Audit App Role Change Password (Ereignisklasse)](../../relational-databases/event-classes/audit-app-role-change-password-event-class.md)|Gibt an, dass ein Kennwort für eine Anwendungsrolle geändert wurde.|  
|[Audit Backup/Restore-Ereignisklasse](../../relational-databases/event-classes/audit-backup-and-restore-event-class.md)|Gibt an, dass eine Sicherung oder eine Wiederherstellungsanweisung ausgegeben wurde.|  
|[Audit Broker Conversation (Ereignisklasse)](../../relational-databases/event-classes/audit-broker-conversation-event-class.md)|Meldet Überwachungsmeldungen, die mit der Dialogsicherheit von Service Broker verbunden sind.|  
|[Audit Broker Login (Ereignisklasse)](../../relational-databases/event-classes/audit-broker-login-event-class.md)|Meldet Überwachungsmeldungen, die mit der Transportsicherheit von Service Broker verbunden sind.|  
|[Audit Change Audit (Ereignisklasse)](../../relational-databases/event-classes/audit-change-audit-event-class.md)|Gibt an, dass eine Änderung an der Ablaufverfolgung vorgenommen wurde.|  
|[Audit Change Database Owner (Ereignisklasse)](../../relational-databases/event-classes/audit-change-database-owner-event-class.md)|Gibt an, dass die Berechtigungen, um den Besitzer der Datenbank zu ändern, überprüft wurden.|  
|[Audit Database Management (Ereignisklasse)](../../relational-databases/event-classes/audit-database-management-event-class.md)|Gibt an, dass eine Datenbank erstellt, geändert oder gelöscht wurde.|  
|[Audit Database Mirroring Login (Ereignisklasse)](../../relational-databases/event-classes/audit-database-mirroring-login-event-class.md)|Meldet Überwachungsmeldungen, die mit der Transportsicherheit der Datenbankspiegelung verbunden sind.|  
|[Audit Database Object Access (Ereignisklasse)](../../relational-databases/event-classes/audit-database-object-access-event-class.md)|Gibt an, dass auf ein Datenbankobjekt, beispielsweise ein Schema, zugegriffen wird.|  
|[Audit Database Object GDR (Ereignisklasse)](../../relational-databases/event-classes/audit-database-object-gdr-event-class.md)|Gibt an, dass ein GDR-Ereignis für ein Datenbankobjekt aufgetreten ist.|  
|[Audit Database Object Management-Ereignisklasse](../../relational-databases/event-classes/audit-database-object-management-event-class.md)|Gibt an, dass eine CREATE-, ALTER- oder DROP-Anweisung auf einem Datenbankobjekt ausgeführt wurde.|  
|[Audit Database Object Take Ownership (Ereignisklasse)](../../relational-databases/event-classes/audit-database-object-take-ownership-event-class.md)|Gibt an, dass eine Änderung des Besitzers für Objekte im Datenbankbereich erfolgt ist.|  
|[Audit Database Operation-Ereignisklasse](../../relational-databases/event-classes/audit-database-operation-event-class.md)|Gibt an, dass verschiedene Vorgänge, wie z.B. CHECKPOINT oder SUBSCRIBE QUERY NOTIFICATIONS, aufgetreten sind.|  
|[Audit Database Principal Impersonation (Ereignisklasse)](../../relational-databases/event-classes/audit-database-principal-impersonation-event-class.md)|Gibt an, dass ein Identitätswechsel innerhalb des Datenbankumfangs aufgetreten ist.|  
|[Audit Database Principal Management-Ereignisklasse](../../relational-databases/event-classes/audit-database-principal-management-event-class.md)|Gibt an, dass Prinzipale aus einer Datenbank erstellt, in einer Datenbank geändert oder gelöscht wurden..|  
|[Audit Database Scope GDR (Ereignisklasse)](../../relational-databases/event-classes/audit-database-scope-gdr-event-class.md)|Gibt an, dass eine GRANT-, REVOKE- oder DENY-Anweisung von Anweisungsberechtigungen durch den Benutzer in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausgelöst wurde.|  
|[Audit DBCC (Ereignisklasse)](../../relational-databases/event-classes/audit-dbcc-event-class.md)|Gibt an, dass ein DBCC-Befehl ausgegeben wurde.|  
|[Überwachungsvolltextereignisklasse](../../relational-databases/event-classes/audit-fulltext-event-class.md)|Gibt an, dass ein Volltextereignis aufgetreten ist.|  
|[Audit Login Change Password-Ereignisklasse](../../relational-databases/event-classes/audit-login-change-password-event-class.md)|Gibt an, dass ein Benutzer sein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldekennwort geändert hat.|  
|[Audit Login Change Property (Ereignisklasse)](../../relational-databases/event-classes/audit-login-change-property-event-class.md)|Gibt an, dass **sp_defaultdb**, **sp_defaultlanguage** oder ALTER LOGIN zum Ändern einer Eigenschaft bei einer Anmeldung verwendet wurden.|  
|[Audit Login (Ereignisklasse)](../../relational-databases/event-classes/audit-login-event-class.md)|Gibt an, dass ein Benutzer sich erfolgreich an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] angemeldet hat.|  
|[Audit Login Failed (Ereignisklasse)](../../relational-databases/event-classes/audit-login-failed-event-class.md)|Gibt an, dass ein Benutzer versucht hat, sich an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anzumelden, und diese Anmeldung einen Fehler erzeugt hat.|  
|[Audit Login GDR-Ereignisklasse](../../relational-databases/event-classes/audit-login-gdr-event-class.md)|Gibt an, dass das [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Anmelderecht hinzugefügt oder entfernt wurde.|  
|[Audit Logout (Ereignisklasse)](../../relational-databases/event-classes/audit-logout-event-class.md)|Gibt an, dass ein Benutzer sich an [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] abgemeldet hat.|  
|[Audit Object Derived Permission-Ereignisklasse](../../relational-databases/event-classes/audit-object-derived-permission-event-class.md)|Gibt an, dass eine CREATE-, ALTER- oder DROP-Anweisung für ein Objekt ausgegeben wurde.|  
|[Audit Schema Object Access (Ereignisklasse)](../../relational-databases/event-classes/audit-schema-object-access-event-class.md)|Gibt an, dass eine Objektberechtigung (wie z.B. SELECT) verwendet wurde.|  
|[Audit Schema Object GDR (Ereignisklasse)](../../relational-databases/event-classes/audit-schema-object-gdr-event-class.md)|Gibt an, dass eine GRANT-, REVOKE- oder DENY-Anweisung von Schemaobjektberechtigungen durch den Benutzer in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgelöst wurde.|  
|[Audit Schema Object Management (Ereignisklasse)](../../relational-databases/event-classes/audit-schema-object-management-event-class.md)|Gibt an, dass ein Serverobjekt erstellt, geändert oder gelöscht wurde.|  
|[Audit Schema Object Take Ownership-Ereignisklasse](../../relational-databases/event-classes/audit-schema-object-take-ownership-event-class.md)|Gibt an, dass die Berechtigungen zum Ändern des Schemaobjektsbesitzers überprüft wurden.|  
|[Audit Server Alter Trace (Ereignisklasse)](../../relational-databases/event-classes/audit-server-alter-trace-event-class.md)|Gibt an, dass die ALTER TRACE-Berechtigung überprüft wurde.|  
|[Audit Server Object GDR (Ereignisklasse)](../../relational-databases/event-classes/audit-server-object-gdr-event-class.md)|Gibt an, dass ein GDR-Ereignis für ein Schemaobjekt aufgetreten ist.|  
|[Audit Server Object Management (Ereignisklasse)](../../relational-databases/event-classes/audit-server-object-management-event-class.md)|Gibt an, dass ein CREATE-, ALTER- oder DROP-Ereignis auf einem Serverobjekt aufgetreten ist.|  
|[Audit Server Object Take Ownership-Ereignisklasse](../../relational-databases/event-classes/audit-server-object-take-ownership-event-class.md)|Gibt an, dass der Besitzer eines Serverobjekts geändert wurde.|  
|[Audit Server Operation (Ereignisklasse)](../../relational-databases/event-classes/audit-server-operation-event-class.md)|Gibt an, dass Überwachungsvorgänge auf dem Server aufgetreten sind.|  
|[Audit Server Principal Impersonation-Ereignisklasse](../../relational-databases/event-classes/audit-server-principal-impersonation-event-class.md)|Gibt an, dass ein Identitätswechsel innerhalb des Serverumfangs aufgetreten ist.|  
|[Audit Server Principal Management (Ereignisklasse)](../../relational-databases/event-classes/audit-server-principal-management-event-class.md)|Gibt an, dass ein CREATE-, ALTER- oder DROP-Ereignis auf einem Serverprinzipal aufgetreten ist.|  
|[Audit Server Scope GDR-Ereignisklasse](../../relational-databases/event-classes/audit-server-scope-gdr-event-class.md)|Gibt an, dass ein GDR-Ereignis für Serverberechtigungen aufgetreten ist.|  
|[Audit Server Starts and Stops (Ereignisklasse)](../../relational-databases/event-classes/audit-server-starts-and-stops-event-class.md)|Gibt an, dass der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienststatus geändert wurde.|  
|[Audit Statement Permission (Ereignisklasse)](../../relational-databases/event-classes/audit-statement-permission-event-class.md)|Gibt an, dass eine Anweisungsberechtigung verwendet wurde.|  
  
## Verwandte Inhalte  
 [Erweiterte Ereignisse](../../relational-databases/extended-events/extended-events.md)  
  
  