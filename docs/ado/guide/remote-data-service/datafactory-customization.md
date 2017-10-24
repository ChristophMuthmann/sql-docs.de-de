---
title: DataFactory Anpassung | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DataFactory customization in RDS [ADO]
ms.assetid: 86d77985-a0d0-405a-8587-c85a20540a0e
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 044e738c69113740290843f14f0b2c14500307e1
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="datafactory-customization"></a>DataFactory-Anpassung
Remote Data Service (RDS) bietet eine Möglichkeit, einfacher Zugriff auf Daten in einem dreistufigen Client-/Server-System durchzuführen. Ein Client-Steuerelement gibt Verbindungs- und Parameter zum Ausführen einer Abfrage auf einem remote-Datenquelle oder Verbindungszeichenfolge und [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt Parameter zum Ausführen eines Updates.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Die Parameter werden an ein Serverprogramm übergeben, die den Datenzugriff Vorgang für die Remotedatenquelle ausführt. RDS bietet ein Standardserverprogramm der [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) Objekt. Die **RDSServer.DataFactory** Objekt zurückgibt, eine **Recordset** von einer Abfrage an den Client erstellte Objekt.  
  
 Allerdings die **RDSServer.DataFactory** ist zum Ausführen von Abfragen und Updates beschränkt. Es kann keine Verbindung oder Befehl Zeichenfolgen eine Überprüfung oder Verarbeitung ausführen.  
  
 Mit ADO, können Sie angeben, die die **DataFactory** funktionieren in Verbindung mit einem anderen Serverprogramm mit dem Namen eine *Handler*. Der Handler kann Clientverbindung und Befehlszeichenfolgen ändern, bevor sie den Zugriff auf die Datenquelle verwendet werden. Darüber hinaus kann der Handler Zugriffsrechte anweisen, die steuern die Fähigkeit des Clients zum Lesen und Schreiben von Daten in der Datenquelle.  
  
 Die Parameter, mit denen der Handler, ändern Sie die Clientparameter und Zugriffsrechte sind in Abschnitte einer Anpassung-Datei angegeben.  
  
 Die folgenden Themen enthalten weitere Informationen zum Anpassen der **DataFactory** Objekt.  
  
-   [Grundlegendes zu der Anpassungsdatei](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)  
  
-   [Connect-Abschnitt der Anpassungsdatei](../../../ado/guide/remote-data-service/customization-file-connect-section.md)  
  
-   [SQL-Abschnitt der Anpassungsdatei](../../../ado/guide/remote-data-service/customization-file-sql-section.md)  
  
-   [UserList-Abschnitt der Anpassungsdatei](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)  
  
-   [Logs-Abschnitt der Anpassungsdatei](../../../ado/guide/remote-data-service/customization-file-logs-section.md)  
  
-   [Erforderliche Clienteinstellungen](../../../ado/guide/remote-data-service/required-client-settings.md)  
  
-   [Schreiben Ihres eigenen benutzerdefinierten Handlers](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



