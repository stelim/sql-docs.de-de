---
title: dm_database_encryption_keys (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_database_encryption_keys
- sys.dm_database_encryption_keys_TSQL
- dm_database_encryption_keys
- dm_database_encryption_keys_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_database_encryption_keys dynamic management view
ms.assetid: 56fee8f3-06eb-4fff-969e-abeaa0c4b8e4
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: bb177f781bee54b908624e1f940c12d5bdaf5a13
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdatabaseencryptionkeys-transact-sql"></a>sys.dm_database_encryption_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen über den Verschlüsselungsstatus einer Datenbank und die ihr zugeordneten Verschlüsselungsschlüssel für die Datenbank zurück. Weitere Informationen über die datenbankverschlüsselung finden Sie unter [transparente datenverschlüsselung &#40; TDE &#41; ](../../relational-databases/security/encryption/transparent-data-encryption.md).  
 
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|Die ID der Datenbank.|  
|encryption_state|**int**|Gibt an, ob die Datenbank verschlüsselt oder nicht verschlüsselt ist.<br /><br /> 0 = Kein Verschlüsselungsschlüssel für die Datenbank vorhanden, keine Verschlüsselung<br /><br /> 1 = Unverschlüsselt<br /><br /> 2 = Verschlüsselung wird ausgeführt<br /><br /> 3 = Verschlüsselt.<br /><br /> 4 = Schlüsseländerung wird ausgeführt<br /><br /> 5 = Entschlüsselung wird ausgeführt<br /><br /> 6 = Schutzänderung wird ausgeführt (Das Zertifikat oder der asymmetrische Schlüssel, das bzw. der zum Verschlüsseln des Verschlüsselungsschlüssels für die Datenbank verwendet wird, wird geändert.)|  
|create_date|**datetime**|Zeigt das Datum der Erstellung des Verschlüsselungsschlüssels an.|  
|regenerate_date|**datetime**|Zeigt das Datum der Neugenerierung des Verschlüsselungsschlüssels an.|  
|modify_date|**datetime**|Zeigt das Datum der Änderung des Verschlüsselungsschlüssels an.|  
|set_date|**datetime**|Zeigt das Datum der Anwendung des Verschlüsselungsschlüssels auf die Datenbank an.|  
|opened_date|**datetime**|Zeigt das Datum an, an dem der Datenbankschlüssel zuletzt geöffnet wurde.|  
|key_algorithm|**nvarchar(32)**|Zeigt den Algorithmus an, der für den Schlüssel verwendet wird.|  
|key_length|**int**|Zeigt die Länge des Schlüssels an.|  
|
          encryptor_thumbprint|**varbinary(20)**|Zeigt den Fingerabdruck der Verschlüsselung an.|  
|encryptor_type|**nvarchar(32)**|**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).<br /><br /> Beschreibt die Verschlüsselung.|  
|percent_complete|**real**|Prozentualer Anteil der bereits abgeschlossenen Änderung des Verschlüsselungsstatus einer Datenbank. Dieser Wert ist 0, wenn es keine Statusänderung gibt.|  
  
## <a name="permissions"></a>Berechtigungen  
Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] benötigen Premium-Ebenen der `VIEW DATABASE STATE` Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard und grundlegenden Organisationsebenen erfordert die **Serveradministrator** oder ein **Azure Active Directory-Administrators** Konto.  
  
## <a name="see-also"></a>Siehe auch  

 [Sicherheitsbezogene dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Transparente Datenverschlüsselung &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)   
 [SQL Server-Verschlüsselung](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [Verschlüsselungsschlüssel für SQL Server und Datenbank &#40;Datenbankmodul&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [Erstellen Sie DATABASE ENCRYPTION KEY &#40; Transact-SQL &#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [ALTER DATABASE ENCRYPTION KEY &#40; Transact-SQL &#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
  
  