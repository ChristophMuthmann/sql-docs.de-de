---
title: "Verschlüsselungsschlüssel für SQL Server und Datenbank (Datenbankmodul) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: keys [SQL Server], database encryption
ms.assetid: 15c0a5e8-9177-484c-ae75-8c552dc0dac0
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a1f811501db4568f9e893fdbdf64205381298368
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="sql-server-and-database-encryption-keys-database-engine"></a>Verschlüsselungsschlüssel für SQL Server und Datenbank (Datenbankmodul)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verwendet Verschlüsselungsschlüssel, um Daten sowie Anmelde- und Verbindungsinformationen zu schützen, die in einer Serverdatenbank gespeichert sind. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] besitzt zwei Arten von Schlüsseln: *symmetrische* und *asymmetrische*. Symmetrische Schlüssel verwenden das gleiche Kennwort, um Daten zu verschlüsseln und zu entschlüsseln. Asymmetrische Schlüssel verwenden ein Kennwort zum Verschlüsseln der Daten (den *öffentlichen* Schlüssel) und ein weiteres zum Entschlüsseln der Daten (den *privaten* Schlüssel).  
  
 Die Verschlüsselungsschlüssel in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]bestehen aus einer Kombination von öffentlichen, privaten und symmetrischen Schlüsseln, die zum Schutz sensibler Daten verwendet werden. Der symmetrische Schlüssel wird während der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Initialisierung erstellt, wenn Sie die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz zum ersten Mal starten. Der Schlüssel wird von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] verwendet, um sensible Daten zu verschlüsseln, die in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]gespeichert werden. Öffentliche und private Schlüssel werden vom Betriebssystem erstellt und zum Schutz des symmetrischen Schlüssels verwendet. Ein Paar aus einem privaten und einem öffentlichen Schlüssel wird für jede [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz erstellt, die sensible Daten in einer Datenbank speichert.  
  
## <a name="applications-for-sql-server-and-database-keys"></a>Anwendungen für SQL&#160;Server- und Datenbankschlüssel  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] hat zwei primäre Anwendungen für Schlüssel: einen *Diensthauptschlüssel* (Service Master Key; SMK), der auf einer und für eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz generiert wurde, sowie einen *Datenbank-Hauptschlüssel* (Database Master Key; DMK), der für eine Datenbank verwendet wird.  
  
 Der Diensthauptschlüssel wird automatisch generiert, wenn die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Instanz zum ersten Mal gestartet wird. Er wird verwendet, um ein Kennwort für einen Verbindungsserver, Anmeldeinformationen und den Datenbank-Hauptschlüssel zu verschlüsseln. Der Diensthauptschlüssel wird mithilfe des auf dem lokalen Computer verwendeten Computerschlüssels unter Verwendung der Windows-Datenschutz-API (DPAPI) verschlüsselt. Die DPAPI verwendet einen Schlüssel, der von den Windows-Anmeldeinformationen des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienstkontos und den Anmeldeinformationen des Computers abgeleitet ist. Der Diensthauptschlüssel kann nur von dem Dienstkonto entschlüsselt werden, unter dem er erstellt wurde, oder von einem Prinzipal, der auf die Anmeldeinformationen des Computers zugreifen kann.  
  
 Der Datenbank-Hauptschlüssel ist ein symmetrischer Schlüssel, der zum Schützen von privaten Schlüsseln der in der Datenbank vorhandenen Zertifikate und asymmetrischen Schlüssel verwendet wird. Er kann auch zum Verschlüsseln von Daten verwendet werden. Allerdings gelten für diesen Schlüssel Längenbeschränkungen, durch die er für Daten weniger praktisch ist als ein symmetrischer Schlüssel.  
  
 Beim Erstellen wird der Hauptschlüssel mithilfe des Triple DES-Algorithmus und eines vom Benutzer angegebenen Kennworts verschlüsselt. Um die automatische Entschlüsselung des Hauptschlüssels zu ermöglichen, wird eine Kopie des Schlüssels mit dem Diensthauptschlüssel verschlüsselt. Er wird sowohl in der Datenbank gespeichert, in der er verwendet wird, als auch in der **master** -Systemdatenbank.  
  
 Die in der **master** -Systemdatenbank gespeicherte Kopie des Datenbank-Hauptschlüssels wird im Hintergrund aktualisiert, sobald der Datenbank-Hauptschlüssel geändert wird. Diese Standardeinstellung kann jedoch mit der **DROP ENCRYPTION BY SERVICE MASTER KEY** -Option der **ALTER MASTER KEY** -Anweisung geändert werden. Ein Datenbank-Hauptschlüssel, der nicht mit dem Diensthauptschlüssel verschlüsselt ist, muss mithilfe der **OPEN MASTER KEY** -Anweisung und eines Kennworts geöffnet werden.  
  
## <a name="managing-sql-server-and-database-keys"></a>Verwalten von SQL Server- und Datenbankschlüsseln  
 Zur Verwaltung der Verschlüsselungsschlüssel gehört das Erstellen neuer Datenbankschlüssel, das Erstellen einer Sicherung der Server- und Datenbankschlüssel und das Wissen darüber, wann und wie die Schlüssel wiederhergestellt, gelöscht oder geändert werden müssen.  
  
 Zum Verwalten symmetrischer Schlüssel können Sie die in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] bereitgestellten Tools für folgende Aufgaben verwenden:  
  
-   Erstellen einer Sicherungskopie der Server- und Datenbankschlüssel, sodass sie zum Wiederherstellen einer Serverinstallation oder im Rahmen einer geplanten Migration verwendet werden können.  
  
-   Wiederherstellen eines zuvor gespeicherten Schlüssels in einer Datenbank. Dadurch kann eine neue Serverinstanz auf vorhandene Daten zugreifen, die sie ursprünglich nicht verschlüsselt hat.  
  
-   Löschen der verschlüsselten Daten in einer Datenbank in dem unwahrscheinlichen Fall, dass Sie nicht mehr auf die verschlüsselten Daten zugreifen können.  
  
-   Erneutes Erstellen von Schlüsseln und erneutes Verschlüsseln von Daten in dem unwahrscheinlichen Fall, dass der Schlüssel nicht mehr sicher ist. Eine bewährte Sicherheitsmethode ist die regelmäßige Neuerstellung der Schlüssel (z.&#160;B. alle paar Monate), um den Server vor Angriffen zu schützen, bei denen versucht wird, die Schlüssel zu entschlüsseln.  
  
-   Hinzufügen oder Entfernen einer Serverinstanz aus einer Serverbereitstellung für horizontales Skalieren, bei der mehrere Server eine einzige Datenbank und den Schlüssel, der für diese Datenbank die umkehrbare Verschlüsselung bereitstellt, gemeinsam nutzen.  
  
## <a name="important-security-information"></a>Wichtige Sicherheitsinformationen  
 Der Zugriff auf Objekte, die durch den Diensthauptschlüssel gesichert sind, erfordert entweder das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienstkonto, das zum Erstellen des Schlüssels verwendet wurde, oder das Computerkonto. Das heißt, dass der Computer an das System gebunden ist, auf dem der Schlüssel erstellt wurde. Sie können das [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Dienstkonto *oder* das Computerkonto ändern, ohne den Zugriff auf den Schlüssel zu verlieren. Wenn Sie jedoch beides ändern, verlieren Sie den Zugriff auf den Diensthauptschlüssel. Wenn Sie den Zugriff auf den Diensthauptschlüssel ohne eines der beiden Elemente verlieren, können Sie keine Daten und Objekte mehr entschlüsseln, die mit dem ursprünglichen Schlüssel verschlüsselt wurden.  
  
 Verbindungen, die mit dem Diensthauptschlüssel gesichert wurden, können nicht ohne den Diensthauptschlüssel wiederhergestellt werden.  
  
 Für den Zugriff auf Objekte und Daten, die mit dem Datenbank-Hauptschlüssel gesichert wurden, ist nur das Kennwort erforderlich, das zum Sichern des Schlüssels verwendet wird.  
  
> [!CAUTION]  
>  Wenn Sie den gesamten Zugriff auf die oben beschriebenen Schlüssel verlieren, verlieren Sie den Zugriff auf die Objekte, Verbindungen und Daten, die mit diesen Schlüsseln gesichert wurden. Sie können den Diensthauptschlüssel wie unter den hier angegebenen Links beschrieben wiederherstellen, oder Sie können den Zugriff mit dem ursprünglichen Verschlüsselungssystem wiederherstellen. Es gibt keine "Hintertür" zum Wiederherstellen des Zugriffs.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Service Master Key](../../../relational-databases/security/encryption/service-master-key.md)  
 Bietet eine kurze Erklärung zum Diensthauptschlüssel und den Best Practices.  
  
 [Erweiterbare Schlüsselverwaltung &#40;EKM&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
 Erklärt, wie Schlüsselverwaltungssysteme eines Drittanbieters mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]verwendet werden.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 [Sichern des Diensthauptschlüssels](../../../relational-databases/security/encryption/back-up-the-service-master-key.md)  
  
 [Wiederherstellen des Diensthauptschlüssels](../../../relational-databases/security/encryption/restore-the-service-master-key.md)  
  
 [Erstellen eines Datenbank-Hauptschlüssels](../../../relational-databases/security/encryption/create-a-database-master-key.md)  
  
 [Sichern eines Datenbank-Hauptschlüssels](../../../relational-databases/security/encryption/back-up-a-database-master-key.md)  
  
 [Wiederherstellen eines Datenbank-Hauptschlüssels](../../../relational-databases/security/encryption/restore-a-database-master-key.md)  
  
 [Erstellen identischer symmetrischer Schlüssel auf zwei Servern](../../../relational-databases/security/encryption/create-identical-symmetric-keys-on-two-servers.md)  
  
 [Aktivieren von TDE in SQL Server mithilfe von EKM](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
  
 [Erweiterbare Schlüsselverwaltung mit Azure Key Vault &#40;SQL Server&#41;](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
 [Verschlüsseln einer Datenspalte](../../../relational-databases/security/encryption/encrypt-a-column-of-data.md)  
  
## <a name="related-content"></a>Verwandte Inhalte  
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md)  
  
 [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-service-master-key-transact-sql.md)  
  
 [Wiederherstellen eines Datenbank-Hauptschlüssels](../../../relational-databases/security/encryption/restore-a-database-master-key.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Sichern und Wiederherstellen von Reporting Services-Verschlüsselungsschlüsseln](../../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [Löschen und erneutes Erstellen von Verschlüsselungsschlüsseln &#40;SSRS-Konfigurations-Manager&#41;](../../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [Hinzufügen und Entfernen von Verschlüsselungsschlüsseln für die Bereitstellung für horizontales Skalieren &#40;SSRS-Konfigurations-Manager&#41;](../../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)   
 [Transparente Datenverschlüsselung &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
  
