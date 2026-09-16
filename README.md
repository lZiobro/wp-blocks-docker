# WordPress Docker Environment

This repository provides a local WordPress development environment using Docker Compose with MySQL 8.0 and custom `wp-content` mounting.

## Purpose

It's main goal is to provide reproducible environment for testing [wp-blocks-rest-api](https://github.com/lZiobro/wp-blocks-rest-api) WordPress plugin. It contains a set of example posts for each category of blocks aswell as indepth concepts for lists and a real-world sample. To check and develop plugin , please visit [wp-blocks-rest-api](https://github.com/lZiobro/wp-blocks-rest-api).

Full list of accessible examples with this installation can be found in [List of accessible examples](#list-of-accessible-examples) section below.

---

## Prerequisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) installed and running.

## Getting Started

### 1. Start the Containers

Run the following command in the project root directory:

```bash
docker compose up -d
```

This will start:
- **WordPress** container on [http://localhost:8080](http://localhost:8080)
- **MySQL 8.0** database container pre-populated with `init.sql`

### 2. Access WordPress

Open your browser and navigate to:
- **Website**: [http://localhost:8080](http://localhost:8080)

- **Admin**: [http://localhost:8080/wp-login.php](http://localhost:8080/wp-login.php)

Default credentials are:

```
username: admin
password: admin
```

### 3. Development Workflow

- Any changes made inside the `./wp-content` folder on your host machine (themes, plugins, uploads) will immediately reflect inside the container.

### 4. Database Export / Backup

To save database changes back to `init.sql`:

```powershell
.\export.ps1
```

Or via Docker Compose directly:

```bash
docker compose exec -T db mysqldump --no-tablespaces -u exampleuser -pexamplepass exampledb > init.sql
```

### 5. Stopping the Environment

To stop the containers:

```bash
docker compose down
```

To stop containers and reset database volumes completely:

```bash
docker compose down -v
```


## List of accessible examples

Note: if you change permalink settings to Plain, the "default" rest-api route will stop working and you'll instead have to request:

```http://localhost:8080/index.php?rest_route=/blocks/v1/posts/{id}```

e.g.

```http://localhost:8080/index.php?rest_route=/blocks/v1/posts/8```

Below is the list of all the accessible posts with url format of 

```http://localhost:8080/wp-json/blocks/v1/posts/{id}```

| Id | Title | Link |
| :-: | :-: | :-: |
| 8 | Text overview  | [Link](http://localhost:8080/wp-json/blocks/v1/posts/8) |
| 12 | Text in-depth - Lists  | [Link](http://localhost:8080/wp-json/blocks/v1/posts/12) |
| 15 | Media overview  | [Link](http://localhost:8080/wp-json/blocks/v1/posts/15) |
| 19 | Design overview  | [Link](http://localhost:8080/wp-json/blocks/v1/posts/19) |
| 21 | Widgets overview  | [Link](http://localhost:8080/wp-json/blocks/v1/posts/21) |
| 23 | Theme overview  | [Link](http://localhost:8080/wp-json/blocks/v1/posts/23) |
| 25 | Embeds overview  | [Link](http://localhost:8080/wp-json/blocks/v1/posts/25) |
| 27 | Complete Article Example  | [Link](http://localhost:8080/wp-json/blocks/v1/posts/27) |
| 30 | Photo gallery 10web  | [Link](http://localhost:8080/wp-json/blocks/v1/posts/30) |