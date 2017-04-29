---
title: DDL-Ereignisse | Microsoft Dokumentation
ms.custom: 
ms.date: 11/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-ddl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DDL events
- DDL triggers, events
- events [SQL Server], DDL
ms.assetid: 62ef24b4-3553-4aed-b62a-670980bae501
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 411eb6c824b073818fbda216ba801d34ee5bcf0b
ms.lasthandoff: 04/11/2017

---
# <a name="ddl-events"></a>DDL-Ereignisse
  Die folgenden Tabellen geben einen Überblick über die DDL-Ereignisse, die verwendet werden können, um einen DDL-Trigger oder eine Ereignisbenachrichtigung auszuführen. Beachten Sie, dass jedes Ereignis einer [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung oder einer gespeicherten Prozedur entspricht. Dabei wird die Anweisungssyntax so geändert, dass Unterstriche (_) zwischen Schlüsselwörtern eingefügt werden.  
  
> [!IMPORTANT]  
>  Gespeicherte Systemprozeduren, die DDL-ähnliche Vorgänge ausführen, können auch DDL-Trigger und Ereignisbenachrichtigungen auslösen. Testen Sie die DDL-Trigger oder Ereignisbenachrichtigungen, um ihre Reaktion auf gespeicherte Systemprozeduren, die ausgeführt werden, zu bestimmen. Die CREATE TYPE-Anweisung und die gespeicherte Prozedur **sp_addtype** lösen z. B. beide einen DDL-Trigger oder eine Ereignisbenachrichtigung aus, die für ein CREATE_TYPE-Ereignis erstellt wird.  
  
## <a name="ddl-statements-that-have-server-or-database-scope"></a>DDL-Anweisungen, die für Server- oder Datenbankbereich gültig sind  
 DDL-Trigger oder Ereignisbenachrichtigungen können erstellt werden, um als Antwort auf die folgenden Ereignisse ausgelöst zu werden, wenn sie in der Datenbank, in der der Trigger oder die Ereignisbenachrichtigung erstellt wurden, oder irgendwo in der Serverinstanz auftreten.  
  
||||  
|-|-|-|  
|CREATE_APPLICATION_ROLE (gilt für die CREATE APPLICATION ROLE-Anweisung und **sp_addapprole**. Wenn ein neues Schema erstellt wird, löst dieses Ereignis auch ein CREATE_SCHEMA-Ereignis aus.)|ALTER_APPLICATION_ROLE (gilt für die ALTER APPLICATION ROLE-Anweisung und **sp_approlepassword**.)|DROP_APPLICATION_ROLE (gilt für die DROP APPLICATION ROLE-Anweisung und **sp_dropapprole**.)|  
|CREATE_ASSEMBLY|ALTER_ASSEMBLY|DROP_ASSEMBLY|  
|CREATE_ASYMMETRIC_KEY|ALTER_ASYMMETRIC_KEY|DROP_ASYMMETRIC_KEY|  
|ALTER_AUTHORIZATION|ALTER_AUTHORIZATION_DATABASE (gilt für die ALTER AUTHORIZATION-Anweisung, wenn ON DATABASE angegeben wird, und **sp_changedbowner**.)||  
|CREATE_BROKER_PRIORITY|CREATE_BROKER_PRIORITY|CREATE_BROKER_PRIORITY|  
|CREATE_CERTIFICATE|ALTER_CERTIFICATE|DROP_CERTIFICATE|  
|CREATE_CONTRACT|DROP_CONTRACT||  
|CREATE_CREDENTIAL|ALTER_CREDENTIAL|DROP_CREDENTIAL|  
|GRANT_DATABASE|DENY_DATABASE|REVOKE_DATABASE|  
|CREATE_DATABASE_AUDIT_SPEFICIATION|ALTER_DATABASE_AUDIT_SPEFICIATION|DENY_DATABASE_AUDIT_SPEFICIATION|  
|CREATE_DATABASE_ENCRYPTION_KEY|ALTER_DATABASE_ENCRYPTION_KEY|DROP_DATABASE_ENCRYPTION_KEY|  
|CREATE_DEFAULT|DROP_DEFAULT||  
|BIND_DEFAULT (gilt für **sp_bindefault**.)|UNBIND_DEFAULT (gilt für **sp_unbindefault**.)||  
|CREATE_EVENT_NOTIFICATION|DROP_EVENT_NOTIFICATION||  
|CREATE_EXTENDED_PROPERTY (gilt für **sp_addextendedproperty**.)|ALTER_EXTENDED_PROPERTY (gilt für **sp_updateextendedproperty**.)|DROP_EXTENDED_PROPERTY (gilt für **sp_dropextendedproperty**.)|  
|CREATE_FULLTEXT_CATALOG (gilt für die CREATE FULLTEXT CATALOG-Anweisung und **sp_fulltextcatalog** , wenn *create* angegeben wird.)|ALTER_FULLTEXT_CATALOG (gilt für die ALTER FULLTEXT CATALOG-Anweisung und **sp_fulltextcatalog** , wenn *start_incremental*, *start_full*, *Stop*oder *Rebuild* angegeben wird, und für **sp_fulltext_database** , wenn *enable* angegeben wird.)|DROP_FULLTEXT_CATALOG (gilt für die DROP FULLTEXT CATALOG-Anweisung und **sp_fulltextcatalog** , wenn *drop* angegeben wird.)|  
|CREATE_FULLTEXT_INDEX (gilt für die CREATE FULLTEXT INDEX-Anweisung und **sp_fulltexttable** , wenn *create* angegeben wird.)|ALTER_FULLTEXT_INDEX (gilt für die ALTER FULLTEXT INDEX-Anweisung und **sp_fulltextcatalog** , wenn *start_full*, *start_incremental*oder *stop* angegeben wird, sowie für **sp_fulltext_column**und **sp_fulltext_table** , wenn eine andere Aktion als *create* oder *drop* angegeben wird.)|DROP_FULLTEXT_INDEX (gilt für die DROP FULLTEXT INDEX-Anweisung und **sp_fulltexttable** , wenn *drop* angegeben wird.)|  
|CREATE_FULLTEXT_STOPLIST|ALTER_FULLTEXT_STOPLIST|DROP_FULLTEXT_STOPLIST|  
|CREATE_FUNCTION|ALTER_FUNCTION|DROP_FUNCTION|  
|CREATE_INDEX|ALTER_INDEX (gilt für die ALTER INDEX-Anweisung und **sp_indexoption**.)|DROP_INDEX|  
|CREATE_MASTER_KEY|ALTER_MASTER_KEY|DROP_MASTER_KEY|  
|CREATE_MESSAGE_TYPE|ALTER_MESSAGE_TYPE|DROP_MESSAGE_TYPE|  
|CREATE_PARTITION_FUNCTION|ALTER_PARTITION_FUNCTION|DROP_PARTITION_FUNCTION|  
|CREATE_PARTITION_SCHEME|ALTER_PARTITION_SCHEME|DROP_PARTITION_SCHEME|  
|CREATE_PLAN_GUIDE (gilt für **sp_create_plan_guide**.)|ALTER_PLAN_GUIDE (gilt für **sp_control_plan_guide** , wenn ENABLE, ENABLE ALL, DISABLE oder DISABLE ALL angegeben wird.)|DROP_PLAN_GUIDE (gilt für **sp_control_plan_guide** , wenn DROP oder DROP ALL angegeben wird.)|  
|CREATE_PROCEDURE|ALTER_PROCEDURE (gilt für die ALTER PROCEDURE-Anweisung und **sp_procoption**.)|DROP_PROCEDURE|  
|CREATE_QUEUE|ALTER_QUEUE|DROP_QUEUE|  
|CREATE_REMOTE_SERVICE_BINDING|ALTER_REMOTE_SERVICE_BINDING|DROP_REMOTE_SERVICE_BINDING|  
|CREATE_SPATIAL_INDEX|||  
|RENAME (gilt für **sp_rename**)|||  
|CREATE_ROLE (gilt für die CREATE ROLE-Anweisung, **sp_addrole**und **sp_addgroup**.)|ALTER_ROLE|DROP_ROLE (gilt für die DROP ROLE-Anweisung, **sp_droprole**und **sp_dropgroup**.)|  
|ADD_ROLE_MEMBER|DROP_ROLE_MEMBER||  
|CREATE_ROUTE|ALTER_ROUTE|DROP_ROUTE|  
|CREATE_RULE|DROP_RULE||  
|BIND_RULE (gilt für **sp_bindrule**.)|UNBIND_RULE (gilt für **sp_unbindrule**.)||  
|CREATE_SCHEMA (gilt für die CREATE SCHEMA-Anweisung, **sp_addrole**, **sp_adduser**, **sp_addgroup**und **sp_grantdbaccess**.)|ALTER_SCHEMA (gilt für die ALTER SCHEMA-Anweisung und **sp_changeobjectowner**.)|DROP_SCHEMA|  
|CREATE_SEARCH_PROPERTY_LIST|ALTER_SEARCH_PROPERTY_LIST|DROP_SEARCH_PROPERTY_LIST|  
|CREATE_SEQUENCE_EVENTS|CREATE_SEQUENCE_EVENTS|CREATE_SEQUENCE_EVENTS|  
|CREATE_SERVER_ROLE|ALTER_SERVER_ROLE|DROP_SERVER_ROLE|  
|CREATE_SERVICE|ALTER_SERVICE|DROP_SERVICE|  
|ALTER_SERVICE_MASTER_KEY|BACKUP_SERVICE_MASTER_KEY|RESTORE_SERVICE_MASTER_KEY|  
|ADD_SIGNATURE (für Signaturvorgänge von Objekten ohne Schemabereich; Datenbank, Assembly, Trigger)|DROP_SIGNATURE||  
|ADD_SIGNATURE_SCHEMA_OBJECT (für Objekte mit Schemabereich; gespeicherte Prozeduren, Funktionen)|DROP_SIGNATURE_SCHEMA_OBJECT||  
|CREATE_SPATIAL_INDEX|ALTER_INDEX kann für räumliche Indizes verwendet werden.|DROP_INDEX kann für räumliche Indizes verwendet werden.|  
|CREATE_STATISTICS|DROP_STATISTICS|UPDATE_STATISTICS|  
|CREATE_SYMMETRIC_KEY|ALTER_SYMMETRIC_KEY|DROP_SYMMETRIC_KEY|  
|CREATE_SYNONYM|DROP_SYNONYM||  
|CREATE_TABLE|ALTER_TABLE (gilt für die ALTER TABLE-Anweisung und **sp_tableoption**.)|DROP_TABLE|  
|CREATE_TRIGGER|ALTER_TRIGGER (gilt für die ALTER TRIGGER-Anweisung und **sp_settriggerorder**.)|DROP_TRIGGER|  
|CREATE_TYPE (gilt für die CREATE TYPE-Anweisung und **sp_addtype**.)|DROP_TYPE (gilt für die DROP TYPE-Anweisung und **sp_droptype**.)||  
|CREATE_USER (gilt für die CREATE USER-Anweisung, **sp_adduser**und **sp_grantdbaccess**.)|ALTER_USER (gilt für die ALTER USER-Anweisung und **sp_change_users_login**.)|DROP_USER (gilt für die DROP USER-Anweisung, **sp_dropuser**und **sp_revokedbaccess**.)|  
|CREATE_VIEW|ALTER_VIEW|DROP_VIEW|  
|CREATE_XML_INDEX|ALTER_INDEX kann für XML-Indizes verwendet werden.|DROP_INDEX kann für XML-Indizes verwendet werden.|  
|CREATE_XML_SCHEMA_COLLECTION|ALTER_XML_SCHEMA_COLLECTION|DROP_XML_SCHEMA_COLLECTION|  
  
## <a name="ddl-statements-that-have-server-scope"></a>DDL-Anweisungen, die für den Serverbereich gültig sind  
 DDL-Trigger oder Ereignisbenachrichtigungen können erstellt werden, um als Antwort auf die folgenden Ereignisse ausgelöst zu werden, wenn sie irgendwo in der Serverinstanz auftreten.  
  
||||  
|-|-|-|  
|ALTER_AUTHORIZATION_SERVER|ALTER_SERVER_CONFIGURATION|ALTER_INSTANCE (gilt für **sp_configure** und **sp_addserver** , wenn eine lokale Serverinstanz angegeben wird.)|  
|CREATE_AVAILABILITY_GROUP|ALTER_AVAILABILITY_GROUP|DROP_AVAILABILITY_GROUP|  
|CREATE_CREDENTIAL|ALTER_CREDENTIAL|DROP_CREDENTIAL|  
|CREATE_CRYPTOGRAPHIC_PROVIDER|ALTER_CRYPTOGRAPHIC_PROVIDER|DROP_CRYPTOGRAPHIC_PROVIDER|  
|CREATE_DATABASE|ALTER_DATABASE (gilt für die ALTER DATABASE-Anweisung und **sp_fulltext_database**.)|DROP_DATABASE|  
|CREATE_ENDPOINT|ALTER_ENDPOINT|DROP_ENDPOINT|  
|CREATE_EVENT_SESSION|ALTER_EVENT_SESSION|DROP_EVENT_SESSION|  
|CREATE_EXTENDED_PROCEDURE (gilt für **sp_addextendedproc**.)|DROP_EXTENDED_PROCEDURE (gilt für **sp_dropextendedproc**.)||  
|CREATE_LINKED_SERVER (gilt für **sp_addlinkedserver**.)|ALTER_LINKED_SERVER (gilt für **sp_serveroption**.)|DROP_LINKED_SERVER (gilt für **sp_dropserver** , wenn ein Verbindungsserver angegeben wird.)|  
|CREATE_LINKED_SERVER_LOGIN (gilt für **sp_addlinkedsrvlogin**.)|DROP_LINKED_SERVER_LOGIN (gilt für **sp_droplinkedsrvlogin**.)||  
|CREATE_LOGIN (gilt für die CREATE LOGIN-Anweisung, **sp_addlogin**, **sp_grantlogin**, **xp_grantlogin**und **sp_denylogin** bei Verwendung für einen nicht vorhandenen Anmeldenamen, der implizit erstellt werden muss.)|ALTER_LOGIN (gilt für die ALTER LOGIN-Anweisung, **sp_defaultdb**, **sp_defaultlanguage**, **sp_password**und **sp_change_users_login** , wenn *Auto_Fix* angegeben wird.)|DROP_LOGIN (gilt für die DROP LOGIN-Anweisung, **sp_droplogin**, **sp_revokelogin**und **xp_revokelogin**.)|  
|CREATE_MESSAGE (gilt für **sp_addmessage**.)|ALTER_MESSAGE (gilt für **sp_altermessage**.)|DROP_MESSAGE (gilt für **sp_dropmessage**.)|  
|CREATE_REMOTE_SERVER (gilt für **sp_addserver**.)|ALTER_REMOTE_SERVER (gilt für **sp_setnetname**.)|DROP_REMOTE_SERVER (gilt für **sp_dropserver** , wenn ein Remoteserver angegeben wird.)|  
|CREATE_RESOURCE_POOL|ALTER_RESOURCE_POOL|DROP_RESOURCE_POOL|  
|GRANT_SERVER|DENY_SERVER|REVOKE_SERVER|  
|ADD_SERVER_ROLE_MEMBER|DROP_SERVER_ROLE_MEMBER||  
|CREATE_SERVER_AUDIT|ALTER_SERVER_AUDIT|DROP_SERVER_AUDIT|  
|CREATE_SERVER_AUDIT_SPECIFICATION|ALTER_SERVER_AUDIT_SPECIFICATION|DROP_SERVER_AUDIT_SPECIFICATION|  
|CREATE_WORKLOAD_GROUP|ALTER_WORKLOAD_GROUP|DROP_WORKLOAD_GROUP|  
  
## <a name="see-also"></a>Siehe auch  
 [DDL-Trigger](../../relational-databases/triggers/ddl-triggers.md)   
 [Ereignisbenachrichtigungen](../../relational-databases/service-broker/event-notifications.md)   
 [DDL-Ereignisgruppen](../../relational-databases/triggers/ddl-event-groups.md)  
  
  

