---
title: Registrieren eines verbundenen Servers (SQL Server Management Studio) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/28/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-registration
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.registerserver.f1
helpviewer_keywords:
- Registered Servers [SQL Server], register connected servers
- connected server registrations [SQL Server]
ms.assetid: 77deb5f5-0f80-484f-8b8b-29afa67ec18f
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 48687c1e245c4e57d75b986e24e87c8a7bcb698f
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="register-a-connected-server-sql-server-management-studio"></a>Registrieren eines verbundenen Servers (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  In diesem Thema wird das Registrieren eines verbundenen Servers in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) beschrieben. Indem Sie den Server registrieren, können Sie die Verbindungsinformationen für Server, auf die Sie häufig zugreifen, speichern. Ein Server kann vor dem Verbinden oder bei der Verbindung im Objekt-Explorer registriert werden.  Sie können Ihre registrierten Server in SSMS anzeigen, indem Sie im Menü zu **Ansicht**\\**Registrierte Server** navigieren.
  
 **In diesem Thema**  
  
-   **So registrieren Sie einen Server mit**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-register-a-connected-server"></a>So registrieren Sie einen Server  
  
Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf einen Server, zu dem Sie bereits eine Verbindung hergestellt haben, und klicken Sie dann auf **Registrieren**.
  
**Servername**  
Dieses Feld zeigt als Standardwert den Namen des Servers an, mit dem Sie die Verbindung hergestellt haben.  Optional können Sie einen Servernamen eingeben oder in der Dropdownliste auswählen.

**Authentifizierung**  
Beim Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sind zwei Authentifizierungsmodi verfügbar: 

-    **Windows-Authentifizierung**  
Mit dem Windows-Authentifizierungsmodus können Benutzer die Verbindung über ein [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows-Benutzerkonto herstellen. 

-    **SQL Server-Authentifizierung**   
Wenn ein Benutzer eine Verbindung mit einem angegebenen Benutzernamen und einem Kennwort von einer nicht vertrauenswürdigen Verbindung herstellt, führt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Authentifizierung durch, indem überprüft wird, ob ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldekonto eingerichtet wurde und ob das angegebene Kennwort mit dem zuvor aufgezeichneten übereinstimmt. Wenn kein Anmeldekonto in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eingerichtet wurde, schlägt die Authentifizierung fehl, und der Benutzer erhält eine Fehlermeldung.

     > [!IMPORTANT]  
     > [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)] Weitere Informationen finden Sie unter [Auswählen eines Authentifizierungsmodus](../../relational-databases/security/choose-an-authentication-mode.md).  

     -    **User name**  
Zeigt den aktuellen Benutzernamen an, zu dem die Verbindung hergestellt wird. Diese schreibgeschützte Option ist nur verfügbar, wenn Sie zum Herstellen der Verbindung die Windows-Authentifizierung ausgewählt haben. Um **Benutzername**zu ändern, melden Sie sich bei dem Computer als ein anderer Benutzer an. 

     -    **Anmeldename**  
Geben Sie den Anmeldenamen für die Verbindung ein. Diese Option ist nur verfügbar, wenn Sie zum Verbinden die Authentifizierung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgewählt haben.  

     -    **Kennwort**  
Geben Sie das Kennwort für die Anmeldung ein. Diese Option kann nur bearbeitet werden, wenn Sie zum Verbinden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung ausgewählt haben. 

     -    **Kennwort speichern**  
Aktivieren Sie dieses Kontrollkästchen, damit das eingegebene Kennwort von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verschlüsselt und gespeichert wird. Diese Option wird nur angezeigt, wenn Sie zum Verbinden die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung ausgewählt haben.  

          > [!NOTE]  
          > Wenn Sie das Kennwort gespeichert haben und für die Zukunft nicht mehr speichern möchten, deaktivieren Sie das Kontrollkästchen, und klicken Sie auf **Speichern**.  

**Name des registrierten Servers**  
Der Name, der unter Registrierte Server angezeigt werden soll. Dieser Name muss mit dem Eintrag im Feld **Servername** nicht übereinstimmen.  
  
**Beschreibung des registrierten Servers**  
Geben Sie eine optionale Beschreibung des Servers ein.  
  
**Test**  
Klicken Sie hier, um die Verbindung mit dem unter **Servername**ausgewählten Server zu testen.  
  
**Speichern**  
Klicken Sie hier, um die Einstellungen des registrierten Servers zu speichern. 

## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Erstellen eines neu registrierten Servers (SQL Server Management Studio)](../../tools/sql-server-management-studio/create-a-new-registered-server-sql-server-management-studio.md)
  
  
