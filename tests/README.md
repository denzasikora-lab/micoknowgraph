# Tests

Place tests for the Python scripts here, mirroring the script organization
where practical. Prefer small, non-sensitive fixtures that can be shared in
the repository. Document how to run the tests when a test suite is added.

## Entity mapping: offline-проверки

Из корня репозитория, в отдельном окружении Python 3.9+:

```sh
python -m pip install -r requirements-test.txt
python -I -m unittest discover -s tests -v
```

Тесты вызывают настоящий `build_mapping.py --offline` в изолированном процессе
с запретом DNS и сетевых соединений через audit hook Python. Входы копируются
во временные каталоги: существующий builder записывает кеш и `build_report.json`
рядом с ними даже в offline-режиме. Исходные файлы checkout проверяются по SHA-256.

Проверяются побайтовое воспроизведение обеих опубликованных TSV, повторная сборка,
реакция на неполный кеш, отсутствие классификации и добавление новой сущности.
Число строк берется из актуального снимка; значения 553 и 1201 не являются
константами тестов.

Отдельно проверяются заголовки и поля таблиц, покрытие сущностей, связность
классификации и mapping, placeholder-строки, синтаксис CURIE и ранги кандидатов.
Маленькие искусственные примеры и поврежденные варианты проверяют, что диагностика
действительно замечает нарушения.

## Диагностика текущих таблиц

```sh
python -I scripts/entity_mapping/validate_mapping.py --report entity-mapping-quality.json
python -I scripts/entity_mapping/validate_mapping.py --strict-duplicates
```

Структурные ошибки дают ненулевой код завершения. Повторные пары
`(entity, concept_id)` раскрываются в предупреждениях с рангами и источниками;
`--strict-duplicates` делает их причиной ненулевого кода. Это позволяет команде
сначала согласовать сохранение provenance, не удаляя кандидатов автоматически.
Объяснимые пустые строки для `map=no` и неразрешенных сущностей допустимы.

Workflow `Entity mapping quality` запускает тесты на Python 3.9 и 3.12,
прикладывает JSON-отчет и выводит диагностику в summary GitHub Actions.
При обновлении снимка нужно согласованно обновить классификацию, входы/кеш и
опубликованные TSV, затем повторить тесты. Они проверяют технические контракты;
научный смысл соответствий и действительность идентификаторов требуют
отдельного экспертного рассмотрения.
