---
title: "Konfigurieren der Dialogsicherheit für Ereignisbenachrichtigungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: service-broker
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- event notifications [SQL Server], security
ms.assetid: 12afbc84-2d2a-4452-935e-e1c70e8c53c1
caps.latest.revision: 
author: BYHAM
ms.author: rickbyh
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e7f03652828e07ca4f89d8c6259e4a682735e947
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="configure-dialog-security-for-event-notifications"></a>Konfigurieren der Dialogsicherheit für Ereignisbenachrichtigungen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Dialogsicherheit sollte für Ereignisbenachrichtigungen konfiguriert werden, die Meldungen an einen Service Broker auf einem Remoteserver senden. Die Dialogsicherheit muss entsprechend dem Modell für die vollständige Sicherheit von [!INCLUDE[ssSB](../../includes/sssb-md.md)] -Dialogen manuell konfiguriert werden. Das Modell für vollständige Sicherheit ermöglicht die Ver- und Entschlüsselung von Nachrichten, die an und von Remoteservern gesendet werden. Obwohl Ereignisbenachrichtigungen nur in eine Richtung gesendet werden, werden andere Nachrichten, z. B. Fehlermeldungen, auch in die Gegenrichtung zurückgegeben.  
  
## <a name="configuring-dialog-security-for-event-notifications"></a>Konfigurieren der Dialogsicherheit für Ereignisbenachrichtigungen  
 Der zum Implementieren der Dialogsicherheit für die Ereignisbenachrichtigung erforderliche Vorgang wird in den folgenden Schritten beschrieben. Diese Schritte schließen Aktionen ein, die sowohl auf dem Quellserver als auch auf dem Zielserver ausgeführt werden müssen. Der Quellserver ist der Server, auf dem die Ereignisbenachrichtigung erstellt wird. Der Zielserver ist der Server, der die Ereignisbenachrichtigungsmitteilung empfängt. Sie müssen die Aktionen in den einzelnen Schritten sowohl für den Quellserver als auch für den Zielserver abschließen, bevor Sie den Vorgang mit dem nächsten Schritt fortsetzen.  
  
> [!IMPORTANT]  
>  Alle Zertifikate müssen mit einem gültigen Start- und Ablaufdatum erstellt werden.  
  
 **Schritt 1: Richten Sie eine TCP-Portnummer und einen Zieldienstnamen ein.**  
  
 Richten Sie den TCP-Port ein, auf dem sowohl der Quellserver als auch der Zielserver Nachrichten empfangen. Sie müssen auch den Namen des Zielservers bestimmen.  
  
 **Schritt 2: Konfigurieren Sie die Verschlüsselung und die Freigabe von Zertifikaten für die Authentifizierung auf Datenbankebene.**  
  
 Führen Sie die folgenden Aktionen sowohl auf dem Quell- als auch auf dem Zielserver aus.  
  
|Quellserver|Zielserver|  
|-------------------|-------------------|  
|Wählen Sie die Datenbank aus bzw. erstellen Sie eine Datenbank, in der die Ereignisbenachrichtigung und der Hauptschlüssel gespeichert werden sollen.|Wählen Sie die Datenbank aus bzw. erstellen Sie eine Datenbank, in der der Hauptschlüssel gespeichert werden soll.|  
|Wenn für die Quelldatenbank kein Hauptschlüssel vorhanden ist, müssen Sie [einen Hauptschlüssel erstellen](../../t-sql/statements/create-master-key-transact-sql.md). Ein Hauptschlüssel muss sowohl in der Quelldatenbank als auch in der Zieldatenbank vorhanden sein, um das jeweilige Zertifikat zu sichern.|Wenn für die Zieldatenbank kein Hauptschlüssel vorhanden ist, müssen Sie einen Hauptschlüssel erstellen.|  
|[Erstellen Sie einen Anmeldenamen](../../t-sql/statements/create-login-transact-sql.md) und einen entsprechenden [Benutzer](../../t-sql/statements/create-user-transact-sql.md) für die Quelldatenbank.|Erstellen Sie einen Anmeldenamen und einen entsprechenden Benutzer für die Zieldatenbank.|  
|[Erstellen Sie ein Zertifikat](../../t-sql/statements/create-certificate-transact-sql.md) , dessen Besitzer der Benutzer der Quelldatenbank ist.|Erstellen Sie ein Zertifikat, dessen Besitzer der Benutzer der Zieldatenbank ist.|  
|[Sichern Sie das Zertifikat](../../t-sql/statements/backup-certificate-transact-sql.md) in einer Datei, auf die der Zielserver zugreifen kann.|Sichern Sie das Zertifikat in einer Datei, auf die der Quellserver zugreifen kann.|  
|[Erstellen Sie einen Benutzer](../../t-sql/statements/create-user-transact-sql.md), indem Sie den Benutzer der Zieldatenbank sowie WITHOUT LOGIN angeben. Dieser Benutzer ist später der Besitzer des Zieldatenbankzertifikats, das aus der Sicherungsdatei erstellt wird. Eine Zuordnung des Benutzers zu einem Anmeldenamen ist nicht erforderlich, da dieser Benutzer nur das in Schritt 3 erstellte Zieldatenbankzertifikat besitzen soll.|Erstellen Sie einen Benutzer, indem Sie den Benutzer der Quelldatenbank sowie WITHOUT LOGIN angeben. Dieser Benutzer ist später der Besitzer des Quelldatenbankzertifikats, das aus der Sicherungsdatei erstellt wird. Eine Zuordnung des Benutzers zu einem Anmeldenamen ist nicht erforderlich, da dieser Benutzer nur das in Schritt 3 erstellte Quelldatenbankzertifikat besitzen soll.|  
  
 **Schritt 3: Geben Sie die Zertifikate frei, und erteilen Sie Berechtigungen für die Authentifizierung auf Datenbankebene.**  
  
 Führen Sie die folgenden Aktionen sowohl auf dem Quell- als auch auf dem Zielserver aus.  
  
|Quellserver|Zielserver|  
|-------------------|-------------------|  
|[Erstellen Sie ein Zertifikat](../../t-sql/statements/create-certificate-transact-sql.md) aus der Sicherungsdatei des Zielzertifikats, und geben Sie dabei den Benutzer der Zieldatenbank als Besitzer an.|Erstellen Sie ein Zertifikat aus der Sicherungsdatei des Quellzertifikats, und geben Sie dabei den Benutzer der Quelldatenbank als Besitzer an.|  
|[Erteilen Sie dem Benutzer der Quelldatenbank die Berechtigung](../../t-sql/statements/grant-transact-sql.md) zum Erstellen der Ereignisbenachrichtigung. Weitere Informationen zu dieser Berechtigung finden Sie unter [CREATE EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-notification-transact-sql.md).|Erteilen Sie dem Benutzer der Zieldatenbank die REFERENCES-Berechtigung für den mit dem [!INCLUDE[ssSB](../../includes/sssb-md.md)] bestehenden Ereignisbenachrichtigungsvertrag: `http://schemas.microsoft.com/SQL/Notifications/PostEventNotification`.|  
|[Erstellen Sie eine Remotedienstbindung](../../t-sql/statements/create-remote-service-binding-transact-sql.md) zum Zieldienst, und geben Sie die Anmeldeinformationen des Zieldatenbankbenutzers an. Durch die Remotedienstbindung ist sichergestellt, dass die an den Zielserver gesendeten Nachrichten mit dem öffentlichen Schlüssel des Zertifikats, dessen Besitzer der Quelldatenbankbenutzer ist, authentifiziert werden.|[Erteilen Sie dem Zieldatenbankbenutzer](../../t-sql/statements/grant-transact-sql.md) die Berechtigungen CREATE QUEUE, CREATE SERVICE und CREATE SCHEMA.|  
||Wenn Sie als Zieldatenbankbenutzer noch keine Verbindung mit der Datenbank hergestellt haben, stellen Sie nun die Verbindung her.|  
||[Erstellen Sie eine Warteschlange](../../t-sql/statements/create-queue-transact-sql.md) für den Empfang der Ereignisbenachrichtigungen, und [erstellen Sie einen Dienst](../../t-sql/statements/create-service-transact-sql.md) für die Übermittlung der Nachrichten.|  
||[Erteilen Sie dem Quelldatenbankbenutzer die SEND-Berechtigung](../../t-sql/statements/grant-transact-sql.md) für den Zieldienst.|  
|Stellen Sie dem Zielserver den Service Broker-Bezeichner der Quelldatenbank zur Verfügung. Dieser Bezeichner kann durch Abfragen der **service_broker_guid** -Spalte der [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) -Katalogsicht abgerufen werden. Verwenden Sie für eine Ereignisbenachrichtigung auf Serverebene den Service Broker-Bezeichner von **msdb**.|Stellen Sie dem Quellserver den Service Broker-Bezeichner der Zieldatenbank zur Verfügung.|  
  
 **Schritt 4: Erstellen Sie Routen, und richten Sie die Authentifizierung auf Serverebene ein.**  
  
 Führen Sie die folgenden Aktionen sowohl auf dem Quell- als auch auf dem Zielserver aus.  
  
|Quellserver|Zielserver|  
|-------------------|-------------------|  
|[Erstellen Sie eine Route](../../t-sql/statements/create-route-transact-sql.md) zum Zieldienst, und geben Sie den Service Broker-Bezeichner der Zieldatenbank und die zu verwendende TCP-Portnummer an.|Erstellen Sie eine Route zum Quelldienst, und geben Sie den Service Broker-Bezeichner der Quelldatenbank und die zu verwendende TCP-Portnummer an. Geben Sie den Quelldienst mithilfe des folgenden bereitgestellten Dienstes an: `http://schemas.microsoft.com/SQL/Notifications/EventNotificationService`.|  
|Wechseln Sie zur **master** -Datenbank, um die Authentifizierung auf Serverebene zu konfigurieren.|Wechseln Sie zur **master** -Datenbank, um die Authentifizierung auf Serverebene zu konfigurieren.|  
|Wenn für die **master** -Datenbank kein Hauptschlüssel vorhanden ist, müssen Sie [einen Hauptschlüssel erstellen](../../t-sql/statements/create-master-key-transact-sql.md).|Wenn für die **master** -Datenbank kein Hauptschlüssel vorhanden ist, müssen Sie einen Hauptschlüssel erstellen.|  
|[Erstellen Sie ein Zertifikat](../../t-sql/statements/create-certificate-transact-sql.md) , mit dem die Datenbank authentifiziert wird.|Erstellen Sie ein Zertifikat, mit dem die Datenbank authentifiziert wird.|  
|[Sichern Sie das Zertifikat](../../t-sql/statements/backup-certificate-transact-sql.md) in einer Datei, auf die der Zielserver zugreifen kann.|Sichern Sie das Zertifikat in einer Datei, auf die der Quellserver zugreifen kann.|  
|[Erstellen Sie einen Endpunkt](../../t-sql/statements/create-endpoint-transact-sql.md), und geben Sie die zu verwendende TCP-Portnummer, FOR SERVICE_BROKER (AUTHENTICATION = CERTIFICATE *Name des Zertifikats*) und den Namen des Authentifizierungszertifikats an.|Erstellen Sie einen Endpunkt, und geben Sie die zu verwendende TCP-Portnummer, FOR SERVICE_BROKER (AUTHENTICATION = CERTIFICATE *Name des Zertifikats*) und den Namen des Authentifizierungszertifikats an.|  
|[Erstellen Sie eine Anmeldung](../../t-sql/statements/create-login-transact-sql.md), und geben Sie den Anmeldenamen des Zielservers an.|Erstellen Sie eine Anmeldung, und geben Sie den Anmeldenamen des Quellservers an.|  
|[Erteilen Sie dem Zielauthentifikator-Anmeldenamen die CONNECT-Berechtigung](../../t-sql/statements/grant-transact-sql.md) für den Endpunkt.|Erteilen Sie dem Quellauthentifikator-Anmeldenamen die CONNECT-Berechtigung für den Endpunkt.|  
|[Erstellen Sie einen Benutzer](../../t-sql/statements/create-user-transact-sql.md), und geben Sie den Zielauthentifikator-Anmeldenamen an.|Erstellen Sie einen Benutzer, und geben Sie den Quellauthentifikator-Anmeldenamen an.|  
  
 **Schritt 5: Geben Sie die Zertifikate für die Authentifizierung auf Serverebene frei, und erstellen Sie die Ereignisbenachrichtigung.**  
  
 Führen Sie die folgenden Aktionen sowohl auf dem Quell- als auch auf dem Zielserver aus.  
  
|Quellserver|Zielserver|  
|-------------------|-------------------|  
|[Erstellen Sie ein Zertifikat](../../t-sql/statements/create-certificate-transact-sql.md) aus der Sicherungsdatei des Zielzertifikats, und geben Sie dabei den Zielauthentifikatorbenutzer als Besitzer an.|Erstellen Sie ein Zertifikat aus der Sicherungsdatei des Quellzertifikats, und geben Sie dabei den Quellauthentifikatorbenutzer als Besitzer an.|  
|Wechseln Sie zu der Quelldatenbank, auf der die Ereignisbenachrichtigung erstellt werden soll. Wenn Sie als Quelldatenbankbenutzer noch keine Verbindung mit der Datenbank hergestellt haben, stellen Sie nun die Verbindung her.|Wechseln Sie zur Zieldatenbank, um Ereignisbenachrichtigungen zu empfangen.|  
|[Erstellen Sie die Ereignisbenachrichtigung](../../t-sql/statements/create-event-notification-transact-sql.md), und geben Sie den Broker-Dienst und den Bezeichner der Zieldatenbank an.||  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Implementieren von Ereignisbenachrichtigungen](../../relational-databases/service-broker/implement-event-notifications.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/create-remote-service-binding-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [CREATE ROUTE &#40;Transact-SQL&#41;](../../t-sql/statements/create-route-transact-sql.md)   
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [CREATE SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [CREATE EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-notification-transact-sql.md)  
  
  
