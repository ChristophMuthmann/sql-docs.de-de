---
title: Kennwort zurücksetzen – Analytics Platform System | Microsoft Docs
description: Die Seite "Kennwort zurücksetzen" können Sie so ändern Sie das Kennwort für die Administratorkonten von Analytics Platform System verwendet.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 63fbb097bf1ca926223ce7c0114c8da5d10cd969
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="password-reset---analytics-platform-system"></a>Das Zurücksetzen des Kennworts - Analyseplattformsystem
Die **Kennwortzurücksetzung** auf der Seite können Sie so ändern Sie das Kennwort für die Administratorkonten von Analytics Platform System verwendet.  
  
> [!WARNING]  
> Verwenden Sie immer die **Configuration Manager** die Einheit für Domänenadministratorkennwort zu aktualisieren. Andere Methoden möglicherweise nicht alle Komponenten von Analytics Platform System aktualisiert und Appliance Zugriffsprobleme verursachen könnte.  
  
Die Kennwörter Analytics Platform System erhalten, wenn das Gerät übermittelt wird. Immer ändern Sie die Kennwörter mit neuen Werten, wenn Sie die Verantwortung für Ihre Anwendung erstellen. Es gibt drei Kennwörter aktualisieren. Die Kennwörter müssen nicht miteinander übereinstimmen.  
  
**-F <*Xxxx*> \Administrator**  
Die **Administrator** der Appliance Domäne.  
  
**. \Administrator**  
Die lokale **Administrator** Konto auf den Computern, auf denen die virtuellen Computer gehostet.  
  
> [!IMPORTANT]  
> Für die Appliance update 1, **Configuration Manager** wird nicht ordnungsgemäß geändert, das Kennwort für die lokale Administratorkonten im gesamten der PDW VM. Wenn dies erforderlich ist, wenden Sie sich an den CSS für Weitere Informationen zu erhalten.  
  
**SA**  
Die **sa** Anmeldung in SQL Server. **SA** ist ein Mitglied der **Sysadmin** festen Serverrolle und SQL Server-Administrator ist. Das Kennwort für die **sa** Anmeldung kann auch geändert werden, mithilfe der **ALTER LOGIN** Anweisung.  
  
## <a name="password-requirements"></a>Für das Domänenkennwort  
Die Anmeldeinformationen des Domänenadministrators und die Anmeldeinformationen des Administrators entsprechen, um die Richtlinien zur kennwortsicherheit für jeden Typ von Anmeldeinformationen. Wenn Sie die Anmeldeinformationen des Domänenadministrators ändern, wird das neue Kennwort aktualisiert, mit der Domäne, falls in der gesamten SQL Server PDW erforderlich.  
  
> [!IMPORTANT]  
> SQL Server PDW unterstützt nicht das Dollarzeichen (**$**) in der Domänenadministrator oder ein lokaler Administratorkennwörter. Die Zeichen **^ % &** sind jedoch PowerShell diese als Sonderzeichen sieht in Kennwörtern, zulässig. Wenn eines dieser Zeichen in Kennwörtern, für den Systemadministrator oder den SQL Server verwendet werden**sa** Konten (die **AdminPassword** und **PdwSAPassword** Parametern während der Setup) klicken Sie dann setup, einschließlich Installation, UPGRADE, REPLACENODE und PATCHEN, schlägt fehl. Um ein erfolgreiches Upgrade sicherzustellen, dass beim aktuellen Kennwörter nicht unterstützte Zeichen enthalten, ändern Sie diese Kennwörter, sodass sie keine solche Zeichen vor dem Ausführen der Aktualisierung enthalten. Nach Abschluss des Upgrades können Sie diese Kennwörter zurück in ihre ursprünglichen Werte festlegen. Weitere Informationen zu kennwortanforderungen finden Sie unter [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md).  
  
## <a name="to-reset-a-password"></a>Zurücksetzen des Kennworts  
  
1.  Herstellen einer Verbindung mit dem Knoten "Zugriffssteuerung", und starten Sie die **Configuration Manager** (**dwconfig.exe**). Weitere Informationen finden Sie unter [Starten des Konfigurations-Managers &#40;Analyseplattformsystem&#41;](launch-the-configuration-manager.md).  
  
2.  Im linken Bereich des der **Configuration Manager**, klicken Sie auf **Kennwortzurücksetzung**.  
  
3.  Wählen Sie den Administrator aus der **Konto** Dropdown-Menü, und geben Sie dann das neue Kennwort in die **Kennwort** und **Kennwort bestätigen** Felder. Klicken Sie auf **übernehmen** zum Speichern der Änderungen.  
  
    Änderungen, die Sie für diese Konten stellen wirken sich nicht auf alle aktuell aktiven Sitzungen, aber bei der nächsten Anmeldung für jeden Benutzer angewendet werden.  
  
    ![SQL Server DWConfig, Kennwort](./media/password-reset/SQL_Server_PDW_DWConfig_TopPW.png "SQL_Server_PDW_DWConfig_TopPW")  
  
## <a name="see-also"></a>Siehe auch  
[Legen Sie das Administratorkennwort für das Anmelden beim AD-Knoten im Modus "Verzeichnisdienste wiederherstellen" &#40;DSRM&#41; &#40;Analyseplattformsystem&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)  
[Starten Sie den Konfigurations-Manager &#40;Analyseplattformsystem&#41;](launch-the-configuration-manager.md)  
  
