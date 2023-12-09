# Database connection pooling

- is a technique used in software applications to efficiently manage and reuse database connections.
- Establishing and tearing down database connections can be a resource-intensive process, especially in scenarios where
  multiple clients or threads need to interact with a database.
- Connection pooling aims to address this issue by maintaining a pool of pre-established database connections that can
  be reused when needed.

## Here's how connection pooling typically works:

## Connection Establishment:

- Initially, a pool of database connections is created and established with the database server.
  The number of connections in the pool is configured based on factors like the anticipated number of concurrent users,
  system resources, and the database server's capacity.

## Connection Request:

- When an application needs to perform a database operation, it requests a connection from the pool rather than creating
  a new connection.

## Connection Reuse:

- If an idle connection is available in the pool, it is handed over to the application.
- This reduces the overhead of establishing a new connection.

## Connection Release:

- Once the application has finished using the connection, it returns it to the pool rather than closing it.
- The connection remains open and is ready to be reused.

## Connection Timeout and Recycling:

- Connections in the pool may have a timeout period.
- If a connection remains unused for a certain duration, it may be closed and removed from the pool to free up
  resources.
- Some connection pools also have the capability to monitor the health of connections and recycle them if they become
  stale or encounter issues.

## Benefits of Database Connection Pooling:

- ## Performance Improvement:
    - Connection pooling reduces the overhead of opening and closing database connections, resulting in better
      performance and response times for database operations.

- ## Resource Utilization:
    - By reusing existing connections, connection pooling minimizes the number of resources (such as memory and CPU)
      consumed by creating new connections.

- ## Scalability:
    - Connection pooling facilitates the efficient management of database connections in scenarios where there are a
      large number of concurrent users or requests.

# Laravel Example

- Laravel, by default, utilizes connection pooling through the underlying database library it relies on, which is
  Eloquent. Eloquent, Laravel's Object-Relational Mapping (ORM) system, manages database connections efficiently,
  including features that are akin to connection pooling.

Under the hood, Laravel uses the Illuminate Database component, which includes a connection pool. The configuration file
for database connections, located at config/database.php, allows you to set various options, including the maximum
number of connections, connection timeout, and other related settings.

Here are some key configurations related to connection pooling:

    'mysql' => [
    'driver' => 'mysql',
    'host' => env('DB_HOST', '127.0.0.1'),
    'port' => env('DB_PORT', '3306'),
    'database' => env('DB_DATABASE', 'forge'),
    'username' => env('DB_USERNAME', 'forge'),
    'password' => env('DB_PASSWORD', ''),
    'unix_socket' => env('DB_SOCKET', ''),
    'charset' => 'utf8mb4',
    'collation' => 'utf8mb4_unicode_ci',
    'prefix' => '',
    'strict' => true,
    'engine' => null,
        // Connection Pooling Configuration
        'options'   => [
            PDO::ATTR_PERSISTENT         => true, // Enable connection pooling
            PDO::ATTR_EMULATE_PREPARES   => true, // Enable query caching
            PDO::ATTR_TIMEOUT            => 60,   // Connection timeout
        ],
    ],

- Keep in mind that connection pooling is more of a concern when using lower-level database access libraries directly. 
- When using **Eloquent**, you can trust that **Laravel** handles these details for you, and you can focus on writing your application logic.
