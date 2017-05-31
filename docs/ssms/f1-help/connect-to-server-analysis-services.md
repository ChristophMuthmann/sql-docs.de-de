---
title: Verbindung mit Server herstellen (Analysis Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connection.login.analysisserver.f1
ms.assetid: 7e277d22-8d4b-422e-8882-7c5dd7a6d915
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 73451189bc401a4167c65261f3adcc5aabb6627c
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-analysis-services"></a>Verbindung mit Server herstellen (Analysis Services)
Verwenden Sie dieses Dialogfeld, um Optionen für Verbindungen mit Computern mit [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] anzuzeigen oder anzugeben.  
  
## <a name="options"></a>enthalten  
**Servertyp**  
Wenn Sie einen Server über den Objekt-Explorer registrieren, wählen Sie den Typ des Servers aus, mit dem eine Verbindung hergestellt wird: [!INCLUDE[ssDE](../../includes/ssde_md.md)], Analysis Services, Reporting Services oder Integration Services. Im verbleibenden Bereich des Dialogfelds werden nur die Optionen angezeigt, die auf den ausgewählten Servertyp zutreffen. Wenn Sie einen Server über „Registrierte Server“ registrieren, ist das Feld **Servertyp** schreibgeschützt, wobei der Feldeintrag mit dem in der Komponente „Registrierte Server“ angezeigten Servertyp übereinstimmt. Zum Registrieren eines anderen Servertyps wählen Sie auf der Symbolleiste "Registrierte Server" die Option [!INCLUDE[ssDE](../../includes/ssde_md.md)], "Analysis Services", "Reporting Services" oder "Integration Services" aus. Anschließend können Sie mit der Registrierung eines neuen Servers beginnen.  
  
**Servername**  
Wählen Sie die Serverinstanz aus, mit der eine Verbindung hergestellt werden soll. Standardmäßig wird die Serverinstanz angezeigt, mit der zuletzt eine Verbindung bestanden hat.  
  
**Authentifizierung**  
Beim Herstellen einer Verbindung mit einer Instanz von Analysis Services werden die folgenden Authentifizierungsmodi unterstützt: [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows-Authentifizierung.  
  
**Windows-Authentifizierungsmodus (Windows-Authentifizierung)**  
Mit dem Modus**Windows-Authentifizierung** können Benutzer die Verbindung über ein Windows-Benutzerkonto herstellen.  
  
**Benutzername**  
Diese Option steht in dieser Version nicht zur Verfügung. Geben Sie den Benutzernamen für die Verbindung ein. Diese Option ist nur verfügbar, wenn Sie die **Windows-Authentifizierung**für die Verbindungsherstellung ausgewählt haben.  
  
**Kennwort**  
Diese Option steht in dieser Version nicht zur Verfügung. Geben Sie das Kennwort für die Anmeldung ein. Sie können diese Option nur bearbeiten, wenn Sie zum Verbinden die Authentifizierung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ausgewählt haben.  
  
**Connect**  
Klicken Sie hier, um eine Verbindung mit dem oben ausgewählten Server herzustellen.  
  
**enthalten**  
Klicken Sie auf diese Schaltfläche, um zusätzliche Optionen für die Serververbindung anzuzeigen, z. B. zum Registrieren eines Servers oder zum Speichern des Kennworts.  
  

