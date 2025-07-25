# mcps-mysql-server

**Repository:** [https://github.com/Shubham9975/mcp-mysql-server.git](https://github.com/Shubham9975/mcp-mysql-server.git)

A MySQL server implementation for the MCP (Model Control Protocol) framework. This server allows you to interact with MySQL databases through the MCP protocol, enabling SQL execution, table/resource listing, and schema retrieval.

## Features

- Execute SQL queries
- List MySQL tables as resources
- Get table schemas
- Configurable through environment variables
- Supports various MySQL character sets and collations

## Installation

### From PyPI

```bash
pip install mcps-mysql-server
```

### From Source (GitHub)

```bash
git clone https://github.com/Shubham9975/mcp-mysql-server.git
cd mcp-mysql-server
pip install .
```
Or for development (editable) mode:
```bash
pip install -e .
```

## Configuration

Set the following environment variables (required for connection):

- `MYSQL_HOST`: MySQL server host (default: "localhost")
- `MYSQL_PORT`: MySQL server port (default: 3306)
- `MYSQL_USER`: MySQL username (**required**)
- `MYSQL_PASSWORD`: MySQL password (**required**)
- `MYSQL_DATABASE`: MySQL database name (**required**)
- `MYSQL_CHARSET`: MySQL character set (default: "utf8mb4")
- `MYSQL_COLLATION`: MySQL collation (default: "utf8mb4_unicode_ci")
- `MYSQL_SQL_MODE`: MySQL SQL mode (default: "TRADITIONAL")

Example:
```bash
export MYSQL_USER="your_user"
export MYSQL_PASSWORD="your_password"
export MYSQL_DATABASE="your_database"
```

## Usage

After setting environment variables, start the server:

```bash
mcps-mysql-server
```

### MCP/Claude/Cursor Integration

Add this to your MCP configuration (e.g., `~/.cursor/mcp.json`):

```json
{
  "mcpServers": {
    "mysql-server": {
      "command": "mcps-mysql-server",
      "env": {
        "MYSQL_HOST": "localhost",
        "MYSQL_USER": "your_user",
        "MYSQL_PASSWORD": "your_password",
        "MYSQL_DATABASE": "your_database"
      }
    }
  }
}
```

## Available Tools

### execute_sql

Execute an SQL query on the MySQL server.

Example:
```sql
SELECT * FROM users LIMIT 10;
```

## Available Resources

- `mysql://tables` — List all tables in the database.
- `mysql://table/{table_name}` — Get the schema of a specific table. Example: `mysql://table/users`

## Development

- All main code is in the `mysql_server/` directory.
- The CLI entry point is implemented in `mcp_mysql_server/launcher.py`.
- Use `pip install -e .` for editable installs during development.
- If you add tests, place them in a `tests/` directory.

## Project Structure

```
mcp-mysql-server/
├── mcp_mysql_server/
│   ├── __init__.py
│   └── launcher.py         # CLI entry point: defines main()
├── mysql_server/
│   ├── __init__.py
│   └── server.py           # Main server logic
├── pyproject.toml          # Build system, metadata, CLI entry point
├── README.md               # Documentation
├── LICENSE                 # License file
└── .gitignore              # Git ignore rules
```

## Troubleshooting

- **Command not found:**  
  Ensure your Python Scripts directory is in your PATH.  
  On Windows, this is usually `C:\Users\<YourUser>\AppData\Local\Programs\Python\Python3x\Scripts`.

## License

MIT License
