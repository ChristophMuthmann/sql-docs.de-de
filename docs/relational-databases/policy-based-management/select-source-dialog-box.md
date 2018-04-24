---
title: Dialogfeld 'Quelle auswählen' | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.dmf.selectsource.f1
ms.assetid: d664c2e5-dd0c-4da8-b27d-aa4ee4fc0ffd
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 18f561937a2ef6e870c067731a6eae26516d0c7e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="select-source-dialog-box"></a>Dialogfeld 'Quelle auswählen'
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Mithilfe dieses Dialogfelds können Sie die Quelle der zu ausführenden Richtlinien auswählen. Um eine oder mehrere XML-Dateien auszuwählen, die Richtlinien enthalten, wählen Sie **Dateien**aus. Um die Richtlinien auszuführen, die auf der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gefunden werden, wählen Sie **Server**aus.  
  
 Es gibt mehrere Möglichkeiten zum Öffnen dieses Dialogfelds.  
  
 **So öffnen Sie dieses Dialogfeld**  
  
-   Klicken Sie im Fenster „Registrierte Server“ mit der rechten Maustaste auf **Lokale Servergruppen** oder unter **Lokale Servergruppen**auf einen beliebigen Server oder unter **Zentrale Verwaltungsserver**auf einen beliebigen Server, und wählen Sie dann **Richtlinien auswerten**aus. Klicken Sie auf der Seite **Richtlinienauswahl** des Dialogfelds **Richtlinien auswerten** auf die Schaltfläche zum Durchsuchen (**...**).  
  
-   Erweitern Sie im Objekt-Explorer **Verwaltung**, erweitern Sie **Richtlinienverwaltung**, klicken Sie mit der rechten Maustaste auf **Richtlinien**, und wählen Sie dann **Richtlinie importieren**aus. Klicken Sie im Dialogfeld **Importieren** auf die Schaltfläche zum Durchsuchen (**...**).  
  
-   Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf einen Server, eine Datenbank oder ein Datenbankobjekt, wählen Sie **Richtlinien**aus, und wählen Sie dann **Auswerten**aus. Klicken Sie auf der Seite **Richtlinienauswahl** des Dialogfelds **Richtlinien auswerten** auf die Schaltfläche zum Durchsuchen (**...**).  
  
## <a name="options"></a>Tastatur  
 **Dateien**  
 Wählen Sie eine oder mehrere XML-Dateien aus, die Richtlinien enthalten.  
  
 **Server**  
 Ermöglicht es Ihnen, einen Server auszuwählen, der die Richtlinien enthält, die Sie ausführen möchten.  
  
 **Servertyp**  
 Nur [!INCLUDE[ssDE](../../includes/ssde-md.md)] -Server enthalten Richtlinien. Dieses Feld ist schreibgeschützt.  
  
 **Servername**  
 Wählen Sie die Serverinstanz aus, mit der eine Verbindung hergestellt werden soll. Standardmäßig wird die Serverinstanz angezeigt, zu der zuletzt eine Verbindung hergestellt wurde.  
  
 **Authentifizierung**  
 Beim Herstellen der Verbindung mit einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]sind zwei Authentifizierungsmodi verfügbar.  
  
 **Windows-Authentifizierungsmodus (Windows-Authentifizierung)**  
 Der Windows-Authentifizierungsmodus ermöglicht Benutzern das Herstellen einer Verbindung über ein Windows-Benutzerkonto.  
  
 **SQL Server-Authentifizierung**  
 Wenn ein Benutzer eine Verbindung mit einem angegebenen Benutzernamen und einem Kennwort von einer nicht vertrauenswürdigen Verbindung herstellt, führt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Authentifizierung durch, indem überprüft wird, ob ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldekonto eingerichtet wurde und ob das angegebene Kennwort mit dem zuvor aufgezeichneten übereinstimmt. Wenn kein Anmeldekonto in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eingerichtet wurde, schlägt die Authentifizierung fehl, und der Benutzer erhält eine Fehlermeldung.  
  
> [!IMPORTANT]  
>  Verwenden Sie nach Möglichkeit die Windows-Authentifizierung.  
  
 **User name**  
 Geben Sie den Benutzernamen für die Verbindung ein. Diese Option ist nur verfügbar, wenn Sie die Windows-Authentifizierung für die Verbindungsherstellung ausgewählt haben.  
  
 **Anmeldename**  
 Geben Sie den Anmeldenamen für die Verbindung ein. Diese Option ist nur verfügbar, wenn Sie zum Herstellen von Verbindungen die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Authentifizierung ausgewählt haben.  
  
 **Kennwort**  
 Geben Sie das Kennwort für die Anmeldung ein. Sie können diese Option nur bearbeiten, wenn Sie zum Verbinden die Authentifizierung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgewählt haben.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Richtlinienverwaltungsknoten &#40;Objekt-Explorer&#41;](../../relational-databases/policy-based-management/policy-management-node-object-explorer.md)   
 [Verwalten von Servern mit der richtlinienbasierten Verwaltung](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
