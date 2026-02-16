# BIRD-UKR: The First Ukrainian Text-to-SQL Benchmark

[Українська версія нижче / Ukrainian version below](#bird-ukr-український-набір-даних-для-text-to-sql)

## Overview

**BIRD-UKR** is the first comprehensive Ukrainian-language benchmark for evaluating NL2SQL (Natural Language to SQL) capabilities of AI models. It is inspired by the English-language [BIRD benchmark](https://bird-bench.github.io/) and fully adapted for Ukrainian — including Ukrainian-language natural language queries, Ukrainian-localized database schemas, and culturally relevant data domains.

Ukrainian remains severely underrepresented in NL2SQL research. BIRD-UKR aims to fill this gap by providing a standardized evaluation corpus for researchers and practitioners working on multilingual Text-to-SQL systems.

## Key Statistics

| Metric | Value |
|---|---|
| Databases | 8 |
| Tables | ~80 |
| Queries | 75+ |
| Difficulty levels | 3 (Simple, Medium, Complex) |
| Language | Ukrainian |
| SQL dialect | PostgreSQL |

## Domains

The dataset covers 8 diverse domains, each with its own schema, sample data, and graded queries:

| # | Domain | Description |
|---|---|---|
| 1 | Hospital (`лікарня`) | Patients, doctors, diagnoses, treatments |
| 2 | Library (`бібліотека`) | Books, readers, lending records |
| 3 | University (`університет`) | Students, faculty, courses, grades |
| 4 | E-commerce (`інтернет_магазин`) | Products, orders, users, reviews |
| 5 | Restaurant (`ресторан`) | Menu, staff, orders, reservations |
| 6 | Travel agency (`туристичне_агентство`) | Tours, clients, bookings |
| 7 | Airline (`авіакомпанія`) | Flights, passengers, tickets |
| 8 | Sports club (`спортивний_клуб`) | Members, coaches, training sessions |

## Query Difficulty Tiers

Queries are stratified into three levels to enable fine-grained evaluation:

- **Simple**: Single-table queries with `WHERE`, `ORDER BY`, `LIMIT`.
- **Medium**: Multi-table `JOIN`s, `GROUP BY`, aggregate functions, `HAVING`.
- **Complex**: Subqueries, window functions, recursive CTEs (`WITH RECURSIVE`), `CASE WHEN`.

## Methodology

The dataset was created using **LLM-assisted corpus generation** — a standard approach in modern NLP dataset construction. Large language models were used to generate Ukrainian natural language queries and corresponding SQL, with the dataset architect (the author) designing the schemas, selecting domains, defining difficulty criteria, and validating outputs. This methodology is consistent with how many contemporary NL2SQL benchmarks are built (see: [Spider-Syn](https://github.com/ygan/Spider-Syn), [Dr.Spider](https://github.com/awslabs/diagnostic-robustness-text-to-sql), etc.).

## Repository Structure

```
BIRD-UKR/
├── database/
│   ├── лікарня/
│   │   ├── schema.sql        # Database schema
│   │   ├── data_*.sql         # Sample data
│   │   ├── sample_queries.sql # NL→SQL query pairs
│   │   └── README.md          # Domain documentation
│   ├── бібліотека/
│   ├── університет/
│   └── ... (8 domains total)
├── import_data.py             # PostgreSQL import script
├── consolidated_progress_plan.md
└── README.md
```

## Quick Start

1. Ensure PostgreSQL is installed and a target database is created.

2. Install dependencies:
   ```bash
   pip install psycopg2-binary
   ```

3. Configure connection in `import_data.py`:
   ```python
   conn = psycopg2.connect(
       host="localhost",
       user="your_user",
       password="your_password",
       dbname="університет"
   )
   ```

4. Run:
   ```bash
   python import_data.py
   ```

## Use Cases

- **Benchmarking multilingual NL2SQL models** on a non-English language with complex morphology
- **Fine-tuning and evaluating LLMs** for Ukrainian-language database interaction
- **Research on cross-lingual transfer** from English NL2SQL to Ukrainian
- **Educational resource** for Ukrainian-language SQL and NLP courses

## Citation

If you use BIRD-UKR in your research, please cite:

```
@misc{shabat2025birdukr,
  title={BIRD-UKR: A Ukrainian-Language Benchmark for Text-to-SQL Evaluation},
  author={Shabat, Volodymyr},
  year={2025},
  url={https://github.com/Leev1tan/BIRD-UKR}
}
```

## Roadmap

- [ ] Upload to HuggingFace Datasets for discoverability
- [ ] Add execution accuracy evaluation scripts
- [ ] Expand query count per domain
- [ ] Add cross-lingual (Ukrainian ↔ English) query pairs
- [ ] Benchmark results for open-source models (Llama, Mistral, GPT-4)

## Related Work

- [BIRD Benchmark](https://bird-bench.github.io/) — the English-language benchmark this project is inspired by
- [MAC-SQL](https://github.com/Leev1tan/mac-sql-ukr) — multi-agent Text-to-SQL system evaluated on BIRD-UKR
- [Awesome Ukrainian NLP](https://github.com/osyvokon/awesome-ukrainian-nlp) — curated list of Ukrainian NLP resources

## License

This dataset is released for research and educational purposes.

## Contact

Volodymyr Shabat — [vshabat64@gmail.com](mailto:vshabat64@gmail.com) | [GitHub](https://github.com/Leev1tan) | [LinkedIn](https://www.linkedin.com/in/volodymyr-shabat-2073b0224/)

---

# BIRD-UKR: Український Набір Даних для Text-to-SQL

## Про Проект

**BIRD-UKR** — це комплексний український бенчмарк для оцінки здатності моделей штучного інтелекту розуміти запити природною українською мовою та генерувати відповідні SQL-запити. Проект є аналогом англомовного набору даних [BIRD (Benchmarking Intermediate Reasoning for text-to-SQL)](https://bird-bench.github.io/), але повністю адаптований для української мови та даних.

Метою проекту є створення повноцінного українського набору даних для задач Text-to-SQL, що включає різноманітні бази даних з різних доменів та запити різного рівня складності.

## Структура Набору Даних

Набір даних включає 8 баз даних з різних доменів, кожна з яких має власну схему, дані та набір запитів:

1. **Лікарня (`лікарня`)**: Медичний заклад з пацієнтами, лікарями, діагнозами.
2. **Бібліотека (`бібліотека`)**: Інформація про книги, читачів, видачі.
3. **Університет (`університет`)**: Студенти, викладачі, курси, оцінки.
4. **Інтернет-магазин (`інтернет_магазин`)**: Товари, замовлення, користувачі.
5. **Ресторан (`ресторан`)**: Меню, персонал, замовлення, резервації.
6. **Туристичне агентство (`туристичне_агентство`)**: Тури, клієнти, бронювання.
7. **Авіакомпанія (`авіакомпанія`)**: Рейси, пасажири, квитки.
8. **Спортивний клуб (`спортивний_клуб`)**: Члени клубу, тренери, заняття.

### Рівні Складності Запитів

Запити поділено на три рівні складності для всебічного тестування моделей:

* **Простий**: Запити до однієї таблиці, проста фільтрація (`WHERE`), сортування (`ORDER BY`), обмеження (`LIMIT`).
* **Середній**: Запити з `JOIN`, групуванням (`GROUP BY`), агрегатними функціями та `HAVING`.
* **Складний**: Підзапити, віконні функції, рекурсивні запити (`WITH RECURSIVE`), умовні вирази (`CASE WHEN`).

## Як Використовувати

Кожна база даних знаходиться у відповідній директорії в `database/` і містить:

* `schema.sql`: Схема бази даних.
* `data_*.sql`: Файли з даними для наповнення таблиць.
* `sample_queries.sql`: Приклади запитів українською мовою та відповідні SQL-запити.
* `README.md`: Детальна документація для конкретної бази даних.

Для імпорту даних у PostgreSQL ви можете використовувати скрипт `import_data.py`.

## Статус Проекту

Розробка всіх 8 баз даних повністю завершена. Це включає схеми, дані, запити та документацію.

Дякуємо за ваш інтерес до проекту BIRD-UKR!
