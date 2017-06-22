---
title: Herstellen einer Verbindung mit einem Microsoft Azure-Abonnement | Microsoft Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cca5a270-643f-4677-8802-98464f19f82a
caps.latest.revision: 4
author: dagiro
ms.author: v-dagir
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6db65c242dc6dd9fd1c6c910d583d026f45422c1
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="connect-to-a-microsoft-azure-subscription"></a>Herstellen einer Verbindung mit einem Microsoft Azure-Abonnement
Verwenden Sie **Mit einem Microsoft-Abonnement verbinden** , um einen vorhandenen Azure-Blobcontainer bei Ihrer Instanz von SQL Server zu registrieren.  Das Dialogfeld erstellt eine SAS und die gespeicherte Zugriffsrichtlinie für einen Azure-Blobcontainer und dann SQL Server-Anmeldeinformationen.  Dieses Dialogfeld wird angezeigt, wenn die Sicherungs- oder Wiederherstellungsaufgabe von SQL Server Management Studio verwendet wird, und der Vorgang ein URL-Medium einbezieht.

## <a name="limitation"></a>Einschränkung
**Mit einem Microsoft-Abonnement verbinden** funktioniert nur mit einem Azure Storage-Konto, das über das Dienstverwaltungs-Bereitstellungsmodell (klassisch) erstellt wurde.  Weitere Informationen zu Azure-Bereitstellungsmodellen finden Sie unter [Azure Resource Manager-Bereitstellung im Vergleich zur klassischen Bereitstellung: Grundlegendes zu Bereitstellungsmodellen und zum Status von Ressourcen](https://azure.microsoft.com/en-us/documentation/articles/resource-manager-deployment-model/).

## <a name="options"></a>Optionen
**Anmelden**     
Melden Sie sich mit dem entsprechenden Azure-Konto an.

**Zu verwendendes Abonnement auswählen**      
Wählen Sie das gewünschte Abonnement aus der Dropdownliste.

**Speicherkonto auswählen**  
Wählen Sie aus der Dropdownliste das gewünschte Speicherkonto aus.

**Blobcontainer auswählen**   
Wählen Sie den gewünschten Blobcontainer aus der Dropdownliste.

**Ablauf der Richtlinie für den gemeinsamen Zugriff**   
Die SAS-Richtlinie läuft an diesem Datum ab.  Die Standardgültigkeitsdauer beträgt ein Jahr ab der Erstellung.  Ändern Sie es nach Bedarf.

**Generierte Shared Access Signature**   
Das Rich-Text-Feld zeigt die generierte SAS an.

**Anmeldeinformationen erstellen**   
Über diese Schaltfläche wird eine gespeicherte Zugriffsrichtlinie sowie eine SAS generiert, und dann werden SQL Server-Anmeldeinformationen erstellt.

