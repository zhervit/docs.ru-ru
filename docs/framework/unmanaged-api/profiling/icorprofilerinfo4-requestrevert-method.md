---
title: Метод ICorProfilerInfo4::RequestRevert
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4.RequestRevert
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::RequestRevert
helpviewer_keywords:
- RequestRevert method, ICorProfilerInfo4 interface [.NET Framework profiling]
- ICorProfilerInfo4::RequestRevert method [.NET Framework profiling]
ms.assetid: 70261da5-5933-4e25-9de0-ddf51cba56cc
topic_type:
- apiref
ms.openlocfilehash: c7ced05692e3030bace10dab9a6793a29fac6c26
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/23/2019
ms.locfileid: "74444840"
---
# <a name="icorprofilerinfo4requestrevert-method"></a>Метод ICorProfilerInfo4::RequestRevert
Восстанавливает исходные версии всех экземпляров указанных функций.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
HRESULT RequestRevert (  
   [in] ULONG    cFunctions,  
   [in, size_is(cFunctions)]  ModuleID    moduleIds[],  
   [in, size_is(cFunctions)]  mdMethodDef methodIds[],  
   [out, size_is(cFunctions)]  HRESULT status[]);  
```  
  
## <a name="parameters"></a>Параметры  
 `cFunctions`  
 [in] Число функций для восстановления.  
  
 `moduleIds`  
 [in] Указывает часть `moduleId` пар (`module`, `methodDef`), которые идентифицируют восстанавливаемые функции.  
  
 `methodIds`  
 [in] Указывает часть `methodId` пар (`module`, `methodDef`), которые идентифицируют восстанавливаемые функции.  
  
 `status`  
 [out] Массив значений HRESULT, перечисленных в разделе «Значения HRESULT для состояния» далее в этом разделе. Каждое значение HRESULT указывает успех или сбой попытки восстановления исходного состояния каждой функции, указанной в параллельных массивах `moduleIds` и `methodIds`.  
  
## <a name="return-value"></a>Возвращаемое значение  
 Этот метод возвращает следующие конкретные результаты HRESULT, а также ошибки HRESULT, которые указывают на сбой метода.  
  
|HRESULT|Описание|  
|-------------|-----------------|  
|S_OK|Была предпринята попытка восстановления исходного состояния всех запросов; однако необходимо проверить массив возвращенных состояний, чтобы определить, какие функции были успешно восстановлены.|  
|CORPROF_E_CALLBACK4_REQUIRED|Чтобы этот вызов поддерживался, профилировщик должен реализовать интерфейс [ICorProfilerCallback4](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback4-interface.md) .|  
|CORPROF_E_REJIT_NOT_ENABLED|Перекомпиляция JIT не была включена. Необходимо включить повторную компиляцию JIT-компилятора во время инициализации с помощью метода [ICorProfilerInfo:: SetEventMask](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-seteventmask-method.md) , чтобы установить флаг `COR_PRF_ENABLE_REJIT`.|  
|E_INVALIDARG|`cFunctions` имеет значение 0, либо `moduleIds` или `methodIds` `NULL`.|  
|E_OUTOFMEMORY|Среде CLR не удалось выполнить запрос, поскольку не хватило памяти.|  
  
## <a name="status-hresults"></a>Значения HRESULT для состояния  
  
|Массив значений HRESULT для состояния|Описание|  
|--------------------------|-----------------|  
|S_OK|Соответствующая функция была успешно возвращена.|  
|E_INVALIDARG|Значение параметра `moduleID` или параметра `methodDef` — `NULL`.|  
|CORPROF_E_DATAINCOMPLETE|Модуль еще не полностью загружен или находится в процессе выгрузки.|  
|CORPROF_E_MODULE_IS_DYNAMIC|Указанный модуль был создан динамически (например, с помощью `Reflection.Emit`). Поэтому он не поддерживается данным методом.|  
|CORPROF_E_ACTIVE_REJIT_REQUEST_NOT_FOUND|Среде CLR не удалось восстановить исходное состояние указанной функции, так как не найден соответствующий активный запрос перекомпиляции. Либо эта перекомпиляция никогда не запрашивалась, либо функция уже была восстановлена.|  
|Прочее|Операционная система возвратила сбой за пределами среды CLR. Например, в случае сбоя системного вызова изменения защиты доступа к странице памяти будет отображаться ошибка операционной системы.|  
  
## <a name="remarks"></a>Заметки  
 При следующем вызове любой из восстановленных функций будет запускаться исходная версия этой функции. Если функция уже выполняется, то будет завершено выполнение запущенной версии.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** см. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** CorProf.idl, CorProf.h  
  
 **Библиотека:** CorGuids.lib  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Интерфейс ICorProfilerInfo4](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-interface.md)
- [Интерфейсы профилирования](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [Профилирование](../../../../docs/framework/unmanaged-api/profiling/index.md)
