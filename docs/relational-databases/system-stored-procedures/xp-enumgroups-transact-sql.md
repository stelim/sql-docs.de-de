---
title: Xp_enumgroups (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_enumgroups_TSQL
- xp_enumgroups
dev_langs:
- TSQL
helpviewer_keywords:
- xp_enumgroups
ms.assetid: 0bd3ed36-e260-469c-a5ff-b033fb9ea59d
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 43366fd6463c885a41ad0304d45c2df1375015f8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792048"
---
# <a name="xpenumgroups-transact-sql"></a>xp_enumgroups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Stellt eine Liste lokaler Microsoft Windows-Gruppen oder lokaler Gruppen bereit, die in einer angegebenen Windows-Domäne definiert sind.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
xp_enumgroups [ 'domain_name' ]  
```  
  
## <a name="arguments"></a>Argumente  
 **"** *Domain_name* **"**  
 Der Name der Windows-Domäne, für die eine Liste von globalen Gruppen aufgezählt wird. *Domänenname* ist **Sysname**, hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**Gruppe**|**sysname**|Name der Windows-Gruppe|  
|**Kommentar**|**sysname**|Eine von Windows bereitgestellte Beschreibung der Windows-Gruppe|  
  
## <a name="remarks"></a>Hinweise  
 Wenn *Domain_name* ist der Name des Windows-basierten Computers, der eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist auf ausgeführt, oder kein Domänenname angegeben wird, **Xp_enumgroups** Listet die lokalen Gruppen auf dem Computer die ausgeführt wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Xp_enumgroups** kann nicht verwendet werden, wenn eine Instanz des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unter Windows 98 ausgeführt wird.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Db_owner** -Datenbankrolle in der **master** Datenbank oder die Mitgliedschaft in der **Sysadmin** -Serverrolle sein.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die Gruppen in der `sales`-Domäne aufgelistet.  
  
```  
EXEC xp_enumgroups 'sales';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Gespeicherte allgemeine erweiterte Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [Xp_loginconfig &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [Xp_logininfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
