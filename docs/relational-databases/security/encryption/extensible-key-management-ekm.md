---
title: "Erweiterbare Schlüsselverwaltung (EKM) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Key Management
- Extensible Key Management
- EKM, described
ms.assetid: 9bfaf500-2d1e-4c02-b041-b8761a9e695b
caps.latest.revision: 46
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 632fec019b757d782e7bd54f6854e815ccd2afcf
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="extensible-key-management-ekm"></a>Erweiterbare Schlüsselverwaltung (Extensible Key Management, EKM)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] stellt Funktionen zur Datenverschlüsselung zusammen mit der *erweiterbaren Schlüsselverwaltung* (Extensible Key Management, EKM) bereit. Dabei wird der Anbieter *Microsoft Cryptographic API* (MSCAPI) zur Verschlüsselung und Schlüsselgenerierung verwendet. Verschlüsselungsschlüssel für die Daten- und Schlüsselverschlüsselung werden in temporären Schlüsselcontainern erstellt und müssen vom Anbieter exportiert werden, bevor sie in der Datenbank gespeichert werden. Dieser Ansatz ermöglicht eine Schlüsselverwaltung mit einer Verschlüsselungsschlüsselhierarchie und Schlüsselsicherung durch [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Da die Einhaltung behördlicher Bestimmungen und der Datenschutz immer wichtiger werden, nutzen Organisationen die Verschlüsselung als Lösung für eine "tiefgreifende Verteidigung". Dieser Lösungsansatz ist jedoch häufig mit den Verwaltungstools für die Datenbankverschlüsselung alleine nicht durchführbar. Hardwarehersteller bieten Produkte an, die die Schlüsselverwaltung in Unternehmen mittels *Hardwaresicherheitsmodulen* (HSM) umsetzen. HSM-Geräte speichern die Verschlüsselungsschlüssel auf Hardware- oder Softwaremodulen. Dies ist eine sicherere Lösung, da die Verschlüsselungsschlüssel von den Verschlüsselungsdaten getrennt werden.  
  
 Etliche Anbieter liefern Hardwaresicherheitsmodule für die Schlüsselverwaltung und die Verschlüsselungsbeschleunigung. HSM-Geräte verwenden Hardwareschnittstellen, bei denen ein Serverprozess als Mittler zwischen einer Anwendung und einem HSM fungiert. Darüber hinaus implementieren die Hersteller MSCAPI-Anbieter mit ihren Modulen, wobei es sich um Hardware oder Software handeln kann. MSCAPI bietet jedoch häufig nur einen Teil der Funktionen an, die von einem HSM bereitgestellt werden. Die Hersteller können außerdem Verwaltungssoftware für Hardwaresicherheitsmodule, Schlüsselkonfiguration und Schlüsselzugriff bereitstellen.  
  
 Die HSM-Implementierungen unterscheiden sich zwischen den Herstellern, und für die Verwendung mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ist eine gemeinsame Schnittstelle erforderlich. Diese Schnittstelle wird zwar von der MSCAPI bereitgestellt, sie unterstützt allerdings nur einen Teil der HSM-Funktionen. Darüber hinaus gibt es noch weitere Einschränkungen: Symmetrische Schlüssel können beispielsweise nicht durch das System selbst persistent gemacht werden, und es fehlt eine sitzungsgerichtete Unterstützung.  
  
 Durch die erweiterbare Schlüsselverwaltung in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] können EKM-/HSM-Drittanbieter ihre Module bei [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]registrieren. Nach der Registrierung können [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Benutzer die auf den EKM-Modulen gespeicherten Verschlüsselungsschlüssel verwenden. Auf diese Weise kann [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] die von diesen Modulen unterstützten erweiterten Verschlüsselungsfunktionen wie die Massenverschlüsselung und -entschlüsselung und Schlüsselverwaltungsfunktionen wie die Schlüsselablaufzeit und die Schlüsselrotation nutzen.  
  
 Beim Ausführen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in einer Azure-VM können von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Schlüssel verwendet werden, die im [Azure-Schlüsseltresor](http://go.microsoft.com/fwlink/?LinkId=521401)gespeichert sind. Weitere Informationen finden Sie im Thema [Erweiterbare Schlüsselverwaltung mit Azure Key Vault &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  
  
## <a name="ekm-configuration"></a>EKM-Konfiguration  
 Die erweiterbare Schlüsselverwaltung wird nicht in jeder Edition von [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Eine Liste der Funktionen, die von den [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Editionen unterstützt werden, finden Sie unter [Von den SQL Server 2016-Editionen unterstützte Funktionen](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 Standardmäßig ist die EKM deaktiviert. Wenn Sie die Funktion aktivieren möchten, verwenden Sie wie im folgenden Beispiel dargestellt den sp_configure-Befehl, der über folgende Option und folgenden Wert verfügt:  
  
```  
sp_configure 'show advanced', 1  
GO  
RECONFIGURE  
GO  
sp_configure 'EKM provider enabled', 1  
GO  
RECONFIGURE  
GO  
```  
  
> [!NOTE]  
>  Wenn Sie den sp_configure-Befehl für diese Option in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Editionen verwenden, die EKM nicht unterstützen, wird ein Fehler angezeigt.  
  
 Wenn Sie die Funktion deaktivieren möchten, legen Sie den Wert auf **0**fest. Weitere Informationen zum Festlegen von Serveroptionen finden Sie unter [sp_configure &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
## <a name="how-to-use-ekm"></a>So verwenden Sie die erweiterbare Schlüsselverwaltung  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Extensible Key Management ermöglicht es, dass die Verschlüsselungsschlüssel, die die Datenbankdateien schützen, auf einem separaten Medium wie einer Smartcard, einem USB-Gerät oder einem EKM-/HSM-Modul gespeichert werden können. Auf diese Weise werden die Daten auch vor Datenbankadministratoren (mit Ausnahme der Mitglieder der sysadmin-Gruppe) geschützt. Die Daten können mit Verschlüsselungsschlüsseln verschlüsselt werden, auf die nur der Datenbankbenutzer auf dem externen EKM-/HSM-Modul zugreifen kann.  
  
 EKM hat außerdem folgende Vorzüge:  
  
-   Zusätzliche Autorisierungsprüfung (ermöglicht die Aufgabentrennung)  
  
-   Bessere Leistung bei der hardwarebasierten Verschlüsselung und Entschlüsselung  
  
-   Externe Generierung von Verschlüsselungsschlüsseln  
  
-   Externe Speicherung von Verschlüsselungsschlüsseln (physische Trennung von Daten und Schlüsseln)  
  
-   Abruf der Verschlüsselungsschlüssel  
  
-   Extern gesteuerte Laufzeit der Verschlüsselungsschlüssel (ermöglicht die Rotation der Verschlüsselungsschlüssel)  
  
-   Leichtere Wiederherstellung der Verschlüsselungsschlüssel  
  
-   Kontrollierbare Verteilung der Verschlüsselungsschlüssel  
  
-   Sichere Beseitigung der Verschlüsselungsschlüssel  
  
 Sie können die erweiterbare Schlüsselverwaltung für eine Kombination aus Benutzername und Kennwort oder andere Methoden verwenden, die vom EKM-Treiber definiert werden.  
  
> [!CAUTION]  
>  Für die Problembehandlung benötigt der technische Support von [!INCLUDE[msCoName](../../../includes/msconame-md.md)] eventuell den Verschlüsselungsschlüssel des EKM-Anbieters. Außerdem kann es sein, dass Sie für die Lösung eines Problems auf Tools und Prozesse des Herstellers zugreifen müssen.  
  
### <a name="authentication-with-an-ekm-device"></a>Authentifizierung bei EKM-Geräten  
 EKM-Module können mehrere Arten der Authentifizierung unterstützen. Jeder Anbieter macht nur eine Art der Authentifizierung für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]verfügbar. Wenn das Modul zum Beispiel die Standardauthentifizierung oder andere Authentifizierungstypen unterstützt, wird nur eine der beiden Arten bereitgestellt.  
  
#### <a name="ekm-device-specific-basic-authentication-using-usernamepassword"></a>EKM-gerätespezifische Standardauthentifizierung mit einer Benutzername-/Kennwortkombination  
 Bei den EKM-Modulen, die die Standardauthentifizierung mit einem *Benutzername/Kennwort*-Paar unterstützen, stellt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] eine transparente Authentifizierung über Anmeldeinformationen bereit. Weitere Informationen über Anmeldenamen finden Sie unter [Anmeldeinformationen &#40;Datenbankmodul&#41;](../../../relational-databases/security/authentication-access/credentials-database-engine.md).  
  
 Sie können für einen EKM-Anbieter einen Identitätsnachweis (Anmeldeinformationen) erstellen und diesen einem Anmeldenamen (sowohl für Windows- als auch für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Konten) zuordnen, sodass der Zugriff auf ein EKM-Modul über eine einzelne Anmeldung möglich ist. Das *Identify* -Feld im Identitätsnachweis enthält den Benutzernamen und das *secret* -Feld ein Kennwort für die Verbindung mit einem EKM-Modul.  
  
 Falls für einen EKM-Anbieter kein mit einem Anmeldenamen verknüpfter Identitätsnachweis vorliegt, werden die dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienstkonto zugeordneten Anmeldeinformationen verwendet.  
  
 Einem Anmeldenamen können mehrere Anmeldeinformationen zugeordnet werden, solange sie für unterschiedliche EKM-Anbieter verwendet werden. Pro EKM-Anbieter und Anmeldung darf es jedoch nur einen zugeordneten Identitätsnachweis geben. Die gleichen Anmeldeinformationen können jedoch auch anderen Anmeldenamen zugeordnet werden.  
  
#### <a name="other-types-of-ekm-device-specific-authentication"></a>Andere Arten der EKM-gerätespezifischen Authentifizierung  
 Bei EKM-Modulen, die eine andere Authentifizierung als die Windows-Authentifizierung oder die Kombination aus *Benutzername und Kennwort* verwenden, muss die Authentifizierung unabhängig von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]erfolgen.  
  
### <a name="encryption-and-decryption-by-an-ekm-device"></a>Verschlüsselung und Entschlüsselung durch ein EKM-Gerät  
 Sie können die folgenden Funktionen verwenden, um Daten mithilfe von symmetrischen und asymmetrischen Schlüsseln zu verschlüsseln und zu entschlüsseln:  
  
|Funktion|Verweis|  
|-------------------------|---------------|  
|Verschlüsselung mit symmetrischen Schlüsseln|[CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)|  
|Verschlüsselung mit asymmetrischen Schlüsseln|[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)|  
|EncryptByKey(key_guid, 'Klartext', …)|[ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbykey-transact-sql.md)|  
|DecryptByKey(ciphertext, …)|[DECRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/decryptbykey-transact-sql.md)|  
|EncryptByAsmKey(key_guid, 'Klartext')|[ENCRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbyasymkey-transact-sql.md)|  
|DecryptByAsmKey(ciphertext)|[DECRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/decryptbyasymkey-transact-sql.md)|  
  
#### <a name="database-keys-encryption-by-ekm-keys"></a>Datenbankschlüsselverschlüsselung mit EKM-Schlüsseln  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] kann mithilfe von EKM-Schlüsseln andere Schlüssel in einer Datenbank verschlüsseln. Sie können sowohl symmetrische als auch asymmetrische Schlüssel auf einem EKM-Gerät erstellen und verwenden. Sie können systemeigene (nicht-EKM) symmetrische Schlüssel mit asymmetrischen EKM-Schlüsseln verschlüsseln.  
  
 Im folgenden Beispiel wird ein symmetrischer Datenbankschlüssel erstellt und mit einem Schlüssel auf einem EKM-Modul verschlüsselt.  
  
```  
CREATE SYMMETRIC KEY Key1  
WITH ALGORITHM = AES_256  
ENCRYPTION BY EKM_AKey1;  
GO  
--Open database key  
OPEN SYMMETRIC KEY Key1  
DECRYPTION BY EKM_AKey1  
```  
  
 Weitere Informationen zu Datenbank- und Serverschlüsseln in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] finden Sie unter [Verschlüsselungsschlüssel für SQL Server und Datenbank &#40;Datenbankmodul&#41;](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md).  
  
> [!NOTE]  
>  EKM-Schlüssel können nicht mit anderen EKM-Schlüsseln verschlüsselt werden.  
>   
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützt keine Signierungsmodule mit den asymmetrischen Schlüsseln, die vom EKM-Anbieter generiert werden.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 [EKM provider enabled (Serverkonfigurationsoption)](../../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)  
  
 [Aktivieren von TDE in SQL Server mithilfe von EKM](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
 [Erweiterbare Schlüsselverwaltung mit Azure Key Vault &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [ALTER CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-cryptographic-provider-transact-sql.md)   
 [sys.cryptographic_providers &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-cryptographic-providers-transact-sql.md)   
 [sys.dm_cryptographic_provider_sessions &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-sessions-transact-sql.md)   
 [sys.dm_cryptographic_provider_properties &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-properties-transact-sql.md)   
 [sys.dm_cryptographic_provider_algorithms &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-algorithms-transact-sql.md)   
 [sys.dm_cryptographic_provider_keys &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-cryptographic-provider-keys-transact-sql.md)   
 [sys.credentials &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-login-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [Sichern und Wiederherstellen von Reporting Services-Verschlüsselungsschlüsseln](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [Löschen und erneutes Erstellen von Verschlüsselungsschlüsseln &#40;SSRS-Konfigurations-Manager&#41;](../../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [Hinzufügen und Entfernen von Verschlüsselungsschlüsseln für die Bereitstellung für horizontales Skalieren &#40;SSRS-Konfigurations-Manager&#41;](../../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)   
 [Sichern des Diensthauptschlüssels](../../../relational-databases/security/encryption/back-up-the-service-master-key.md)   
 [Wiederherstellen des Diensthauptschlüssels](../../../relational-databases/security/encryption/restore-the-service-master-key.md)   
 [Erstellen eines Datenbank-Hauptschlüssels](../../../relational-databases/security/encryption/create-a-database-master-key.md)   
 [Sichern eines Datenbank-Hauptschlüssels](../../../relational-databases/security/encryption/back-up-a-database-master-key.md)   
 [Wiederherstellen eines Datenbank-Hauptschlüssels](../../../relational-databases/security/encryption/restore-a-database-master-key.md)   
 [Erstellen identischer symmetrischer Schlüssel auf zwei Servern](../../../relational-databases/security/encryption/create-identical-symmetric-keys-on-two-servers.md)  
  
  

