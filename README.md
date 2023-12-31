Agnostic Database Migrations
============================

[![PyPI](https://img.shields.io/pypi/v/agnostic.svg?style=flat-square)](https://pypi.python.org/pypi/agnostic)
[![GitHub Workflow Status (with event)](https://img.shields.io/github/actions/workflow/status/mehaase/agnostic/test.yml?style=flat-square&label=Integration%20Tests)](https://github.com/mehaase/agnostic/actions/workflows/test.yml)
[![Coverage](https://img.shields.io/codecov/c/github/mehaase/agnostic?style=flat-square)](https://coveralls.io/github/mehaase/agnostic?branch=master)

Overview
--------

Agnostic is a light-weight, easy-to-learn, and flexible database migration tool
in which migration scripts are written in pure SQL. It is agnostic towards
database, programming language, and object relational mapper (ORM).

Super Quick Start
-----------------

Here is an absurdly brief introduction to Agnostic:

```shell
~/myapp $ mkdir migrations

~/myapp $ agnostic -t postgres -u myuser -d mydb bootstrap
Migration table created.

~/myapp $ cat > migrations/add_cell_phone.sql
ALTER TABLE customer ADD cell_phone VARCHAR(255);
^D

~/myapp $ cat > migrations/add_nickname.sql
ALTER TABLE customer ADD nickname VARCHAR(255);
^D

~/myapp $ agnostic -t postgres -u myuser -d mydb migrate
Backing up "mydb" to "/tmp/tmpm8glpgaa".
About to run 2 migrations in "mydb":
    * Running migration add_cell_phone (1/2)
    * Running migration add_nickname (2/2)
Migrations completed successfully.
Removing backup "/tmp/tmpm8glpgaa".
```

For a not-quite-as-quick-but-still-pretty-quick start, please refer to the
[full documentation](https://agnostic.readthedocs.io/).
