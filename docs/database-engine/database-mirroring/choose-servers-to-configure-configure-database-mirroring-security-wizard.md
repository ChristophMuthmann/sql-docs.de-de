---
title: Zu konfigurierende Server auswählen (Assistent zum Konfigurieren der Sicherheit für die Datenbankspiegelung) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
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
- sql13.swb.configdbmsecurwiz.choosesrvrs.f1
ms.assetid: 59e23ff3-d7ee-4e32-9629-0b54d3a258f7
caps.latest.revision: 25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 27a9b06d3afb1f0a5bd6e94907becbbaa7592950
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="choose-servers-to-configure-configure-database-mirroring-security-wizard"></a>Zu konfigurierende Server auswählen (Assistent zum Konfigurieren der Sicherheit für die Datenbankspiegelung)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Mithilfe dieser Seite können Sie angeben, welche Serverinstanzen nachfolgend konfiguriert werden sollen. Sie müssen mindestens eine Serverinstanz auswählen, bevor Sie den Assistenten fortsetzen können.  
  
 Wenn Sie ein Kontrollkästchen für eine Serverinstanz deaktivieren, nimmt der Assistent keine Änderung an dieser Instanz vor. Sie werden jedoch vom Assistenten aufgefordert, Informationen zur Instanz einzugeben und diese Informationen als Teil der Konfiguration der übrigen Serverinstanzen zu speichern. Wenn Sie beispielsweise das Kontrollkästchen für die Zeugenserverinstanz deaktivieren, werden Sie vom Assistenten aufgefordert, das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto des Zeugen einzugeben, da eine Anmeldung für dieses Konto als Teil der Sicherheitskonfiguration erstellt werden muss, die in den Prinzipal- und Spiegelserverinstanzen gespeichert wird.  
  
 **So konfigurieren Sie die Datenbankspiegelung mithilfe von SQL Server Management Studio**  
  
-   [Einrichten einer Datenbank-Spiegelungssitzung mithilfe der Windows-Authentifizierung &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [Starten des Assistenten zum Konfigurieren der Sicherheit für die Datenbankspiegelung &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Tastatur  
 **Prinzipalserverinstanz**  
 Wählen Sie diese Option aus, um die Sicherheit für den Prinzipalserver zu konfigurieren.  
  
 **Spiegelserverinstanz**  
 Wählen Sie diese Option aus, um die Sicherheit für den Spiegelserver zu konfigurieren.  
  
 **Zeugenserverinstanz**  
 Wählen Sie diese Option aus, um die Sicherheit für den Zeugenserver zu konfigurieren (falls vorhanden).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datenbankeigenschaften &#40;Seite Wird gespiegelt&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
