---
title: Schützen von RDS | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS security [ADO]
ms.assetid: 82fb1330-d6c6-4c17-ad3e-d417ff822b25
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0a1e409789ffae5114272fc0a3ce5c42eec82cb2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="securing-rds-applications"></a>Schützen von RDS
Dieses Thema enthält Sicherheitsinformationen für RDS.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="microsoft-internet-explorer-security-issues"></a>Microsoft Internet Explorer-Sicherheitsprobleme  
 Mit neuen sicherheitserweiterungen, die Microsoft Internet Explorer hinzugefügt werden sind einige ADO und RDS-Objekte beschränkt, nur in Umgebungen mit "sicheren" Modus ausgeführt. Dies erfordert, dass Sie diese Probleme, z. B. verschiedene Zonen, Sicherheitsstufen, restriktive Verhalten, unsichere Operationen und Sicherheitseinstellungen angepasst.  
  
## <a name="security-and-your-web-server"></a>Sicherheit und den Webserver  
 Bei Verwendung der [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) -Objekt, auf dem Internetinformationsdienste-Webserver, denken Sie daran, dass dies ein potenzielles Sicherheitsrisiko erstellt. Externe Benutzer, die gültige Datenquellenname (DSN), Benutzer-ID und Kennwortinformationen abgerufen werden konnte Seiten zum Senden von einer beliebigen Abfrage an, die Datenquelle geschrieben werden. Gegebenenfalls eingeschränkteren Zugriff auf eine Datenquelle ist eine Option zum Aufheben der Registrierung, und löschen die **RDSServer.DataFactory** Objekt (msadcf.dll), und verwenden Sie stattdessen benutzerdefinierten Geschäftsobjekte mit hartcodierten Abfragen.  
  
 Weitere Informationen zu den sicherheitsauswirkungen mit dem RDSServer.DataFactory-Objekt finden Sie unter Microsoft Security Bulletin MS99-025 auf der Website der Microsoft-Sicherheit.  
  
## <a name="client-impersonation-and-security"></a>Clientidentitätswechsel und Sicherheit  
 Wenn die **Kennwortauthentifizierung** Eigenschaft für den IIS-Webserver Windows NT Challenge/Response-Authentifizierung (für Windows NT 4.0) oder integrierte Windows-Authentifizierung (für Windows 2000) festgelegt ist, dann sind Geschäftsobjekten im Sicherheitskontext des Clients aufgerufen. Dies ist ein neues Feature in RDS 1.5, die über HTTP Clientidentitätswechsel ermöglicht. Wenn Sie in diesem Modus arbeiten, die Anmeldung an den Webserver (IIS) nicht anonym ist, aber verwendet werden, die Benutzer-ID und Kennwort an, unter der Client-Computer ausgeführt wird. Wenn die ODBC-Datenquellennamen für die vertrauenswürdige Verbindung verwenden eingerichtet werden, erfolgt der Zugriff auf Datenbanken, z. B. SQL Server, auch im Sicherheitskontext des Clients. Aber dies funktioniert nur, wenn die Datenbank auf demselben Computer wie der IIS befindet. die Clientanmeldeinformationen können nicht auf noch einen anderen Computer übertragen werden.  
  
 Angenommen, ein Client John Doe, UserID = "HerbertD" und das Kennwort = "geheimer" auf einem Clientcomputer angemeldet ist. Er führt eine browserbasierte Anwendung, die für den Zugriff benötigt die **RDSServer.DataFactory** zu erstellenden Objekts ein [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) durch das Ausführen einer SQL-Abfrage auf dem Computer "MyServer" IIS ausgeführt wird. "EigenerServer", ein System mit ausgeführtem Windows NT Server 4.0, Windows NT Challenge/Response-Authentifizierung verwenden eingerichtet ist, die ODBC-DSN hat "Vertrauenswürdige Verbindung verwenden" ausgewählt und der Server enthält außerdem die SQL Server-Datenquelle. Wenn auf dem Webserver eine Anforderung empfangen wird, fordert den Client für den Benutzer-ID und das Kennwort. Daher die Anforderung angemeldet ist "EigenerServer" problemgruppen "HerbertD" / "Geheime" anstelle von IUSER_MyServer (der Standard ist, wenn anonyme Kennwort-Authentifizierung aktiviert ist). Auf ähnliche Weise beim Anmelden an SQL Server, "HerbertD" / "Geheime" verwendet wird.  
  
 IIS Windows NT Challenge/Response-Authentifizierungsmodus kann folglich HTML-Seiten, ohne dass der Benutzer aufgefordert wird explizit für die Benutzer-ID und Kennwort benötigten Informationen zum Anmelden bei der Datenbank erstellt werden soll. Wenn die IIS-Standardauthentifizierung verwendet wurden, gehören klicken Sie dann dazu auch erforderliche Daten.  
  
## <a name="password-authentication"></a>Kennwort-Authentifizierung  
 RDS mit IIS-Webserver ausgeführt wird, in einem der drei Modi Kennwortauthentifizierung kommunizieren kann: anonym, Standard, oder NT Challenge/Response-Authentifizierung (integrierte Windows-Authentifizierung in Windows 2000 genannt). Diese Einstellungen definieren, wie ein Webserver steuert den Zugriff durch, wie etwa das vorschreiben, dass explizite Zugriffsberechtigungen auf dem NT-Webserver verfügen über einen Clientcomputer.


