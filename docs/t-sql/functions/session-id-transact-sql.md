---
title: SESSION_ID (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 02/23/2018
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 9feb899a0a46a04ad52ef15fb801e2eb4866e478
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47698568"
---
# <a name="sessionid-transact-sql"></a>SESSION_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Gibt die ID der aktuellen [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]- oder [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)]-Sitzung zurück.  
  
 ![Symbol zum Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Symbol zum Themenlink") [Transact-SQL Syntax Conventions &#40;Transact-SQL&#41; (Transact-SQL-Syntaxkonventionen (Transact-SQL))](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
SESSION_ID ( )  
```  
  
## <a name="return-value"></a>Rückgabewert  
 Gibt einen **nvarchar(32)**-Wert zurück.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Die Sitzungs-ID wird jeder Benutzerverbindung beim Herstellen der Verbindung zugewiesen und bleibt für die Dauer der Verbindung bestehen. Wenn die Verbindung beendet wird, wird die Sitzungs-ID freigegeben.  
  
 Die Sitzungs-ID beginnt mit den Buchstaben „SID“. Für diese muss die Groß-/Kleinschreibung beachtet werden. Außerdem müssen sie groß geschrieben werden, wenn die Sitzungs-ID in [!INCLUDE[DWsql](../../includes/dwsql-md.md)]-Befehlen verwendet wird.  
  
 Sie können die Sicht [sys.dm_pdw_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) abfragen, um dieselben Informationen wie diese Funktion abzurufen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die ID der aktuellen Sitzung zurückgegeben.  
  
```  
SELECT SESSION_ID();  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [DB_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)   
 [VERSION &#40;SQL Data Warehouse&#41;](../../t-sql/functions/version-transact-sql-configuration-functions.md)
  
  
