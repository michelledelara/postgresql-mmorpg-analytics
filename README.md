# 🎮 MMORPG PostgreSQL Database & SQL Analytics

> Relational database project built with PostgreSQL to practice data modeling and analytical SQL using a fictional MMORPG dataset.

## 📌 About the Project

This project was created to practice relational database design and SQL analysis using PostgreSQL and pgAdmin.

The database simulates an MMORPG environment with characters, guilds, items and inventories.

The project demonstrates how relational data can be structured, connected and analyzed using SQL.

---

## 🗄️ Database Structure

The database currently contains four main tables:

### personagens

Stores character information such as:

- name
- race
- class
- faction
- level
- realm
- guild

### guildas

Stores guild information including:

- guild name
- faction
- realm

### itens

Stores game items and attributes such as:

- item name
- type
- rarity
- item level

### inventario

Connects characters and items through a many-to-many relationship.

It also stores:

- quantity
- equipped status

---

## 🔗 Relational Model

The project includes different types of database relationships.

```text
GUILDAS
   |
   | 1:N
   ↓
PERSONAGENS
   |
   | N:N
   ↓
INVENTARIO
   ↑
   |
 ITENS
```

The `inventario` table acts as a junction table between characters and items.

---

## 🧠 SQL Concepts Practiced

The project includes practical examples of:

- CREATE TABLE
- INSERT
- UPDATE
- SELECT
- PRIMARY KEY
- FOREIGN KEY
- JOIN
- LEFT JOIN
- GROUP BY
- HAVING
- COUNT()
- SUM()
- AVG()
- MAX()
- subqueries
- Common Table Expressions (CTEs)
- weighted averages
- Window Functions
- RANK()
- DENSE_RANK()
- ROW_NUMBER()

---

## 📊 Analytical Queries

The database can answer questions such as:

- How many characters belong to each faction?
- How many characters belong to each guild?
- Which items does each character own?
- How many items does each character have?
- What is the average item level for each character?
- What is the weighted average item level considering item quantity?
- Which character owns the highest-level item?
- How can characters be ranked based on their inventory?

---

## 🏆 Character Ranking Example

A CTE and Window Function are used to generate a ranking based on weighted average item level:

```sql
WITH pontuacao AS (
    SELECT
        personagens.nome AS personagem,
        ROUND(
            SUM(itens.nivel_item * inventario.quantidade)::NUMERIC
            / NULLIF(SUM(inventario.quantidade), 0),
            2
        ) AS nivel_medio_ponderado
    FROM inventario
    JOIN personagens
        ON inventario.personagem_id = personagens.id
    JOIN itens
        ON inventario.item_id = itens.id
    GROUP BY personagens.nome
)

SELECT
    personagem,
    nivel_medio_ponderado,
    RANK() OVER (
        ORDER BY nivel_medio_ponderado DESC
    ) AS ranking
FROM pontuacao
ORDER BY ranking;
```

Example result:

```text
Thrall     | 100.00 | 1
Sylvanas   | 70.00  | 2
Jaina      | 22.50  | 3
Tyrande    | 10.00  | 4
Anduin     | 1.00   | 5
```

---

## 🛠️ Technologies

- PostgreSQL
- pgAdmin 4
- SQL
- Relational Database Modeling
- Data Analysis

---

## 🚀 Project Roadmap

- [x] Create PostgreSQL database
- [x] Create relational tables
- [x] Implement Primary Keys
- [x] Implement Foreign Keys
- [x] Create one-to-many relationships
- [x] Create many-to-many relationships
- [x] Insert sample data
- [x] Practice JOIN operations
- [x] Create aggregation queries
- [x] Use subqueries
- [x] Use CTEs
- [x] Use Window Functions
- [ ] Add faction-based ranking with PARTITION BY
- [ ] Add additional analytical queries
- [ ] Document complete database schema

---

## 🎯 Project Goal

The goal of this project is to demonstrate practical knowledge of PostgreSQL, relational database modeling and analytical SQL.

```text
RAW GAME DATA
      ↓
RELATIONAL MODEL
      ↓
SQL QUERIES
      ↓
DATA AGGREGATION
      ↓
ANALYTICAL INSIGHTS
```

> A well-designed relational database transforms structured data into information that can support analysis and decision-making.

---

## ⚠️ Disclaimer

This is an educational and portfolio project using a fictional MMORPG database.

Game-related names used in sample data are included solely for educational purposes. This project is not affiliated with or endorsed by any game publisher.
