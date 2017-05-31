---
title: "Erstellen von Anmeldeinformationen – Authentifizieren beim Azure-Speicher | Microsoft Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2014
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.backuptourl.createcred.f1
ms.assetid: 0622619d-27c5-4ff0-83e5-cde31648c27a
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3bf85ebdf78e42466474e6c68a43219fbb546bd1
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="create-credential---authenticate-to-azure-storage"></a>Erstellen von Anmeldeinformationen – Authentifizieren beim Azure-Speicher
  Im Dialogfeld **URL-Sicherung – Erstellen von Anmeldeinformationen** können Sie neue SQL-Anmeldeinformationen erstellen.  
  
 Wenn Sie die Anmeldeinformationen mithilfe dieses Dialogfelds erstellen, müssen Sie ein Windows Azure-Verwaltungszertifikat bereitstellen, das dem lokalen Zertifikatspeicher hinzugefügt wurde, oder ein Veröffentlichungsprofil angeben, das auf den Computer heruntergeladen wurde, um das Abonnement und die Speicherkontoinformationen zu überprüfen.  
  
 **SQL-Anmeldeinformationen**  
 Geben Sie den Namen für die SQL-Anmeldeinformationen an, die Sie erstellen möchten.  
  
## <a name="windows-azure-credentials"></a>Windows Azure-Anmeldeinformationen  
 **Verwaltungszertifikat**  
 Mit dieser Option geben Sie ein Zertifikat aus dem lokalen Zertifikatspeicher an, das mit dem Verwaltungszertifikat von Windows Azure übereinstimmt. Weitere Informationen zu Windows Azure-Verwaltungszertifikaten finden Sie unter [Erstellen eines Verwaltungszertifikats für Windows Azure](http://go.microsoft.com/fwlink/?LinkId=320781).  
  
 **Abonnement**  
 Wählen Sie die zugehörige Windows Azure-Abonnement-ID für das Verwaltungszertifikat aus dem lokalen Zertifikatspeicher, oder geben bzw. fügen Sie sie ein.  
  
 **Veröffentlichungsprofil**  
 Verwenden Sie diese Option, wenn ein Veröffentlichungsprofil auf Ihren Computer heruntergeladen wurde. Bei dieser Option werden die Abonnement-ID und das Zertifikat automatisch aufgefüllt.  
  
> [!CAUTION]  
>  SQL Server unterstützt derzeit die Version 2.0 des Veröffentlichungsprofils. Weitere Informationen zum Herunterladen der unterstützten Version des Veröffentlichungsprofils finden Sie unter [Herunterladen des Veröffentlichungsprofils 2.0](http://go.microsoft.com/fwlink/?LinkId=396421).  
  
## <a name="storage-account"></a>Speicherkonto  
 Geben Sie den Namen des Speicherkontos an, in dem die Sicherungsdateien gespeichert werden sollen.  
  
  
