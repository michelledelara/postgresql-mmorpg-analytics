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
