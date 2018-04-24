---
title: Prinzipalserverinstanz (Assistent zum Konfigurieren der Sicherheit für die Datenbankspiegelung) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: database-mirroring
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.configdbmsecurwiz.principalsrvr.f1
ms.assetid: 58af27d7-c5dd-4669-be6b-b472bc2c8ef4
caps.latest.revision: 36
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7baf8a9de820ef4d7829174b9606b00d8bc79511
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="principal-server-instance-configure-database-mirroring-security-wizard"></a>Prinzipalserverinstanz (Assistent zum Konfigurieren der Sicherheit für die Datenbankspiegelung)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Auf dieser Seite können Informationen zur Serverinstanz der Prinzipaldatenbank angegeben werden. Die Prinzipaldatenbank ist die Kopie der Datenbank, durch die die Spiegelungssitzung begonnen wird. Nach Beginn der Sitzung ist die Prinzipaldatenbank die Kopie der Datenbank, von der Benutzeränderungen angenommen werden. (Im Falle eines Failovers werden die Prinzipal- und Spiegelungsrollen vertauscht, d. h. die ursprüngliche Prinzipaldatenbank bleibt möglicherweise nicht als Prinzipaldatenbank erhalten.)  
  
 **So konfigurieren Sie die Datenbankspiegelung mithilfe von SQL Server Management Studio**  
  
-   [Einrichten einer Datenbank-Spiegelungssitzung mithilfe der Windows-Authentifizierung &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [Starten des Assistenten zum Konfigurieren der Sicherheit für die Datenbankspiegelung &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Tastatur  
 **Prinzipalserverinstanz**  
 Da eine Datenbankspiegelung in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] immer auf dem Prinzipalserver konfiguriert wird, handelt es sich bei der aktuellen Serverinstanz immer um die Prinzipalserverinstanz.  
  
 **Überwachungsport**  
 Das Verhalten dieser Option hängt auf folgende Weise davon ab, ob für diese Serverinstanz der Spiegelungsendpunkt vorhanden ist:  
  
-   Wenn für diese Serverinstanz der Überwachungsport nicht vorhanden ist, wird im Textfeld **Port** die Portnummer 5022 angezeigt. Sie können jede verfügbare Portnummer verwenden, wie z. B. 7022.  
  
-   Wenn der Spiegelungsendpunkt bereits vorhanden ist, wird die Portnummer dieses Endpunkts angezeigt. Wenn Sie diesen Port ändern müssen, verwenden Sie den Befehl ALTER ENDPOINT. Weitere Informationen finden Sie unter [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md).  
  
> [!NOTE]  
>  Eine Portnummer ist erforderlich.  
  
 **Endpunktname**  
 Wenn der Spiegelungsendpunkt für diese Serverinstanz vorhanden ist, wird der Endpunktname hier angezeigt. Ist der Endpunkt nicht vorhanden, dann können Sie den Namen für den Endpunkt hier festlegen.  
  
 **Durch diesen Endpunkt gesendete Daten verschlüsseln**  
 Standardmäßig ist die Verschlüsselung aktiviert. Wenn diese Option aktiviert ist, dann ist die Verschlüsselung erforderlich (nicht nur unterstützt), und es werden die Standardwerte für alle Verschlüsselungsoptionen verwendet. Weitere Informationen finden Sie unter [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md).  
  
 Um die Verschlüsselung zu deaktivieren, deaktivieren Sie das Kontrollkästchen. Um die Verschlüsselung wieder zu aktivieren, aktivieren Sie das Kontrollkästchen.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Der Datenbankspiegelungs-Endpunkt &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Datenbankeigenschaften &#40;Seite Wird gespiegelt&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Erstellen eines Endpunkts der Datenbankspiegelung für Windows-Authentifizierung (Transact-SQL)](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)   
 [Starten des Datenbankspiegelungs-Monitors &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
