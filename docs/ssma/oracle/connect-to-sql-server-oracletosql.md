---
title: Herstellen einer Verbindung mit SQLServer (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4ef384ea-5f3e-4f70-ad7c-b62d7b0da628
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: v-pelars
ms.workload: Inactive
ms.openlocfilehash: bdc151d76e5caadbdc7ce1763db99e68c77392ed
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="connect-to-sql-server--oracletosql"></a>Herstellen einer Verbindung mit SQLServer (OracleToSQL)
Verwenden der **Herstellen einer Verbindung mit SQL Server** im Dialogfeld für die Verbindung mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , die Sie zum migrieren möchten. Für den Zugriff auf die **Herstellen einer Verbindung mit SQL Server** Dialogfeld auf die **Datei** Menü klicken Sie auf **Herstellen einer Verbindung mit SQL Server**.  
  
## <a name="options"></a>enthalten  
**Servername**  
Geben Sie an, oder wählen Sie die Instanz von SQL Server für die Verbindung. Standardmäßig ist die Instanz, der Sie zuletzt verbunden angezeigt.  
  
-   Wenn Sie eine Verbindung mit der Standardinstanz auf dem lokalen Computer herstellen, geben Sie entweder **"localhost"** oder einen Punkt (**.**).  
  
-   Wenn Sie eine Verbindung mit der Standardinstanz auf einem anderen Computer herstellen, geben Sie den Namen des Computers aus.  
  
-   Wenn Sie eine Verbindung mit einer benannten Instanz auf einem anderen Computer herstellen, geben Sie den Computernamen, einen umgekehrten Schrägstrich und den Instanznamen, z. B. *"EigenerServer"*\\*MyInstance*.  
  
**Serverport**  
Wenn die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ist nicht zum Akzeptieren von Verbindungen auf dem standardmäßigen Standardport (1433), geben Sie die Portnummer konfiguriert. Andernfalls lassen Sie diesen Wert leer.  
  
**Datenbank**  
Geben Sie die Datenbank, um Objekte und Daten zu migrieren. Diese Option ist nicht verfügbar, wenn es sich bei einer erneuten Verbindung zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**Authentifizierung**  
Wählen Sie die Authentifizierungsmethode, die verwendet wird, für die Verbindung [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Um Ihre aktuelle Windows-Konto zu verwenden, wählen Sie Windows-Authentifizierung. Angeben einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Anmeldenamen und ein Kennwort wählen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Authentifizierung.  
  
**Benutzername**  
Bei Verwendung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Authentifizierung, geben Sie den Anmeldenamen für diese Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Wenn Sie Windows-Authentifizierung verwenden, ist diese Option nicht verfügbar.  
  
**Kennwort**  
Bei Verwendung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Authentifizierung, geben Sie das Kennwort für die Anmeldung für diese Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Wenn Sie Windows-Authentifizierung verwenden, ist diese Option nicht verfügbar.  
  
**Verbindung verschlüsseln**  
Stellen Sie sichere Verbindung mit SQL Server herstellen möchten, verwenden Sie durch Überprüfen der Verbindung Verschlüsseln der **Verbindung verschlüsseln** Kontrollkästchen.  
  
**TrustServerCertificate**  
Wenn Sie diese Option verwenden möchten, wählen Sie die **vertrauenswürdiges Serverzertifikat** Kontrollkästchen.  
  
> [!NOTE]  
> So aktivieren Sie **vertrauenswürdiges Serverzertifikat**, "Encrypt" müssen festgelegt werden, um **"true"**.  
  
